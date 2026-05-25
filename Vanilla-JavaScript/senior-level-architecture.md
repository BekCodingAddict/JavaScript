---
title: "Senior-Level Architecture"
tags: [javascript, vanilla-js, architecture]
type: moc
related: [[global-state-store]], [[pub-sub-event-communication]], [[level-up-vanilla-js]], [[_MOC-Vanilla-JS]]
---

# Senior-Level Vanilla JS Architecture

> The complete system: DOM utilities + component pattern + Pub/Sub events + global state store.

---

## Full Stack of Patterns

Each layer builds on the previous. You can adopt them incrementally.

1. [[dom-selection-shorthand]] - Base utility layer
2. [[level-up-vanilla-js]] - Folder structure, components, HTTP
3. [[pub-sub-event-communication]] - Decoupled event system (EventBus)
4. [[global-state-store]] - Centralized Redux-style state

---

## Data Flow

User Action -> Component -> Action function -> Store.setState() -> EventBus.emit("state:change") -> All subscribed components update UI

No component ever imports another component - everything flows through the store and event bus.

---

## Framework Equivalents

| This System | React | Vue | Angular |
|---|---|---|---|
| EventBus | Redux dispatch | emit | Service RxJS |
| Store | Redux store | Vuex / Pinia | NgRx |
| Actions | Action creators | Mutations | Effects |
| state:change event | store.subscribe | Watchers | Observables |

---

## All Notes in This System

- [[dom-selection-shorthand]] - dollar / dollar-dollar DOM utilities
- [[level-up-vanilla-js]] - Components, HTTP wrapper, page structure
- [[pub-sub-event-communication]] - EventBus implementation
- [[global-state-store]] - Store, actions, and state subscriptions

---

<-[[Vanilla-JavaSscript]]]
