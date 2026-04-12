---
name: typescript-architecture
description: TypeScript structural maintainability -- premature abstraction, unnecessary indirection, dead code, cross-module coupling, and over-engineered types. Use when creating new modules or services, refactoring across multiple files, designing interfaces or module boundaries, adding architectural layers, or reviewing TypeScript code structure. Also use when the user asks to "check for dead code", "find unnecessary abstractions", "check coupling", "simplify types", or wants a structural review. Do NOT use for type safety, code clarity, or naming issues (use typescript skill). Do NOT use for style/formatting, performance, or security.
---

# Maintainability Review

When this skill is loaded, output exactly this block before any other response:

```
░▀█▀░█▀▀░░░░░█▀█░█▀▄░█▀▀░█░█░▀█▀░▀█▀░█▀▀░█▀▀░▀█▀░█░█░█▀▄░█▀▀
░░█░░▀▀█░▄▄▄░█▀█░█▀▄░█░░░█▀█░░█░░░█░░█▀▀░█░░░░█░░█░█░█▀▄░█▀▀
░░▀░░▀▀▀░░░░░▀░▀░▀░▀░▀▀▀░▀░▀░▀▀▀░░▀░░▀▀▀░▀▀▀░░▀░░▀▀▀░▀░▀░▀▀▀
```

**Note: The current year is 2026. Use this when searching for recent documentation.**

TypeScript structural maintainability from the perspective of the next developer who has to modify this code six months from now. Avoid structural decisions that make code harder to understand, change, or delete -- not because they are wrong today, but because they will cost disproportionately tomorrow.

This skill covers structural maintainability only. Type safety, naming, and code clarity belong to the `typescript` skill.

## Finding Categories

### Premature Abstraction

A generic solution built for a specific problem. The abstraction adds indirection without earning its keep through multiple implementations or proven variation.

Signals: interfaces with one implementor, abstract classes with a single subclass, generics that are always instantiated with the same concrete type, factories for a single variant, configuration for values that will not change, extension points with zero consumers.

```ts
// WRONG: interface with a single implementor, factory for one type
interface NotificationSender {
  send(message: string): Promise<void>;
}

class EmailNotificationSender implements NotificationSender {
  async send(message: string): Promise<void> {
    await this.smtp.send(message);
  }
}

function createSender(kind: string): NotificationSender {
  if (kind === "email") return new EmailNotificationSender();
  throw new Error(`Unknown sender: ${kind}`);
}
```

```ts
// CORRECT: direct implementation until a second sender exists
class EmailSender {
  async send(message: string): Promise<void> {
    await this.smtp.send(message);
  }
}
```

### Unnecessary Indirection

More than two levels of delegation to reach actual logic. Each layer adds cognitive cost; flag when the layers add no behavior.

Signals: wrapper classes that pass through every call, service classes that delegate to a single repository without adding logic, barrel files that re-export an entire directory creating hidden dependency graphs.

```ts
// WRONG: three layers, middle two add nothing
class UserController {
  async getUser(id: string) {
    return this.userService.getUser(id);
  }
}
class UserService {
  async getUser(id: string) {
    return this.userRepository.getUser(id);
  }
}
class UserRepository {
  async getUser(id: string) {
    return db.query<User>("SELECT * FROM users WHERE id = $1", [id]);
  }
}
```

```ts
// CORRECT: collapse until layers earn distinct behavior
class UserController {
  async getUser(id: string) {
    return this.userRepository.getUser(id);
  }
}
class UserRepository {
  async getUser(id: string) {
    return db.query<User>("SELECT * FROM users WHERE id = $1", [id]);
  }
}
```

```ts
// WRONG: barrel file that re-exports everything, hiding what depends on what
// utils/index.ts
export * from "./strings";
export * from "./dates";
export * from "./http";
export * from "./crypto";
// A consumer importing { formatDate } from "./utils" silently depends on the entire barrel

// CORRECT: import from the specific module
import { formatDate } from "./utils/dates";
```

### Dead or Unreachable Code

Code that is not called is not an asset; it is a maintenance liability. Every dead path is a path someone will read, try to understand, and hesitate to delete.

