#### JS Questions:

#### Explain event delegation

Event Propagation encompasses both event bubbling and event capturing. Event capturing is supported in few browsers and is rarely used.

There are situations where a single event, like a mouse click, may be handled by more than 1 event handler defined at different levels of the DOM hierarchy. The event bubbling process starts by executing the event handler for the individual elements at the lowest level (ex. links, table cells). From there the event “bubbles up” to the containing elements (ex. table or form) and higher level elements (like the body of the page). At the end the event is handled by the highest level in the DOM hierarchy (document element). 


#### Explain how `this` works in JavaScript

What `this` is
- A special identifier that is automatically defined in the scope of every function.
- An elegant way of implictly passing along an object reference
- `this` is not an author-time binding but a runtime binding. It is contextual based on the conditions of the function's invocation. It has to do with how the function was called, not where it was called.
- `this` is a binding made for each function invocation, based entirely on its call-site (how the function is called).

What `this` IS NOT

- It does not let a function get a reference to itself
- `this` DOES NOT refer to a function's lexical scope
- You CANNOT use a `this` reference to look something up in a lexical scope. It is not possible.

How do we find the call-site, how the function is called

- The call-site we care about is in the invocation before the currently executing function.
- Inspect the call-site and determine if one of the 4 rules apply.


**Rule #1**: standalone function invocation, `this` is global object

```
function foo() {
    console.log( this.a ); //resolves to global variable a
}

var a = 2;

foo(); // 2
```

- NOTE: If strict mode is in effect, the global object is not eligible for the default binding, so the this is instead set to undefined.

**Rule #2**: When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

```
function foo() {
    console.log( this.a );
}

var obj = {
    a: 2,
    foo: foo
};

obj.foo(); // 2
```

#### Explain how prototypal inheritance works

Each object has an internal link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype.

Instead of classes, an object inherits from another object.

 In addition to their set of properties, almost all objects also have a prototype. A prototype is another object that is used as a fallback source of properties. When an object gets a request for a property that it does not have, its prototype will be searched for the property, then the prototype’s prototype, and so on.

A prototype can be used at any time to add new properties and methods to all objects based on it.

* What do you think of AMD vs CommonJS?
* Explain why the following doesn't work as an IIFE: `function foo(){ }();`.
  * What needs to be changed to properly make it an IIFE?
* What's the difference between a variable that is: `null`, `undefined` or undeclared?
  * How would you go about checking for any of these states?
* What is a closure, and how/why would you use one?
* What's a typical use case for anonymous functions?
* How do you organize your code? (module pattern, classical inheritance?)
* What's the difference between host objects and native objects?
* Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?
* What's the difference between `.call` and `.apply`?
* Explain `Function.prototype.bind`.
* When would you use `document.write()`?
* What's the difference between feature detection, feature inference, and using the UA string?
* Explain AJAX in as much detail as possible.
* Explain how JSONP works (and how it's not really AJAX).
* Have you ever used JavaScript templating?
  * If so, what libraries have you used?
* Explain "hoisting".
* Describe event bubbling.
* What's the difference between an "attribute" and a "property"?
* Why is extending built-in JavaScript objects not a good idea?
* Difference between document load event and document ready event?
* What is the difference between `==` and `===`?
* Explain the same-origin policy with regards to JavaScript.
* Make this work:
```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```
* Why is it called a Ternary expression, what does the word "Ternary" indicate?
* What is `"use strict";`? what are the advantages and disadvantages to using it?
* Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`
* Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
* Why would you use something like the `load` event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
* Explain what a single page app is and how to make one SEO-friendly.
* What is the extent of your experience with Promises and/or their polyfills?
* What are the pros and cons of using Promises instead of callbacks?
* What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
* What tools and techniques do you use debugging JavaScript code?
* What language constructions do you use for iterating over object properties and array items?
* Explain the difference between mutable and immutable objects.
  * What is an example of an immutable object in JavaScript?
  * What are the pros and cons of immutability?
  * How can you achieve immutability in your own code?
* Explain the difference between synchronous and asynchronous functions.
* What is event loop?
  * What is the difference between call stack and task queue?
