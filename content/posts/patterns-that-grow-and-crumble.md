---
title: 'Patterns That Grow and Patterns That Crumble'
date: 2026-02-04 21:00:26 -0900
draft: false
description: Why patterns that ship features fast when teams are small, crumble as organizations grow.
thumbnail:
  url: /img/crumble-building.jpg
  author: Peter Hermann
  authorURL: https://unsplash.com/@tama66
  originURL: https://unsplash.com/photos/brown-wooden-house-near-green-trees-during-daytime-XRNSn4gt8Hs
  origin: Unsplash

author: Paige Watson
tags:
  - Quality
  - Design
  - Architecture
  - Code
---

## The System That Worked... Until It Didn't

*Before we dive in: **Mercato** (the company used in this blog post) isn't real. It's a composite example based on
patterns I've seen across many organizations. The architectural challenges and organizational dynamics, however, are
very real.*

Six experienced Java developers built a retail POS platform the "right" way. Clean layered architecture. Service objects
that coordinated business logic. Inheritance hierarchies eliminating duplication. An early microservices split to
prepare for scaling later.

The architecture diagram looked like it belonged in a conference talk.

`OrderService` orchestrated checkout flows. A well-designed inheritance tree captured the nuances between retail and
online transactions. Controllers stayed thin, repositories stayed focused, services handled business rules. During
design reviews, the team felt confident they were making defensible choices and for eighteen months, they were right.

Features shipped fast. New requirements like gift cards, loyalty programs, and shipping integrations found their natural
places in the system. Leadership praised velocity. Investors saw a platform that could scale.

Then the team grew. Six developers became forty. The one cohesive team split into Platform, Checkout, Promotions,
Enterprise, Integrations, and Analytics. The product expanded to mobile checkout, multi-location inventory, promotional
rules, region-specific taxes, and enterprise features for retailers with hundreds of locations.

No single catastrophic decision broke the system. Just subtle friction slowly grinding away.

Pull requests to `OrderService` started colliding. Three teams needed to modify checkout logic in the same sprint. The
`Order` hierarchy grew to nine subclasses with overridden methods that interacted in surprising ways. Processing a
partial refund with a promotional discount required touching four repositories and coordinating across three teams.

Developers started avoiding parts of the system.

> "Don't touch the checkout flow unless you really have to."

The team's architectural discussions shifted from "how should we design this?" to "how do we work around what's there?"
Onboarding took longer. Simple changes required more coordination. The metrics leadership watched, like features per
sprint, velocity, and deployment frequency all stayed steady, but the team felt the weight.

During yet another coordination meeting about holiday promotional pricing, someone said it:
> "When did this architecture stop helping us and start fighting us?"

The question hung there, because nothing was *obviously wrong*. Most of it still looked like industry best practices.
The
patterns hadn't failed immediately, they succeeded long enough to become entrenched. They just weren't built to grow
with the system or the organization around it.

Here's what nobody talks about: patterns don't fail in isolation. Context changes. Business requirements evolve, teams
grow, coordination costs shift. And organizations fail to notice until the architecture that once accelerated delivery
has become the thing slowing it down.

This is about four common patterns that looked like good decisions, how they quietly evolved from helpful structures
into organizational liabilities, why even experienced teams make these choices and what you might do about it.

---

## The Good and the Not So Good

Not all patterns age the same way.

Some enable learning. They reduce coordination costs as teams grow. They make refactoring safer and boundaries clearer.
When you add your tenth developer, these patterns will help, instead of hurt.

Other patterns freeze assumptions. They concentrate power or complexity in places that become bottlenecks. They require
organizational heroics to maintain. When you add your tenth developer, these patterns start to show up as pain.

The difference isn't always obvious early on. Both kinds of patterns can look good in a design review. Both can ship
features fast when the team is small. The distinction emerges under pressure, when business requirements shift weekly,
when new developers join monthly, or when the thing you built six months ago needs to change in ways you didn't
anticipate.

Here's the truth: a pattern grows if it tolerates change, and crumbles if it requires stability.

### The Growth Test

Ask these questions about any architectural choice:

**What happens when a developer modifies this?**  
If the answer is "they'll probably break something," you've centralized knowledge in ways that don't scale.

**What happens when requirements change weekly?**  
If the answer is "we'd need to coordinate across multiple teams," you've coupled things that the business treats as
independent.

**Does adding a feature require touching unrelated code?**  
If so, you've optimized for the system you had, not the system you're building.

**Can you refactor this without a multi-week project?**  
If not, you've locked yourself into decisions that made sense when context was different, but no longer does.

**Does this reduce or increase coordination cost?**  
The pattern might look elegant on paper, but if it requires three teams to align before shipping a feature, then it's
scaling organizational friction.

You can run this test on any pattern: inheritance hierarchies, service boundaries, layering strategies, whatever. The
patterns that grow well distribute knowledge, localize change, and make boundaries explicit. The patterns that crumble
centralize decision-making, hide behavior behind abstractions, and resist incremental evolution.

Most patterns crumble because they optimize for elegance over adaptability. Or they solve yesterday's problem,
while tomorrow's requirements are already different. Or they look like a "best practices" but those practices
assume a context you don't actually have.

The uncomfortable truth: the patterns that will crumble aren't bad decisions when they are made. They were
reasonable responses to the pressures and advice experienced developers receive. They just won't grow.

