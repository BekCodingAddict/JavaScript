---
title: "setInterval"
tags: [javascript, fundamentals, timing, async]
type: reference
related: [[set-timeout]], [[_MOC-Fundamentals]]
---

# setInterval

> Repeatedly executes a function at a fixed time interval until explicitly stopped.

---

## Overview

Unlike `setTimeout` which runs once, `setInterval` keeps running the function on every interval tick until `clearInterval()` is called.

---

## Syntax

```javascript
setInterval(function, delay, arg1, arg2, ...);
```

| Parameter | Description |
|---|---|
| `function` | The function to execute on each tick |
| `delay` | Interval time in milliseconds |
| `arg1, arg2, ...` | Optional arguments passed to the function |

---

## Basic Example

```javascript
const intervalId = setInterval(() => {
  console.log("Hello");
}, 1000);
// Logs "Hello" every second
```

---

## Stopping the Interval

```javascript
clearInterval(intervalId);
// Stops the "Hello" logs immediately
```

Always store the return value so you can stop it later.

---

## Practical Pattern — Auto Stop After N Ticks

```javascript
let count = 0;
const id = setInterval(() => {
  count++;
  console.log(`Tick ${count}`);
  if (count >= 5) clearInterval(id);
}, 1000);
```

---

## Use Cases

- Live clocks and countdown timers
- Polling an API for real-time updates
- Animating UI elements at a fixed rate
- Checking a condition until it's met

---

## Key Points

- Interval is a **minimum** — if the callback takes longer than the delay, ticks can stack up
- For recursive timing that avoids stacking, prefer `setTimeout` called inside itself
- Always `clearInterval` when the component/element is removed to avoid memory leaks

---

## Related

- [[set-timeout]] — Execute code once after a delay
- [[Fundamentals]] — Fundamentals hub
