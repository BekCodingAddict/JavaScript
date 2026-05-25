---
title: "setTimeout"
tags: [javascript, fundamentals, timing, async]
type: reference
related: [[set-interval]], [[promises]], [[promise-object]], [[_MOC-Fundamentals]]
---

# setTimeout

> Executes a function **once** after a specified delay in milliseconds.

---

## Overview

`setTimeout` is part of JavaScript's async model. It schedules code to run in the future without blocking the current execution thread.

---

## Syntax

```javascript
setTimeout(function, delay, arg1, arg2, ...)
```

| Parameter | Description |
|---|---|
| `function` | The function to execute after the delay |
| `delay` | Time in milliseconds to wait |
| `arg1, arg2, ...` | Optional arguments passed to the function |

---

## Basic Example

```javascript
setTimeout(() => {
  console.log("This message appears after 2 seconds.");
}, 2000);
```

---

## With Arguments

```javascript
function greet(name, timeOfDay) {
  console.log(`Good ${timeOfDay}, ${name}!`);
}

setTimeout(greet, 3000, "Bekki", "morning");
// Logs: "Good morning, Bekki!" after 3 seconds
```

---

## Cancelling

```javascript
const timerId = setTimeout(() => {
  console.log("This won't run");
}, 5000);

clearTimeout(timerId); // Cancels before it fires
```

---

## Key Points

- Delay is a **minimum** — actual execution may be later depending on call stack
- `delay = 0` still runs asynchronously (after current call stack clears)
- Returns a numeric ID used with `clearTimeout()`

---

## Related

- [[set-interval]] — Repeat code at fixed intervals
- [[promises]] — Promises are often combined with setTimeout for async simulation
- [[promise-object]] — See delayed Promise examples
- [[Fundamentals]] — Fundamentals hub
