---
title: "event.stopPropagation()"
tags: [javascript, fundamentals, events]
type: concept
related: [[prevent-default]], [[_MOC-Fundamentals]]
---

# event.stopPropagation()

> Prevents an event from bubbling up to parent elements in the DOM tree.

---

## Overview

When a user interacts with an element, the event normally **bubbles up** through every ancestor in the DOM, triggering any matching listeners on the way. `stopPropagation()` breaks that chain at the point you call it.

---

## Syntax

```javascript
element.addEventListener("click", (event) => {
  event.stopPropagation();
});
```

---

## Example — Block Event Bubbling

```javascript
document.querySelector(".child").addEventListener("click", (event) => {
  event.stopPropagation();
  console.log("Child clicked!");
});

document.querySelector(".parent").addEventListener("click", () => {
  console.log("Parent clicked!");
});
```

Clicking `.child` logs only `"Child clicked!"` — the parent listener never fires.

---

## Using Both Together

```javascript
document.querySelector(".button").addEventListener("click", (event) => {
  event.preventDefault();
  event.stopPropagation();
  console.log("Button click handled, no default action or bubbling!");
});
```

Useful when building nested interactive components (modals, dropdowns, nested cards).

---

## Key Points

- Stops the event from reaching **parent** listeners — siblings are unaffected
- Does **not** cancel default browser behavior — use `preventDefault()` for that
- `stopImmediatePropagation()` also blocks other listeners on the **same** element

---

## Related

- [[prevent-default]] — Cancel the browser's default action
- [[Fundamentals]] — Fundamentals hub
