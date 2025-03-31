---
title: 'TDD: The Ultimate ADHD-Friendly Development Practice'
date: 2025-03-10 13:01:26 -0900
draft: false
description: How Test-Driven Development helps with cognitive overload, decision paralysis, and debugging distractions.
thumbnail:
  url: /img/testing-center.jpg
  author: Joshua Lawrence
  authorURL: https://unsplash.com/@orangetiephotography
  originURL: https://unsplash.com/photos/yellow-and-black-no-parking-sign-KlQE824pwxs
  origin: Unsplash

author: Paige Watson
tags:
  - ADHD
  - Neurodiversity
  - Software Development
  - Quality Code
  - Test-Driven Development
---

If you have ADHD, traditional software development workflows can feel overwhelming. Large tasks, vague requirements, and
long debugging sessions create mental roadblocks that make it hard to start, stay on track, or finish without
distraction. But what if there was a way to break down work into **tiny, manageable steps** while constantly getting
feedback that keeps you engaged?

That’s exactly what **Test-Driven Development (TDD)** does for me. Instead of trying to hold an entire problem in my
head at
once, TDD forces me to take one small step at a time—reducing cognitive overload, preventing decision paralysis, and
eliminating debugging distractions.

For me, adopting TDD was one of the biggest game-changers in managing my ADHD while coding. In this post, I’ll explain
why TDD is an ADHD-friendly practice, how it reduces common struggles like being overwhelmed and working memory issues,
and walk through a simple example to show how it works in action.

## Why ADHD Brains Struggle with Traditional Coding Approaches

ADHD affects the way we approach complex problems. We often experience:

1. **Cognitive Overload** – Trying to hold too many details in our heads at once leads to mental exhaustion.
2. **Decision Paralysis** – Not knowing where to start makes it difficult to begin coding.
3. **Hyper-Focus** – Diving deep into code can spiral into endless rabbit holes.

Most traditional coding approaches make these challenges worse. Writing large amounts of code before testing it means
keeping multiple things in working memory: what the code is _supposed_ to do, how it fits into the bigger system, and
all
the possible edge cases. When something breaks, debugging is chaotic—leading to frustration, wasted time, and
distraction.

TDD flips this process on its head by **reducing cognitive load**, **providing a clear starting point**, and
**removing the need for debugging** sessions.

## How TDD Works with ADHD Thinking

Test-Driven Development follows a simple cycle:

1. **Write a failing test** (_Red_)
2. Make it pass with **the simplest possible solution** (_Green_)
3. **Refactor** the code to improve it (_Refactor_)

This aligns perfectly with how ADHD brains work:

- **Breaking work into tiny steps**: This helps me to not get overwhelmed
- **Immediate feedback loops**: This keeps the code engaging and gives me the Dopamine hit that I crave
- **A structured process**: It reduces decision paralysis, because I know practice, and can rely on my tests to assure
  that I am writing code that satifies the requirement I am working on.
- **No debugging rabbit holes**: Failing tests tell you exactly where the issue is, and due to the small size of the
  code I can immediately pinpoint the issues.

Instead of trying to solve an entire problem in one go, TDD forces you to focus on **just one small step at a time**.

## TDD in Action: A Simple Example

Let’s say we need to write a function that adds two numbers together. Instead of jumping in and writing the function
immediately, we follow the **TDD cycle**.

### Step 1: Write a Failing Test (Red)

Before we write any actual implementation, we first write a test that describes what our function should do:

```java
public class CalculatorTest {
   @Test
   public void addingTwoAndThree_ReturnsFive() {
      Calculator calc = new Calculator();
      int result = calc.add(2, 3);
      assertThat(result).isEqualTo(5);
   }
}
```

We haven’t written the add method yet, so this test fails. That’s good! It tells us exactly what we need to do next.

### Step 2: Write the Simplest Code to Make the Test Pass (Green)

Now, we implement just enough code to pass the test:

```java
public class Calculator {
   public int add(int a, int b) {
     return 5;
   }
}
```

When we run the test again, it passes. We’ve written functional code without overthinking, debugging, or getting
distracted.

### Step 3: Refactor if Necessary (Refactor)

The code is already simple, so there’s nothing to refactor here. But if this were a more complex problem, this step
would let us clean up the code while still being confident it works—because our test will immediately catch mistakes.

### Repeat from Step 1 (Red)

This time we can add another version of the test to **triangulate and achieve the behavior that we want**:

```java
public class CalculatorTest {
   @Test
   public void addingTwoAndThree_ReturnsFive() {
      Calculator calc = new Calculator();
      int result = calc.add(2, 3);
      assertThat(result).isEqualTo(5);
   }
   @Test
   public void addingOneAndTwo_ReturnsThree() {
      Calculator calc = new Calculator();
      int result = calc.add(1, 2);
      assertThat(result).isEqualTo(3);
   }
}
```

Of course, now we can update the function to pass both tests:

```java
public class Calculator {
   public int add(int a, int b) {
     return a+b;
   }
}
```

Then refactor, if necessary.

## How TDD Helps with ADHD Struggles

### 1. Reduces Cognitive Overload

Instead of juggling multiple requirements in your head, TDD lets you focus on **one small thing** at a time. When each
test is written, it acts as a guide, reducing the need to remember what you were working on.

**Before TDD:** “_Wait, what was I trying to do again?_”  
**With TDD:** “My failing test tells me exactly what to do next.”

### 2. Eliminates Decision Paralysis

ADHD brains struggle with figuring out where to start, especially when the task feels _big or ambiguous_. TDD removes
this problem by making the next step obvious: write a test, make it pass, repeat.

**Before TDD:** “_Ugh, this feature is huge. Where do I even begin?_” (_Queue the paralyzing overload_)  
**With TDD:** “I’ll start by writing the simplest failing test.”

### 3. Prevents Debugging Distractions

Debugging is a common ADHD trap. Without a clear process, it’s easy to get sucked into irrelevant details or chase
tangents that don’t actually solve the problem. TDD prevents this because failing tests immediately pinpoint the
issue, eliminating guesswork.

**Before TDD:** “_Why is this not working? Let’s print debug logs for the entire app…_”  
**With TDD:** “There's a defect in the code somewhere. Let's write a failing test that replicates the defect. When the
tests pass, we'll know we fixed it.”

### 4. Keeps Engagement High

ADHD brains thrive on immediate feedback and visible progress. TDD provides a steady stream of small wins—each
passing test feels like a mini dopamine hit, keeping motivation strong.

**Before TDD:** “_Ugh, I’ve been coding for hours, and I don’t even know if this works yet_.”  
**With TDD:** “Yes! My test just passed! On to the next one.”

## Conclusion: TDD as a Tool for ADHD-Friendly Coding

Test-Driven Development isn’t just a best practice for writing high-quality code, it’s a lifeline for ADHD developers. By
breaking work into small, manageable steps, providing clear direction, and eliminating debugging chaos, TDD turns an
overwhelming coding session into a structured, engaging workflow.

If you struggle with focus, task paralysis, or distractions while coding, give TDD a try. It might just be the key to
working with your ADHD brain instead of against it.

In the next post, I’ll dive into another ADHD-friendly development strategy:
**Mob Programming and Body Doubling—How Collaboration Helps ADHD Developers Stay on Track.**
