---
title: Refactoring Legacy Code
date: 2024-11-25 15:00:26 -0900
draft: false
description: Legacy code can be a beast:: fragile, complex, and often lacking the necessary tests to ensure changes don’t introduce defects.
thumbnail:
  url: /img/strangler-fig.jpg
  author: David Clode
  authorURL: https://unsplash.com/@davidclode
  origin: https://unsplash.com/photos/brown-tree-with-green-leaves-aLL-IrVdW0c
  originName: Unsplash

tags:
  - Quality Code
  - Refactoring
  - Legacy Code
---

## Refactoring Legacy Code

Legacy code can be a beast: fragile, complex, and often lacking the necessary tests to ensure changes don’t introduce
defects. But fear not! There are techniques you can use to effectively work with and extend it in a safe and effective
manner.

We will delve into:

- Managing and improving legacy code
- Utilizing Test-Driven Development (TDD) effectively
- Applying the Strangler Fig Pattern to incrementally refactor code without breaking existing functionality

### Learning Outcomes
- Understand the concepts of the Strangler Fig Pattern
- Use Interfaces and Dependency Injection to isolate legacy code to be changed
- Learn the benefits for using the Strangler Fig Pattern as opposed to an application rewrite

### Presentation Dates
{{< table "table-hover" >}}
| Date       | Location                                                                                 | Recording Link                                         |
|------------|------------------------------------------------------------------------------------------|--------------------------------------------------------|
| 2024-07-09 | [Tek Caffe](https://www.linkedin.com/company/tek-caffe/)                                          | [YouTube](https://www.youtube.com/live/5k5r6QMt6Xk)                |
{{< /table >}}

### Resources
[Slide Deck](https://prezi.com/p/edit/7zadgc933w57/)

### Links
[Bad Elevator](https://github.com/MyTurnyet/BadElevator) code base for practice (Java)  
Llewellyn Falco's [Youtube talk](https://youtu.be/wp6oSVDdbXQ?si=yUx2lLEwks8TZB-t) on referenced in the Tek Caffe video