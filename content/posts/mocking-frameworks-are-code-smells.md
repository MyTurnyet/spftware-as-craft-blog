---
title: 'Mocking Frameworks are Code Smells'
date: 2025-10-31 07:48:26 -0900
draft: true
description: If you need a mocking framework, your design is broken. Learn why mocking frameworks are symptoms of tight coupling and poor architecture.
thumbnail:
  url: /img/interface-code.jpg
  author: Paige Watson
  authorURL: https://www.linkedin.com/in/paige-is-xp/
  originURL:
  origin: Software As Craft

author: Paige Watson
tags:
  - Quality
  - SOLID
  - Design
  - Architecture
  - Code
  - Testing
---

## The Uncomfortable Truth

You've probably done it hundreds (if not thousands) of times without thinking. A test needs to verify some logic, but
that logic depends on a database, or a web service, or some other external system. So you reach for your mocking
framework (Mockito, Moq, Jest mocks, etc.) and start setting up expectations. `when(this).thenReturn(that)`. You get
your test passing and move on.

But here's the uncomfortable truth: **if you need a mocking framework, your design is broken.**

I'm not saying your code doesn't work. I'm not saying you're a bad developer. I'm saying that the need for a mocking
framework is a symptom: a code smell that reveals deeper architectural problems you've been ignoring. Tight coupling.
Bloated dependencies. Testing implementation details instead of behavior. These are the real problems. And mocking
frameworks let you write tests without fixing or even addressing the real problems.

In this post, I'll show you exactly what mocking frameworks hide, why they create massive technical debt when your
dependencies change, and what you should do instead. By the end, you'll understand why mocking frameworks should never
be used, and you'll have better alternatives that lead to cleaner, more maintainable code.

## What Mocking Frameworks Hide

Mocking frameworks are seductive. They make it easy to write tests for hard-to-test code. But that ease comes at a
cost: they hide the design problems that make your code hard to test in the first place.

### Tight Coupling

When you mock a dependency, you're working around the fact that your code is tightly coupled to that dependency. Your
class can't function without it. Your tests can't run without simulating it. But instead of questioning why your code is
so dependent on this thing, you just mock it and move on.

The mocking framework becomes a band-aid. It lets you write tests for tightly coupled code without decoupling it. And
because your tests pass, you think everything is fine. Meanwhile, your codebase becomes more and more entangled, harder
to change, harder to understand, and harder to maintain.

If you can't test your code without mocking, your code is too coupled. Period.

### Complex, Bloated Dependencies

Here's a scenario you've probably encountered: you need to test a method that uses a dependency, but that dependency has
twenty methods. So you fire up your mocking framework and start stubbing them out.
`when(dependency.method1()).thenReturn(value1)`,
`when(dependency.method2()).thenReturn(value2)`, and on and on.

Stop. Look at what you're doing.

**If you're mocking a class with twenty methods but only using two of them, that class is doing too much.** It probably violates
the Single Responsibility Principle. It's most likely a god object. It shouldn't exist in that form.

But the mocking framework lets you pretend this is fine. You can mock all twenty methods (or just the two you need, with
the rest returning default values), write your test, and never confront the fact that your dependency is bloated and
doing too much.

The real fix is to break that dependency into smaller, more focused pieces. But you won't do that as long as mocking
makes the pain tolerable.

### Testing Implementation, Not Behavior

Here's the most insidious problem: mocking frameworks force you to test implementation details.

When you write `when(userRepository.findById(123)).thenReturn(user)`, you're not just testing that your code produces
the right output given the right input. You're testing that your code calls `findById` with the argument `123`. You're
testing *how* your code works, not *what* it does.

This is backwards. Tests should verify behavior ("what your code accomplishes"), not implementation details about how it
accomplishes it. When tests depend on implementation, they break every time you refactor, even when the behavior hasn't
changed. They become a maintenance burden instead of a safety net.

Mocking frameworks encourage this because they require you to specify exactly which methods get called with which
arguments. They make it easy to write brittle tests that know too much about your code's internals. And when those tests
inevitably break during refactoring, you'll blame the tests, not the mocking framework that led you down this path.

