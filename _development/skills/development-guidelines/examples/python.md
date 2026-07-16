# Development Guidelines — Python examples

Code examples for the rules in [`../SKILL.md`](../SKILL.md). Section headings
mirror that document. The prose, rules, and rationale live in `SKILL.md`; this
file holds only the Python illustrations.

Conventions used in this file:

- **Enums**: `enum.StrEnum` (Python 3.11+).
- **Hard-fail built-ins**: `ValueError` for bad values, `TypeError` for wrong types.
- **Polymorphism**: `abc.ABC` with `@abstractmethod`.
- **Mocking**: `unittest.mock` (stdlib).
- **Type hints**: modern syntax — built-in generics and `X | None` unions.
- **Tests**: Gherkin feature files executed with [behave](https://behave.readthedocs.io/).

---

## Exception strategy — custom exception

```python
# Python
class MissingConfigError(Exception):
    """Raised when a required configuration key is absent."""


raise MissingConfigError(f"Required config key '{key}' is not set")
```

## Exception strategy — runtime/built-in exception

Use the language's standard hard-fail mechanism: `raise ValueError(...)` for an
invalid value, `raise TypeError(...)` for a wrong type.

```python
raise ValueError(f"Expected a positive amount, got {amount}")
```

---

## Null / None / missing value checks

```python
# Python — required config
import os

api_key = os.environ.get("API_KEY")
if not api_key:
    raise ValueError("API_KEY environment variable is required")
```

Do not rely on the language to raise an `AttributeError`/`TypeError` downstream
— check early, fail early, with a message that names the missing value.

---

## What NOT to do

```python
# BAD — silently continues with broken state
api_key = config.get("api_key")
if not api_key:
    logger.warning("api_key missing, using empty string")
    api_key = ""

# BAD — swallows the exception
try:
    result = parse(data)
except Exception:
    result = None

# BAD — logs and returns None, callers will blow up later with no context
def get_user(user_id: str) -> User | None:
    user = db.find(user_id)
    if user is None:
        logger.error(f"User {user_id} not found")
        return None  # caller gets a silent None with no traceback here
    return user
```

```python
# GOOD — raises immediately with context
def get_user(user_id: str) -> User:
    user = db.find(user_id)
    if user is None:
        raise UserNotFoundError(f"User '{user_id}' not found")
    return user
```

---

## Enums for classification values

```python
# BAD — magic strings repeated and unvalidated
def schedule(job: dict) -> None:
    if job["kind"] == "backfill":
        ...
    elif job["kind"] == "streaming":
        ...
    # typo "streming" is a valid str and silently misroutes

# GOOD — a closed set the type checker and runtime enforce
from enum import StrEnum


class JobKind(StrEnum):
    BACKFILL = "backfill"
    STREAMING = "streaming"


def schedule(kind: JobKind) -> None:
    match kind:
        case JobKind.BACKFILL:
            ...
        case JobKind.STREAMING:
            ...
        case _:
            raise ValueError(f"Unhandled job kind: {kind}")
```

---

## Mocking — what to mock and what not to

Mock I/O boundaries with `unittest.mock`; verify real behaviour of real code.
The examples below are expressed as behave scenarios and their step definitions.

```gherkin
# features/user_service.feature
Feature: UserService.get_user

  # BAD — this scenario only proves the mock returns what we told it to.
  # It exercises the mock, not UserService. Do not write tests like this.
  Scenario: get_user returns the stubbed user (BAD — worthless)
    Given a user repository stubbed to return user "1"
    When I get user "1"
    Then the returned user id is "1"

  # GOOD — the mock only isolates the DB; the assertion checks the real guard
  # logic inside UserService (it must raise when the repository finds nothing).
  Scenario: get_user raises when the user is not found (GOOD)
    Given a user repository that finds no user
    When I get user "missing-id"
    Then a UserNotFoundError is raised
```

```python
# features/steps/user_service_steps.py
from unittest.mock import Mock

from behave import given, when, then

from myapp.users import UserService, UserNotFoundError


@given('a user repository stubbed to return user "{user_id}"')
def step_repo_returns_user(context, user_id):
    context.repo = Mock()
    context.repo.find.return_value = {"id": user_id}


@given("a user repository that finds no user")
def step_repo_returns_none(context):
    context.repo = Mock()
    context.repo.find.return_value = None


@when('I get user "{user_id}"')
def step_get_user(context, user_id):
    service = UserService(context.repo)
    context.error = None
    try:
        context.result = service.get_user(user_id)
    except UserNotFoundError as exc:
        context.error = exc


@then('the returned user id is "{user_id}"')
def step_assert_user_id(context, user_id):
    # This asserts only that the mock echoed its stub back — proves nothing.
    assert context.result["id"] == user_id


@then("a UserNotFoundError is raised")
def step_assert_raises(context):
    assert isinstance(context.error, UserNotFoundError)
```

Preferred mocking tool: `unittest.mock` (`Mock`, `MagicMock`, `patch`).

---

## Architecture for testability — dependency injection

```python
# BAD — hardwired dependency, cannot be replaced in tests
class OrderService:
    def __init__(self) -> None:
        self.db = PostgresDatabase()  # cannot inject a fake


# GOOD — dependency injected, swap freely in tests
class OrderService:
    def __init__(self, db: OrderRepository) -> None:
        self._db = db
```

## Architecture for testability — polymorphism

```python
# Python — depend on an abstract type, not a concrete implementation
from abc import ABC, abstractmethod


class PaymentGateway(ABC):
    @abstractmethod
    def charge(self, amount: int, token: str) -> ChargeResult:
        ...


class OrderService:
    def __init__(self, gateway: PaymentGateway) -> None:
        self._gateway = gateway
        # test passes a FakePaymentGateway; production passes StripeGateway
```

---

## Test-driven development — red-green-refactor with behave

One **Scenario** = one behaviour. Work one scenario at a time: write the
scenario and its steps, run `behave`, watch it fail for the right reason (RED),
then write only enough production code to make it pass (GREEN), then refactor
with the full suite green.

### RED — write one failing scenario

```gherkin
# features/user_lookup.feature
Feature: Looking up a user

  Scenario: fetching a missing user fails loudly
    Given a user repository with no user "missing-id"
    When I fetch user "missing-id"
    Then a UserNotFoundError is raised
```

```python
# features/steps/user_lookup_steps.py
from unittest.mock import Mock

from behave import given, when, then

from myapp.users import UserService, UserNotFoundError


@given('a user repository with no user "{user_id}"')
def step_empty_repo(context, user_id):
    context.repo = Mock()
    context.repo.find.return_value = None


@when('I fetch user "{user_id}"')
def step_fetch(context, user_id):
    service = UserService(context.repo)
    context.error = None
    try:
        context.user = service.get_user(user_id)
    except UserNotFoundError as exc:
        context.error = exc


@then("a UserNotFoundError is raised")
def step_expect_error(context):
    assert isinstance(context.error, UserNotFoundError), (
        f"expected UserNotFoundError, got {context.error!r}"
    )
```

Run it and confirm it fails because the behaviour is missing (not an import
typo):

```console
$ behave features/user_lookup.feature
...
0 scenarios passed, 1 failed
```

### GREEN — write only enough production code to pass

```python
# myapp/users.py
class UserNotFoundError(Exception):
    """Raised when a user id has no matching record."""


class UserService:
    def __init__(self, repo) -> None:
        self._repo = repo

    def get_user(self, user_id: str) -> "User":
        user = self._repo.find(user_id)
        if user is None:
            raise UserNotFoundError(f"User '{user_id}' not found")
        return user
```

```console
$ behave features/user_lookup.feature
...
1 scenario passed, 0 failed
```

### REFACTOR — clean up with the full suite green

Improve names/structure of production and step code, then run the whole suite
(`behave`) and confirm every scenario still passes before moving to the next
behaviour.
