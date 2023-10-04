The Direct Object Model, or DOM, is an in-memory object representation of an HTML document. It provides a way to interact with a web page using JS and provides functionality to build modern interactive user experiences.

When you're in the dev tools of a webpage looking at HTML, that's actually a visual representation of the DOM. It can be different from the HTML you wrote in a couple different ways:
 - If there are mistakes in your HTML that your browser fixed for you
 - JavaScript can manipulate the DOM

The DOM is a hierarchical structure of tree nodes
 - Besides the nodes that represent HTML tags and automatic insertions, the DOM includes other nodes (i.e. text nodes that appear in the document)
 - There are also whitespace text nodes we call empty nodes, but all text nodes are actually the same. Empty nodes are not reflected visually in the web browser.

In the context of DOM, a node is a single point in the node tree

The `document` node is the top most DOM node that represents the entire HTML document
 - Since it's the parent of all nodes in the DOM, we can use it to call `querySelector` and search the entire DOM for an element that matches a selector
 - ie. to find the first paragraph tag in the HTML: `document.querySelector('p')

The `nodeName` property contains a string that represents the node type 
 - For text nodes, the `nodeName` is `#text` for comments, it's `#comment`

`nodeType` returns a number that represents a node type constant

the `nodeValue` property returns the value of a node. Element nodes don't have values. The value of textNodes is the textual content of the node
 - When you need the text within an element, you can use the `textContent` property. You can think of it as the `nodeValue` for all the Element's child nodes concatenated to a single string.

### Nodes and Elements
 - All DOM objects are nodes
 - All DOM objects have a type that inherits from Node, which means they all have properties and methods they inherit from Node.
 - The most common DOM object types are element and text
 - The element type is further broken down into dozens of subtypes

A node's type is important because it determines what properties and methods it provides to a developer

`EventTarget` is at the top of the inheritance hierarchy of the DOM. It provides the event handling behavior that supports interactive web apps. `Node` provides
common behavior to all nodes.

## Traversing Nodes
Parent nodes have the following properties:
 - `childNodes`: live collection of all child nodes
 - `firstChild`: `childNodes[0]` or `null`
 - `lastChild`

Child Nodes have the following properties:
 - `parentNode`: immediate parent
 - `nextSibling`: `parentNodes.childNodes[n+1]` or `null`
 - `previousSibling`: `parentNodes.childNodes[n-1]` or `null`

Walking the tree describes a process of visiting every node that has a child, grandchild, etc relationship with a given node, and doing something with each of them.
We use a recursive function to do this:

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

This solution has one function that walks the tree and one that does something with each node (logs the `nodeName`)

### Element Attributes

We can access the attributes of an element using these methods:
 - `getAttribute(name)` to retrieve the value of some attribute `name`. Returns value of attribute as string
 - `setAttribute(name, newValue)` to set attribute of name to newValue. Returns undefined
 - `hasAttribute(name)` to check whether attribute has `name`. Returns true or false.

You can access `id`, `name`, `title`, and `value` values using property access and assignment operations
 - i.e. `p.id = "complex"`
 - `class` uses `className` property since the former is a reserved keyword

The `classList` property is usually better to use. `classList` references a special array-like `DOMTokenList` object that has its own properties and methods

The `style` attribute on an Element references a `CSSStyleDeclaration` object. You can use the `style` attribute to alter any CSS property

### Finding DOM Nodes
We can use `document.getElementById(id)` to return an element with a given id

Using our `walk` function to get elements by name:
```JS
function getElementsByTagName(tagName) {
  let matches = [];

  walk(document.body, (node) => {
    if (node.nodeName.toLowerCase() === tagName) {
      matches.push(node);
    }
  });

  return matches;
}

getElementsByTagName("p").forEach((paragraph) =>
  paragraph.classList.add("article-text")
);
```

DOM provides a similar method for tags and classes:
 - `document.getElementsByTagName(tagName)` returns `HTMLCollection` or `NodeList` of matching elements
 - `document.getElementsByClassName(className)` returns `HTMLCollection` or `NodeList` of matching elements
 - These methods return array-like objects, not actual arrays
 - Whether `HTMLCollection` or `NodeList` is returned depends on the browser

We can also find elements by using a CSS selector:
 -  `document.querySelector(selectors)` returns the first matching element or `null`
 -  `document.querySelectorAll(selectors)` returns `NodeList` of matching elements
 -  These methods are available on all elements, not just `document`

```JS
<div id="divOne"></div>
<div id="divTwo"></div>
```
```JS
> document.querySelector('#divTwo, #divOne');
= <div id="divOne"></div>    // returns the first matching element;
                             // div with an id of `divOne` matched first
> document.querySelectorAll('#divTwo, #divOne');
= NodeList(2) [div#divOne, div#divTwo]
```

The `textContent` property allows you to access the text of an element.
 - ie. `document.querySelector('a').textContent` finds the text associated with the first anchor tag
 - be careful when setting `textContent`, doing so removes all child nodes from the element and replaces it with a text node that contains the value
 - The best strategy to update the text with JS is place the text within an element. The element type does not matter (`div` or `span`, etc)

### Creating and Moving DOM Nodes
We can add a paragraph with `createElement` and `appendChild`

```JS
let paragraph = document.createElement('p');
paragraph.textContent = 'This is a test.';
document.body.appendChild(paragraph);
```

You can create nodes in two ways. You can create empty nodes with the `document.create` methods, or you can clone an existing node hierarchy:
 - `document.createElement(tagName)` returns a new element node
 - `document.createTextNode(text)` returns a new text node
 - `node.cloneNode(deepClone)` returns a copy of `node`
   - typically use `true` for the `deepClone` argument
  
You can append, insert, or replace nodes with methods on the node's parent:
 - `parent.appendChild(node)` Appends a node to the end of parent.childNodes
 - `parent.insertBefore(node, targetNode)` Inserts a `node` into `parent.childNodes` before `targetNode`
 - `parent.replaceChild(node, targetNode)` removes `targetNode`  from `parent.childNodes` and inserts `node` in its place

`document.appendChild` causes an error. Use `document.body.appendChild` instead

These methods insert a node before, after, or within an Element:
 - `element.insertAdjacentElement(position, newElement)` Inserts `newElement` at `position` relative to `element`
 - `element.insertAdjacentText(position, text)` Inserts Text node that contains `text` at `position` relative to `element`

** `position` must be a string value: `beforebegin`, `afterbegin`, `beforeend`, `afterend`

You can remove a node using:
 - `node.remove()`
 - `parent.removeChild(node)`







