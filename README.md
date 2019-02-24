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

### Explain the methods map, filter and reduce
```javascript
//map 
const numbers = [2, 4, 8, 10];
const halves = numbers.map(x => x / 2);
// halves is [1, 2, 4, 5]

//filter
const words = ["spray", "limit", "elite", "exuberant", "destruction", "present"];

const longWords = words.filter(word => word.length > 6);
// longWords is ["exuberant", "destruction", "present"]

//reduce
const total = [0, 1, 2, 3].reduce((sum, value) => sum + value, 1);
// total is 7
```

### Provide examples of user-defined reusable modules implemented in Node.js
```javascript
function Person(name, age) {
        var name = name;
        var age = age;

        return {
            setName: function(value) {
                name = value;
            },
            setAge: function(value) {
                age = value;
            },
            getInfo: function() {
                return {
                    name: name,
                    age: age
                }
            }
        };
    }

    module.exports = Person;
```
+ Can then be imported in another js file with require('./person.js')

## ES6,7,8... and TypeScript

### Provide examples and explain the es2015 features: let, arrow functions, this, rest parameters, de-structuring assignments, maps/sets etc.

### Let
```javascript
let i = 5;
for (let i = 0; i < 10; i++) {
  // some statements
}
// Here i is 5
```
+ Let has block-scope which means it cannot be accessed outside a block  {

### Arrow function

```javascript
var materials = [
  'Hydrogen',
  'Helium',
  'Lithium',
  'Beryllium'
];

console.log(materials.map(material => material.length));
// expected output: Array [8, 6, 7, 9]
```
+ An arrow function expression is a syntactically compact alternative to a regular function expression, although without its own bindings to the this, arguments, super, or new.target keywords. Arrow function expressions are ill suited as methods, and they cannot be used as constructors.

### This

It has different values depending on where it is used:

+ In a method, this refers to the owner object.
+ Alone, this refers to the global object.
+ In a function, this refers to the global object.
+ In a function, in strict mode, this is undefined.
+ In an event, this refers to the element that received the event.
+ Methods like call(), and apply() can refer this to any object.


### Rest Paramaters
```javascript
function sum(...theArgs) {
  return theArgs.reduce((previous, current) => {
    return previous + current;
  });
}

console.log(sum(1, 2, 3));
// expected output: 6
```

### Destructuring

```javascript
var x = [1, 2, 3, 4, 5];
var [y, z] = x;
console.log(y); // 1
console.log(z); // 2
```
+ A nice way to assign a known value to a new variable

### Maps

```javascript
var myMap = new Map();

var keyString = 'a string',
    keyObj = {},
    keyFunc = function() {};

// setting the values
myMap.set(keyString, "value associated with 'a string'");
myMap.set(keyObj, 'value associated with keyObj');
myMap.set(keyFunc, 'value associated with keyFunc');

myMap.size; // 3

// getting the values
myMap.get(keyString);    // "value associated with 'a string'"
myMap.get(keyObj);       // "value associated with keyObj"
myMap.get(keyFunc);      // "value associated with keyFunc"

myMap.get('a string');   // "value associated with 'a string'"
                         // because keyString === 'a string'
myMap.get({});           // undefined, because keyObj !== {}
myMap.get(function() {}); // undefined, because keyFunc !== function () {}
```
### Explain and demonstrate how es2015 supports modules (import and export) similar to what is offered by NodeJS.
Export
```javascript
//------ lib.js ------
    export const sqrt = Math.sqrt;
    export function square(x) {
        return x * x;
    }
    export function diag(x, y) {
        return sqrt(square(x) + square(y));
    }
```

Import
```javascript
    import { square, diag } from 'lib';
    console.log(square(11)); // 121
    console.log(diag(4, 3)); // 5
```
### Provide an example of ES6 inheritance and reflect over the differences between Inheritance in Java and in ES6.

Class definition
```javascript
class Shape {
    constructor (id, x, y) {
        this.id = id
        this.move(x, y)
    }
    move (x, y) {
        this.x = x
        this.y = y
    }
}
```

Inheritance example
```javascript
class Rectangle extends Shape {
    constructor (id, x, y, width, height) {
        super(id, x, y)
        this.width  = width
        this.height = height
    }
}
class Circle extends Shape {
    constructor (id, x, y, radius) {
        super(id, x, y)
        this.radius = radius
    }
}
```

### Provide a number of examples to demonstrate the benefits of using TypeScript, including, types, interfaces, classes and generics
```javascript
Class Employee  {
            private firstName: string;
            private lastName: string;
            private email: string;
            private address: string;
}
```
+ With classes we get a more java like feel to it.

```javascript
interface Vehicle {
color: string;
make: string;
}
class Car implements Vehicle {
color: string;
make: string;
constructor(color: string, make:string) {
    this.color = color;
    this.make = make;
}
}
```
+ The implements also has similarities to java.

```javascript
function makeCar(car: T) {
   return car;
}
let v = new Car("Blue", "Ford");
let mycar = makeCar(v);
alert("my car is  " + mycar.color + "  " + mycar.make);
```

+The advantage of using “Generics” is that you can tell the compiler up front what the type is going to be. This will make program run a little bit faster, as “Object Type” has already been identified during compile time. Take a look at the following code for how to use a generic:

### Explain the ECMAScript Proposal Process for how new features are added to the language (the TC39 Process)

![javscript](http://exploringjs.com/impatient-js/img-book/c3d3200e87d0fb399346597fe342ca5c4bb69d0e.svg)

+ Different proposals all go through stages, There are five stages: a strawman stage, and 4 “maturity” stages. The TC39 committee must approve acceptance for each stage.

## Callback, promises and Async await
### How callback hell looks 
```javascript
fs.readdir(source, function (err, files) {
  if (err) {
    console.log('Error finding files: ' + err)
  } else {
    files.forEach(function (filename, fileIndex) {
      console.log(filename)
      gm(source + filename).size(function (err, values) {
        if (err) {
          console.log('Error identifying file size: ' + err)
        } else {
          console.log(filename + ' : ' + values)
          aspect = (values.width / values.height)
          widths.forEach(function (width, widthIndex) {
            height = Math.round(width / aspect)
            console.log('resizing ' + filename + 'to ' + height + 'x' + height)
            this.resize(width, height).write(dest + 'w' + width + '_' + filename, function(err) {
              if (err) console.log('Error writing file: ' + err)
            })
          }.bind(this))
        }
      })
    })
  }
})
```

### Promises avoid the callback hell by being more readable

```javascript 
someAsyncOperation(someParams)
.then(function(result){
    // Do something with the result
})
.catch(function(error){
    // Handle error
});
```
+ This way is much more readable, but can stille be confusing if there were to be way more .then  added to the code. 

### Implement our own promise solution

```javascript
function getData() {
    return new Promise((resolve, reject)=>{
        $.ajax({
            url: `http://www.omdbapi.com/?t=The+Matrix`,
            method: 'GET'
            }).done((response)=>{
                //this means my api call suceeded, so I will call resolve on the response
                resolve(response);
            }).fail((error)=>{
                //this means the api call failed, so I will call reject on the error
                reject(error);
            });
    });
}
```
+ This function returns a new promise, which we can call .then on if we want more things to happen when this function is done.

### Example(s) that demonstrate error handling with promises

```javascript
function getData() {
    return new Promise((resolve, reject)=>{
        $.ajax({
            url: `http://www.omdbapi.com/?t=The+Matrix`,
            method: 'GET'
            }).done((response)=>{
                //this means my api call suceeded, so I will call resolve on the response
                resolve(response);
            }).fail((error)=>{
                //this means the api call failed, so I will call reject on the error
                reject(error);
            });
    });
}
```
+ Let's say somethings goes wrong in the ajax call, then the ajax call would enter .fail with error and then call reject(error), meaning the promise was rejected and then the function returns the error
