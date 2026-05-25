---
title: "Promise Object"
tags: [javascript, fundamentals, async]
type: reference
related: [[promises]], [[set-timeout]], [[_MOC-Fundamentals]]
---

# Promise Object

> The `Promise` object represents the eventual completion or failure of an async operation and its resulting value.

---

## Constructor

```javascript
const myPromise = new Promise((resolve, reject) => {
  if (/* operation successful */) {
    resolve("Operation successful");
  } else {
    reject("Operation failed");
  }
});
```

- `resolve(value)` — call when the operation succeeds
- `reject(reason)` — call when the operation fails

---

## States

| State | Description |
|---|---|
| **Pending** | Initial state — neither fulfilled nor rejected |
| **Fulfilled** | `resolve` was called |
| **Rejected** | `reject` was called |

---

## Instance Methods

### `.then(onFulfilled)`

```javascript
myPromise.then((value) => {
  console.log(value);
});
```

### `.catch(onRejected)`

```javascript
myPromise.catch((error) => {
  console.error(error);
});
```

### `.finally(onSettled)`

```javascript
myPromise.finally(() => {
  console.log("Operation complete");
});
```

---

## Full Example

```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    const success = true;
    setTimeout(() => {
      success
        ? resolve("Data fetched successfully")
        : reject("Error fetching data");
    }, 2000);
  });
};

fetchData()
  .then((message) => console.log(message))
  .catch((error) => console.error(error))
  .finally(() => console.log("Fetch attempt finished"));
```

---

## Simulating Delay

```javascript
const wait = (milliseconds) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(`Waited for ${milliseconds} milliseconds`);
    }, milliseconds);
  });
};

wait(2000).then((message) => console.log(message));
```

---

## Related

- [[promises]] — High-level overview, async/await, chaining
- [[set-timeout]] — Used frequently inside Promises to simulate delay
- [[Fundamentals]] — Fundamentals hub
