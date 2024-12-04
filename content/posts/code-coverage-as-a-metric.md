---
title: 'Code Coverage as a Metric'
date: 2024-12-04T09:53:19-08:00
draft: true
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
How many times have we heard a team or manager brag about the level of test coverage in their code base.  "We have 80% Code Coverage on all our services!"
My first thought when I hear this is summed up nicely in a quote from **Steve Kuo**: "What 20% of the code is it ok for there to be a significantly higher chance of defects and less maintainability?"  

## Code Coverage Definition
Before going into my thoughts on the use of code coverage as a metric, I want to set the definition of what "Code Coverage" means when I talk about it.


According to [Wikipedia](https://en.wikipedia.org/wiki/Code_coverage):
"In software engineering, code coverage, also called test coverage, is a percentage measure of the degree to which the source code of a program is executed when a particular test suite is run."


[Sonarqube](https://www.sonarsource.com/) uses a [mathematical formula](https://docs.sonarsource.com/sonarqube-server/9.9/user-guide/metric-definitions/#tests) to calculate coverage based on evaluating testing of line and conditionals within a file:
> Coverage (coverage): A mix of **Line coverage** and **Condition coverage**. It's goal is to provide an even more accurate answer the question  
> 'How much of the source code has been covered by the unit tests?'.
>
> Coverage = (CT + LC)/(B + EL) where:  
> CT = conditions that have been evaluated to 'true' at least once  
> CF = conditions that have been evaluated to 'false' at least once  
> LC = covered lines = linestocover - uncovered_lines  
> B = total number of conditions  
> EL = total number of executable lines (lines_to_cover)  

Using these definitions and formulas, we can get a number as a percentage of our code that has been evaluated by automated tests, either unit, integration or functional in nature.

## The tyrrany of metrics