Signals: commented-out code blocks, unused exports (no internal or external importers), unreachable branches after early returns or type narrowing, backwards-compatibility shims for things that have not shipped, feature flags guarding the only implementation, unused function parameters that are not required by an interface contract.

```ts
// WRONG: dead code preserved "just in case"
export async function processOrder(order: Order): Promise<OrderResult | null> {
  if (!order.isValid) return null;

  // Legacy wholesale path -- removed in v2.3
  // if (order.type === "wholesale") {
  //   return processWholesale(order);
  // }

  const result = calculateTotal(order);
  return result;

  // Unreachable -- analytics was moved to event handler
  await sendAnalytics(order);
}

// Exported but imported nowhere in the codebase
export function legacyOrderFormat(order: Order): LegacyOrder {
  return { ...order, version: 1 };
}
```

```ts
// CORRECT: delete dead code; git history preserves it
export async function processOrder(order: Order): Promise<OrderResult | null> {
  if (!order.isValid) return null;
  return calculateTotal(order);
}
```

### Cross-Module Coupling

Changes in one module force changes in another for no domain reason. The modules are bound by implementation accident, not by domain relationship.

Signals: circular imports, modules importing another module's internal/private members, shared mutable state across module boundaries, a change in module A's internal structure breaking module B's compilation.

```ts
// WRONG: billing reaches into user module internals
// billing/invoice.ts
import { User } from "../users/models";

export function createInvoice(user: User): Invoice {
  // billing reads user's internal discount tiers directly
  const discount = (user as any)._internalDiscountTier;
  const taxRegion = user.taxMetadata.region; // user.taxMetadata is an implementation detail
  return { discount, taxRegion, /* ... */ };
}
```

```ts
// CORRECT: billing receives what it needs through a defined contract
// billing/invoice.ts
interface InvoiceCustomer {
  discountRate: number;
  taxRegion: string;
}

export function createInvoice(customer: InvoiceCustomer): Invoice {
  return { discount: customer.discountRate, taxRegion: customer.taxRegion, /* ... */ };
}
```

### Type-Level Over-Engineering

Complex type machinery that is harder to maintain than the problem it solves. The type system should serve the developer, not the other way around.

Signals: deeply nested conditional types, recursive mapped types for a fixed set of cases, template literal type gymnastics for simple string patterns, utility types that require reading TypeScript compiler internals to understand.

NEVER flag type complexity that prevents runtime bugs -- a complex type that catches real errors at compile time is earning its cost. Only flag type complexity that exists for elegance or generality with no concrete safety payoff.

```ts
// WRONG: recursive conditional type for 3 known cases
type DeepPartial<T> = T extends object
  ? T extends Array<infer U>
    ? Array<DeepPartial<U>>
    : { [K in keyof T]?: DeepPartial<T[K]> }
  : T;

// Used exactly once, for a Config type with 2 levels of nesting
type PartialConfig = DeepPartial<Config>;
```

```ts
// CORRECT: write the partial type directly
interface PartialConfig {
  server?: {
    port?: number;
    host?: string;
  };
  database?: {
    url?: string;
    pool?: number;
  };
}
```

```ts
// ACCEPTABLE: complex type that catches real bugs
// A mapped type over a route config that ensures every route has a matching handler
// is complex but prevents missing-handler errors at compile time -- do not flag
type RouteHandlers<R extends RouteConfig> = {
  [K in keyof R]: (params: InferParams<R[K]>) => Response;
};
```

### Scattered Boundary Parsing

External data (HTTP requests, API responses, file reads, environment variables, queue messages) should be parsed into typed data once at the entry point. When parsing scatters, the same external data format gets validated in multiple places, and those validations drift.

```ts
// WRONG: multiple modules each parse the same API response
// services/orders.ts
const res = await fetch("/api/orders");
const data = await res.json();
const orders = data.orders as Order[]; // trusts shape, no validation

// services/analytics.ts
const res = await fetch("/api/orders");
const data = await res.json();
if (!Array.isArray(data.orders)) throw new Error("Bad response");
const orders = data.orders.map((o: any) => ({ id: o.id, total: o.total }));
// Different validation, different shape extraction -- will drift
```

