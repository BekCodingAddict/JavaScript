## setInterval

>setInterval is a JavaScript function that repeatedly executes a specified function or code snippet at fixed time intervals (in milliseconds) until it is explicitly stopped. Unlike setTimeout, which runs a function once after a delay, setInterval will keep running the function over and over at the specified interval.

### Sytnax

```javascript
setInterval(function, delay, arg1, arg2, ...);
```
- function: The function or code to be executed repeatedly.
- delay: The interval time in milliseconds.
- arg1, arg2, ...: Optional arguments to pass to the function.

- Example:
  - Here’s a basic example that logs "Hello" to the console every second:
```javascript
const intervalId = setInterval(() => {
  console.log("Hello");
}, 1000);
```
- Stopping setInterval:
  - To stop setInterval, use clearInterval and pass it the ID returned by setInterval.
``` javascript
clearInterval(intervalId);
```
In the above example, calling clearInterval(intervalId) will stop the "Hello" logs from printing to the console every second.

- Use Cases:
  - Updating a clock or timer
  - Repeatedly checking for a condition in real-time apps
  - Running animations
