The XMLHttpRequest is a built in JS API that allows you to make http requests from a web page to a server or another resource. It provides a way to send and receive data between the web browser and a server asynchronously without having to refresh the entire page. XMLHttpRequest is commonly used for fetching data, making API requests, and updating parts of a web page without a full page reload.

# Working With Web APIs Book
Some options for the http command that are used:
-p: What to output: H and B for request headers and body, h and b for response headers and body
-a: Authenticate with this username:password combination
-help: View command options and documentation

### APIs
An API provides a way for computer systems to interact with each other

Use cases for APIS:
 - share data between systems
 - enabling automation
 - leverage existing services

A data serialization format describes how programs convert data into a form that is more easily or efficiently stored or transferred. The stored or transferred data can then be converted back into the original data at any time by the original program or any other program that can understand its format.
 - JSON is the most common data serialization format used by web APIs today

### REST and CRUD
REST stands for representational state transfer and is used to describe a set of conventions for how to build APIs.

A good way to think about REST is as a way to define everything you might want to do with two values, what and how:
 - What resource is being acted upon
 - how are we changing/interacting with the resource

CRUD generally maps to the main 4 HTTP methods (GET POST PUT DELETE)

A RESTful design is one in which any action a user needs to make can be accomplished using CRUD operations on one or many resources. 
 - By limiting access to CRUD, REST requires you to think in a resource oriented way



## AJAX
When someone says they made an "AJAX request", they refer to an HTTP request from a web browser that does not perform a full page reload.

Two other main benefits of AJAX are:
 - it lets us use all HTTP methods, where HTML forms only allow GET and POST
 - it gives us more control over the headers and data format of our requests. (i.e. we can request data in HTML, JSON, or XML format)

When requesting a resource via JS, the developer must write code that initiates the request and optionally handles the response

Use the XMLHttpRequest object to send an HTTP request with JS. This object is part of the browser API, not the JS language

To send a request, we must provide the same parameters we would use when sending an HTTP request from any other language or tool: a method, a host, and a path.
```JS
let request = new XMLHttpRequest(); // Instantiate new XMLHttpRequest object
request.open('GET', '/path');       // Set HTTP method and URL on request
request.send();                     // Send request
```
This code sends a GET request for /path from the local host. Below are some properties of the request object:
```JS
request.responseText;                       // body of response
request.status;                             // status code of response
request.statusText;                         // status text from response

request.getResponseHeader('Content-Type');  // response header
```

XMLHttpRequest methods:
 - `open(method, url)` -- opens a connection to `url` using `method`
 - `send(data)` -- Send the request, optionally sending along `data`
 - `setRequestHeader(header, value)` -- set HTTP `header` to `value`
 - `abort()` -- cancel an active request
 - `getResponseHeader(header)` -- Return the response's value for `header`

XMLHttpRequest properties:
Property	      Writable	Default Value	Description
- timeout	      Yes	      0	           Maximum time a request can take to complete (in milliseconds)
- readyState	  No		                 What state the request is in
- responseText	No	      null         Raw text of the response's body.
- response	    No	      null	       Parsed content of response, not meaningful in all situations

### XMLHttpRequest Events

To run some code when an event occurs on an `XMLHttpRequest` object, we can use the same `addEventListener` method that we used for handling user or page events:

```JS
let request = new XMLHttpRequest();

request.addEventListener('load', event => {
  let xhr = event.target;   // the request is available as event.target
                            // if you can't access it from an outer scope.
});
```
`loadstart` and `loadend` fire during an `XMLHttpRequest` cycle -- One when it sends the request and one when the response loading ends.

Before `loadend` triggers, another event will fire based on whether the request succeeded: `load`, `abort`, `error`, or `timeout`

There are several different request serialization formats:
 - Query string / URL encoding
   - `encodeURIComponent` lets you encode a name or value using this format
   - You can then combine the name/value pairs with `=` and combine the resulting strings with `&`
   - You can also use this with POST requests but you must set a content-type header of `application/x-www-form-urlencoded`
 - JSON
   - You must set the content-type header to `application/json; charset=utf-8`
   -  

Using the `formData` API to serialize your data:
```JS
let form = document.getElementById('form');

form.addEventListener('submit', event => {
  // prevent the browser from submitting the form
  event.preventDefault();

  let data = new FormData(form);

  let request = new XMLHttpRequest();
  request.open(form.method, `https://ls-230-web-store-demo.herokuapp.com/${form.getAttribute('action')}`);

  request.addEventListener('load', () => {
    if (request.status === 201) {
      console.log(`This book was added to the catalog: ${request.responseText}`);
    }
  });

  request.send(data);
});
```

### Submitting a form via XHR
There are 3 steps to submitting a form using JavaScript:
 1. serialize the form data
 2. send the request using `XMLHttpRequest`
 3. handle the response

Post request:
```JS
let request = new XMLHttpRequest();
request.open('POST', 'https://lsjs230-book-catalog.herokuapp.com/books');

request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

let data = 'title=Effective%20JavaScript&author=David%20Herman';

request.addEventListener('load', () => {
  if (request.status === 201) {
    console.log(`This book was added to the catalog: ${request.responseText}`);
  }
});

request.send(data);
```
Line 4 above is used to encode POST parameters

`formData` makes it easy to serialize form data. It uses a different serialization format called multipart

### Cross Origin Requests
A cross-origin request happens when the page tries to access a resource from a different origin (could be a different scheme, host, or port)
 - Could be a request for an image, JS file, or any other resource
 - Most important cross origin request for our purposes is from one domain to another

`XHR` objects by default can't send cross origin requests due to security problems

APIs that share across domains using Cross-Origin Resource Sharing (CORS) to allow access
 - Applications use custom HTTP request and response headers to implement the mechanism of both systems knowing enough about each other to determine whether the response should succeed or fail
 - According to this specification, every `XMLHttpRequest` sent by the browser must have an `Origin` header that contains the origin of the requesting page
 - The server uses this header to determine if it should send a corresponding header in the response






