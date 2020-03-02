---
title: Cypress.io
definition: E2E testing framework
tags: e2e test
---

## Learning

- [Cypress in a Nutshell](https://youtu.be/LcGHiFnBh3Y)
- [Testing Pyramid](https://testingjavascript.com/)
- [Case Studies](https://cypress.io/case-studies/)
- [Case Studies Slides](https://cypress.slides.com/cypress-io/)

## Useful commands

### find

```javascript
// Yield 'footer' within '.article'
cy.get('.article').find('footer');
```

From
[Gatspy](https://github.com/gatsbyjs/gatsby/blob/master/packages/gatsby-cypress/src/commands.js#L5):

```javascript
Cypress.Commands.add(`getTestElement`, (selector, options = {}) =>
  cy.get(`[data-testid="${selector}"]`, options),
);
```
