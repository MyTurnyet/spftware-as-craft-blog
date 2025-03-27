---
title: 'Code Coverage as a Metric'
date: 2024-12-04 15:00:26 -0900
draft: false
description: Code Coverage is a terrible metric and gives a false sense of security.
thumbnail:
  url: /img/measuring-tape.jpg
  author: Mark Wilkinson Hughes
  authorURL: https://unsplash.com/@markowihu
  originURL: https://unsplash.com/photos/a-tape-measure-is-on-a-wooden-table-VdB1EHqEzX0
  origin: Unsplash

author: Paige Watson
tags:
  - Quality
  - Testing
  - Metrics
  - Code
---

How many times have we heard a team or manager brag about the level of test coverage in their code base.  "We have 80%
Code Coverage on all our services!"
My first thought when I hear this is summed up nicely in a quote from **Steve Kuo**: "What 20% of the code is it ok for
there to be a significantly higher chance of defects and less maintainability?"

## Code Coverage Definition

Before going into my thoughts on the use of code coverage as a metric, I want to set the definition of what "Code
Coverage" means when I talk about it.

According to [Wikipedia](https://en.wikipedia.org/wiki/Code_coverage):
"In software engineering, code coverage, also called test coverage, is a percentage measure of the degree to which the
source code of a program is executed when a particular test suite is run."

[Sonarqube](https://www.sonarsource.com/) uses
a [mathematical formula](https://docs.sonarsource.com/sonarqube-server/9.9/user-guide/metric-definitions/#tests) to
calculate coverage based on evaluating testing of line and conditionals within a file:
> Coverage (coverage): A mix of **Line coverage** and **Condition coverage**. It's goal is to provide an even more
> accurate answer the question  
> 'How much of the source code has been covered by the unit tests?'.
>
> Coverage = (CT + LC)/(B + EL) where:  
> CT = conditions that have been evaluated to 'true' at least once  
> CF = conditions that have been evaluated to 'false' at least once  
> LC = covered lines = linestocover - uncovered_lines  
> B = total number of conditions  
> EL = total number of executable lines (lines_to_cover)

Using these definitions and formulas, we can get a number as a percentage of our code that has been evaluated by
automated tests, either unit, integration or functional in nature.

## The tyrrany of metrics

The problem with a metric like "Code Coverage" is that it focuses and rewards an outcome, and not a behavior.

In
_[The Tyranny of Metrics](https://www.amazon.com/Tyranny-Metrics-Jerry-Z-Muller-ebook/dp/B07K458MZG)_, [Jerry Z. Muller](https://press.princeton.edu/our-authors/muller-jerry-z)
argues that an over-reliance on quantitative metrics often leads to counterproductive behaviors, where the numbers
themselves become the goal rather than the underlying quality they were meant to measure. This phenomenon is
particularly evident in software development, where code coverage is frequently used as a proxy for test quality.
Teams aiming for an arbitrary coverage percentage—say, 90%—often end up writing superficial or meaningless tests just to
satisfy the metric, rather than focusing on whether those tests genuinely improve the reliability and maintainability of
the system.  
To paraphrase [Goodhart's Law](https://en.wikipedia.org/wiki/Goodhart%27s_law): When coverage becomes a target rather than an informative tool, it encourages gaming the system rather than
writing thoughtful, valuable tests.

> "When a measure becomes a target, it ceases to be a good measure"  
> -- Charles Goodhart

Code coverage numbers fail as a meaningful measure of quality because they tell us what code has been executed during
tests but say nothing about whether the tests are actually effective. A suite with 100% coverage can still miss critical
edge cases, lack assertions, or fail to catch regressions if it is composed of weak, poorly structured tests. Meanwhile,
a lower coverage percentage with well-designed tests that target high-risk areas of the codebase can provide far greater
confidence in the system. High coverage might look impressive in a report, but without considering the depth, intent,
and robustness of the tests themselves, it remains a shallow and misleading indicator of true software quality.
