---
title: RxJS
definition: Reactive Extensions For JavaScript
tags: reactive observable
---

# Learning

> Think of RxJS as Lodash for events.

ReactiveX combines the Observer pattern with the Iterator pattern and functional programming with collections to fill
the need for an ideal way of managing sequences of events.

* [RxJs](https://rxjs-dev.firebaseapp.com/guide/overview)
* [reactive.how](https://reactive.how/)
* [Learn RxJs](https://www.learnrxjs.io/)
* [RxViz](https://rxviz.com/)
* [RxMarbles](https://rxmarbles.com/)

# Blog & Clips

* [RxJS Operators - Explanation, Real World Use Cases, and Anti Patterns](https://www.youtube.com/watch?v=Dsku0F4lU3A)
* [RxJS best practices in Angular](https://blog.strongbrew.io/rxjs-best-practices-in-angular/)
* [RxJS: Don’t Unsubscribe](https://medium.com/@benlesh/rxjs-dont-unsubscribe-6753ed4fda87)
* [Hot vs Cold Observables](https://medium.com/@benlesh/hot-vs-cold-observables-f8094ed53339)

# [Observable](https://rxjs-dev.firebaseapp.com/guide/observable)

Observables are lazy Push collections of multiple values. An Observable is a lazily evaluated computation that can
synchronously or asynchronously return zero to (potentially) infinite values from the time it's invoked onwards.

|        | SINGLE     | MULTIPLE     |
| ------ |----------- | ------------ |
| *Pull* | `Function` | `Iterator`   |
| *Push* | `Promise`  | `Observable` |

|        | PRODUCER   | CONSUMER     |
| ------ |----------- | ------------ |
| *Pull* | *Passive:* produces data when requested. | *Active:* decides when data is requested. |
| *Push* | *Active:* produces data at its own pace. | *Passive:* reacts to received data. |

> Observables are like functions with zero arguments, but generalize those to allow multiple values.
> I.e. Observables can "return" multiple values over time (with multiple `subscriber.next(value)`).

> Subscribing to an Observable is analogous to calling a Function.
> Each call to `observable.subscribe()` triggers its own independent setup for that given subscriber.

> Observables are able to deliver values either synchronously or asynchronously.


> In an Observable Execution, zero to infinite Next notifications may be delivered. If either an Error or Complete
> notification is delivered, then nothing else can be delivered afterwards.

> When you subscribe, you get back a Subscription, which represents the ongoing execution. Just call unsubscribe()
> to cancel the execution.

An 'raw/naked' Observable without ReactiveX types would result in  rather straightforward JavaScript.

```JavaScript
function subscribe(subscriber) {
  const intervalId = setInterval(() => {
    subscriber.next('hi');
  }, 1000);

  return function unsubscribe() {
    clearInterval(intervalId);
  };
}

const unsubscribe = subscribe({next: (x) => console.log(x)});

// Later:
unsubscribe(); // dispose the resources
```

The reason why we use Rx types like Observable, Observer, and Subscription is to get safety (such as the Observable
 Contract) and composability with Operators.

# Operators

## exhaustMap

Drag & drop, first subscribe needs to finish until I subscribe to next, we don't want that a second touch event e.g.
with second finger cancels current subscription. You don't care about latest.

## switchMap

Autocomplete, we just care about the result of the last value, therefore we unsubscribe from current observable when
new value and subscribe to new observable

## concatMap

Do one after the other, you care about response and their order

## mergeMap

You care about response but not about their order
