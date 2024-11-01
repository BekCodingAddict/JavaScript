## event.preventDefault()

>In JavaScript, event.stopPropagation() and event.preventDefault() are commonly used to control how events behave in the DOM. Here’s what each does:

- Purpose: Prevents the default behavior of an element.
- How it Works: Some elements have default actions tied to them (e.g., links navigating to a URL, form submissions). Calling preventDefault() stops these default actions without stopping event propagation.
  Example:
```javascript
document.querySelector("a").addEventListener("click", (event) => {
  event.preventDefault(); // Prevents link navigation
  console.log("Link click prevented!");
});
```
In this example, if you click on the link, the browser won’t navigate to the link’s URL, but "Link click prevented!" will still be logged.

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
