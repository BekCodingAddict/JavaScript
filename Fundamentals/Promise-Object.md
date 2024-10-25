### JavaScript Promise Object
>[!TIP]
>The JavaScript Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises provide a way to handle asynchronous operations more elegantly than using callback functions, offering a clearer and more structured approach.

- Promise Syntax:
  - A Promise is created using the new Promise constructor:
```javascript
const myPromise = new Promise((resolve, reject) => {
  // Asynchronous operation here
  if (/* operation successful */) {
    resolve('Operation successful');
  } else {
    reject('Operation failed');
  }
});
```
  - resolve: The function to call if the operation completes successfully.
  - reject: The function to call if the operation fails.

- Examples:
  - Here’s a simple example of a Promise simulating a delay using setTimeout:
```javascript
const wait = (milliseconds) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(`Waited for ${milliseconds} milliseconds`);
    }, milliseconds);
  });
};

wait(2000).then((message) => {
  console.log(message); // Logs: Waited for 2000 milliseconds
});
```
### Promise Methods:
- then(): Handles the result if the promise is fulfilled.
```javascript
myPromise.then((value) => {
  console.log(value); // If resolved, logs the resolved value
});
```

- catch(): Handles errors if the promise is rejected.
```javascript
myPromise.catch((error) => {
  console.error(error); // Logs the error message
});
```
-  finally(): Executes code regardless of the outcome.
  ```javascript
myPromise.finally(() => {
  console.log('Operation complete');
});
```
- Promise States
  - Pending: Initial state, neither fulfilled nor rejected.
  - Fulfilled: The operation completed successfully (resolve was called).
  - Rejected: The operation failed (reject was called).\

- Example of a Promise with .then(), .catch(), and .finally()
```javascript
const fetchData = () => {
  return new Promise((resolve, reject) => {
    const success = true;
    setTimeout(() => {
      success ? resolve("Data fetched successfully") : reject("Error fetching data");
    }, 2000);
  });
};

fetchData()
  .then((message) => console.log(message))  // If resolved
  .catch((error) => console.error(error))   // If rejected
  .finally(() => console.log("Fetch attempt finished")); // Always executes
```
In this example:
  - If success is true, "Data fetched successfully" will log after 2 seconds.
  - If success is false, "Error fetching data" will log after 2 seconds.
  - Finally, "Fetch attempt finished" will log in both cases, after the promise is settled.
