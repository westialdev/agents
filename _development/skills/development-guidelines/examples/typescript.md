# Development Guidelines — TypeScript examples

Code examples for the rules in [`../SKILL.md`](../SKILL.md). Section headings
mirror that document. The prose, rules, and rationale live in `SKILL.md`; this
file holds only the TypeScript illustrations.

---

## Exception strategy — custom exception

```typescript
// TypeScript / JavaScript
throw new MissingConfigError(`Required config key '${key}' is not set`);
```

## Exception strategy — runtime/built-in exception

Use the language's standard hard-fail mechanism: `throw new Error(...)`.

---

## Null / None / missing value checks

```typescript
// TypeScript — required config
const apiKey = process.env.API_KEY;
if (!apiKey) {
    throw new Error("API_KEY environment variable is required");
}
```

---

## What NOT to do

```typescript
// BAD — silently continues with broken state
const apiKey = config.get("api_key");
if (!apiKey) {
    logger.warning("api_key missing, using empty string");
    apiKey = "";
}

// BAD — swallows the exception
let result;
try {
    result = parse(data);
} catch (error) {
    result = null;
}

// BAD — logs and returns null, callers will blow up later with no context
function getUser(userId: string): User | null {
    const user = db.find(userId);
    if (!user) {
        logger.error(`User ${userId} not found`);
        return null;  // caller will get a silent null with no traceback here
    }
    return user;
}
```

```typescript
// GOOD — raises immediately with context
function getUser(userId: string): User {
    const user = db.find(userId);
    if (!user) {
        throw new UserNotFoundError(`User '${userId}' not found`);
    }
    return user;
}
```

---

## Enums for classification values

```typescript
// BAD — magic strings repeated and unvalidated
function schedule(job: { kind: string }) {
    if (job.kind === "backfill") { /* ... */ }
    else if (job.kind === "streaming") { /* ... */ }
    // typo "streming" compiles fine and silently misroutes
}

// GOOD — a closed set the compiler enforces
enum JobKind {
    Backfill = "backfill",
    Streaming = "streaming",
}

function schedule(job: { kind: JobKind }) {
    switch (job.kind) {
        case JobKind.Backfill: /* ... */ break;
        case JobKind.Streaming: /* ... */ break;
    }
}
```

---

## Mocking — what to mock and what not to

```typescript
// BAD — testing that a mock returns what you told it to return
test('get user', () => {
    const repo = {
        find: jest.fn().mockReturnValue({ id: "1" })
    };
    const service = new UserService(repo);
    const result = service.getUser("1");
    expect(result).toEqual({ id: "1" });  // this only proves the mock works
});
```

```typescript
// GOOD — mock isolates I/O; test verifies real logic (e.g., enrichment, guard)
test('get user raises when not found', () => {
    const repo = {
        find: jest.fn().mockReturnValue(null)
    };
    const service = new UserService(repo);
    expect(() => service.getUser("missing-id")).toThrow(UserNotFoundError);
});
```

Preferred mocking tool: Jest (`jest.fn()`, `jest.spyOn()`) / Vitest.

---

## Architecture for testability — dependency injection

```typescript
// BAD — hardwired dependency, cannot be replaced in tests
class OrderService {
    private db: PostgresDatabase;

    constructor() {
        this.db = new PostgresDatabase();  // cannot inject a fake
    }
}

// GOOD — dependency injected, swap freely in tests
class OrderService {
    constructor(private db: OrderRepository) {}
}
```

## Architecture for testability — polymorphism

```typescript
// TypeScript
interface PaymentGateway {
    charge(amount: number, token: string): Promise<ChargeResult>;
}

class OrderService {
    constructor(private gateway: PaymentGateway) {}
    // test passes FakePaymentGateway; production passes StripeGateway
}
```
