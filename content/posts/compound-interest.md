---
title: "Compound Interest Works Both Ways"
date: 2025-10-16 07:48:26 -0900
draft: true
description: "Every shortcut is a loan against your future velocity, and the interest rate is brutal."
thumbnail:
  url: /img/street-money-sign.jpg
  author: Aleksandr Popov
  authorURL: https://unsplash.com/@5tep5?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText
  originURL: https://unsplash.com/photos/people-walking-on-street-during-night-time-iQqqo2zpmTI
  origin: Unsplash

tags:
  - Quality
  - Design
  - Architecture
  - Delivery
---

Picture this: You have a \$5,000 balance on a credit card with a 22% APR. You make the minimum payment of \$150 every
month, thinking you're being responsible. A year later, you've paid $1,800 but your balance has only dropped to \$4,300.
You paid nearly two grand and barely made a dent. The rest went to interest.

That's {{< link "https://en.wikipedia.org/wiki/Compound_interest" >}}compound interest{{< /link >}} working against you.
Small debts that seem manageable today become crushing burdens tomorrow
because the cost grows exponentially. The math is elegant and merciless.

Here's the uncomfortable truth about software development: every shortcut you take, every time you skip the craft
practices that make code maintainable, you're taking out a loan. And the interest rate? It's brutal. That "quick hack"
to ship by Friday becomes the foundation that three other features build on top of. Now changing it requires touching a
dozen files instead of one. What took an hour to write will take three days to fix, if you can even afford to fix it at
all. You're not moving faster. You're borrowing velocity from your future self, and the interest compounds daily.

## The Visibility Problem

Your office has a leaky roof. Water is dripping into the conference room. How long before someone fixes it? Hours, maybe
a day. A security breach exposes customer data. You mobilize a war room immediately. Revenue drops 10%
quarter-over-quarter. Every executive is in crisis mode. Customer churn spikes. You throw resources at retention. These
problems are visible. They hurt. They demand attention.

### Why Technical Debt Doesn't Ring Alarm Bells

{{< link "https://martinfowler.com/bliki/TechnicalDebt.html" >}}Technical debt{{< /link >}} is silent. Code that takes
three times longer to change than it should? That gets normalized. "That's
just a complex part of the system." Developers spending 60% of their time tracking down mystery bugs that shouldn't
exist? "That's just how it is here." A feature that should take a week taking a month because the foundation is so
brittle? "This code is old, what do you expect?"

The compounding is invisible {{< link "https://c2.com/doc/oopsla92.html" >}}until it becomes catastrophic{{< /link >}}.
Each "just this once" decision seems perfectly rational in
isolation. We'll skip writing tests this sprint—we're behind schedule. We'll copy-paste this code instead of refactoring
the abstraction—it's faster. We'll merge this PR without proper review—the customer is waiting. Every single choice
makes sense at the moment. But compound interest doesn't care about individual moments. It cares about trajectories.

Here's the key insight: companies can't feel technical debt in real-time the way they feel customer churn or cost
overruns. The credit card sends you a statement every month showing exactly how much you owe. Technical debt has no
statement. It shows up as "development is slower than it used to be" or "we can't ship features as fast as our
competitors." By the time it's visible enough to demand attention, you're already paying crushing interest on a massive
principal.

## The Prevention Paradox

Let me tell you about two developers at the same company.

Developer A worked all weekend. The production system went down Friday evening. It was a {{<
link "https://en.wikipedia.org/wiki/Cascading_failure" >}}cascading failure{{< /link >}} that took out the
payment processor. Customers couldn't check out. Revenue stopped. Developer A pulled an all-nighter debugging, found the
race condition, deployed a fix, and had the system back up by Sunday morning. Monday's all-hands meeting opens with the
CEO personally thanking Developer A. "This is the kind of dedication that makes us great." Developer A gets a spot bonus
and becomes the obvious candidate for the next promotion.

Developer B shipped three features last quarter. They all went smoothly into production. No late-night pages. No
emergency deploys. No customer complaints. Developer B's code is well-structured, thoughtfully designed, and carefully
validated before it ships. When other developers need to modify Developer B's work, it takes them the expected amount of
time because the code is clear and maintainable. Developer B's name never comes up at the all-hands.

### Why Craft Looks Like a Luxury

Here's the uncomfortable question: Which developer created more value?

The honest answer is probably Developer B. But you'd never know it from how they're recognized. Developer A is visible
because problems are visible. Developer B is invisible because prevention is inherently invisible. The outages that
never happened, the bugs that never existed, the features that shipped on schedule because the foundation was solid—none
of that triggers your organizational alarm bells.

