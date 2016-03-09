#### JS Questions:

---

#### Explain event delegation

Event Propagation encompasses both event bubbling and event capturing. Event capturing is supported in few browsers and is rarely used.

There are situations where a single event, like a mouse click, may be handled by more than 1 event handler defined at different levels of the DOM hierarchy. The event bubbling process starts by executing the event handler for the individual elements at the lowest level (ex. links, table cells). From there the event “bubbles up” to the containing elements (ex. table or form) and higher level elements (like the body of the page). At the end the event is handled by the highest level in the DOM hierarchy (document element). 

---

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
---

#### Explain how prototypal inheritance works

Each object has an internal link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype.

Instead of classes, an object inherits from another object.

 In addition to their set of properties, almost all objects also have a prototype. A prototype is another object that is used as a fallback source of properties. When an object gets a request for a property that it does not have, its prototype will be searched for the property, then the prototype’s prototype, and so on.

A prototype can be used at any time to add new properties and methods to all objects based on it.

---

#### What do you think of AMD vs CommonJS?

CommonJS and AMD are specifications (or formats) on how modules and their dependencies should be declared in javascript applications.

CommonJS: it's a project to define a common API and ecosystem for JavaScript. One part of CommonJS is the Module specification. Node.js and RingoJS are server-side JavaScript runtimes, and yes, both of them implement modules based on the CommonJS Module spec.

AMD (Asynchronous Module Definition) is another specification for modules. RequireJS is probably the most popular implementation of AMD. One major difference from CommonJS is that AMD specifies that modules are loaded asynchronously - that means that modules are only loaded as they are needed, as opposed to loading all modules up front.

AMD is generally more used in client-side (in-browser) JavaScript development due to this, and CommonJS Modules are generally used server-side. However, you can use either module spec in either environment - for example, RequireJS offers directions for running in Node.js and browserify is a CommonJS Module implementation that can run in the browser.

---

#### Explain why the following doesn't work as an IIFE: `function foo(){ }();`.

By placing the anonymous function in parentheses (a group context), the entire group is evaluated and the value returned. The returned value is actually the entire anonymous function itself, so all we have to do is add two parentheses after it to invoke it.

What needs to be changed to properly make it an IIFE? Parentheses around the whole thing.

The pair of parenthesis surrounding the anonymous function turns the anonymous function into a function expression or variable expression. So instead of a simple anonymous function in the global scope, or wherever it was defined, we now have an unnamed function expression `(function foo(){ })();`.

---

#### What's the difference between a variable that is: `null`, `undefined` or undeclared?

- `undeclared` variables don’t even exist
- `undefined` variables exist, but don’t have anything assigned to them
- `null` variables exist and have null assigned to them

Further reading: http://stackoverflow.com/questions/833661/what-is-the-difference-in-javascript-between-undefined-and-not-defined/834095#834095.

How would you go about checking for any of these states?

---

####What is a closure, and how/why would you use one?

A Closure is a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope.

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

//generates closure
var add5 = makeAdder(5);
//uses closure
var add10 = makeAdder(10);

console.log(add5(2));  // 7
```

Examples:

- A use of closure is to call a function that generates another function or group of functions but hides all the state in private variables within the closure.
- Variables from the closure are part of the function itself, no matter how it's called later. This is useful for events/callbacks.

Further: http://howtonode.org/why-use-closure

---

#### What's a typical use case for anonymous functions?

- Anonymous functions can be used to store a bit of functionality in a variable and pass that piece of functionality around. 
- Passing it as an argument to a function is a typical use case, for example a callback function.

---

#### How do you organize your code? (module pattern, classical inheritance?)

---


#### What's the difference between host objects and native objects?

- Native: an object in an ECMAScript implementation whose semantics are fully defined by this specification rather than by the host environment.
- Native objects: Object (constructor), Date, Math, parseInt, eval, string methods like indexOf and replace, array methods, etc.
- Native objects have an internal [[Class]] property of one of the following: "Arguments", "Array", "Boolean", "Date", "Error", "Function", "JSON", "Math", "Number", "Object", "RegExp", and "String".
- A Host object is an object provided by the environment in order to serve a specific purpose to that environment not defined in by the specification.
- Host objects (assuming browser environment): window, document, location, history, XMLHttpRequest, setTimeout, getElementsByTagName, querySelectorAll.

---


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

---

#### What is the difference between `==` and `===`?

`==` will compare equality after doing type conversions. the rules by which certain cases are converted are complicated and hard to memorize. `===` will compare equality without doing any type conversions.

3 == 3 will be true and 3 == ‘3’ will be true, but 3 === ‘3’ will be false and 3 === 3 will be true.

---

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
