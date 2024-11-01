## event.stopPropagation()

>In JavaScript, event.stopPropagation() and event.preventDefault() are commonly used to control how events behave in the DOM. Here’s what each does:

- Purpose: Stops the event from bubbling up to parent elements.
- How it Works: When an event (e.g., a click) occurs, it normally propagates (bubbles) up the DOM tree, triggering any event listeners on parent elements. Calling stopPropagation() prevents this.
- Example:
```javascript
document.querySelector(".child").addEventListener("click", (event) => {
  event.stopPropagation(); // Stops the event from reaching the parent
  console.log("Child clicked!");
});

document.querySelector(".parent").addEventListener("click", () => {
  console.log("Parent clicked!");
});
```
If you click on the .child element, only the "Child clicked!" message will be logged, because stopPropagation() prevents the click event from reaching .parent.


