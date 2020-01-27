---
title: NgRx
definition:
  Set of RxJS-powered state management libraries for Angular, inspired by Redux.
tags: rxjs state management angular redux
---

- [NgRx: Patterns and Techniques](https://blog.nrwl.io/ngrx-patterns-and-techniques-f46126e2b1e5)
- [Angular: You may not need NgRx!](https://blog.angularindepth.com/angular-you-may-not-need-ngrx-e80546cc56ee)
- [Level up your NgRx game](https://itnext.io/level-up-your-ngrx-game-42652afc25bd)
- [Reducing the Boilerplate with NgRx - Brandon Roberts & Mike Ryan](https://youtu.be/t3jx0EC-Y3c)
- [Good Action Hygiene with NgRx Mike Ryan](https://youtu.be/JmnsEvoy-gY)
- [Angular Service Layers: Redux, RxJs and Ngrx Store - When to Use a Store And Why?](https://blog.angular-university.io/angular-2-redux-ngrx-rxjs/)
- [Quantum NgRx Facades | Sam Julien | #AngularConnect](https://www.youtube.com/watch?v=eq8n7iuHxQo)
  - use `createSelector(selOne, selTwo, (one, two) => one && two)` to compose
    state
  - Prefer duplication over the wrong abstraction. - Sandi Metz
  - AHA: Avoid Hasty Abstractions - Kent C. Dodds
  - [Don't abstract away actions](https://youtu.be/eq8n7iuHxQo?t=1396)
