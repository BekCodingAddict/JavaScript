---
title: "Pub/Sub Event Communication"
tags: [javascript, vanilla-js, patterns, architecture, events]
type: pattern
related: [[global-state-store]], [[dom-selection-shorthand]], [[level-up-vanilla-js]], [[_MOC-Vanilla-JS]]
---

# Pub/Sub Event Communication

> Decouple components so they communicate through an Event Bus — never directly with each other.

---

## The Problem Without Pub/Sub

| Without Pub/Sub | With Pub/Sub |
|---|---|
| Components call each other directly → tight coupling | No component depends on any other |
| Hard to add or remove components | Extremely scalable |
| Everything piled into `main.js` | Clean, distributed logic |
| Breaks easily when features are added | Stable as system grows |

---

## Step 1 — Create the Event Bus

```javascript
// core/events.js
class EventBus {
  constructor() {
    this.events = {};
  }

  on(event, callback) {
    if (!this.events[event]) this.events[event] = [];
    this.events[event].push(callback);
  }

  emit(event, data) {
    if (!this.events[event]) return;
    this.events[event].forEach((cb) => cb(data));
  }

  off(event, callback) {
    if (!this.events[event]) return;
    this.events[event] = this.events[event].filter((cb) => cb !== callback);
  }
}

export const eventBus = new EventBus();
```

---

## Step 2 — Publisher Component

```javascript
// components/LoginModal.js
import { eventBus } from "../core/events.js";

export default class LoginModal {
  submitSuccess(user) {
    eventBus.emit("user:login", user); // broadcast the event
    this.close();
  }
}
```

---

## Step 3 — Subscriber Component

```javascript
// components/Navbar.js
import { eventBus } from "../core/events.js";
import { $ } from "../core/dom.js";

export default class Navbar {
  constructor() {
    this.usernameLabel = $("#usernameLabel");

    eventBus.on("user:login", (user) => {
      this.usernameLabel.textContent = `Welcome, ${user.username}!`;
    });
  }
}
```

`LoginModal` and `Navbar` **don't know each other exist** — they only know the event name.

---

## Step 4 — Main Initialization

```javascript
// main.js
import Navbar from "./components/Navbar.js";
import LoginModal from "./components/LoginModal.js";

new Navbar();
const loginModal = new LoginModal();
```

---

## Event Naming Convention

Use `namespace:action` format for clarity:

```
user:login
user:logout
cart:updated
modal:open
theme:changed
```

---

## Where This Pattern Is Used

- React Context / Redux event dispatching
- Vue's `emit` system
- Angular services communication
- Large-scale Vanilla JS apps

---

## Related

- [[global-state-store]] — Combine Pub/Sub with centralized state
- [[dom-selection-shorthand]] — `$` utility used in subscribers
- [[level-up-vanilla-js]] — Full architecture context
- [[Vanilla-JavaSscript]] — Vanilla JS hub
