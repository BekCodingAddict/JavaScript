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

### When to Use Them Together

You might want to stop both the default action and event propagation, like when you have nested clickable elements and also want to prevent the default action of a link or form:
```javascript
document.querySelector(".button").addEventListener("click", (event) => {
  event.preventDefault();
  event.stopPropagation();
  console.log("Button click handled, no default action or bubbling!");
});
```
This combination is helpful if you’re building complex, nested UI components.
