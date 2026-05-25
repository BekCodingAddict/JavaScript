---
title: "Promises"
tags: [javascript, fundamentals, async]
type: concept
related: [[promise-object]], [[_MOC-Fundamentals]]
---

# Promises

> A Promise represents a value that may be available now, later, or never — the foundation of async JavaScript.

---

## Overview

Promises give us a structured way to handle operations that take time: API calls, file reads, timers. Instead of nesting callbacks, we chain `.then()` and `.catch()`.

---

## States

| State | Meaning |
|---|---|
| **Pending** | Operation has not completed yet |
| **Fulfilled** | Operation completed successfully |
| **Rejected** | Operation failed |

A Promise transitions from `pending` → `fulfilled` or `pending` → `rejected`. It **never** goes back.

---

## Creating a Promise

```javascript
const myPromise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Operation succeeded!");
  } else {
    reject("Operation failed.");
  }
});
```

---

## Consuming a Promise

```javascript
myPromise
  .then((message) => {
    console.log(message); // "Operation succeeded!"
  })
  .catch((error) => {
    console.error(error);
  })
  .finally(() => {
    console.log("Operation finished."); // Always runs
  });
```

| Method | Runs when |
|---|---|
| `.then()` | Promise is fulfilled |
| `.catch()` | Promise is rejected |
| `.finally()` | Either outcome |

---

## Async / Await

Syntactic sugar over Promises — makes async code read like synchronous code.

```javascript
async function asyncFunction() {
  try {
    const result = await myPromise;
    console.log(result);
  } catch (error) {
    console.error(error);
  } finally {
    console.log("Operation finished.");
  }
}

asyncFunction();
```

---

## Related

- [[promise-object]] — Deep dive into the Promise constructor and all methods
- [[Fundamentals]] — Fundamentals hub