```ts
// CORRECT: parse once at the boundary, consume typed data everywhere
// clients/orders.ts
import { z } from "zod";

const OrderSchema = z.object({
  id: z.string(),
  total: z.number(),
  status: z.enum(["pending", "shipped", "delivered"]),
});
const OrdersResponseSchema = z.object({ orders: z.array(OrderSchema) });

export type Order = z.infer<typeof OrderSchema>;

export async function fetchOrders(): Promise<Order[]> {
  const res = await fetch("/api/orders");
  const parsed = OrdersResponseSchema.parse(await res.json());
  return parsed.orders;
}

// services/orders.ts and services/analytics.ts both call fetchOrders()
// and receive fully typed Order[] -- no re-validation, no drift
```

Three anti-patterns to flag:

- **Duplicated parsing.** The same external data source is validated or parsed in more than one module. The validations will diverge silently.
- **Deep boundary validation.** A module far from the entry point does its own `typeof` / shape checking on data that should have been parsed at the boundary. This couples internal modules to external data formats.
- **Hand-written types for external schemas.** An `interface` that mirrors an API response or database row, maintained by hand rather than derived from a schema (Zod, OpenAPI, Prisma). Hand-written types drift from reality without compiler protection.

### Error Flow Across Module Boundaries

Invisible error paths create implicit coupling. When module A throws and module B catches, B must know what A throws without any type system help. That is undocumented coupling -- the caller depends on implementation details of the thrower.

**At module boundaries where callers need to distinguish between error types, make the error contract explicit.** Within a module, throwing is fine -- the catch is local and the coupling is contained.

```ts
// WRONG: caller must know what createUser throws by reading its implementation
// users/service.ts
export function createUser(data: UserInput): User {
  if (emailExists(data.email)) throw new Error("Email taken");
  if (!validEmail(data.email)) throw new Error("Invalid email");
  return db.insert(data);
}

// handlers/signup.ts
try {
  const user = createUser(input);
} catch (e) {
  // What errors can this throw? No type help. Must read the source.
  if (e.message === "Email taken") { /* ... */ }  // string matching on error messages
}
```

```ts
// CORRECT: discriminated union makes the error contract explicit at the boundary
// users/service.ts
type CreateUserResult =
  | { ok: true; user: User }
  | { ok: false; error: "email_taken" | "invalid_email" };

export function createUser(data: UserInput): CreateUserResult {
  if (emailExists(data.email)) return { ok: false, error: "email_taken" };
  if (!validEmail(data.email)) return { ok: false, error: "invalid_email" };
  return { ok: true, user: db.insert(data) };
}

// handlers/signup.ts
const result = createUser(input);
if (!result.ok) {
  // Compiler knows the exact error values. Adding a new error type
  // forces every caller to handle it.
  switch (result.error) {
    case "email_taken": /* ... */
    case "invalid_email": /* ... */
  }
}
```

Never rely on `@throws` JSDoc as the only documentation of an error contract that callers depend on. JSDoc is not compiler-enforced -- it drifts from reality silently.

## Confidence Calibration

| Level | Threshold | When to apply |
|---|---|---|
| High | 0.80+ | The problem is objectively provable: the abstraction has one implementor and you can verify it, the dead code is provably unreachable, the indirection adds a layer with no added behavior, the type utility is used once for a case that could be written directly |
| Moderate | 0.60-0.79 | The finding involves judgment about abstraction boundaries, coupling severity, or whether a type utility earns its complexity. Real issues, but reasonable people can disagree on the threshold |
| Low | Below 0.60 | Primarily a preference or the "better" approach is debatable. **Suppress entirely -- do not flag or mention** |

## Exclusions

Do NOT flag:

- **Domain-driven complexity.** A tax calculation with many branches is not over-engineered if the tax code really has that many rules. Complexity that mirrors domain complexity is justified.
- **Justified abstractions.** If an interface has 3+ implementors, the abstraction is earning its keep.
- **Framework-mandated patterns.** If the framework requires a factory, a base class, or a specific inheritance hierarchy, the indirection is not the author's choice.
- **Type safety issues.** `any`, unsafe casts, missing null checks, exhaustive handling. These belong to the `typescript` skill.
- **Naming and code clarity.** Vague names, boolean parameters, nested ternaries. These belong to the `typescript` skill.
- **Style preferences.** Formatting, import order, semicolons. Linter concerns.

