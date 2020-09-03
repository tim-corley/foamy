## Virtual DOM

The (regular) DOM - Documet Object Model - is a tree representation of the page, starting from the `<html>` tag and going into every child - which are called nodes. this tree is kept in browser memory and directly linked to what is displayed on a page. the DOM has an API that you can use to traverse it, access nodes, filter them, and modify them. 

 - thie DOM API syntax:
  ```javascript
  document.getElementById(id)
  document.createElement(name)
  parentNode.appendChild(node)
  element.innerHTML
  element.getAttribute()
  window.scrollTo()
  ...
  ```

React keeps a copy of the DOM - this is called the Virtual DOM 

Each time the DOM change the browser has to perform two operations:
 - repaint - visual/content change that does not impact the layout or positioning relative to other elements
 - reflow - recalculate the layout of a portion of the page or the entire page

React uses a virtual DOM to help the browser use less resources when changes are required. 

When `setState()` is called on a component - specifying a state different than the previous one - React marks that component as __dirty__. React ony updates when a component changes the state explicitly.

What happens next:
 - React updates the Virtual DOM relative to the components marked as dirty
 - Run the diffing alogorithm to reconcile the changes
 - Updates the real DOM 

Why the Virtual DOM is helpful: __batching__
 - React batches much of the changes and performs a unique update to the real DOM by changing all the elements that need to be changed at the same time. So the repaint and reflow operations the browser must perform are executed just once. 