---
title: "event.preventDefault()"
tags: [javascript, fundamentals, events]
type: concept
related: [[stop-propagation]], [[_MOC-Fundamentals]]
---

# event.preventDefault()

> Stops the browser's default behavior for an element — without stopping the event from propagating.

---

## Overview

Some elements have built-in default actions:
- `<a>` navigates to a URL
- `<form>` submits and reloads the page
- `<input type="checkbox">` toggles its checked state

Calling `preventDefault()` cancels that default action while still letting the event bubble up the DOM.

---

## Syntax

```javascript
element.addEventListener("click", (event) => {
  event.preventDefault();
});
```

---

## Example — Prevent Link Navigation

```javascript
document.querySelector("a").addEventListener("click", (event) => {
  event.preventDefault();
  console.log("Link click prevented!");
});
```

Clicking the link will **not** navigate anywhere, but the click event still fires normally.

---

## Using Both Together

When you need to stop both the default action **and** event bubbling:

```javascript
document.querySelector(".button").addEventListener("click", (event) => {
  event.preventDefault();
  event.stopPropagation();
  console.log("Button click handled, no default action or bubbling!");
});
```

Useful in complex nested UI components like modals or dropdowns.

---

## Key Points

- Does **not** stop event propagation — use `stopPropagation()` for that
- Works on `click`, `submit`, `keydown`, and other cancellable events
- Not all events are cancellable — check `event.cancelable` first

---

## Related

- [[stop-propagation]] — Stop the event from bubbling up
- [[Fundamentals]] — Fundamentals hub