---

## How Growth Changes Everything

Back at Mercato, the retail POS platform that worked so well for eighteen months, hit an inflection point. Not a
technical crisis, just **success**.

A major retail chain signed on, and then another. Then investors showed up with growth capital. The founders hired
aggressively. The product roadmap exploded with features retailers actually wanted.

**New features:**

- Mobile checkout for in-store associates
- Multi-location inventory with real-time sync
- Promotional rules engine (buy-one-get-one, bundle pricing, seasonal discounts)
- Loyalty program integration
- Region-specific tax calculations
- Returns across channels (bought online, returned in-store)
- Third-party integrations (Shopify, Square, existing ERP systems)
- Enterprise features for retailers with hundreds of locations

**Team changes:**

- Six developers became forty
- One team became seven: Platform, Checkout, Promotions, Enterprise Retail, Integrations, Analytics, Infrastructure
- New teams meant new managers
- New managers meant new processes
- New processes meant coordination overhead

The codebase grew. Not just lines of code, but conceptual surface area as well. The simple checkout flow from version
1.0
now had to handle:

- Online orders
- In-store purchases
- Mobile transactions
- Mixed cart types (physical + digital)
- Gift cards
- Store credit
- Partial payments
- Split tender
- Layaway
- Pre-orders

Every new feature touched the same core services. Every new team needed to modify checkout logic. Every sprint brought
merge conflicts in `OrderService`. Every release required more coordination between teams.

Leadership noticed velocity slowing but blamed normal "scaling challenges." Developers noticed the architecture fighting
them, but didn't have time to fix it. They had features to ship.  
Metrics stayed steady because teams worked harder to
compensate for architectural friction.

Here's what happened to those four "reasonable" architectural decisions:

1. The **central service** that coordinated checkout became a bottleneck every team depended on.
2. The **inheritance hierarchy** that eliminated duplication became a maze of overridden behavior nobody fully
   understood.
3. The **layered architecture** that looked professional scattered business logic across controllers, services,
   repositories, and utilities with no clear owner.
4. The **microservices split** that prepared for scale created coordination overhead that dwarfed any benefit from
   independent deployment.

None of these patterns broke suddenly. They eroded.
Like [compound interest]({{% relref compound-interest %}}) working in reverse.

---

## Pattern #1: The God Services

Let's start with `PlatformService`.

When the team first built Mercato's checkout flow, they created a service to coordinate everything. It made sense.
The `CheckOut` flow had rules, and those rules needed to live somewhere.

```java
public class PlatformService {

    public Receipt processOrder(Order order) {
        validateOrder(order);
        applyPromotions(order);
        calculateTax(order);
        reserveInventory(order);
        chargePayment(order);
        updateLoyaltyPoints(order);
        notifyFulfillment(order);
        return generateReceipt(order);
    }
}
```

Clean. Easy to understand. One place to look when checkout broke.

Then promotions got complicated. Taxes needed region-specific rules. Loyalty programs needed custom point
calculations. Enterprise customers needed fraud checks. The mobile checkout needed different validation process. Returns
needed refund logic.

Six months later:

```java
public class PlatformService {

    private final TaxService taxService;
    private final PromotionEngine promotionEngine;
    private final InventoryService inventoryService;
    private final PaymentProcessor paymentProcessor;
    private final LoyaltyService loyaltyService;
    private final FraudDetector fraudDetector;
    private final FulfillmentService fulfillmentService;
    private final NotificationService notificationService;
    private final AuditLogger auditLogger;
    private final AnalyticsTracker analyticsTracker;

    public Receipt processOrder(Order order) { /* ... */ }
    public void processReturn(Return returnRequest) { /* ... */ }
    public void processExchange(Exchange exchange) { /* ... */ }
    public void applyPromotion(Order order, Promotion promo) { /* ... */ }
    public void recalculateTax(Order order) { /* ... */ }
    public void adjustInventory(Order order, Adjustment adjustment) { /* ... */ }
    public void processPartialRefund(Order order, Refund refund) { /* ... */ }
    public void validateEnterprisePricing(Order order) { /* ... */ }
    // ... 40 more methods
}
```

Two thousand lines. Ten injected dependencies. Forty-seven methods. Three teams making changes weekly.

### Why It Worked Early

When the team was small, centralization felt like clarity. One service handled checkout. Have a question about checkout
logic? Check `PlatformService`. Need to add a feature? Extend `PlatformService`. Everything in one place.

Leadership loved it. "We can find all our business rules in one service." Sounded responsible.

### Why It Crumbled

Centralization doesn't scale with teams.

**The coordination tax:** Three teams needed to modify checkout logic in the same sprint. Pull requests collided. Merge
conflicts occurred weekly. No team could work on it independently.

**The knowledge bottleneck:** Only two developers really understood the service. They became gatekeepers. Every PR
needed their review. They were in every planning meeting. When one left the company, the team panicked.

**The fear factor:** The service was so central that breaking it broke _everything_. Developers stopped refactoring. "It
works, don't touch it" became the rule. Technical debt accumulated because the risk of change felt too high.

**The testing nightmare:** Integration tests for one checkout path didn't catch interactions with promotional logic
three
methods away. Functional tests took minutes (or hours) to run and broke for unrelated reasons.

