Sequential code is when each line runs in sequence. Asynchronous code is when it doesn't run continuously or even when the runtime encounters it.

`setTimeout` is a function that takes a callback function and a time to wait in milliseconds. It sets a timer for the duration before invoking the callback function

```JS
setTimeout(() => {           
  console.log('!');          
}, 3000);
```

A similar function `setInterval` invokes the callback function again and again at intervals until it is told to stop.

```JS
function save() {
  // Send the form values to the server for safe keeping
}

// Call save() every 10 seconds
let id = setInterval(save, 10000);

// Later, perhaps after the user submits the form
clearInterval(id);
```

An `event` is an object that represents some occurence, it contains information about what happened and where it happened

A lot of web apps consist of setting up and displaying the user interface, and handling events resulting from user or browser actions. The first one is typically 
achieved with HTML, which lets us focus on handling events

### Adding event listeners

Event listeners are functions that the JS runtime calls when a particular event occurs

There are 4 steps needed to set up an event handler:
 - Identify the event you need to handle
 - Identify the element that will receive the event
 - Define a function to call when this event occurs
 - Register the function as an event listener

### The event object:
If we need more information about an event, the argument passed into the event handler provides this information. It's an `event` object that provides contextual information about the event

Some useful properties on the `Event` objet include: 
 - `type` -- the name of the event, i.e. 'click'
 - `currentTarget` -- the current object that the event object is on. It always refers to the element that has an event listener attached to it.
 - `target` -- the object on which the event occurred, i.e. the element clicked by the user.

Here are some properties specifically related to mouse events:
 - `button` -- This is a read-only property that indicates which button was pressed
 - `clientX` -- The horizontal position of the mouse when the event occurred
 - `clientY` -- The vertical position of the mouse when the event occurred
   - `clientX` and `clientY` return values relative to the visible area of a page: the # of pixes from the upper left corner of the browser's viewport.
  
Here are some keyboard-specific properties:
 - `key` -- The string value of the pressed key
 - `shiftKey` -- boolean value that indicates whether the user pressed the shift key
 - `alkKey`, `ctrlKey`, `metaKey` -- boolean that indicates whether the user presssed the alt, control, or meta (command) key
 
** if  you are manipulating the DOM with an event listener, use the `DOMContentLoaded` event (I think)

`setInterval(callback, interval)` repeatedly executes `callback` every `interval` milliseconds

## JS Promises
Promises solve the problem that callbacks solve. They are objects that represent an eventual value

A `Promise` is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason

A Promise is in one of three states: pending, fulfilled, or rejected.

```JS
var promise = new Promise(function(resolve, reject) {
  // do a thing, possibly async, then…

  if (/* everything turned out fine */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});
```
Note: All synchronous code runs before asynchronous code






