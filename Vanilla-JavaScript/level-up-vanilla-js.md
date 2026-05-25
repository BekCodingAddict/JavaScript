---
title: "Level Up Vanilla JS"
tags: [javascript, vanilla-js, architecture, patterns]
type: guide
related: [[dom-selection-shorthand]], [[pub-sub-event-communication]], [[senior-level-architecture]], [[_MOC-Vanilla-JS]]
---

# Level Up Vanilla JS

> Step-by-step guide to structuring Vanilla JS like a senior developer — modular, scalable, and maintainable.

---

## Step 1 — Folder Structure

```
static/
 └── js/
      ├── core/
      │    ├── dom.js         ← $ / $$ utilities
      │    ├── http.js        ← fetch wrapper
      │    └── events.js      ← EventBus
      ├── components/
      │    ├── Modal.js
      │    ├── Dropdown.js
      │    └── FormValidator.js
      ├── pages/
      │    ├── homepage.js
      │    └── profile.js
      └── main.js
```

---

## Step 2 — Smart DOM Utilities

```javascript
// core/dom.js
export const $ = (selector, scope = document) => scope.querySelector(selector);
export const $$ = (selector, scope = document) => [...scope.querySelectorAll(selector)];

export const on = (el, event, selector, handler) => {
  el.addEventListener(event, (e) => {
    if (e.target.closest(selector)) handler(e);
  });
};
```

See [[dom-selection-shorthand]] for full explanation.

---

## Step 3 — HTTP Wrapper

```javascript
// core/http.js
export async function get(url) {
  const res = await fetch(url);
  if (!res.ok) throw new Error(res.statusText);
  return res.json();
}

export async function post(url, data) {
  const res = await fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });
  if (!res.ok) throw new Error(res.statusText);
  return res.json();
}
```

---

## Step 4 — Reusable UI Components

### Modal

```javascript
// components/Modal.js
import { $ } from "../core/dom.js";

export default class Modal {
  constructor(selector) {
    this.el = $(selector);
    this.closeBtn = this.el.querySelector("[data-close]");
    this.init();
  }

  init() {
    this.closeBtn.addEventListener("click", () => this.close());
  }

  open() { this.el.classList.add("open"); }
  close() { this.el.classList.remove("open"); }
}
```

### Dropdown

```javascript
// components/Dropdown.js
export default class Dropdown {
  constructor(selector) {
    this.selector = selector;
    this.init();
  }

  init() {
    document.addEventListener("click", (e) => {
      const btn = e.target.closest(this.selector);
      if (!btn) return;
      btn.nextElementSibling.classList.toggle("open");
    });
  }
}
```

### Form Validator

```javascript
// components/FormValidator.js
export default class FormValidator {
  constructor(formSelector) {
    this.form = document.querySelector(formSelector);
    this.form.addEventListener("submit", (e) => this.validate(e));
  }

  validate(e) {
    const requiredFields = this.form.querySelectorAll("[required]");
    let valid = true;

    requiredFields.forEach((field) => {
      if (!field.value.trim()) {
        valid = false;
        field.classList.add("error");
      } else {
        field.classList.remove("error");
      }
    });

    if (!valid) e.preventDefault();
  }
}
```

---

## Step 5 — Main Entry File

```javascript
// main.js
import Modal from "./components/Modal.js";
import Dropdown from "./components/Dropdown.js";
import FormValidator from "./components/FormValidator.js";

new Dropdown("[data-dropdown]");
new Modal("#loginModal");

// Page-specific code — only loads what's needed
if (document.body.dataset.page === "home") {
  import("./pages/homepage.js").then((m) => m.init());
}

if (document.body.dataset.page === "profile") {
  import("./pages/profile.js").then((m) => m.init());
}
```

---

## Step 6 — Django Template Integration

```html
<body data-page="home">
  <div id="loginModal" class="modal">
    <button data-close>×</button>
  </div>

  <script type="module" src="{% static 'js/main.js' %}"></script>
</body>
```

---

## Junior vs Senior Comparison

| Feature | Junior | Senior |
|---|---|---|
| Script style | One giant file | Structured modules |
| Maintenance | Hard | Easy |
| Reusable UI | No | Yes |
| Page performance | Low | High (code splitting) |
| Code readability | Poor | Clear |

---

## Related

- [[dom-selection-shorthand]] — The `$` / `$$` utility used throughout
- [[pub-sub-event-communication]] — Component communication layer
- [[senior-level-architecture]] — Full system with state management
- [[Vanilla-JavaSscript]] — Vanilla JS hub
