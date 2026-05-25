---
title: "Global State Store"
tags: [javascript, vanilla-js, patterns, architecture, state-management]
type: pattern
related: [[pub-sub-event-communication]], [[dom-selection-shorthand]], [[senior-level-architecture]], [[_MOC-Vanilla-JS]]
---

# Global State Store

> A Redux-style centralized state store built in Vanilla JS — one source of truth for your entire app.

---

## Goal

| Feature | Status |
|---|---|
| Single global source of truth | Like Redux Store |
| Components subscribe to changes | Auto UI updates |
| Actions update state predictably | No direct mutation |
| Components never talk to each other | Decoupled by design |
| Works with Pub/Sub event system | Fully integrated |

---

## Step 1 — Create the Store

```javascript
// core/store.js
import { eventBus } from "./events.js";

export class Store {
  constructor(initialState = {}) {
    this.state = initialState;
  }

  getState() {
    return { ...this.state }; // immutable copy — no direct mutation
  }

  setState(newState) {
    this.state = { ...this.state, ...newState };
    eventBus.emit("state:change", this.getState());
  }
}

export const store = new Store({
  user: null,
  theme: "light",
});
```

---

## Step 2 — Action Functions

Actions are the only way to update state — equivalent to Redux reducers.

```javascript
// core/actions.js
import { store } from "./store.js";

export function loginUser(userData) {
  store.setState({ user: userData });
}

export function logoutUser() {
  store.setState({ user: null });
}

export function toggleTheme() {
  const { theme } = store.getState();
  store.setState({ theme: theme === "light" ? "dark" : "light" });
}
```

---

## Step 3 — Connect Components to State

```javascript
// components/Navbar.js
import { eventBus } from "../core/events.js";
import { store } from "../core/store.js";
import { $ } from "../core/dom.js";

export default class Navbar {
  constructor() {
    this.usernameLabel = $("#usernameLabel");

    // React to every state change
    eventBus.on("state:change", (state) => {
      this.usernameLabel.textContent = state.user
        ? `Welcome, ${state.user.username}!`
        : "Guest";
    });

    // Load initial UI from current state
    const { user } = store.getState();
    this.usernameLabel.textContent = user ? `Welcome, ${user.username}!` : "Guest";
  }
}
```

---

## Step 4 — Component Triggers a State Update

```javascript
// components/LoginModal.js
import { loginUser } from "../core/actions.js";

export default class LoginModal {
  submitSuccess(user) {
    loginUser(user); // updates global store → triggers state:change → UI updates everywhere
  }
}
```

---

## Architecture Comparison

| Your Custom Store | Framework Equivalent |
|---|---|
| `Store` class | Redux `createStore` |
| `setState()` | `dispatch(action)` |
| Action functions | Reducers / Action Creators |
| `state:change` event | `store.subscribe()` |
| `getState()` | `store.getState()` |

---

## Related

- [[pub-sub-event-communication]] — The Event Bus this store depends on
- [[dom-selection-shorthand]] — DOM utility used in components
- [[senior-level-architecture]] — Full project structure
- [[Vanilla-JavaSscript]] — Vanilla JS hub
