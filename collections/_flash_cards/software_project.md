---
title: Software Project
definition: Aspects & requirement on a "perfect" project setup
tags: software project architecture process environment tools
---

### Testing

- E2E test (user scenario, generating (time-depending) test data)
- Component test (test component or multiple components as blackbox)
  - Storybook: challenge testing `@Output` and service calls in Cypress tests
- Unit test (test a single/smaller function/logic)
- Visual test (detect visual/css changes)
- Performance test (did a change significantly decrease the speed)
- Complete Test Environment as close to production as possible (DB)

### Code style

- linting
  - TypeScript, CSS, HTML
  - Prettier, EsLint, StyleLint

How to integrate/run these in IDE on save?

### CI/CD

- GitHub Actions
- Reporting

### Analytics (what is how used)

- FullStory
- MixPanel

### Feature Flags

- featureflagservices.io

### Error reporting by user

### API

- How to "share" interface (JsonSchema, openAPI, TypeScript)?

### Authentication / Login

### Maintaining / Updating dependencies

### Domain Models

- Are models/types from backend kept the same in UI or are they converted to
  different types. I.e. do presentational component use API types or their own?

### ORM

### Confirmation/alerts

- error from backend API call (#SnackBar)

### Development Process

How should a new feature/component be developed.

### Project (file) structure

How is the source code organized. Nrwl/nx

### Code Architecture

What patterns are followed.

### Accessibility

### Internationalisation

### PO <> UX/UI <> DEV

- From idea to released feature

### Scrum

- How are (new/urgent) bugs handled
- How is technical depth handled
- How is refinement done?