This is the {{< link "https://en.wikipedia.org/wiki/Prevention_paradox" >}}prevention paradox{{< /link >}}. Good craft
practices are insurance. They prevent problems from happening in the first
place. But insurance doesn't generate dopamine hits. Nobody celebrates the fire that never started. Nobody throws a
party for the weekend you didn't have to work.

And here's where it gets insidious: we've created a {{< link "https://en.wikipedia.org/wiki/Perverse_incentive" >
}}perverse incentive structure{{< /link >}}. Organizations that consistently reward
visible problem-solving over invisible problem-prevention end up creating a culture that actually needs fires to justify
its heroes. Why spend time on thoughtful design when the real career advancement comes from weekend heroics? The system
literally incentivizes creating the conditions for future emergencies.

What happens when developers try to push back? When they raise concerns about the growing technical debt, about the
shortcuts that are compounding, about the need to invest in craft before the system becomes unmaintainable? They get
dismissed.

"We don't have time for that right now." "That's gold-plating." "Perfect is the enemy of good." "The business needs
features, not {{< link martin-fowlers-refactoring >}}refactoring{{< /link >}}." "We'll come back to that later." These
phrases are so common they've become
mantras—comfortable ways to silence uncomfortable truths. The developer who says "we need to slow down and do this
right" gets labeled as an obstructionist, someone who doesn't understand the business pressure, someone who isn't a team
player.

Meanwhile, the same organization will mobilize instantly when the accumulated debt causes a crisis. Suddenly there's
time. Suddenly there's budget. Suddenly leadership understands that quality matters. But only after the compound
interest has already done its damage.

## The Root Cause

Let's be honest about what's actually happening here. The pressure is real. The quarterly earnings call is real. The
board meeting where you have to show progress is real. The OKRs you committed to are real. The customer who's
threatening to churn if you don't ship that feature is real. I'm not dismissing any of this.

But here's what's also real: most organizations have turned short-term pressure into a perpetual state of emergency.
It's not that you're occasionally in crisis mode—crisis mode has become your default operating procedure. Every sprint
is urgent. Every release is critical. Every quarter is make-or-break. And when everything is an emergency, nothing is an
emergency. You've just normalized dysfunction.

### Short-Term Cycles Create False Urgency

Watch what happens in your organization. The sprint is two weeks. The team estimates they can deliver five features if
they maintain reasonable engineering practices. Management pushes for seven. "The market won't wait." "Our competitors
are moving faster." "We need this to hit the quarter." So the team commits to seven and drops the practices that make
development sustainable. Ship now, clean up later.

Except "later" never comes. Because next sprint? Also urgent. Next quarter? Also critical. Next year? Well, now the
codebase is so fragile that making any change risks breaking something else, so you're moving even slower, which creates
even more pressure to cut corners, which makes you even slower. The compound interest is compounding.

What actually happens when you promise "we'll clean it up later"? Let me tell you exactly what happens. That quick hack
you shipped? Three months later, it's the foundation for two other features. Now you can't refactor it without
coordinating across multiple teams. Six months later, it's part of a customer-facing API that you've documented. Now you
can't change it without a deprecation cycle and migration plan. A year later, nobody remembers why it was built that
way, but everyone's afraid to touch it because "it works and we don't have time for a production incident right now."

You didn't defer the work. You made it exponentially more expensive. That one-hour shortcut now requires a multi-team,
multi-quarter initiative with technical design reviews, migration plans, and customer communication. The interest has
compound so thoroughly that you can't afford to pay the principal anymore.

And the culture? It amplifies every part of this cycle. You celebrate the team that crunched to ship seven features,
even though five would have been sustainable. That teaches everyone that heroics are valued over sustainability. Which
reinforces short-term thinking. Which creates more emergencies. Which requires more heroics. The system feeds itself.

Here's the uncomfortable truth: most organizations aren't in an existential crisis. They're in perpetual false urgency.
There's a difference, and it matters.

## Rare Exception vs. Common Delusion

I want to be clear: genuine constraints exist. There are moments when an organization faces a real, existential threat
that justifies extraordinary measures. The early-stage startup with three months of runway and no clear path to revenue.
The company facing a competitive threat so immediate and severe that failing to respond now means irrelevance. The
regulatory deadline that will literally shut down your business if you miss it.

These situations are real. They're just extraordinarily rare.

