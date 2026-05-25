---
title: "Vanilla JavaScript — Map of Content"
tags: [javascript, vanilla-js, moc]
type: moc
related: [[_HOME]]
---

# Vanilla JavaScript

> Senior-level patterns and architecture for building scalable apps without frameworks.

---

## Architecture

- [[senior-level-architecture]] — Folder structure, module system, page-level design
- [[level-up-vanilla-js]] — Step-by-step guide to senior-level Vanilla JS

## Patterns

- [[pub-sub-event-communication]] — Decoupled component communication via Event Bus
- [[global-state-store]] — Redux-style centralized state management
- [[dom-selection-shorthand]] — `$` / `$$` DOM utility helpers

---

## Pattern Dependency Map

```
dom-selection-shorthand
        ↓
level-up-vanilla-js
        ↓
pub-sub-event-communication
        ↓
global-state-store
        ↓
senior-level-architecture
```

← [[JAVASCRIPT]]
