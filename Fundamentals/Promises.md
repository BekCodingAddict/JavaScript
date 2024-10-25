# JavaScript Promises
>[!NOTE]
>Promises are a way to handle asynchronous operations in JavaScript. They represent a value that may be available now, later, or never, allowing us to manage things like API calls, reading files, or other tasks that take time.

### Here's a quick overview:
- States: A promise has three possible states:
  - Pending: The operation has not completed yet.
  - Fulfilled: The operation completed successfully.
  - Rejected: The operation failed.
- Syntax:
```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation
  const success = true; // This is just for example
  
  if (success) {
    resolve("Operation succeeded!");
  } else {
    reject("Operation failed.");
  }
});
```

- Using Promises:
  - .then(): Executes when the promise is fulfilled.
  - .catch(): Executes when the promise is rejected.
  - .finally(): Runs after either fulfillment or rejection.
```javascript
myPromise
  .then((message) => {
    console.log(message); // Output: "Operation succeeded!"
  })
  .catch((error) => {
    console.error(error); // If it failed
  })
  .finally(() => {
    console.log("Operation finished."); // Always runs
  });
```
- Async/Await: Introduced as syntactic sugar for Promises, making async code look synchronous.
  - Example:\
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