Here's what distinguishes genuine emergency mode from perpetual false urgency: Genuine emergency mode is time-boxed. You
can point to a specific end date or trigger condition. "We have until the end of Q2 to land this customer, or we're out
of business." "We need to ship compliance features by December 15th, or we lose our license to operate." There's a
finish
line.

Genuine emergency mode is explicit. Everyone knows why the emergency exists and what success looks like. There's
conscious acknowledgment that you're taking on debt and a concrete plan for how you'll recover once the emergency
passes. "We're skipping testing for the next six weeks, and we're allocating the entire following quarter to
stabilization and paying down technical debt."

Genuine emergency mode is exceptional. It's not your operating rhythm. It's a deviation from the norm that everyone
recognizes as unsustainable and temporary.

Perpetual false urgency? It has none of these characteristics. There's no finish line—next quarter is always just as
urgent. There's no explicit acknowledgment of the trade-offs—cutting corners is just "how we work." There's no recovery
plan—the debt accumulates indefinitely. It's not exceptional, it's the default.

So here's the question you need to ask yourself honestly: Which one describes your organization?

Are you genuinely in a rare, time-boxed crisis with a clear end state and a plan to recover? Or have you simply
normalized operating in a state of permanent emergency because it's the only mode you know?

Most organizations will claim they're the exception. "You don't understand our competitive landscape." "Our industry
moves too fast." "We're still proving ourselves to investors." "We're in growth mode." These explanations feel
compelling from the inside. But statistically, most of you reading this are not the exception. You're the norm. You've
just gotten so accustomed to the compound interest payment that you've forgotten what sustainable velocity feels like.

The trap is that claiming exception status lets you avoid the uncomfortable acknowledgment that you have a choice. As
long as you believe you're in genuine crisis mode, you can tell yourself that cutting corners is forced upon you. But if
you're in perpetual false urgency—and most of you are—then you're choosing this. Every day, you're choosing to pay
compound interest instead of building compound growth.

## What This Really Means

Let's strip away the comfortable abstractions and name what's actually happening.

You are always making a choice. There is no neutral position. Every time you ship code, you're either investing in your
future capacity or borrowing against it. When you tell yourself you're "just being pragmatic" or "balancing business
needs with engineering concerns," you're not avoiding the choice: you're choosing to pretend the choice doesn't exist.

Skipping craft practices isn't "moving faster." Stop using that language. It's lying to yourself. You are taking out a
loan against your future velocity. The feature ships today, but the codebase becomes harder to change tomorrow. That's
not speed, that's taking out a loan, and like any loan, it comes with interest. Compounding interest.

The question isn't "can we afford to invest in quality?" That's the wrong question, and it's designed to make craft
sound like a luxury. The real question is: "Can we afford the exponentially growing cost of not investing?" Because that
cost is not optional. You're paying it whether you acknowledge it or not. It shows up as longer development cycles, more
bugs, more production incidents, more time spent debugging instead of building, and eventually, the complete inability
to respond to market changes because your codebase is too fragile to modify safely.

### Making the Implicit Explicit

So let's name the trade-offs clearly. Right now, today, with the choices you're making about engineering practices, you
are choosing:

**Short-term feature delivery over long-term organizational velocity.** You're optimizing for what ships this quarter at
the expense of what you'll be able to ship next year. That might be the right choice, but own it. Don't pretend you're
doing both.

**Visible heroics over sustainable pace.** You're rewarding the dramatic saves instead of the boring prevention. You're
creating a culture where people are incentivized to work in ways that create emergencies. That might be what you want,
but say it out loud.

**Quarterly results over compound growth.** You're choosing to pay compound interest instead of earning it. Every
quarter, you're a little slower than you could have been. Every year, the gap between where you are and where you could
be gets wider. That might be acceptable to you, and that's fine, but acknowledge the trajectory your choices put your
company on.

**Crisis mode over intentional improvement.** You're choosing to operate in a state where there's "never time" to fix
the
underlying issues because you're always fighting fires. And many of those fires exist because you made this same choice
last quarter. That might be unavoidable, but at least be honest that it's a choice.

Here's the thing: these might be the right choices for your organization _at this moment_. I'm not here to tell you that
you're wrong. Maybe you are in that genuinely rare moment where the existential threat justifies extraordinary measures.
Maybe you've consciously decided that you'd rather optimize for short-term results and accept the compound interest
cost. Maybe you've run the numbers and determined that the technical debt you're taking on is worth the market position
you'll gain.

Those can be defensible decisions. But they're only defensible if you're honest about what you're choosing and what it
costs. The problem isn't that organizations make trade-offs. The problem is that most organizations make these
trade-offs implicitly, without acknowledgment, without measurement, and without any plan for how to recover. They treat
it as inevitable rather than chosen. They pretend there's no alternative rather than owning the decision.

