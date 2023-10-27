# Written Exam
## Document Object Model ([Lesson 1: The DOM](https://launchschool.com/lessons/ba24c7d4/assignments/b3398a18)) ([Lesson 1: A Hierarchy of Nodes](https://launchschool.com/lessons/ba24c7d4/assignments/b07683bb))

  - The Document Object Model, or DOM for short, is an object representation of an HTML document that can be interacted and manipulated by JavaScript. This provides the functionality to build interactive applications in the browser.

  - The DOM is a tree of nodes. Both elements and text nodes make up the structure of this tree.
      - Text nodes can contain just whitespace.
      - Remember that tags that have any whitespace between them will have a text node between them.
      - To traverse, you would have to systematically visit all child nodes recursively

```js
function walk(node, callback) {
  callback(node);                                                   // do something with node
  for (let index = 0; index < node.childNodes.length; index += 1) { // for each child node
    walk(node.childNodes[index], callback);                         // recursively call walk()
  }
}
```

### `Node` ([Lesson 1: Node Properties](https://launchschool.com/lessons/ba24c7d4/assignments/653b6917)) ([Lesson 1: Traversing Nodes](https://launchschool.com/lessons/ba24c7d4/assignments/c1ac1a3d)) ([Lesson 1: Creating and Moving DOM Nodes](https://launchschool.com/lessons/ba24c7d4/assignments/6e349f0c)) ([MDN: Node](https://developer.mozilla.org/en-US/docs/Web/API/Node))

  - `Node` is an abstract base class of which all other DOM nodes inherit. It contains common methods used among all node types.

  - All DOM objects are `Node`s

  - `nodeType` ([MDN: nodeType property](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeType))
      - Is used to determine a node's type.
      - `Node.ELEMENT_NODE` or `1` is an element node
      - `Node.TEXT_NODE` or `3` is a text node
      - `Node.COMMENT_NODE` or `8` is a comment node
      - `Node.DOCUMENT_NODE` or `9` is the document node

  - `nodeValue` ([MDN: nodeValue property](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeValue))
      - References the value of a node.
      - Element nodes do not have a value. `null`
      - Text nodes do, which is the text contained by the node

  - `childNodes` ([MDN: childNodes property](https://developer.mozilla.org/en-US/docs/Web/API/Node/childNodes))
      - Is a live collection `NodeList` of children the node is a parent of
      - A live collection updates with the DOM
      - `NodeList` is not an Array.

  - `firstChild` ([MDN: firstChild property](https://developer.mozilla.org/en-US/docs/Web/API/Node/firstChild))
      - Gets the first child node
      - If no child nodes, it returns `null`
      - Is read-only

  - `lastChild` ([MDN: lastChild property](https://developer.mozilla.org/en-US/docs/Web/API/Node/lastChild))
      - Gets the last child node
      - If no child nodes, it returns `null`
      - Is read-only

  - `nodeName` ([MDN: nodeName property](https://developer.mozilla.org/en-US/docs/Web/API/Node/nodeName))
      - References the name of the node
      - The value of `tagName` for an `Element`
      - `"#text"` for a text node
      - `"#comment"` for a comment.
      - `"#document"` for the document node

  - `textContent` ([MDN: textContent property](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent))
      - Is the text content of all the nodes inside the `Element`
      - Gets the text from all elements
      - when overwritten, removes all child nodes and adds one text node.

  - `parentNode` ([MDN: parentNode property](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentNode))
      - Is the parent of the node
      - Is read-only
      - `Document` never has a parent, thus will have a `null` value for this property

  - `parentElement` ([MDN: parentElement property](https://developer.mozilla.org/en-US/docs/Web/API/Node/parentElement))
      - Is the parent if the parent is an `Element`
      - Is read-only
      - Returns `null` if the parent is not an `Element`
      - Returns `null` if there is no parent

  - `nextSibling` ([MDN: nextSibling property](https://developer.mozilla.org/en-US/docs/Web/API/Node/nextSibling))
      - Is the next child node of the parent after the receiving node.
      - If there is no node following this one, it has a value of `null`
      - `node.parentNode.childNodes[n + 1]` if `n` is the current node's position.

  - `previousSibling` ([MDN: previousSibling property](https://developer.mozilla.org/en-US/docs/Web/API/Node/previousSibling))
      - Is the previous child node of the parent before the receiving node.
      - If there is no node preceding this one, it has a value of `null`
      - `node.parentNode.childNodes[n - 1]` if `n` is the current node's position.

  - `cloneNode(deepClone)` ([MDN: cloneNode() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/cloneNode))
      - Is a method that returns a copy of the node
      - `deepClone` is an optional argument.
          - If `true` it will clone each individual node within its subtree
          - If `false`, which it defaults to, it only copies the node it was called on
      - Does not copy event listeners added with `addEventListener()`
      - The new node will have no parent and not be part of the document until inserted

  - `appendChild(node)` ([MDN: appendChild() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild))
      - Adds a node to the end of the list of children of a specified parent node
      - Returns the newly added node
      - If the node given existed in the document, `appendChild` will move it from its current location to the new location.

  - `insertBefore(node, targetNode)` ([MDN: insertBefore() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore))
      - Inserts a node prior to a target child of a specified parent node.
      - If the node being inserted already exists in the document, `insertBefore` moves it to its new location
      - Returns the added child
      - if `targetNode` is `null`, `insertBefore` acts like `appendChild`

  - `replaceChild(node, targetNode)` ([MDN: replaceChild() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/replaceChild))
      - Repaces a target child node with a new node for a specified parent node
      - Returns the target node that was replaced
      - If the new node being added already exists in the document, `replaceChild` moves it from its current location.
      - The removed node will be removed from the document have no parent node.

  - `removeChild(node)` ([MDN: removeChild() method](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild))
      - Removes a child node from a parent
      - Returns the removed node
      - The removed node is no longer part of the document and has no parent

### `Document` ([Lesson 1: Node Properties](https://launchschool.com/lessons/ba24c7d4/assignments/653b6917)) ([Lesson 1: Finding DOM Nodes](https://launchschool.com/lessons/ba24c7d4/assignments/07b3fded)) ([Lesson 1: Creating and Moving DOM Nodes](https://launchschool.com/lessons/ba24c7d4/assignments/6e349f0c)) ([MDN: Document](https://developer.mozilla.org/en-US/docs/Web/API/Document))

  - `Document` is the top level `Node` for the tree, everything descends from it.

  - `Document` inherits `Node`

  - is represented by the `document` variable in the browser

  - `body` ([MDN: body property](https://developer.mozilla.org/en-US/docs/Web/API/Document/body))
      - references the body element tag for the document

  - `getElementById(id)` ([MDN: getElementById() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById))
      - Finds the first element by its `id` name (There should only be one)
      - Returns `null` if one is not found

  - `getElementsByTagName(tagName)` ([MDN: getElementsByTagName() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName))
      - Gets a list of all elements with a `tagName`
      - Returns a live `HTMLCollection`
      - `tagName` does not have to be uppercase
      - Searches the whole document

  - `getElementsByClassname(className)` ([MDN: getElementsByClassName() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName))
      - Gets a list of all elements that have the given `className`
      - Returns a live `HTMLCollection`
      - searches the whole document

  - `querySelector(selectors)` ([MDN: querySelector() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector))
      - Finds the first element that matches the css `selectors`
      - Returns `null` if an element is not found
      - searches the whole document

  - `querySelectorAll(selectors)` ([MDN: querySelectorAll() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll))
      - Gets a list of all elements that match the css `selectors`
      - Returns a static `NodeList`
      - searches the whole document

  - `createElement(tagName)` ([MDN: createElement() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement))
      - Creates an object that inherits from `Element` that has `tagName`
      - The new element is not part of the document until inserted.

  - `createTextNode(text)` ([MDN: createTextNode() method](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode))
      - Creates a new `TextNode` that contains `text`
      - The new `TextNode` is not part of the document until inserted.

### `Element` ([Lesson 1: Element Attributes](https://launchschool.com/lessons/ba24c7d4/assignments/c4315283)) ([Lesson 1: Traversing Elements](https://launchschool.com/lessons/ba24c7d4/assignments/06c73362)) ([MDN: Element](https://developer.mozilla.org/en-US/docs/Web/API/Element))

  - `Element` is the base class for every element in the HTML document and gives common functionality to all elements

  - `Element` inherits `Node`

  - `tagName` ([MDN: tagName property](https://developer.mozilla.org/en-US/docs/Web/API/Element/tagName))
      - Is the name for the tag in HTML
      - Will be in all capital letters

  - `getAttribute(name)` ([MDN: getAttribute() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/getAttribute))
      - returns the value of the `name` attribute on the element
      - returns `null` or `""` if it does not exist

  - `setAttribute(name, newValue)` ([MDN: setAttribute() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/setAttribute))
      - Sets atrribute `name` to `newValue`
      - Creates or modifies it as needed

  - `hasAttribute(name)` ([MDN: hasAttribute() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/hasAttribute))
      - Checks if element has attribute `name`

  - `removeAttribute(name)` ([MDN: removeAtrribute() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/removeAttribute))
      - Remove attribute `name`, value and all, from an element

  - Common attribute properties:
      - `id` ([MDN: id property](https://developer.mozilla.org/en-US/docs/Web/API/Element/id))
          - Is the `id` attribute attached to the element tag
      - `name`
          - Some elements, such as an input require a `name` attribute.
      - `title` ([MDN: HTMLElement: title property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/title))
          - Alt text usually
      - `value`
          - Some elements have a `value`
          - Will be string value.

  - `className` ([MDN: className property](https://developer.mozilla.org/en-US/docs/Web/API/Element/className))
      - The full value of the `class` attribute
      - same as invoking `getAttribute('class')`
      - Space separated class names.

  - `classList` ([MDN: classList property](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList))
      - Is a list of class names that make up the `class` attribute of the element
      - Is a live `DOMTokenList`
      - `add(name)`
          - appends `name` to the class names
      - `remove(name)`
          - If `name` is part of the class names, removes it
      - `toggle(name)`
          - If `name` is not part of the class names, add it
          - otherwise remove it
      - `contains(name)`
          - Checks if `name` is part of the class names
      - `length`
          - returns the number of class names

  - `style` ([MDN: HTMLElement: style property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/style))
      - List of all css styles applied to this element
      - Is a live `CSSStyleDeclaration` and is read-only
      - can access CSS properties as properties
          - names with `-` are instead camelCased
          - though `-` names can be used with bracket notation

  - `children` ([MDN: children property](https://developer.mozilla.org/en-US/docs/Web/API/Element/children))
      - read-only list of child elements
      - is a live `HTMLCollection`
      - Only contains `Element` objects

  - `firstElementChild` ([MDN: firstElementChild property](https://developer.mozilla.org/en-US/docs/Web/API/Element/firstElementChild))
      - First child element
      - `element.children[0]` or `null`

  - `lastElementChild` ([MDN: lastElementChild property](https://developer.mozilla.org/en-US/docs/Web/API/Element/lastElementChild))
      - last child element
      - `element.children[element.children.length - 1]` or `null`

  - `childElementCount` ([MDN: childElementCount property](https://developer.mozilla.org/en-US/docs/Web/API/Element/childElementCount))
      - The number of children elements the element has
      - `element.children.length`

  - `nextElementSibling` ([MDN: nextElementSibling property](https://developer.mozilla.org/en-US/docs/Web/API/Element/nextElementSibling))
      - The next child element of the parent element relative to itself
      - `parent.children[n + 1]` where `n` is the current elements index or `null`

  - `previousElementSibling` ([MDN: previousElementSibling property](https://developer.mozilla.org/en-US/docs/Web/API/Element/previousElementSibling))
      - The previous child element of the parent element relative to itself
      - `parent.children[n - 1]` where `n` is the current elements index or `null`

  - `remove()` ([MDN: remove() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/remove))
      - Removes the element from the document.
      - The element is no longer rendered, nor will it respond to events
      - Event listeners stay on it.

  - Insertion:
      - `insertAdjacentElement(position, newElement)` ([MDN: insertAdjacentElement() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentElement))
          - Inserts a `newElement` relative to the calling elements `position`
          - if the `newElement` is already part of the document, removes it before adding it to its new position
      - `insertAdjacentText(position, text)` ([MDN: insertAdjacentText() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentText))
          - Inserts a new `TextNode` with string `text` as its content relative to the calling elements position
      - `insertAdjacentHTML(position, html)` ([MDN: insertAdjacentHTML() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/insertAdjacentHTML))
          - Inserts `html` as string relative to the position of the calling element
          - The `html` is then converted to `DOM` objects and inserted
      - `position` is:
          - `"beforebegin"`
              - Before the element
          - `"afterbegin"`
              - Before the first child of the element, as a child of the element
          - `"beforeend"`
              - After the last child of the element, as a child of the element
          - `"afterend"`
              - After the element

  - `innerHTML` ([MDN: innerHTML property](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML))
      - Gets or sets the HTML contained within the element
      - Overwrites all within it when set
      - Converts HTML into DOM objects and inserts them as children

  - `getElementsByTagName(tagName)` ([MDN: getElementsByTagName() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByTagName))
      - Gets a list of all elements with a `tagName`
      - Returns a live `HTMLCollection`
      - `tagName` does not have to be uppercase
      - Searches the subtree starting from, but not including, calling `Element`.

  - `getElementsByClassname(className)` ([MDN: getElementsByClassName() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/getElementsByClassName))
      - Gets a list of all elements that have the given `className`
      - Returns a live `HTMLCollection`
      - Searches the subtree starting from, but not including, calling `Element`.

  - `querySelector(selectors)` ([MDN: querySelector() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelector))
      - Finds the first element that matches the css `selectors`
      - Returns `null` if an element is not found
      - Searches the subtree starting from, but not including, calling `Element`.

  - `querySelectorAll(selectors)` ([MDN: querySelectorAll() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/querySelectorAll))
      - Gets a list of all elements that match the css `selectors`
      - Returns a static `NodeList`
      - Searches the subtree starting from, but not including, calling `Element`.

  - `closest(selectors)` ([MDN: closest() method](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest))
      - Finds the first direct ancestor that matches selectors
      - If none is found, returns `null`
      - Checks element itself

## Asynchronous JavaScript

  - JavaScript is a mostly single threaded language

  - JavaScript has what is called the Event Loop, in which it queues asyncronous tasks for execution.

  - The event loop can only push execution on the call stack when it is empty
      - ([Youtube: What the heck is the event loop anyway](https://www.youtube.com/watch?v=8aGhZQkoFbQ&embeds_referring_euri=https%3A%2F%2Flaunchschool.com%2F&feature=emb_imp_woyt))

### `setTimeout` and `setInterval` ([Lesson 2: Asynchronous Execution with setTimeout](https://launchschool.com/lessons/519eda67/assignments/be20d8f9)) ([Lesson 2: Repeating Execution with setInterval](https://launchschool.com/lessons/519eda67/assignments/c1f5bc94))

  - `setTimeout(callback, delay)` ([MDN: setTimeout() global function](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout))
      - calls `callback` sometime after `delay` has been lapsed
          - The timing of the call depends on the call stack being empty, thus isn't 100% accurate, a `delay` of `0` still has to wait for the call stack to be empty.
      - `delay` is in milliseconds
      - returns an `id` that can be used with `clearTimeout(id)` to stop a timed task
      - Not part of the JavaScript standard, but most environments make it available.

  - `setInterval(callback, interval)` ([MDN: setInterval() global function](https://developer.mozilla.org/en-US/docs/Web/API/setInterval))
      - calls `callback` every `interval` has lapsed.
      - `interval` is in milliseconds
      - returns an `id` that be used with `clearInterval(id)` to stop it
      - Not part of the JavaScript Standard, but most environments make it available.

### Event Listeners(Event Handlers) ([Lesson 2: User Interfaces and Events](https://launchschool.com/lessons/519eda67/assignments/ca8101e5)) ([Lesson 2: Page Lifecycle Events](https://launchschool.com/lessons/519eda67/assignments/6ce4b02c)) ([Lesson 2: Page Lifecycle Events](https://launchschool.com/lessons/519eda67/assignments/6ce4b02c)) ([Lesson 2: User Events](https://launchschool.com/lessons/519eda67/assignments/23af603e)) ([Lesson 2: Capturing and Bubbling](https://launchschool.com/lessons/519eda67/assignments/1753933a)) ([Lesson 2: Preveinging Propagation and Default Behaviors](https://launchschool.com/lessons/519eda67/assignments/170c068b)) ([Lesson 2: Event Delegation](https://launchschool.com/lessons/519eda67/assignments/c89c4059))

  - UI needs to be able to respond to user interactions which will not happen sequentially, thus need to be handled asyncronously
      - This means that they are inherently event-driven.

  - An **event** is an object that represents some occurence
      - It contains information describing what happend and where.
      - browser triggers events for different actions such as page loading, user input, and browser performing specific actions

  - `addEventListener(type, eventHandler, useCapture)` ([MDN: EventTarget: addEventListener() method](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener))
      - Allows you to register "event listeners" that watch for events on specific nodes of the document.
      - `eventHandler(event)` takes a callback that will be called when the event fires on the node or its descendants
          - The `event` object will give information about the `event` based on `type`
          - `event.type` - the type of event that fired
          - `event.currentTarget` - the object the event is attached to
          - `event.target` - the object on which the event occured
          - The execution context on the callback will be `event.currentTarget`
          - Will also have properties related to the event such as:
              - `key` - a string representation of the key pressed
              - `'button'` - which mouse button clicked
      - `type` is a string describing the event type ([Event reference](https://developer.mozilla.org/en-US/docs/Web/Events))
          - `'DOMContentLoaded'` - fires once the DOM is constructed
          - `'Load'` - fires once the page is displayed and embedded assets are loaded
          - `'click'` - The user clicks somewhere
          - `'keydown'` and `'keyup'` - occurs as a user presses a key
          - `'mouseenter'` and `'mouseleave'` happen as a user moves the mouse
          - `'submit'` happens as a user submits a form
          - `'focus'` happens when you focus a form input
          - `'blur'` opposite of `'focus'`
          - `'contextmenu'` happens on right click
      - `useCapture` defines if the event handler should trigger during the capture phase
          - defaults to `false` and triggers during the bubble phase instead.

  - Code that accesses the DOM should be executed only after the `DOMContentLoaded` event fires
      - Best practice is to wrap such code in a callback attached to a `DOMContentLoaded` event listener
      - This is because JavaScript is evaluated prior to the DOM being constructed, thus code will run before the DOM is fully constructed, thus may introduce errors.

  - **Capturing phase** and **Bubbling Phase**
      - When an event happens, it propagates through its handlers in three distinct phases.
          - Capturing Phase
              - it goes through the heirarchy starting with the top down to the `target` of the event sending the event target to each node inbetween
          - Target Phase
              - Technically part of both the capturing and bubbling phases, but is when the event fires on the `target`
          - Bubbling Phase
              - Starting with `target`, the event is sent to each of its ancestors, "bubbling" up.
      - We can stop propagation using two methods on the event object
          - `preventDefault()` ([MDN: preventDefault() method](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault))
              - Prevents the browser from implementing the default action from its event
              - Like stopping a form from being submitted or stopping a link from loading a new page when clicked
          - `stopPropagation()` ([MDN: stopPropagation() method](https://developer.mozilla.org/en-US/docs/Web/API/Event/stopPropagation))
              - stops the event from continuing its propagation through the capturing/bubbling phases.

  - Event Delegation is the practice of registering a event listener on a common ancestor and handling all child events through a single event handler.
      - Lessens the number of event handlers you must register, thus improving performance.
      - Allows new elements to be added and still be handled by the same event handler instead of having to adding a new one each time you add another.
      - Best practice to bind handlers to individual elements when project is small and reduce as the code grows in size.

### `Promise` ([Assignment: Promises and async/await](https://launchschool.com/gists/58925b8e))

  - `Promise` is an object that represents and eventual value.

  - `Promises` resolve asynchronously and allow for methods to deal with that eventual value

  - a `Promise` can only succeed or fail once, and only one of the two options happen

  - Promises fix some of the messiness of events for uses that don't necessarily need to hook up an event listener like requests.

  - `Promise(executor)` ([MDN: Promise() constructor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/Promise))
      - Used to create a `Promise` object
      - `executor` is a callback that receives two functions as parameters: `resolve` and `reject`
          - `resolve` takes a value that would be the return value of the promise
          - `reject` takes a value that describes the error
      - Any errors thrown during the promise will cause the promise to be rejected

  - Promise can be in one of three states:
      - pending: neither fulfilled nor rejected
      - fulfilled: operation was completed successfully
      - rejected: operation failed

  - You can later add a success/failure callback asynchronously
      - These can be chained to occur sequentially
      - `then(onFulfilled, onRejected)` ([MDN: Promise.prototype.then()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then))
          - Is used to act on a resolved promise
          - returns a `Promise` object
          - can be chained
          - if a promise is rejected, the onRejected callback is used, if none is given it will be replaced with an internal thrower function that returns a rejected promise.
      - `catch(onRejected)` ([MDN: Promise.prototype.catch()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/catch))
          - Schedules a callback to be called when a promise is rejected
          - Shortcut for `Promise.prototype.then(undefined, onRejected)`
      - `finally(onFinally)`
          - Schedules a callback to be called regardless of whether it was resolved or rejected
          - Returns an equivalent promise to the one it was called on.

  - `Promise.race(iterable)` ([MDN: Promise.race()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/race))
      - Takes a collection of promises
      - Creates a `Promise` that Settles with the same state as the first promise in the collection, whether that is resolved or rejected
      - All promises still execute.

  - `Promise.all(iterable)` ([MDN: Promise.all()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all))
      - Takes a collection of promises
      - Returns a Promise that either:
          - Fulfilled if all `Promise` objects in the collection are fulfilled.
          - Rejected when any `Promise` was rejected.
      - If a `Promise` is rejected it immediately is rejected when it is
      - Its fulfilled value is a collection of the values of the `Promises` or the rejection reason of the first rejected promise

  - `Promise.any(iterable)` ([MDN: Promise.any()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/any))
      - Opposite of `all()`, similar to `race()`
      - Resolves on the first promise resolving
      - Rejects if all rejected

  - `Promise.allSettled(iterable)` ([MDN: Promise.allSettled()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/allSettled))
      - Similar to `all()`
      - Resolves once all promises in collection are settled regardless of if they were resolved or rejected
      - returns an array of outcome objects(see docs)

  - `Promise.resolve(value)` ([MDN: Promise.resolve()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/resolve))
      - Resolves a promise into a non-thenable value
          - Continues to call `then()` until it receives a non-thenable value
      - If passed a non-thenable object, returns a promise that automatically resolves to that value.

  - `Promise.reject(reason)` ([MDN: Promise.reject()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/reject))
      - Returns a rejected `Promise`
      - essentially `new Promise((resolve, reject) => reject(reason))`

#### `async` and `await` ([MDN: async function expression](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/async_function)) ([MDN: await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await))

  - Syntactic sugar for promise fulfillment

  - `async` changes a function to an asyncronous function, which wraps it in a promise(thus returning a promise)

  - `await` is like a `then` method stopping execution until the promise object it is awaiting is settled and either returning its value or throwing its error.
      - Technically works for any object with a `then` method that works like a promise - a "thenable" object
      - `await` can only be used in an asynchronouse function or at the top level
      - `await` will convert non-`Promise` values to a promise before it unwraps the promise

## Web APIs ([Book: What is an API?](https://launchschool.com/books/working_with_apis/read/defining_api#whatisanapi))

  - An **API** is an Application Programming Interface
      - Provides a way for computer systems to interact with each other
      - A web API is an API that works through HTTP

  - An API provider is the system that provides the API for other parties to use.
      - Would be the server normally

  - An API consumer uses the API to do something.
      - Would normally be the client. A server could be a client.

  - APIs can:
      - Share Data
      - Enable Automation
      - Levarage Existing Services
          - Searching multiple platforms
          - Allows you to build on top of other specialized systems to focus on your objectives and not worry about every single part

  - APIs deliver structured data by serializing it ([Book: Media Types](https://launchschool.com/books/working_with_apis/read/media_types))
      - XML (Extensible Markup Language)
      - HTML
      - JSON (JavaScript Object Notation)

  - REST ([REST and CRUD](https://launchschool.com/books/working_with_apis/read/rest_and_crud))
      - REST is representational state transfer
      - Is a set of conventions for how to build APIs by using a resource-oriented philosophy and implementing CRUD.
          - Read -> GET
          - Create -> POST
          - Update -> PUT
          - Delete -> DELETE
      - RESTful APIs implement these conventions

| Objective | How |  | What |  |
|:---:|:---:|:---:|:---:|:---:|
|  | Operation | HTTP Method | Resource | Path |
| Get the information about a $RESOURCE | Read | GET | $RESOURCE | /$RESOURCEs/:id |
| Add a $RESOURCE to the system | Create | POST | $RESOURCEs Collection | /$RESOURCEs |
| Make a change to a $RESOURCE | Update | PUT | $RESOURCE | /$RESOURCEs/:id |
| Remove a $RESOURCE from the system | Delete | DELETE | $RESOURCE | /$RESOURCEs/:id |

### XMLHttpRequest ([Lesson 3: Making a Request with XMLHttpRequest](https://launchschool.com/lessons/3728e24b/assignments/8406c779)) ([XMLHttpRequest Events](https://launchschool.com/lessons/3728e24b/assignments/fbf53f89))
  - `XMLHttpRequest` ([MDN: XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest))
      - Used to make HTTP requests with JavaScript.
      - Inherits from EventTarget, thus can listen for events
      - Is not part of the language, instead is part of the browser API
      - Object must be constructed with `new XMLHttpRequest()` before any required methods can be called.

  - `XMLHttpRequest.prototype.open(method, url)` ([MDN: open() method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/open))
      - Initializes a request, must be called after the object is constructed, but before any other method or property change.
      - `method` is the HTTP method the request will make
      - `url` is the URL of the request.

  - `XMLHttpRequest.prototype.send(data)` ([MDN: send() method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/send))
      - Used to send the request asynchronously(synchronous requests exist, but don't use them)
      - result is delivered using events
      - `data` is optional and is the request's body.
      - If no `Accept` header has been set, it uses an `Accept` header with type `"*/*"`

  - `XMLHttpRequest.prototype.setRequestHeader(header, value)` ([MDN: setRequestHeader() method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/setRequestHeader))
      - Used to set header values for a request
      - `header` is the header name to be changed.
      - `value` is the value you want to set the header

  - `XMLHttpRequest.prototype.getResponseHeader(headerName)` ([MDN: getResponseHeader() method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/getResponseHeader))
      - Used to get a header value from a response
      - `headerName` is the name of the header you are looking for
      - If no header is available with that name, it returns `null`
      - If the response has not yet been received will return `null`

  - `XMLHttpRequest.prototype.abort()` ([MDN: abort() method](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/abort))
      - If a request has already been sent, aborts the request.
      - `readyState` is set to `XMLHttpRequest.UNSENT` and `status` is set to `0`.

  - `XMLHttpRequest` objects have these properties:
      - `status` ([MDN: status property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/status))
          - The status code of the response.
          - Is read-only
          - Will be `0` until the response is received
      - `statusText`([statusText property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/statusText))
          - String of the text of the response text (like `"OK"`)
          - Is read-only
          - Until response is received will be empty string.
      - `readyState` ([readyState property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState))
          - Represents the current state of the request
              - `0` `UNSENT` - `open()` has not been called
              - `1` `OPENED` - `open()` has been called
              - `2` `HEADERS_RECEIVED` - `send()` has been called and the headers and status are available
              - `3` `LOADING` - Downloading; `responseText` holds partial data
              - `4` `DONE` - The operation is complete
          - Is read-only
      - `responseText` ([MDN: responseText property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseText))
          - The raw text body of the response
          - `null` if the request failed
          - `""` if the request has not be sent yet
          - Until full response is received will contain what has been
              - Has full text at `XMLHttpRequest.DONE`.
          - is read-only
      - `response` ([response property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/response))
          - Is the parsed response text in the form of an object based on the `responseType` property
              - `ArrayBuffer`
              - `Blob`
              - `Document`
              - or a simple `Object`
          - Is `null` if not complete or unsuccessful and `responseType` is not `'text'`
          - Is the same as `responseText` if `responseType` is `'text'`
          - is read-only
      - `responseType` ([responseType property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/responseType))
          - Specifies the type of data contained in the response
          - Based on what it is, `response` will parse the body accordingly
          - Set after `open()`, but before `send()`
          - Values can be:
              - `""` same as `"text"`
              - `"arraybuffer"` is a `ArrayBuffer` contianing binary data
              - `"blob"` is a `Blob` containing binary data
              - `"document"` is a HTML or XML document based on MIME type of the received data
              - `"json"` makes an `Object` based on the JSON
              - `"text"` raw text as a string.
      - `timeout` ([MDN: timeout property](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout))
          - How many milliseconds it will wait until the request times out
          - default is `0`, which means there is no timeout.
          - When a timeout happens, a `'timeout'` event will fire.

  - `XMLHttpRequest` can listen for events.
      - `'loadstart'` - Occurs when request is sent
      - `'loadend'` - Occurs once response is loaded and all other events have fired.
      - `'load'` - Fires when the complete response loaded successfully
          - Does not necessarily mean that the request was completely succesful, just that we got a response.
      - `'abort'` - Fires when a request was interrupted
      - `'error'` - fires when an error occured
      - `'timeout'` - fires when a response wasn't received before the timeout period finished.
      - `event.target` will be the request listening for the response.

### Data Serialization ([Lesson 3: Data Serialization](https://launchschool.com/lessons/3728e24b/assignments/8d61ddc0)) ([Lesson 3: Example: Loading HTML via XHR](https://launchschool.com/lessons/3728e24b/assignments/9fe48235)) ([Lesson 3: Example: Submitting a Form via XHR](https://launchschool.com/lessons/3728e24b/assignments/df377cb8)) ([Lesson 3: Example: Loading JSON via XHR](https://launchschool.com/lessons/3728e24b/assignments/073eee03)) ([Lesson 3: Example: Sending JSON via XHR](https://launchschool.com/lessons/3728e24b/assignments/b4d20ff2))

  - URL Encoding
      - Takes place when we encode the data to be added as a query string
      - Can set the `'Content-Type'` header with a value of `'application/x-www-form-urlencoded; charset=utf-8'` to use on non-GET requests as part of the body
      - `encodeURIComponent(string)` ([MDN: encodeURIComponent](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/encodeURIComponent))
          - Encodes a string to a uri encoed string by replacing certain characters with escape sequences.
          - use with key and value to make query strings and url encoded bodies.

  - Multipart Forms
      - POST request that includes a file upload or `FormData` objects to collect data.
      - Does not encode anything, instead splits the body into multiple sections.
      - `'Content-Type'` set to `'multipart/form-data'`
      - `FormData(form)` ([MDN: FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData))
          - Used to convert a forms input into a Multi part data
          - Only gets fields with the `name` attribute
          - Can be sent directly with `send()`

  - JSON
      - JavaScript Object Notation
      - `'Content-Type'` is `'application/json; charset=utf-8'`
      - `JSON.stringify(object)` ([MDN: JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify))
          - Used to serialize a avaScript object to a JSON string.
          - Can't serialize complex types like `Date`
      - `JSON.parse(string)` ([JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse))
          - Parses a JSON string back into a simple JavaScript object or array(or string, number boolean, null)
      - `responseType = 'json'`
          - By setting `responseType` on the `XMLHttpRequest` object, the response will automatically get parsed from JSON

## CORS ([Lesson 3: Cross-Domain XMLHttpRequests with CORS](https://launchschool.com/lessons/3728e24b/assignments/b86f1e8e))

  - An origin is the combined scheme, hostname, and port of the URL.

  - A cross-origin request occurs when a page tries to access a resource from a different origin.

  - Cross-domain requests have security vulnerabilities
      - An attacker can masquarade as an application from a different origin to do malicious things.

  - `XMLHttpRequest` can not send a cross-origin request by default.

  - CORS
      - Stands for Cross-Origin Resource Sharing
      - Is a specification that defines how the browser and server must communicate when accessing resources across origins.
      - `XMLHttpRequest` will have a `Origin` header that is the origin of the requesting page
          - The server uses this header to determine if it should send a corresponding header in the response.
          - The browser automatically adds the `Origin` header.
          - If the server wants to make the resource available it will set the `Access-Control-Allow-Origin` header either to:
              - The exact origin of the request
              - or `*`, which means any origin.
          - If the browser does not receive the correct `Access-Control-Allow-Origin` header, it will throw an error and not let the script access the response even it sent the correct response.

### Fetch API ([Lesson 4: AJAX Requests](https://launchschool.com/lessons/e1800f40/assignments/d70d5f28)) ([MDN: Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API))

  - `fetch(resource, options)` ([MDN: fetch() global function](https://developer.mozilla.org/en-US/docs/Web/API/fetch))
      - Is a promise based alternative to `XMLHttpRequest`
      - `resource` is the URL
      - `options` are various custom settings for the request
          - `method` - the HTTP method like `'GET'`
          - `headers` - headers you want to set for the request
          - `body` - The data to be sent
      - Returns a `Promise` that resolves to a `Response` object

  - `Response` ([MDN: Response](https://developer.mozilla.org/en-US/docs/Web/API/Response))
      - Represents a response
      - `status` - the status code of the response
      - `headers` - an object with the response headers
          - `get(headerName)` - retrieves a header value
      - `json()` - returns a promise that resolves to an object created by parsing received JSON.
      - `text()` - returns a promise that resolves to a text representation of the response body.

## Third Party Libraries
### jQuery ([Lesson 4: jQuery](https://launchschool.com/lessons/e1800f40/assignments/3fbf6d66)) ([Lesson 4: Read: jQuery DOM Traversal](https://launchschool.com/lessons/e1800f40/assignments/ac2edb24)) ([Lesson 4: Read: jQueryEvents](https://launchschool.com/lessons/e1800f40/assignments/3fc62ebf)) ([Lesson 4: AJAX Requests](https://launchschool.com/lessons/e1800f40/assignments/d70d5f28))

  - jQuery is a library that provides an API to work with the DOM and browser APIs.

  - jQuery is a function that wraps a collection of DOM elements and some methods into an object.
      - either `jQuery()` or more commonly `$()`
      - It always wraps a collection, not a single element, though it could be a collection of 1
      - When a single element is passed to it, it wraps it as a collection of just that element
      - When a string is passed, it treats it like it calls `querySelectorAll()` and wraps the result in the object
      - jQuery collections are not live.
      - If a function is passed, it treats it like it was added to the `'DOMContentLoaded'` loaded event listener as a callback
          - You can also do `$(document).ready(function() { ... })`
      - methods called on the jQuery object typically apply to all elements in the inner collection.

  - Getter and Setter
      - Some jQuery methods have two forms. If they take a single argument, they are a getter. If they take two arguments, they are a setter.
      - EX: `css(property, value)` -  if you don't pass the `value`, it gets the value

  - Most jQuery methods allow for method chaining.
      - Setter methods and methods that don't return a specific value all return the current jQuery object.

  - Often jQuery methods allow for you to pass on object for multiple settings
      - EX: `css(propObject)` allows you to change multipe css properties by passing an object with property names as keys and their values as values.

#### Traversal

  - `parent(selector˚)` ([jQuery: .parent()](https://api.jquery.com/parent/))
      - Gets the parent of each element in the current collection and returns it as a jQuery collection of the parents
      - `selector˚` is an optional selector to filter out results
          - EX `$li.parent('.cool')` will only have parents that have the `cool` class

  - `closest(selector)` ([jQuery: .closest()](https://api.jquery.com/closest/))
      - Gets the closest ancestor for each element in current collection that matches a `selector`.
      - The elements themselves can also match.

  - `find(selector)` ([jQuery: .find()](https://api.jquery.com/find/))
      - Gets the descendants of each element in the current collection that matches a `selector`.
      - This travels as far down the DOM as it can.

  - `children(selector˚)` ([jQuery: .children()](https://api.jquery.com/children/))
      - Gets the children of each element in the current collection
      - `selector˚` is optional and will filter children by the selection
      - Only goes one level deep(direct children)

  - `next(selector˚)` ([jQuery: .next()](https://api.jquery.com/next/))
      - Gets the following sibling of each element in the current collection
      - `selector˚` is optional and will filter the results by the selection

  - `nextAll(selector˚)` ([jQuery: .nextAll()](https://api.jquery.com/nextAll/))
      - Gets all following siblings of each element in the current collection
      - `selector` is optional and will filter siblings by the selection

  - `prev(selector˚)` ([jQuery: .prev()](https://api.jquery.com/prev/))
      - Gets the preceding sibling of each element in the current collection
      - `selector˚` is optional and will filter the results by the selection

  - `prevAll(selector˚)` ([jQuery: .prevAll()](https://api.jquery.com/prevAll/))
      - Gets all preceding siblings of each element in the current collection
      - `selector˚` is optional and will filter siblings by the selection

  - `siblings(selector˚)` ([jQuery: .siblings()](https://api.jquery.com/siblings/))
      - Gets all siblings of each element in the current collection
      - `selector˚` is optional and will filter siblings by the selection

  - `first()` ([jQuery: .first()](https://api.jquery.com/first/))
      - Reduces the collection to the first element in the collection

  - `last()` ([jQuery: .last()](https://api.jquery.com/last/))
      - Reduces the collection to the last element in the collection

  - `get(index)` ([jQuery: .get(index)](https://api.jquery.com/get/#get1))
      - Returns the element at `index` in the collection
      - same as bracket notation.

#### Events

  - `on(events, selector˚, data˚, handler)` ([jQuery: .on()](https://api.jquery.com/on/))
      - Used to add event handlers to elements in collection.
      - `events` is a space-separated list of event types like `'click'`
      - `handler` is the call back for the event listener
      - `selector˚` is an optional selector that prevents the callback from being called on event targets that do not match the selector
          - Is like adding a guard clause to your event handler
          - `.on('click', 'a', handler)` is like adding `if (event.target.tagName !== 'A') return` to the start of your handler

  - `click(handler)` ([jQuery: .click()](https://api.jquery.com/click-shorthand/))
      - Is shorthand for `.on('click', handler)`

  - `submit(handler)` ([jQuery: .submit()](https://api.jquery.com/submit-shorthand/))
      - Is shorthand for `.on('submit', handler)`

  - `off(events, selector˚, handler˚)` ([jQuery: .off()](https://api.jquery.com/off/))
      - Unbinds event listeners from elements
      - `events` is a space-separated list of events
      - `selector˚` is an optional selector to choose specific elements to unbind the event from
      - `handler˚` is an optional specific handler to unbind.
      - If more than the `events` argument is given, it will only remove event handlers that match the specificity given by the selectors and handler.

  - `trigger(eventType)` ([jQuery: .trigger()](https://api.jquery.com/trigger/))
      - Fires event `eventType` on each element of collection collection

#### Manipulation

  - `text(text˚)` ([jQuery: .test()](https://api.jquery.com/text/))
      - when called with no arguments, returns the combined text of all elements in the collection
      - When `text˚` is passed, sets the content of each element in the collection to the specified text

  - `html(htmlString˚)` ([jQuery: .html()](https://api.jquery.com/html/))
      - when called with no arguments, returns the first element in the collection's raw html
      - When `htmlString˚` is passed, sets the content of each element to the html.

  - `val(value˚)` ([jQuery: .val()](https://api.jquery.com/val/))
      - when called with no arguments, returns the first element in the collections value attribute value.
      - when passed `value˚`, sets the value of each element to that value.

  - `remove(selector˚)` ([jQuery: .remove()](https://api.jquery.com/remove/))
      - `selector˚` is an optional selector to filter the removed elements
      - removes elements from the collection from the DOM.
      - removes data and events as well

  - `addClass(className)` ([jQuery: .addClass()](https://api.jquery.com/addClass/))
      - adds `className` to each elements class list

  - `removeClass(className)` ([jQuery: .removeClass()](https://api.jquery.com/removeClass/))
      - removes `className` from each elements class list

  - `hide(duration˚)` ([jQuery: .hide()](https://api.jquery.com/hide/))
      - hides each element in the collection
      - if `duration˚`, will animate for that number of milliseconds

  - `show(duration˚)` ([jQuery: .show()](https://api.jquery.com/show/))
      - shows each element in the collection
      - if `duration˚`, will animate for that number of milliseconds
  - `css(propertyName, value˚)` ([jQuery: .css()](https://api.jquery.com/css/))
      - If `propertyName` is the only value passed, gets the css properties value for the first element
      - If `value˚` is passed, sets the css property to the value for each element in the collection
      - can instead take an object with `property:value` to set multiple property values.

  - `width(value˚)` ([jQuery: .width()](https://api.jquery.com/width/))
      - if no arguments are passed, returns the width of the first element
      - If `value˚` is passed, sets width to that value for each element in the collection

  - `height(value˚)` ([jQuery: .height()](https://api.jquery.com/height/))
      - if no arguments are passed, returns the height of the first element
      - If `value˚` is passed, sets height to that value for each element in the collection

  - `append(content)` ([jQuery: .append()](https://api.jquery.com/append/))
      - appends `content` to the end of each element in the collection
      - will clone copies of inserted content to additional targets if more than one element in collection
      - `content` can be:
          - htmlString
          - `Element`
          - Text
          - Array
          - jQuery object

#### AJAX ([AJAX Requests](https://launchschool.com/lessons/e1800f40/assignments/d70d5f28))

  - `$.ajax(settings)` ([jQuery: jQuery.ajax()](https://api.jquery.com/jquery.ajax/))
      - Completes an AJAX
      - `settings` is an object containing settings for the request
          - `url` property - the url of the request`
          - `type` property - the method GET, POST, etc
              - same as `method`
          - `dataType` property - the dataType accepted from the server
          - `contentType` property - the data's format being sent to the server
              - defaults to `"application/x-www-form-urlencoded; charset=UTF-8"`
          - `data` property - the body of the request(or query string)
              - should already be encoded if it is a string using the encoding for `contentType`
          - `headers` property - object containing headers for request

  - `done(callback)` ([jQuery: deferred.done()](https://api.jquery.com/deferred.done/))
      - Used to add a callback when the AJAX request completes successfully

  - `fail(callback)` ([jQuery: deferred.fail()](https://api.jquery.com/deferred.fail/))
      - Used to add a callback when the AJAX request fails.

  - `then(doneCallback, failCallback)` ([jQueyr: deferred.then()](https://api.jquery.com/deferred.then/))
      - Is a combination of `done()` and `fail()`

### Handlebars ([Lesson 4: HTML Templating with JavaScript](https://launchschool.com/lessons/e1800f40/assignments/c8f5970c))

  - Handlebars is a library built to help template HTML with javaScript
      - It allows you to add logic to your templates without allowing plain JavaScript inside the template

  - Handlebars has no dependency

  - include templates in HTML with `script` element
      - `<script type='text/x-handlebars'>`

  - `Handlebars.compile(templateString)`
      - compiles a template into a rendering function
      - `templateString` is the raw string of the template, got from the script element by pulling it from the DOM.
      - Returned function takes an object and uses that object to fill template
          - The function returns a string with raw html that must be inserted into desired HTML

  - `{{property}}`
      - Replaces the text in the template with the property of the object passed to the renderer.

  - `{{#if property}}` `{{else}}` `{{/if}}`
      - `if` helper
      - Checks for truthiness of property

  - `{{#each property}}` `{{/each}}`
      - `each` helper
      - Iterates over a `property` collection applying each element in the collection to the template
      - `{{@index}}` is the current index of the loop

  - Partials
      - `Handlebars.registerPartial(partialName, templateHTML)`
          - Registers partial
      - `{{> partialName}}`
          - Inserts partial into template
