---
title: RxJS
definition: Reactive Extensions For JavaScript
tags: reactive observable
---

* [RxJS Operators - Explanation, Real World Use Cases, and Anti Patterns](https://www.youtube.com/watch?v=Dsku0F4lU3A)
* [RxJS best practices in Angular](https://blog.strongbrew.io/rxjs-best-practices-in-angular/)
* [RxJS: Don’t Unsubscribe](https://medium.com/@benlesh/rxjs-dont-unsubscribe-6753ed4fda87)

## exhaustMap

drag & drop, first subscribe needs to finish until I subscribe to next, we don't want that a second touch event e.g. with second finger cancels current subscription. You don't care about latest.

## switchMap

autocomplete, we just care about the result of the last value, therefore we unsubscribe from current observable when new value and subscribe to new observable

## concatMap

do one after the other, you care about response and their order

## mergeMap

you care about response but not about