You have a choice. You're making it right now. The question is: are you making it consciously, or are you letting it
happen by default?

## Starting the Conversation

If you've made it this far, you're probably feeling uncomfortable. Good. That's the point. But let me be clear about
something: this isn't about blame.

This isn't about pointing fingers at managers who pushed for too many features, or executives who set aggressive
timelines, or developers who took shortcuts. Those are all symptoms of systemic misalignment. The real issue is that
most organizations have created systems where rational actors, making locally sensible decisions, collectively produce a
compounding disaster.

The fix isn't individual heroics. It's not about developers working harder to "do it right" despite organizational
pressure. It's not about managers suddenly "getting it" and giving engineering unlimited time. It's about changing the
system itself—changing what you measure, what you celebrate, and what you incentivize.

So here are some questions to ask in your organization. Not to start a fight, but to start a conversation:

**What percentage of your engineering time goes to unplanned work and firefighting?** Track it for a month. If it's more
than 20%, you're not building a product, you're servicing debt. And that number compounds.

**Who gets recognized and promoted?** Look at your last three promotions or performance reviews. Were they the
firefighters or the fire preventers? The people who pulled weekends to fix emergencies, or the people whose code never
created emergencies? What you reward is what you'll get more of.

**When you skip craft practices to hit a deadline, do you have a concrete plan to pay back that debt?** Not "we'll do it
later." An actual plan. Time allocated. Committed to. If the answer is no, stop calling it a loan. Call it what it is:
permanent damage.

**Are you in genuine emergency mode, or have you normalized perpetual crisis?** Be honest. Use the criteria from
earlier: time-boxed, explicit, exceptional. If you can't point to a specific end date and recovery plan, you're not in
emergency mode. You're in dysfunction mode.

**What would compound growth look like for your engineering organization?** Not just shipping features, but getting
faster at shipping features. Building capability that makes the next feature easier than the last one. That's what craft
practices create. That's what you're trading away.

The philosophical shift needed here is fundamental. You need to change what you measure. Stop measuring only feature
output. Start measuring cycle time trends. Measure unplanned work percentage. Measure time-to-fix for bugs. Measure how
many times you have to touch a piece of code to get it right. These are leading indicators of technical health.

Change what you celebrate. Stop throwing parties for weekend war rooms. Start recognizing the teams whose releases are
boring because they're smooth. Start celebrating the refactoring that prevented the outage that never happened. Make
prevention visible.

Change what you incentivize. If your bonus structure, promotion criteria, and performance reviews all reward short-term
feature delivery and visible heroics, don't be surprised when that's what you get. You need to explicitly value
sustainable pace and prevention.

Here's the crucial part: I'm talking about principles, not prescriptions. I'm not here to tell you that you need to do
{{< link tdd-wikipedia >}}TDD{{< /link >}}, or {{< link pair-programming-wikipedia >}}pair programming{{< /link >}},
or {{< link mob-programming-wikipedia >}}mob programming{{< /link >}}, or any specific practice. Different
organizations, different contexts,
different practices. What matters is the mindset shift: treating sustainable quality as an investment that generates
compound returns, not a cost that slows you down.

The specific practices are just implementations of that mindset. The mindset is what changes the trajectory from
compound interest working against you to compound interest working for you.

## The Uncomfortable Truth

If you're still reading this, you probably already know this is true in your organization. You've seen the patterns.
You've felt the compound interest payments. You've watched the velocity slow down quarter after quarter. You've heard
the developers raise concerns and watched those concerns get dismissed. You've been in the meetings where "we'll come
back to that later" turns into "we can't afford to fix this now."

The question isn't whether you understand the problem. You do. The question is whether you're willing to acknowledge the
choice you're making.

Because here's the thing about compound interest: it works both ways. Every day you choose the shortcut, you're choosing
exponential drag on your future. Every day you invest in craft, you're choosing exponential growth. Every sprint you
push for unsustainable velocity, the compound interest grows. Every sprint you protect sustainable practices, the
compound returns accumulate.

The math is elegant and merciless. You can't opt out. You're on one curve or the other. The only question is which one.

The conversation starts with honesty. Stop pretending there's no trade-off. Stop claiming you're the rare exception when
you're the common case. Stop treating technical debt as inevitable when it's chosen. Start talking honestly about which
compound interest curve you're actually on and whether that's the trajectory you want for your organization.

You have a choice. You're making it right now. Make it consciously.
