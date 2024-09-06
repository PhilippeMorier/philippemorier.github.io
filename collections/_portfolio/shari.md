---
title: SHARI
definition: Shared Hydrated Available Retrieved Impacted
tags: state management ngrx
---

State belongs to the store if it is SHARI.

- **S**hared: Shared state is accessed by many components and services
- **H**ydrated: State that is persisted and hydrated from storage
- **A**vailable: State that needs to be available when re-entering routes
- **R**etrieved: State that needs to be retrieved with a side effect
- **I**mpacted: State that is impacted by actions from other sources

See:
[Reducing the Boilerplate with NgRx - Brandon Roberts & Mike Ryan](https://youtu.be/t3jx0EC-Y3c)