## The Real Cost: When Libraries Change

The problems I've described so far might seem abstract. Let me make them concrete with a scenario you've probably lived
through: changing a library.

### The JSON Library Nightmare

Your team decides to switch JSON parsing libraries. Maybe you're moving from org.json to Jackson for better performance.
Maybe you're adopting Gson for cleaner APIs. The reasons don't matter. What matters is this: it's a simple implementation
swap. The behavior stays the same: parse JSON, get objects.

But now you have to update your tests. Hundreds of them. Thousands, maybe.

Every test that mocked your JSON library now needs to be rewritten. `when(jsonParser.parse(input)).thenReturn(object)`
becomes `when(objectMapper.readValue(input, Class)).thenReturn(object)`. Different method names. Different signatures.
Different mocking setup. You're not changing behavior. You're not adding features. You're just updating mocks because you
changed an implementation detail.

This is a week of tedious, error-prone work that provides zero business value. And here's the kicker: **your production
code might have changed in twenty places, but your tests changed in a thousand.**

### The Logging Framework Disaster

Or consider switching logging frameworks. You're moving from Log4j to Logback (especially after those security
vulnerabilities). Or maybe you're adopting SLF4J as a facade. Again, the behavior is the same: write logs.

But every test that mocked your logger now breaks. Every `when(logger.info(message))` needs to be updated. Every
verification that `logger.error()` was called needs to change. You're spending days updating tests for code that has
nothing to do with your application's actual behavior.

The logging framework is an implementation detail. It's infrastructure. Your tests shouldn't know or care which logging
library you use. But because you mocked it, they do.

### The Uncomfortable Question

Here's what this reveals: **if your tests break when you swap implementations, you're testing the wrong thing.**

Your tests should verify that your code does what it's supposed todo.  The behavior, the outcomes, the business logic 
should not verify that you're using Jackson instead of Gson, or Logback instead of Log4j. Those are implementation
details, and implementation details should be swappable without breaking tests.

But mocking frameworks couple your tests to those implementation details. They turn every dependency into a contract that
your tests enforce. Change the dependency, and your tests demand you rewrite them.

This is technical debt at its worst. You're paying compound interest on every mock you write. And the bill comes due every
time you need to change a library, refactor an interface, or swap an implementation.

## What You Should Do Instead

So if mocking frameworks are out, what's the alternative? How do you write tests for code that depends on databases,
external APIs, or other hard-to-test components?

The answer isn't a different tool. It's better architecture.

### Hexagonal Architecture: Push Dependencies to the Edges

The fundamental problem that makes you reach for mocks is this: your business logic is tangled up with your
infrastructure. Your domain code directly depends on databases, HTTP clients, file systems, and other I/O operations.

Hexagonal Architecture (also called Ports & Adapters) solves this by pushing all external dependencies to the edges of
your system. Your core business logic doesn't know about databases or APIs. It only knows about interfaces (ports) that
define what it needs.

Here's a simple example in Java:

```java
// Port (interface) - defines what the domain needs
public interface UserRepository {
    User findByEmail(String email);
    void save(User user);
}

// Domain logic - depends only on the interface
public class UserService {
    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }

    public void registerUser(String email, String password) {
        if (repository.findByEmail(email) != null) {
            throw new UserAlreadyExistsException();
        }
        User user = new User(email, password);
        repository.save(user);
    }
}
```

Notice: `UserService` has no idea how users are stored. It doesn't know about JDBC, Hibernate, or any database. It just
knows it can find and save users through the `UserRepository` interface.

Now testing is trivial—no mocking framework needed:

```java
class FakeUserRepository implements UserRepository {
    private final Map<String, User> users = new HashMap<>();

    public User findByEmail(String email) {
        return users.get(email);
    }

    public void save(User user) {
        users.put(user.getEmail(), user);
    }
}

@Test
void shouldNotRegisterDuplicateUser() {
    FakeUserRepository repository = new FakeUserRepository();
    UserService service = new UserService(repository);

    service.registerUser("test@example.com", "password");

    assertThrows(UserAlreadyExistsException.class,
        () -> service.registerUser("test@example.com", "password"));
}
```

