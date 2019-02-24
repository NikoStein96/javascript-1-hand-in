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

