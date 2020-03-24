---
title: NgRx
definition:
  Set of RxJS-powered state management libraries for Angular, inspired by Redux.
tags: rxjs state management angular redux
---

Blog

- [NgRx: Patterns and Techniques](https://blog.nrwl.io/ngrx-patterns-and-techniques-f46126e2b1e5)
- [Angular: You may not need NgRx!](https://blog.angularindepth.com/angular-you-may-not-need-ngrx-e80546cc56ee)
- [Level up your NgRx game](https://itnext.io/level-up-your-ngrx-game-42652afc25bd)
- [Angular Service Layers: Redux, RxJs and Ngrx Store - When to Use a Store And Why?](https://blog.angular-university.io/angular-2-redux-ngrx-rxjs/)

Clip

- [Reducing the Boilerplate with NgRx - Brandon Roberts & Mike Ryan](https://youtu.be/t3jx0EC-Y3c)
- [Good Action Hygiene with NgRx Mike Ryan](https://youtu.be/JmnsEvoy-gY)
- [You might not need NgRx - Mike Ryan - AngularConnect 2018](https://youtu.be/omnwu_etHTY)
- [Quantum NgRx Facades - Sam Julien - #AngularConnect](https://www.youtube.com/watch?v=eq8n7iuHxQo)
  - use `createSelector(selOne, selTwo, (one, two) => one && two)` to compose
    state
  - Prefer duplication over the wrong abstraction. - Sandi Metz
  - AHA: Avoid Hasty Abstractions - Kent C. Dodds
  - [Don't abstract away actions](https://youtu.be/eq8n7iuHxQo?t=1396)
- [💥 Understanding NgRx - Why State Management, what are the Benefits?](https://youtu.be/0NpLwr3n_7g)