This test is simple, fast, and resilient. No mocking framework. No magic. Just a straightforward implementation of the
interface that serves the test's needs.

### Hand-Written Test Doubles: Only What You Need

The `FakeUserRepository` above is a simplified implementation used for testing, a "Test Double". Unlike mocks, test doubles
are real implementations. They follow the same interface contract as your production code.

And here's the key: **test doubles only implement what they need to.** If `UserRepository` had twenty methods but your
test only uses two, your test double only implements those two. The others can throw `UnsupportedOperationException` or
return null. This makes the bloat obvious.

Here's a TypeScript example:

```typescript
// Port (interface)
interface OrderProcessor {
    processPayment(order: Order): PaymentResult;
    sendConfirmationEmail(order: Order): void;
    updateInventory(order: Order): void;
}

// Test double - only implements what this test needs
class TestOrderProcessor implements OrderProcessor {
    processedOrders: Order[] = [];

    processPayment(order: Order): PaymentResult {
        this.processedOrders.push(order);
        return { success: true, transactionId: "test-123" };
    }

    sendConfirmationEmail(order: Order): void {
        // This test doesn't care about emails
        throw new Error("Not implemented");
    }

    updateInventory(order: Order): void {
        // This test doesn't care about inventory
        throw new Error("Not implemented");
    }
}

test("should process order payment", () => {
    const processor = new TestOrderProcessor();
    const service = new OrderService(processor);

    service.placeOrder(testOrder);

    expect(processor.processedOrders).toContain(testOrder);
});
```

If you find yourself implementing dozens of methods in a test double, that's a signal: your interface is doing too much.
Break it apart.

### The Benefits: Clarity and Resilience

With this approach:

- **Your tests are clear**: No magic mocking DSL. Just plain code implementing interfaces.
- **Your tests are fast**: Test doubles use in-memory data structures, not mocking reflection.
- **Your tests are resilient**: Swap the real implementation (JDBC → MongoDB) and tests don't break.
- **Your design improves**: Dependencies on bloated interfaces become obvious and painful.

Most importantly, **your architecture improves**. When you can't reach for a mocking framework to paper over bad design,
you're forced to create good design. You're forced to decouple. You're forced to think about interfaces and
dependencies. You're forced to separate concerns.

Good architecture makes mocking frameworks unnecessary. And the absence of mocking frameworks forces good architecture.
It's a virtuous cycle.

## Stop Reaching for the Framework

Here's the bottom line: mocking frameworks are a crutch. They let you test bad design without fixing it. They let you
ignore tight coupling, bloated dependencies, and tangled architecture. They make you feel productive while you accumulate
technical debt that will cost you dearly when libraries change, interfaces evolve, or codebases grow.

You don't need them.

What you need is better design. When you feel the urge to reach for Mockito, Moq, or Jest mocks, stop. Ask yourself:
**Why is this code hard to test?** The answer is usually that your design is broken. Your classes are too coupled. Your
dependencies are too complex. Your business logic is tangled with infrastructure.

Fix the design. Don't mock around it.

Start by separating concerns. Push external dependencies to the edges. Define clean interfaces that represent what your
domain needs, not how your infrastructure works. Build your core logic to depend on abstractions, not implementations.

Then write simple test doubles—plain implementations of those interfaces that serve your tests' needs. No frameworks. No
magic. Just code.

### The Challenge

I challenge you to try this: for your next feature, write tests without a mocking framework. When you hit something that
feels hard to test, resist the urge to mock. Instead, redesign. Extract an interface. Decouple the dependency. Create a
test double.

It will feel uncomfortable at first. Mocking frameworks have made us lazy. But you'll quickly discover that the
discomfort is growth. You're learning to write better code, not just passing tests.

Your tests will become clearer. Your architecture will improve. And when you need to swap that JSON library or update
that logging framework, your tests won't break. Because they never cared about those implementation details in the first
place.

Mocking frameworks are code smells. Stop using them. Start writing better code.
