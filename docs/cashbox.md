---
hide:
  - toc
---

# Cashbox

[https://github.com/matt328/cashbox](https://github.com/matt328/cashbox)

Cashbox is a playground to experiment with Angular and various 'serverless' backends. The current
implementation uses Google's Firebase. It uses the domain of simple budget tracking, and is admittedly a bit out of date at this point with Angular 12.

Design goals:

- Keep things simple and use pure, idiomatic Angular concepts with as few external dependencies as
  is practical.
- Use realtime asynchronous server communication so that multiple users can collaborate on a budget
  simultaneously. This is not all that practical in a real world application, but affords the opportunity
  to do something other than boring old REST.
- Use conventional commits for semantic release, and eventually progressive deployment.
- Keep things simple using Karma for unit testing and coverage
- Allow development of components more easily using storybook to be able to stage up components in various states to allow a more efficient dev loop.
- Use functional reactive programming with rxjs to be able to compose the application of nothing more than a series of pipelines that declaratively describe the data flow between UI elements and backend data store.
