# Development Guidelines — Go examples

Code examples for the rules in [`../SKILL.md`](../SKILL.md). Section headings
mirror that document. The prose, rules, and rationale live in `SKILL.md`; this
file holds only the Go illustrations.

Go has no exceptions. "Errors must explode" maps onto Go like this:

- **Domain and I/O failures are `error` values**, returned to the caller,
  wrapped with context, and never discarded. Returning the error *is* raising
  it; ignoring it is swallowing it.
- **Programmer errors** (broken contract, nil dependency, unhandled enum member)
  `panic`. A panic is the hard crash the base rules ask for.
- **At the top** (`main`, a command), an error that reaches the end stops the
  process with a non-zero exit: `log.Fatal` or `os.Exit(1)` after printing it.

Conventions used in this file:

- **Errors**: sentinel errors (`errors.New`) and typed error structs, wrapped
  with `fmt.Errorf("...: %w", err)`, inspected with `errors.Is` / `errors.As`.
- **Enums**: a string-backed defined type with constants, a parse function at
  the boundary, and the [`exhaustive`](https://github.com/nishanths/exhaustive)
  linter (in `golangci-lint`) for switches.
- **Polymorphism**: small interfaces, declared by the package that consumes
  them, satisfied implicitly.
- **Mocking**: hand-written fakes first; [`testify/mock`](https://github.com/stretchr/testify)
  or [`go.uber.org/mock`](https://github.com/uber-go/mock) when a fake would
  need call recording.
- **Tests**: the standard `testing` package and `go test`, in an external
  `_test` package so tests use only the public API. Projects that specify
  behaviour in Gherkin use [godog](https://github.com/cucumber/godog) instead,
  with the same red-green-refactor cycle.

---

## Exception strategy — custom exception

Use a **sentinel error** when callers only need to know *which* failure it was,
and a **typed error** when the failure carries context fields. Wrap either with
`%w` so the caller can still match it.

```go
// Go — sentinel error: callers match it with errors.Is
var ErrMissingConfig = errors.New("missing config")

return fmt.Errorf("required config key %q is not set: %w", key, ErrMissingConfig)
```

```go
// Go — typed error: callers extract the context with errors.As
type UserNotFoundError struct {
	ID string
}

func (e *UserNotFoundError) Error() string {
	return fmt.Sprintf("user %q not found", e.ID)
}

return nil, &UserNotFoundError{ID: id}

// caller
var notFound *UserNotFoundError
if errors.As(err, &notFound) {
	// handle selectively, notFound.ID is available
}
```

## Exception strategy — runtime/built-in exception

For a programmer error, use `panic` with a message that names the broken
contract. Do not use `panic` for conditions a caller can reasonably expect
(a missing record, a failed request): return an error.

```go
if amount <= 0 {
	panic(fmt.Sprintf("charge: expected a positive amount, got %d", amount))
}
```

At the top of the program, an error that nobody could handle ends the process:

```go
func main() {
	if err := run(); err != nil {
		log.Fatalf("badala: %v", err) // prints and exits with status 1
	}
}
```

---

## Null / None / missing value checks

```go
// Go — required config: LookupEnv distinguishes unset from empty
apiKey, ok := os.LookupEnv("API_KEY")
if !ok || apiKey == "" {
	return fmt.Errorf("API_KEY environment variable is required: %w", ErrMissingConfig)
}
```

```go
// Go — required dependency: a nil collaborator is a programmer error
func NewOrderService(repo OrderRepository) *OrderService {
	if repo == nil {
		panic("NewOrderService: repo is required")
	}
	return &OrderService{repo: repo}
}
```

Do not rely on a nil pointer dereference downstream: it panics far from the
cause, with no name for the missing value. Check early, fail early, with a
message that names it.

---

## What NOT to do

```go
// BAD — silently continues with broken state
apiKey := os.Getenv("API_KEY")
if apiKey == "" {
	log.Println("API_KEY missing, using empty string")
}

// BAD — discards the error
result, _ := parse(data)

// BAD — recovers and carries on as if nothing happened
defer func() { _ = recover() }()

// BAD — logs and returns nil, nil: the caller gets a nil user and no error
func (s *UserService) GetUser(ctx context.Context, id string) (*User, error) {
	user, err := s.repo.Find(ctx, id)
	if err != nil || user == nil {
		log.Printf("user %s not found", id)
		return nil, nil // caller dereferences nil later, far from here
	}
	return user, nil
}
```

```go
// GOOD — returns the failure immediately, with context, matchable by the caller
func (s *UserService) GetUser(ctx context.Context, id string) (*User, error) {
	user, err := s.repo.Find(ctx, id)
	if err != nil {
		return nil, fmt.Errorf("get user %q: %w", id, err)
	}
	if user == nil {
		return nil, &UserNotFoundError{ID: id}
	}
	return user, nil
}
```

---

## Enums for classification values

Go has no enum keyword. Use a string-backed defined type with constants, parse
untrusted strings at the boundary, and switch over every member.

```go
// BAD — magic strings repeated and unvalidated
func schedule(kind string) {
	switch kind {
	case "backfill":
		// ...
	case "streaming":
		// ...
	}
	// typo "streming" compiles fine and silently does nothing
}
```

```go
// GOOD — a named set; outside input must pass through ParseJobKind
type JobKind string

const (
	JobKindBackfill  JobKind = "backfill"
	JobKindStreaming JobKind = "streaming"
)

func ParseJobKind(s string) (JobKind, error) {
	switch k := JobKind(s); k {
	case JobKindBackfill, JobKindStreaming:
		return k, nil
	}
	return "", fmt.Errorf("unknown job kind %q", s)
}

func schedule(kind JobKind) {
	switch kind {
	case JobKindBackfill:
		// ...
	case JobKindStreaming:
		// ...
	default:
		panic(fmt.Sprintf("schedule: unhandled job kind %q", kind))
	}
}
```

A Go string type cannot make invalid values impossible to construct: any
`JobKind("x")` compiles. Close the gap with the two guards above: parse at the
boundary, and a `default` that panics. Turn on the `exhaustive` linter so a
member added later and missing from a switch fails the build.

---

## Mocking — what to mock and what not to

Mock I/O boundaries with a fake that implements the consumer's interface;
verify real behaviour of real code.

```go
// internal/users/service_test.go
package users_test

import (
	"context"
	"errors"
	"testing"

	"example.com/app/internal/users"
)

type fakeRepo struct {
	user *users.User
	err  error
}

func (f fakeRepo) Find(ctx context.Context, id string) (*users.User, error) {
	return f.user, f.err
}

// BAD — this test only proves the fake returns what we told it to.
// It exercises the fake, not UserService. Do not write tests like this.
func TestGetUserReturnsStubbedUser(t *testing.T) {
	svc := users.NewUserService(fakeRepo{user: &users.User{ID: "1"}})

	got, err := svc.GetUser(context.Background(), "1")

	if err != nil {
		t.Fatal(err)
	}
	if got.ID != "1" { // only proves the fake echoed its stub back
		t.Fatalf("got id %q, want %q", got.ID, "1")
	}
}

// GOOD — the fake only isolates the database; the assertion checks the real
// guard inside UserService (it must fail when the repository finds nothing).
func TestGetUserFailsWhenNotFound(t *testing.T) {
	svc := users.NewUserService(fakeRepo{})

	_, err := svc.GetUser(context.Background(), "missing-id")

	var notFound *users.UserNotFoundError
	if !errors.As(err, &notFound) {
		t.Fatalf("expected UserNotFoundError, got %v", err)
	}
	if notFound.ID != "missing-id" {
		t.Fatalf("error names id %q, want %q", notFound.ID, "missing-id")
	}
}
```

When the test must check *how* a boundary was called (arguments, call count),
use a mocking library instead of growing the fake:

```go
// testify/mock — same GOOD test, with call verification
type mockRepo struct{ mock.Mock }

func (m *mockRepo) Find(ctx context.Context, id string) (*users.User, error) {
	args := m.Called(ctx, id)
	user, _ := args.Get(0).(*users.User) // nil when the stub returns nil
	return user, args.Error(1)
}

func TestGetUserQueriesRepoOnceAndFails(t *testing.T) {
	repo := &mockRepo{}
	repo.On("Find", mock.Anything, "missing-id").Return(nil, nil).Once()
	svc := users.NewUserService(repo)

	_, err := svc.GetUser(context.Background(), "missing-id")

	var notFound *users.UserNotFoundError
	if !errors.As(err, &notFound) {
		t.Fatalf("expected UserNotFoundError, got %v", err)
	}
	repo.AssertExpectations(t)
}
```

Preferred mocking tools: hand-written fakes; `testify/mock` or
`go.uber.org/mock` (`mockgen`) when calls must be verified.

---

## Architecture for testability — dependency injection

```go
// BAD — hardwired dependency, cannot be replaced in tests
type OrderService struct {
	db *PostgresDatabase
}

func NewOrderService() *OrderService {
	return &OrderService{db: NewPostgresDatabase()} // cannot inject a fake
}

// GOOD — dependency injected through the constructor, swap freely in tests
type OrderService struct {
	repo OrderRepository
}

func NewOrderService(repo OrderRepository) *OrderService {
	if repo == nil {
		panic("NewOrderService: repo is required")
	}
	return &OrderService{repo: repo}
}
```

## Architecture for testability — polymorphism

Accept interfaces, return structs. Declare the interface in the package that
uses it, with only the methods it needs; implementations satisfy it implicitly.

```go
// Go — the consumer owns a small interface
type PaymentGateway interface {
	Charge(ctx context.Context, amount int64, token string) (ChargeResult, error)
}

type OrderService struct {
	gateway PaymentGateway
	// test passes a fakeGateway; production passes a *stripe.Gateway
}

// in the test package: fail the build if the fake drifts from the interface
var _ orders.PaymentGateway = fakeGateway{}
```

---

## Test-driven development — red-green-refactor with go test

One **test function** (or one table row) = one behaviour. Work one test at a
time: write it, run `go test`, watch it fail for the right reason (RED), then
write only enough production code to make it pass (GREEN), then refactor with
the full suite green.

### RED — write one failing test

```go
// internal/users/lookup_test.go
package users_test

import (
	"context"
	"errors"
	"testing"

	"example.com/app/internal/users"
)

type emptyRepo struct{}

func (emptyRepo) Find(ctx context.Context, id string) (*users.User, error) {
	return nil, nil
}

func TestFetchingMissingUserFailsLoudly(t *testing.T) {
	svc := users.NewUserService(emptyRepo{})

	_, err := svc.GetUser(context.Background(), "missing-id")

	var notFound *users.UserNotFoundError
	if !errors.As(err, &notFound) {
		t.Fatalf("expected UserNotFoundError, got %v", err)
	}
}
```

Run it. In Go the first red is often a compilation failure, and that counts
(Three Laws, rule 2), as long as what is missing is the behaviour under test,
not a typo in an import path:

```console
$ go test ./internal/users/ -run TestFetchingMissingUserFailsLoudly
# example.com/app/internal/users_test [example.com/app/internal/users.test]
internal/users/lookup_test.go:14:63: undefined: users.User
internal/users/lookup_test.go:19:15: undefined: users.NewUserService
internal/users/lookup_test.go:23:22: undefined: users.UserNotFoundError
FAIL	example.com/app/internal/users [build failed]
FAIL
```

### GREEN — write only enough production code to pass

```go
// internal/users/service.go
package users

import (
	"context"
	"fmt"
)

type User struct {
	ID string
}

type UserRepository interface {
	Find(ctx context.Context, id string) (*User, error)
}

type UserNotFoundError struct {
	ID string
}

func (e *UserNotFoundError) Error() string {
	return fmt.Sprintf("user %q not found", e.ID)
}

type UserService struct {
	repo UserRepository
}

func NewUserService(repo UserRepository) *UserService {
	return &UserService{repo: repo}
}

func (s *UserService) GetUser(ctx context.Context, id string) (*User, error) {
	user, err := s.repo.Find(ctx, id)
	if err != nil {
		return nil, fmt.Errorf("get user %q: %w", id, err)
	}
	if user == nil {
		return nil, &UserNotFoundError{ID: id}
	}
	return user, nil
}
```

```console
$ go test ./internal/users/ -run TestFetchingMissingUserFailsLoudly
ok  	example.com/app/internal/users	0.002s
```

The nil check on `repo` in the constructor is not here yet: no test asks for it.
It arrives with its own red test in the next cycle. The `err` from `Find` is
returned rather than left out, because discarding it is banned (see "What NOT
to do"); its own test, that a repository failure reaches the caller wrapped,
comes next.

### REFACTOR — clean up with the full suite green

Improve names and structure of production and test code, then run the whole
suite with the race detector (`go test -race ./...`) and `go vet ./...`, and
confirm everything passes before moving to the next behaviour.