Here's what nobody says out loud: the god service didn't slow delivery _at first_. It accelerated it. That's what made
it
dangerous. By the time the pattern became a bottleneck, it was a weight-bearing architecture. Ripping it out would halt
development of new features, in some estimates, for months.

### The Organizational Force

Metrics obsession drove this pattern into the ground.

Leadership measured **velocity**: features shipped per sprint. Modifying `PlatformService` shipped features fast because
"everything was in one place." Refactoring into cohesive boundaries would look like a sprint with no "user-facing" work.
So teams kept adding to the pile, and kept hitting their velocity goals.

The architecture mirrored the incentive structure, and the incentive structure rewarded short-term velocity over
long-term adaptability.

### What Actually Scales

Here's the alternative they eventually moved toward:

```java
public class CheckoutWorkflow {

    private final PricingEngine pricing;
    private final InventoryAllocator inventory;
    private final PaymentProcessor payments;
    
    public CheckoutWorkflow(PricingEngine pricing, InventoryAllocator inventory, PaymentProcessor payments){
         this.pricing = pricing;
         this.inventory = inventory;
         this.payments = payments;
    }

    public Receipt process(Order order) {
        pricing.applyPricing(order);
        inventory.reserve(order);
        payments.charge(order);
        return Receipt.from(order);
    }
}

public class ItemPricingEngine implements PricingEngine {
    public void applyPricing(Order order) {
        // Handles promotions, tax, discounts
        // Owns its domain, doesn't leak into checkout orchestration
    }
}

public class DefaultInventoryAllocator implements InventoryAllocator {
    public void reserve(Order order) {
        // Handles inventory logic
        // Team can modify without touching checkout code
    }
}

public class CashPaymentProcessor implements PaymentProcessor {
    public void charge(Order order) {
        // Handles payment logic
        // Team can have multiple for different types of payments
    }
}
```

No god service. Just collaborating objects with clear responsibilities.

**What changed:**

- Teams could modify pricing logic without touching checkout orchestration
- Unit tests became focused: `ItemPricingEngine`, `DefaultInventoryAllocator`, `CashPaymentProcessor` behavior can be
  tested independently
- Knowledge is distributed across teams instead of siloing
- Refactoring became safe. Changing inventory logic didn't risk breaking promotions

The coordination cost dropped because changes stayed local. The fear dropped because boundaries were explicit. The
knowledge bottleneck disappeared because each component was small enough for new developers to understand.

> Centralization of code _feels_ like clarity... until it becomes control.

---

## Pattern #2: The Inheritance Explosion

Retail transactions come in different flavors. Online orders, in-store purchases, enterprise bulk orders, promotional
transactions. The team needed to model these differences.

Inheritance seemed obvious.

```java
public abstract class Order {
    private List<LineItem> items;
    private Customer customer;

    public abstract Money calculateTotal();
    public abstract void validate();
}

public class RetailOrder extends Order {
    @Override
    public Money calculateTotal() {
        return items.stream()
            .map(LineItem::getPrice)
            .reduce(Money.zero(), Money::add);
    }
}

public class OnlineOrder extends Order {
    @Override
    public Money calculateTotal() {
        Money subtotal = super.calculateTotal();
        return subtotal.add(calculateShipping());
    }
}
```

Clean. Each order type overrode the methods that differed. DRY principles were applied. It felt like textbook
object-oriented design.

Then **promotions** arrived.

```java
public class PromotionalOrder extends RetailOrder {
    private Promotion promotion;

    @Override
    public Money calculateTotal() {
        Money subtotal = super.calculateTotal();
        return promotion.apply(subtotal);
    }
}
```

Then seasonal promotions needed special handling.

```java
public class SeasonalPromotionalOrder extends PromotionalOrder {
    @Override
    public Money calculateTotal() {
        Money baseTotal = super.calculateTotal();
        if (isHolidaySeason()) {
            return applyBonusDiscount(baseTotal);
        }
        return baseTotal;
    }
}
```

Then enterprise customers needed bulk pricing that sometimes stacked with promotions, but sometimes didn't.

```java
public class EnterprisePromotionalOrder extends PromotionalOrder {
    @Override
    public Money calculateTotal() {
        // Wait, do we call super.calculateTotal()?
        // Or go back to RetailOrder.calculateTotal()?
        // Enterprise pricing might conflict with seasonal rules...
    }
}
```

Six months in, the hierarchy looked like this:

```
Order
  ├── RetailOrder
  ├── OnlineOrder
  │     └── OnlinePromotionalOrder
  ├── EnterpriseOrder
  │     └── EnterprisePromotionalOrder
  └── PromotionalOrder
        ├── SeasonalPromotionalOrder
        ├── LoyaltyPromotionalOrder
        └── BundlePromotionalOrder
```

Nine subclasses. Methods overriding methods overriding methods. Business logic scattered across the tree. A discount bug
in `SeasonalPromotionalOrder` broke enterprise pricing. Nobody knew why until they traced through four levels of
`super.calculateTotal()` calls.

### Why It Worked Early

Inheritance eliminated duplication. All orders needed customer info, line items, validation. The base class held shared
behavior. Subclasses added specifics. Early code reviews praised it.

Obsession with DRY code felt like craftsmanship.

### Why It Crumbled

Retail domains don't have clean hierarchies, they have compositional behavior.

**Fragile base classes:** Changes to `Order.calculateTotal()` risk breaking seven subclasses in surprising ways.

