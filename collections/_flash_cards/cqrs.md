---
title: CQRS
definition: Command Query Responsibility Segregation
tags: messaging protocol
---

CQRS is an architectural pattern that separates reading and writing into two
different models. This means that every method should either be a Command that
performs an action or a Query that returns data. A Command cannot return data
and a Query cannot change the data.
