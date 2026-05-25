---
title: "Memory Management"
tags: [javascript, fundamentals, memory]
type: concept
related: [[_MOC-Fundamentals]]
---

# Memory Management

> How JavaScript handles referencing, garbage collection, and memory — compared with Python.

---

## JS vs Python at a Glance

| Feature | Python (CPython) | JavaScript (V8) |
|---|---|---|
| **Primary mechanism** | Reference Counting | Reachability-based GC |
| **Handles circular refs?** | Needs cyclic GC | Built-in, automatic |
| **Generational GC?** | Yes (3 generations) | Yes (multi-generational) |
| **Manual control?** | Limited via `gc` module | None — fully automatic |
| **Objects stored** | Heap | Heap |
| **Primitives stored** | Stack | Stack (most engines) |

---

## Referencing in JavaScript

Variables don't hold objects directly — they hold **references (pointers)** to objects in memory.

```javascript
let a = { name: "Alice" };
let b = a;

b.name = "Bob";
console.log(a.name); // "Bob" — same object in memory
```

### Primitive vs Reference Types

| Type | Stored | Copied |
|---|---|---|
| Primitive (string, number, boolean, null, undefined, symbol, bigint) | Stack | By **value** |
| Object / Array / Function | Heap | By **reference** |

```javascript
let x = 10;
let y = x; // y is an independent copy

let a = {};
let b = a; // b points to the same object
```

---

## Garbage Collection in JavaScript

JavaScript uses **automatic garbage collection** — you cannot free memory manually.

### Reachability

An object is **reachable** if it can be accessed from a root:
- Global variables
- The call stack (local variables, parameters)
- Active closures

If nothing can reach an object, it is **garbage collected**.

```javascript
function create() {
  let obj = { name: "Alice" };
  return obj;
}

let user = create(); // obj is reachable through user
user = null;         // obj is now unreachable → collected
```

---

## Modern JS Engine Strategies (V8)

| Strategy | Purpose |
|---|---|
| **Generational GC** | Short-lived vs long-lived objects |
| **Incremental GC** | Runs in small steps — avoids blocking UI |
| **Concurrent GC** | Runs parallel with code execution |
| **Compacting GC** | Reorganizes memory, reduces fragmentation |

---

## JS vs Python — Conceptual Summary

| Concept | Python | JavaScript |
|---|---|---|
| **When memory is freed** | Refcount = 0 or GC detects cycles | When unreachable |
| **GC timing** | Relatively predictable | Non-deterministic |
| **Circular references** | Needs GC module | Automatic |
| **Best practice** | Break cycles manually | Set unused refs to `null` |

---

## Best Practices

- Set large objects to `null` when done: `user = null`
- Avoid lingering closures holding large scopes
- Be careful with global variables — they are always reachable (never collected)
- Detach event listeners when removing DOM elements

---

## Related

- [[Fundamentals]] — Fundamentals hub