**Behavioral surprises:** A seasonal discount overrode promotional logic that enterprise customers depended on. The bug
report said "enterprise orders are wrong." The fix required understanding all three levels of inheritance.

**Testing brittleness:** Tests for `RetailOrder` passed. Tests for `PromotionalOrder` passed. Tests for
`SeasonalPromotionalOrder` passed. Production behavior failed because of interactions between overridden methods.

**Onboarding nightmare:** New developers asked "which calculateTotal() is actually called?"  
The answer: "Depends on runtime type, and whether seasonal logic is active, and whether the customer is an enterprise
customer."

Inheritance works when your domain stops evolving. When did **your** domain stop evolving?

### The Organizational Force

Early DRY obsession created this problem.

Code reviews flagged duplication. "We calculate totals in three places. Use inheritance." The team eliminated
duplication
without asking whether the duplication was accidental or essential. Retail pricing and promotional pricing looked
similar but evolved independently.

The patterns crumbled because domain boundaries didn't match the inheritance tree. Business rules changed at different
rates. Seasonal promotions changed monthly. Enterprise pricing changed per contract while retail pricing stayed stable.
The hierarchy couldn't flex with the domain changes.

### What Actually Scales

They eventually moved to composition:

```java
public class Order {
    private List<LineItem> items;
    private Customer customer;
    private PricingStrategy pricing;

    public Order(PricingStrategy pricing) {
        this.pricing = pricing;
    }

    public Money calculateTotal() {
        return pricing.calculate(this);
    }
}

public interface PricingStrategy {
    Money calculate(Order order);
}

public class RetailPricing implements PricingStrategy {
    public Money calculate(Order order) {
        return order.getItems().stream()
            .map(LineItem::getPrice)
            .reduce(Money.zero(), Money::add);
    }
}

public class PromotionalPricing implements PricingStrategy {
    private final PricingStrategy base;
    private final Promotion promotion;

    public Money calculate(Order order) {
        Money basePrice = base.calculate(order);
        return promotion.apply(basePrice);
    }
}

public class EnterprisePricing implements PricingStrategy {
    public Money calculate(Order order) {
        // Enterprise pricing logic isolated
        // Doesn't interact with seasonal promotions
    }
}
```

Now pricing is a capability you compose, not a behavior you inherit.

**What changed:**

- They added loyalty pricing without touching enterprise logic
- Pricing strategies were tested independently
- Combining strategies (promotional + seasonal) was easier without deep inheritance
- Business rules could change independently. Seasonal discount logic didn't risk breaking enterprise contracts

Behavior evolves without hierarchy collapse. New developers read one strategy class instead of tracing through four
levels of overrides.

> The class hierarchy became a historical record of past product decisions. Composition became a way to adapt to future
> ones.

---

## Pattern #3: Layered Architecture Tangles

The team followed the standard playbook: Controllers handle HTTP, Services handle business logic, Repositories handle
data access.

```
controllers/
  RefundController.java
services/
  RefundService.java
  OrderService.java
repositories/
  OrderRepository.java
  PaymentRepository.java
utilities/
  TaxCalculator.java
  DiscountCalculator.java
```

Each layer had a clear purpose. The architecture diagrams looked professional. Code reviews checked that controllers
stayed
thin and business logic lived in services.

Then someone needed to implement refunds.

Refund logic touched everything:

- Reverse the payment
- Recalculate taxes
- Adjust promotional discounts
- Update inventory
- Modify loyalty points
- Notify the customer

The layers couldn't contain it.

```java
// RefundController.java
@PostMapping("/refunds")
public ResponseEntity<RefundResponse> processRefund(@RequestBody RefundRequest request) {
    refundService.processRefund(request);
    return ResponseEntity.ok(new RefundResponse("success"));
}

// RefundService.java
public class RefundService {
    private final OrderRepository orderRepository;
    private final PaymentRepository paymentRepository;
    private final TaxCalculator taxCalculator;
    private final DiscountCalculator discountCalculator;
    private final InventoryService inventoryService;
    private final LoyaltyService loyaltyService;

    public void processRefund(RefundRequest request) {
        Order order = orderRepository.findById(request.getOrderId());

        // Reverse payment - but which layer owns this?
        Payment payment = paymentRepository.findByOrder(order);
        payment.reverse();
        paymentRepository.save(payment);

        // Recalculate tax - utility layer
        Money taxAdjustment = taxCalculator.recalculateTaxForRefund(order);

        // Adjust discounts - another utility
        Money discountAdjustment = discountCalculator.adjustForRefund(order);

        // Update inventory - cross-service call
        inventoryService.returnItems(order.getItems());

        // Update loyalty points - another service
        loyaltyService.adjustPoints(order.getCustomer(), order.getTotal());

        order.markRefunded(taxAdjustment, discountAdjustment);
        orderRepository.save(order);
    }
}
```

The logic was scattered across six classes in four layers. Finding "refund behavior" meant reading code in controllers,
services, repositories, and utilities. No single place in the domain owned **refunds**.

Then the Promotions team needed to change discount calculation for refunds. They modified `DiscountCalculator` and broke
the loyalty point logic that depended on discount timing. The bug took three days to find because the dependency crossed
layers and services.

### Why It Worked Early

Layers felt like organization. As a rule: Controllers don't talk to databases, Services don't handle HTTP.
Code reviews re-enforced the boundaries.

