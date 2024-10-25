## setTimeout
>[!TIP]
>In JavaScript, setTimeout is a function used to execute a piece of code or function after a specified delay (in milliseconds). It's part of the asynchronous behavior in JavaScript, allowing tasks to be scheduled to run in the future, rather than blocking the current execution.

- Syntax:
```javascript
setTimeout(function, delay, arg1, arg2, ...)
```
  - function: The function you want to execute after the delay.
  - delay: The time (in milliseconds) to wait before executing the function.
  - arg1, arg2, ...: Optional arguments to pass to the function when it’s called.

- Example:
```javascript
setTimeout(() => {
  console.log("This message appears after 2 seconds.");
}, 2000); // In this example, "This message appears after 2 seconds."
// will log to the console after a 2-second delay.
```  
- Example with Named Function:
```javascript
function greet(name, timeOfDay) {
  console.log(`Good ${timeOfDay}, ${name}!`);
}

setTimeout(greet, 3000, 'Bekki', 'morning');
```
After 3 seconds, this will log "Good morning, Bekki!" to the console.
