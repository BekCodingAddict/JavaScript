---
title: "DOM Selection Shorthand Utility"
tags: [javascript, vanilla-js, patterns, dom]
type: pattern
related: [[level-up-vanilla-js]], [[pub-sub-event-communication]], [[_MOC-Vanilla-JS]]
---

# DOM Selection Shorthand Utility

> A two-line utility that replaces verbose `querySelector` calls with `$` and `$$` — the foundation of clean Vanilla JS.

---

## The Utility

```javascript
// core/dom.js
export const $ = (selector, scope = document) => scope.querySelector(selector);
export const $$ = (selector, scope = document) => [...scope.querySelectorAll(selector)];
```

---

## What `$` and `$$` Do

| Code | Equivalent | Returns |
|---|---|---|
| `$(selector)` | `document.querySelector(selector)` | Single element |
| `$$(selector)` | `document.querySelectorAll(selector)` | Real Array |

**Before:**
```javascript
document.querySelector(".btn");
document.querySelectorAll(".item");
```

**After:**
```javascript
$(".btn");
$$(".item");
```

---

## The `scope` Parameter

The second parameter defines **where to search** in the DOM. Default is the entire document.

```javascript
// Search only inside a specific section
const section = $("#profile");
const buttons = $$("button", section);
```

This improves performance and prevents unintended matches.

---

## Why `[...]` in `$$`

`querySelectorAll()` returns a `NodeList` — not a real array. You can't use `.map()`, `.filter()`, or `.reduce()` on it.

Spreading into `[...]` converts it to a **real Array**:

```javascript
$$(".item").forEach((el) => el.classList.add("active"));
$$(".card").map((el) => el.dataset.id);
$$(".input").filter((el) => el.value !== "");
```

---

## Why This is Senior-Level

- Eliminates repetitive boilerplate across every file
- Scoped selections prevent accidental global matches
- Array conversion enables the full `.map()` / `.filter()` toolkit
- Acts as the base utility imported by every component

---

## Related

- [[level-up-vanilla-js]] — Full architecture using this utility
- [[pub-sub-event-communication]] — Components that use `$` for DOM access
- [[Vanilla-JavaSscript]] — Vanilla JS hub