Leadership liked it. "Our architecture follows industry standards."

### Why It Crumbled

Layers should model technology, not domain boundaries.

**Scattered logic:** Refund behavior lived in six places. No team owned it. Changes required touching unrelated files.

**Cross-layer leaks:** `RefundService` knew about payments, taxes, discounts, inventory, loyalty. It wasn't a service—it
was a transaction script in a service-shaped object.

**Coordination overhead:** Changing refund behavior required coordinating across Controllers, Services, Repositories,
and Utilities. Every team had opinions. No team had responsibility.

**Testing confusion:** _Test the controller?_ No need, it's thin. _Test the service?_ It's hard because it coordinates
seven dependencies. _Mock everything?_ Tests are now brittle and need lots of extra code. _Test the workflow?_ Which
layer does that belong in?

The architecture optimized for diagrams, not for the workflows the business actually cared about.

### The Organizational Force

Cargo-cult best practices drove this pattern.

Enterprise consultants pushed layered architecture templates. "This is how professional systems look." Code reviews
enforced layer separation without asking whether the layers mapped to how the business actually thought about features.

The team measured velocity by features shipped. Moving to vertical slices would look like re-architecture work with no
user-facing value. So refund logic kept scattering across layers, and teams kept working around the structure instead of
fixing it.

### What Actually Scales

They eventually carved out vertical workflows:

```java
public class RefundWorkflow {
    private final PaymentGateway payments;
    private final PricingEngine pricing;
    private final InventoryAllocator inventory;
    private final CustomerNotifier notifier;

    public RefundResult process(Order order, RefundRequest request) {
        Money refundAmount = pricing.calculateRefund(order, request);

        payments.refund(order.getPayment(), refundAmount);
        inventory.returnItems(request.getItems());
        order.markRefunded(refundAmount);

        notifier.sendRefundConfirmation(order.getCustomer(), refundAmount);

        return RefundResult.success(refundAmount);
    }
}

public class PricingEngine {
    public Money calculateRefund(Order order, RefundRequest request) {
        // All pricing logic—tax, discounts, promotions—in one place
        // Owns the domain, doesn't leak across layers
    }
}
```

One workflow object per business capability. Refund logic in one place. Pricing logic in one place.

**What changed:**

- Promotions team can change discount logic in `PricingEngine` without touching refund orchestration
- Tests became focused on single functionalities. Testing refund workflow end-to-end, and test pricing independently
- New developers understand refunds by reading one class
- Changes stay local, so they can modify pricing without risking inventory logic

The layers disappeared. Domain boundaries emerged. Teams could modify their areas without coordination meetings.

> A layered architecture without clear domain seams is just a stack of indirect calls.

---

## Pattern #4: Premature Microservices

The team made the split early. "We need to scale, so let's design for it now."

They created five services:

- `orders-service`
- `inventory-service`
- `promotions-service`
- `payments-service`
- `customer-service`

Each service had its own repo, database, deployment pipeline. Clean boundaries on paper. Independence in theory.

Then someone needed to implement `checkout`.

Checkout required:

1. Validate customer account (`customer-service`)
2. Check inventory availability (`inventory-service`)
3. Apply promotional discounts (`promotions-service`)
4. Calculate final price (_which service?_)
5. Charge payment (`payments-service`)
6. Create order (`orders-service`)
7. Reserve inventory (`inventory-service` again)
8. Update customer loyalty points (`customer-service` again)

Eight network calls. Four services. One business transaction.

```java
public class CheckoutOrchestrator {
    private final CustomerServiceClient customerClient;
    private final InventoryServiceClient inventoryClient;
    private final PromotionsServiceClient promotionsClient;
    private final PaymentsServiceClient paymentsClient;
    private final OrdersServiceClient ordersClient;

    public CheckoutResult checkout(CheckoutRequest request) {
        // 1. Validate customer
        Customer customer = customerClient.getCustomer(request.getCustomerId());
        if (!customer.isActive()) {
            return CheckoutResult.failure("inactive customer");
        }

        // 2. Check inventory
        InventoryResponse inventory = inventoryClient.checkAvailability(request.getItems());
        if (!inventory.allAvailable()) {
            return CheckoutResult.failure("items unavailable");
        }

        // 3. Get promotional discount
        PromotionResponse promotion = promotionsClient.validatePromotion(
            request.getPromoCode(),
            request.getCustomerId()
        );

        // 4. Calculate price (wait, who owns this?)
        Money subtotal = calculateSubtotal(request.getItems());
        Money discount = promotion.getDiscountAmount();
        Money tax = calculateTax(subtotal.minus(discount));  // Tax logic duplicated here?
        Money total = subtotal.minus(discount).add(tax);

        // 5. Charge payment
        PaymentResponse payment = paymentsClient.charge(
            request.getPaymentMethod(),
            total
        );
        if (!payment.isSuccess()) {
            return CheckoutResult.failure("payment failed");
        }

        // 6. Create order
        OrderResponse order = ordersClient.createOrder(request, total);

        // 7. Reserve inventory (hope this doesn't fail after payment succeeded)
        inventoryClient.reserve(request.getItems(), order.getId());

        // 8. Update loyalty points
        customerClient.addLoyaltyPoints(request.getCustomerId(), total);

        return CheckoutResult.success(order.getId());
    }
}
```

Looks fine until something fails.

