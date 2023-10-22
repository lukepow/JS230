## Lesson 1: the DOM

###  Node properties
- `nodeName`
- `nodeValue` - for text nodes, the text value
- `textContent` - for non-text nodes, the text value
- `p instanceof Element` - checks whether an object has a type that matches or inherits from a named type
- `tagName` - checks the HTML tag name

### Traversing Nodes
- `childNodes` live collection of all child nodes
- `firstChild` and `lastChild`
- `parentNode`
- `nextSibling` and `previousSibling`

Walking the DOM Tree:
```JS
// walk() calls the function "callback" once for each node
function walk(node, callback) {
  callback(node);                                                   // do something with node
  for (let index = 0; index < node.childNodes.length; index += 1) { // for each child node
    walk(node.childNodes[index], callback);                         // recursively call walk()
  }
}

walk(document.body, node => {                                // log nodeName of every node
  console.log(node.nodeName);
});
```

### Element Attributes
 - `getAttribute(name)` - retrieve value of attribute as a string
 - `setAttribute(name, newvalue)`
 - `hasAttribute(name)` - returns true or false
 - You can access `id`, `name`, `title`, `className` and `value` attributes as properties of the `Element`
 - You can interact with the `classList` property with `add(name)`, `remove(name)`, `toggle(name)`, `contains(name)`, and `length`
 - You can use the `style` attribute as follows: `h1.style.color = 'red';`

### Creating and Moving DOM Nodes
```JS
let paragraph = document.createElement('p');
paragraph.textContent = 'This is a test.';
document.body.appendChild(paragraph);
```

 - `node.cloneNode(deepClone)` - argument should be true or false depending on if you want a deep clone
 - `parent.appendChild(node)` - append node to the end of `parent.childNodes`
 - `parent.insertBefore(node, targetNode)`
 - `parent.replaceChild(node, targetNode)`
 - `element.insertAdjacentElement(position, newElement)` - inserts newElement at position relative to element
 - `element.insertAdjacentText(position, text)`
   - `position` must be `beforebegin`, `afterbegin`, `beforeend`, or `afterend`
 - `node.remove()` and `parent.removeChild(node)`
 -   



