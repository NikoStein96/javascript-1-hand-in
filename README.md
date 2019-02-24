### Explain the differences between Java and JavaScript. You should include both topics related to the fact that Java is a compiled language and JavaScript a scripted language, and general differences in language features.
+ JavaScript is an interpreted language, not a compiled language. A program such as Java needs to be compiled before it is run. The source code is passed through a program called a compiler, which translates it into bytecode that the machine understands and can execute.
+ JavaScript is a untyped language, which means we don't have to specify what type a variable is, like we have to do in Java which is a statically typed language, where you have to make sure you assign the right types to the variable.
+ JavaScript normally was used for frontend work, but can now also be used as a backend end language thanks to node.js, which offers a runtime enviroment away from the browser. 

### Explain the two strategies for improving JavaScript: ES6 (es2015) + ES7, versus Typescript. What does it require to use these technologies: In our backend with Node and in (many different) Browsers
+ ES6 and ES7 include some features in the JavaScript language, that the modern browsers do not yet support, therefore someone invented babel which transpiles our ES6+ code into javascript code that is supported by the browser.
+ TypeScript is a superset of JavaScript that features static typing. One of the big benefits is to enable IDEs to provide a richer environment for spotting common errors as you type the code.

### Explain generally about node.js, when it “makes sense” and npm, and how it “fits” into the node echo system.
+ Node.js is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient, perfect for data-intensive real-time applications that run across distributed devices.
+ npm package manager, is as the name says a way to manage our javascript packages. With npm we can import other JavaSript modules to our own code fast and easy.

### Explain about the Event Loop in Node.js
+ JavaScript is a single threaded language, which normally means we can only do one thing at a time. But in JavaScript we can still do things asynchronous because of the event loop.
+ When a javascript function is running it's put on the stack, and when it's done it pops of the stack. 
+ With the help of the browser API functions such as setTimeOut or fetch are handled in the background within the browser, so we can execute other code in the meantime.
+ When the browser is done, it sends the callback function to the callback queue and waits for the event loop to see if the stack is empty, and then sends it into the stack.
![javascript](https://cdn-images-1.medium.com/max/800/1*7GXoHZiIUhlKuKGT22gHmA.png)

### Explain (some) of the purposes with the tools Babel and WebPack, using  examples from the exercises
+ WebPack is used for bundling JavaScript modules together into one file, since the browser doesn't support ES6 modules. Therefore it bundles all the JavaScript code into one large file, which the browser understands.
+ Babel as mentioned earlier is a tool for transpiling next generation javascript into older versions that are supported by the browser.

### Explain the purpose of “use strict” and Linters, exemplified with ESLint 
+ Linters are used for catching syntax errors and other stuff. It can also read your code, and see that what you have typed is maybe not what you really ment and therefore suggest something else that makes more sense. It's a good tool, that takes time to use but saves you time debugging. 

## Explain using sufficient code examples the following features in JavaScript. 

### Variable/function-Hoisting
```javascript
console.log("Example 1:");
decLater = 5;
console.log('------------------------------------');
console.log("x should be 5, eventough it's not declared yet.");
console.log("x is:" + x);
console.log('------------------------------------');
decLater x;
console.log('------------------------------------');
```
+ As we see in the code even though i declared the variable later it still contained the value it was assigned earlier. Which is what hoisting is, in JavaScript we can declare functions and variables independent of when they are used.

### this in JavaScript and how it differs from what we know from Java/.net.
```javascript
/**
 * A function's this keyword behaves a little differently in JavaScript compared to other 
 * languages. In most cases, the value of this is determined by how a function is called. 
 * It can't be set by assignment during execution, and it may be different each time the 
 * function is called.
*/

console.log('------------------------------------');
console.log("This Explained:");
console.log('------------------------------------');

// Example 1 (Global Context):
// In the global execution context (outside of any function),
// this refers to the global object, whether in strict mode or not.
console.log(this.document === document); // true

// In web browsers, the window object is also the global object:
console.log(this === window); // true

this.a = 37;
console.log(window.a); // 37
//Example 2 (Shadowing this):

function Car(make,model) {
  this.make = make;
  this.model = model;
  this.show = function(){setTimeout(function(){ //This function gets it's own "this"
    console.log(this.make + ", " + this.model);
  },0)};
}
var car = new Car("Volvo","V70");
car.show(); //undefined, undefined
```
+ In java the this keyword is global

### Function Closures and the JavaScript Module Pattern
```javascript
var add = (function () {
  var counter = 0;
  return function () {counter += 1; return counter}
})();
```
+ the counter in add work just like how private in Java works, now we can only access the counter variable by calling the add function we can't alter the counter variable directly.

### Javascript Module Pattern
```javascript
function greeter(name) {
        var name = name;
        return {
            greeting: function() {
                return "Hi " + name;
            }
        }
    }
    console.log(greeter("Jens").greeting());
```
+ The objective is to hide the variable accessibility from the outside world. 


### Immediately-Invoked Function Expressions (IIFE)
```javascript
(() => {
	console.log("This function gets called immediately");
})();
```
+ self explanatory, the last parentheses make sure the function is called immediately.

### JavaScripts Prototype
```javascript
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};
```
+ The prototype make us able to add new properties to the objects constructor.

### User-defined Callback Functions (writing your own functions that take a callback)
```javascript 
function doSomething(callback) {
    // ...

    // Call the callback
    callback('stuff', 'goes', 'here');
}

function foo(a, b, c) {
    // I'm the callback
    alert(a + " " + b + " " + c);
}

doSomething(foo);
```
+ user defined callbacks are a good way to avoid writing redundant code. We can create one function, but we can tell that function to do different things.