Payment succeeds but inventory reservation fails. Now you need compensating transactions, distributed saga patterns, and
eventual consistency. The simple checkout flow became a distributed systems PhD thesis.

Then debugging got interesting. A checkout failed. Where? Logs were scattered across five services. Trace IDs were lost
between
hops. The Promotions team deployed a breaking API change. Checkout broke in production. The Orders team got paged.

### Why It Worked Early

Microservices sounded responsible. "We're building for scale." Independent deployment meant teams could move fast. Each
service had clear ownership.

Leadership loved it. "We're using modern architecture."

### Why It Crumbled

The domain was still tightly coupled. Splitting services didn't change that.

**Coordination explosion:** Every feature required changes across multiple services. The Promotions team couldn't ship
discount logic without coordinating with Orders and Payments. "Independent" services required joint releases.

**Distributed debugging:** Production issues required tracing through five services with separate logs, separate
monitoring, separate deployment times. A timeout in `inventory-service` manifested as a vague error in `orders-service`.

**Consistency nightmares:** Charge the payment, but inventory reservation fails. Should we refund the payment? What if
the refund fails? Now you need distributed transaction coordinators, sagas, and compensating logic. The 10-line checkout
method became 200 lines of error handling.

**Testing brittleness:** Integration tests required **five** services to be running. The CI pipelines became flaky.
Tests passed
locally, failed in CI because `promotions-service` was on a different version.

**Operational overhead:** Five deployments instead of one. Five databases to monitor. Five sets of logs. Five on-call
rotations. The infrastructure team spent more time managing services than developers spent writing features.

Microservices don't reduce coupling. They redistribute it into places you can't easily see.

### The Organizational Force

Leadership chased the scalability myths. "Netflix uses microservices" became architecture policy. Conferences inevitably
pushed distributed systems. Nobody asked whether Mercato's scale justified the operational cost.

The team split services before learning how to operate distributed systems. Before building observability. Before
understanding domain boundaries. They imported complexity years before they needed it.

### What Actually Scales

They eventually re-aggregated services into domain boundaries:

```java
// Bounded context: Checkout
public class CheckoutService {
    private final PricingEngine pricing;
    private final InventoryAllocator inventory;
    private final PaymentProcessor payments;
    private final CustomerAccount accounts;

    public CheckoutResult process(CheckoutRequest request) {
        Customer customer = accounts.validate(request.getCustomerId());

        Money total = pricing.calculate(request);
        inventory.reserve(request.getItems());
        payments.charge(request.getPaymentMethod(), total);

        customer.addLoyaltyPoints(total);

        return CheckoutResult.success();
    }
}
```

This is neither a monolith nor microservices. A service boundary matched how the business thought about checkout.

**What changed:**

- One deployment for checkout features
- Transactions stayed local as payment and inventory in the same boundary
- Tests ran in milliseconds without network calls
- Debugging meant reading one codebase
- Teams could split later when actual scale demanded it

The services started as a distributed system. They evolved into a modular monolith with clear boundaries. When scale
actually arrived, they extracted the pieces that needed independent scaling—not everything, just the bottlenecks.

> We scaled the architecture before we scaled the problem.
 ---                                                                                                                                                                                                      

## Stepping Back: The Pattern Behind the Patterns

You've just read about four architectural decisions that looked reasonable, worked for a while, then slowly became
organizational liabilities. Each pattern failed in its own way: centralized services became bottlenecks, inheritance
hierarchies became mazes, layers scattered logic, microservices multiplied coordination costs.

But here's what connects them: none of these were obviously bad decisions when they were made. The team that built
Mercato wasn't inexperienced. They weren't ignoring best practices, they were following them. They made choices that any
of us might make, given the same context, the same pressures, and the same industry advice.

So why did these patterns crumble? **The answer isn't in the code.**

Four different architectural choices. Same underlying problem.

None of these patterns failed because the developers were inexperienced. The team knew their craft. They followed
industry advice. They made defensible choices.

### Why these Patterns Failed

The patterns failed because organizational forces pushed them past their breaking point.

#### God Services ← Metrics Obsession

Leadership measured features per sprint. Modifying `PlatformService` shipped features fast because "everything was in
one place." Refactoring into cohesive boundaries would look like a sprint with zero user-facing work.

> The metrics rewarded centralization and the architecture followed.

#### Inheritance Hierarchies ← DRY Obsession

Code reviews flagged duplication. "We calculate pricing in three places. Use inheritance." The team eliminated
duplication without asking whether it was accidental or essential.

> The process rewarded eliminating duplication. The architecture mirrored the code review culture.

#### Layered Tangles ← Cargo-Cult Structure

Enterprise consultants pushed layered architecture templates. "This is how professional systems look." Code reviews
enforced layer separation without asking whether layers matched how the business thought about features.

> The team measured professionalism by adherence to structure. The architecture became performative.

#### Premature Microservices ← Scaling Fear

Leadership heard "Netflix uses microservices" and made it architecture policy. Conferences pushed distributed systems as
best practice. Nobody asked whether Mercato's scale justified the operational cost.

> The industry signaled that microservices meant maturity. The architecture chased credibility.

---

## The Meta-Pattern

> [Technical debt]({{% relref compound-interest %}}) is organizational debt wearing a compiler-approved disguise.

The patterns crumbled because:

- **Incentives optimized for short-term velocity** over long-term adaptability
- **Processes rewarded visible activity** over structural improvement
- **Culture prioritized industry trends** over domain understanding
- **Leadership measured output** instead of sustainable pace

Every architectural choice exists in an ecosystem of incentives. When those incentives misalign with long-term health,
architecture decays. Not because developers make mistakes, but because organizations reward the wrong things.

Here's what makes it insidious: the patterns worked long enough to become entrenched. By the time coordination costs
became visible, rearchitecting would halt feature development. So teams compensated and worked harder, coordinated more,
built workarounds. The metrics stayed steady. Leadership saw success. Developers felt the weight.

The god service didn't fail when it was created. It failed when the team grew and the incentive structure prevented
refactoring.

The inheritance hierarchy didn't fail when code reviews praised it. It failed when business rules evolved independently
and DRY culture prevented untangling.

The layered architecture didn't fail when consultants recommended it. It failed when features cut across layers and
"layer-purity" rules prevented vertical workflows.

The microservices split didn't fail at launch. It failed when coordination costs exceeded any scaling benefit and
sunk-cost fallacy prevented consolidation.

### What Changes

**If you only fix the code**, the organizational forces will recreate the same patterns.

**If the metrics reward velocity over adaptability**, teams will choose short-term speed.

**If code reviews enforce rules without understanding context**, teams will follow structure over domain clarity.

**If leadership measures output without understanding coordination costs**, teams will build around architectural
friction
instead of fixing it.

The patterns that grow aren't just technical choices. They're technical choices aligned with organizational learning.

---

## Patterns for Scaling

You've seen the alternatives threaded through each pattern. Here's why they work.

### Ports and Adapters (Hexagonal Architecture)

Instead of `PlatformService` knowing about Stripe, SendGrid, PostgreSQL, and Redis, isolate those at boundaries.

```java
public interface PaymentGateway {
    PaymentResult charge(PaymentMethod method, Money amount);
}

public class StripePaymentGateway implements PaymentGateway {
    // Stripe-specific logic isolated
}

public class CheckoutService {
    private final PaymentGateway payments;  // doesn't know about Stripe

    public CheckoutResult process(Order order) {
        payments.charge(order.getPaymentMethod(), order.getTotal());
        // ...
    }
}
```

**Why it scales:**

- Swap Stripe for Square without touching checkout logic
- Test checkout without network calls, instead inject a fake gateway
- Infrastructure changes stay at the boundaries
- Domain logic is protected from external API changes

> Change should be isolated at boundaries. Teams can modify adapters without touching domain code.

### Composition Over Inheritance

You saw this with `PricingStrategy`. Instead of subclasses overriding behavior, compose capabilities.

```java
PricingStrategy retail = new RetailPricing();
PricingStrategy seasonal = new SeasonalDiscount(retail);
PricingStrategy loyalty = new LoyaltyBonus(seasonal);

Order order = new Order(loyalty);
```

Behavior stacks. You can combine seasonal + loyalty without creating `SeasonalLoyaltyPromotionalOrder`.

**Why it scales:**

- Add capabilities without modifying the existing classes
- Test all strategies independently
- Combine strategies in ways inheritance can't support
- Business rules can change independently

> Hierarchies freeze assumptions. Composition tolerates evolution.

### Feature-Based Modules (Vertical Slices)

Instead of organizing by technology layer, organize by business capability.

```
checkout/
  CheckoutWorkflow.java
  PricingEngine.java
  InventoryAllocator.java
  PaymentProcessor.java

refunds/
  RefundWorkflow.java
  RefundPricing.java
  InventoryReturn.java

promotions/
  PromotionEngine.java
  DiscountRules.java
```

Teams own features, not layers.

**Why it scales:**

- Promotions team changes discount logic without touching checkout
- Refund features stay in one place and are easier to understand
- Reduce coordination costs as changes stay local
- New developers understand features, not layers

> Vertical slices align code with how the business thinks.

### Explicit Domain Models

Instead of anemic domain objects with services doing all the work:

```java
// Anemic
public class Order {
    private Money total;
    public Money getTotal() { return total; }
    public void setTotal(Money total) { this.total = total; }
}

// Elsewhere, scattered logic
public class OrderService {
    public void applyDiscount(Order order, Discount discount) {
        Money newTotal = order.getTotal().minus(discount.getAmount());
        order.setTotal(newTotal);
    }
}
```

Put behavior where it belongs:

```java
public class Order {
    private Money total;
    private List<Discount> discounts;

    public void applyDiscount(Discount discount) {
        discounts.add(discount);
        this.total = recalculateTotal();
    }

    private Money recalculateTotal() {
        // Logic lives with data
    }
}
```

**Why it scales:**

- Intent is visible in code: `order.applyDiscount()` instead of `orderService.applyDiscount(order)`
- Behavior stays cohesive: discount logic lives with order logic
- Less procedural drift as services don't accumulate random methods
- New developers understand domain objects by reading them

> Objects with behavior, not data bags with services.

### Modular Monolith First

Instead of splitting microservices early, build modules with clear boundaries.

```java
// Modules with interfaces
package com.mercato.checkout;

public interface CheckoutService {
    CheckoutResult process(CheckoutRequest request);
}

// Implementation stays internal
class CheckoutWorkflow implements CheckoutService {
    // Internal details hidden
}
```

Modules can *become* services when scale demands it. But you don't have to pay the coordination cost until you need
independent scaling.

**Why it scales:**

- Boundaries are clear without network overhead
- Modules can extract to services later, if needed
- Teams own modules, not layers
- Refactoring stays local. Change are made to module internals without affecting callers

> Start with boundaries. Split services when scale demands it, not before.
---

### Evolutionary Architecture

Stop calling it "technical debt" like it's something you pay down once. Architecture evolves continuously.

**Practical techniques:**

**Strangler Pattern:** Extract boundaries incrementally. Don't halt features for rearchitecture. Carve seams while
shipping.

**Collaborative Refactoring:** Schedule time for teams to improve structure together. This reduces fear and distributes
knowledge.

**Fitness Functions:** Add automated checks for architectural rules. "No service can depend on more than three others."
Tests fail if these boundaries erode.

**Rotating Ownership:** Move developers between teams periodically. Break knowledge silos and reveals where boundaries
aren't clear.

**Contract Tests:** Define module interfaces. Tests should fail if internal changes break contracts. Refactor Safely
with confidence.

#### The Real Difference

These patterns aren't "better" in some absolute sense. They're better at tolerating change.

God services centralized knowledge. Extracted collaborators distributed it.

Inheritance locked behavior into trees. Composition made behavior flexible.

Layers optimized for diagrams. Vertical slices optimized for features.

Microservices split everything. Modular monoliths split what needed splitting.

The patterns that crumble optimize for elegance, reuse, or industry credibility. The patterns that grow optimize for
learning, change, and team scaling.

---

## Craft Is Evolution, Not Perfection

Here's the uncomfortable question: if your architecture looks exactly the same as it did three years ago, either your
domain stopped evolving or your organization stopped learning.

Most teams choose the third option: compensate. Work harder. Coordinate more. Build workarounds. The metrics stay
steady. Leadership sees success. Developers feel the weight.

That's not craftsmanship, it's organizational dysfunction disguised as engineering discipline.

### Patterns Are Temporary Decisions

Every architectural choice is a hypothesis about the future. God services hypothesize centralization helps. Inheritance
hypothesizes domain behavior maps to trees. Layers hypothesize technology boundaries matter more than feature
boundaries. Microservices hypothesize coordination cost is worth scaling flexibility.

Some hypotheses turn out wrong. That's fine. The problem isn't making wrong choices—it's treating those choices as
permanent.

The teams that thrive evolve their architecture as they learn. The teams that struggle defend their architecture
because "we already built it this way."

Sunk cost fallacy applies to code.

### Architecture Must Reflect Reality

Your architecture should match:

- How the business thinks about features
- How teams are organized
- How domain concepts relate
- How frequently different pieces change

If your architecture doesn't match reality, one of two things happens:

**Option 1:** The business adapts to the architecture. Features get slower. Simple changes require coordination. Teams
avoid improvements because the structure fights them.

**Option 2:** The architecture adapts to the business. Boundaries shift. Patterns evolve. Teams refactor continuously.

Most organizations choose Option 1 without realizing it. The architecture becomes the constraint, not the business
domain.

### A Challenge

Look at your codebase right now.

**Ask:**

- Is there a service everyone's afraid to touch?
- Is there a class hierarchy nobody fully understands?
- Is there business logic scattered across layers with no clear owner?
- Are there service boundaries that create coordination overhead without providing value?

If yes: those patterns are crumbling. They worked once. They don't work now and continuing to wait won't fix them.

**Ask your organization:**

- Do we measure velocity without measuring coordination cost?
- Do we reward shipping features without rewarding structural improvement?
- Do we follow industry patterns without asking if they fit our context?
- Do we avoid refactoring because leadership sees it as "not delivering value"?

If yes: the organizational forces that created those patterns are still active. Fixing the code won't fix the problem.
The patterns will recreate themselves.

### What You Can Do

You don't need permission to write better code. You do need permission to change how teams work.

**Tactically:**

- Extract seams from god services incrementally
- Replace inheritance with composition one hierarchy at a time
- Carve vertical slices while shipping features
- Consolidate microservices that create coordination overhead

**Strategically:**

- Make coordination cost visible—track how many teams touch each feature
- Make refactoring a team practice, not something individuals do alone
- Build architectural fitness functions so boundaries don't erode silently
- Rotate developers between teams so knowledge distributes

**Culturally:**

- Challenge the metrics—velocity without adaptability is technical debt accumulation
- Challenge the processes—code reviews should ask "does this match our domain?" not just "does this follow the pattern?"
- Challenge the trends—conference talks describe systems at Netflix scale, not your scale

The patterns that crumbled at "_Mercato_" weren't unique. You've seen them. Maybe you've built them. The question isn't
whether you've made these choices, it's whether you're still defending them.

Architecture isn't something you get right once. It's something you evolve continuously. The best systems aren't
elegant, they're adaptable. The best teams aren't the ones that avoid mistakes, they're the ones that learn from them
fast
enough to matter.

If your architecture looks the same as it did three years ago, what does that say about your organization's capacity to
learn?

---

If this resonated, you might also enjoy:

- [Compound Interest Works Both Ways]({{% relref compound-interest %}})
- [Stop Naming Everything `Impl`]({{% relref stop-naming-everything-impl %}})
- [Mocking Frameworks are Code Smells]({{% relref mocking-frameworks-are-code-smells %}})
