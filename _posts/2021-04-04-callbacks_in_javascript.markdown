---
layout: post
title:      "Callbacks in Javascript"
date:       2021-04-04 07:51:33 -0400
permalink:  callbacks_in_javascript
---


## An Overview

For a general definition on the concept of callbacks in Computer Programming I'd say that they are a callable piece of code within your program that is passed into another piece of code which actually calls it from within itself. Many programming languages use callbacks. Some of the more popular ones are C, C#, C++, Python, and of course Javascript.
In Javascript callbacks are simply an executable function that is passed to another function which will execute or return it at some point in time. The function that recieves the callback is called a [higher-order function](https://en.wikipedia.org/wiki/Higher-order_function) which is defined as *A function that returns a function*. This works because functions in Javascript are [First-class](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function) meaning that they can be treated as if they were any other variable.
## Types of Callbacks
Callbacks in Javascript can be used both synchronously and  asynchronously.  Synchronous callbacks are executed right before its outer function (higher order function) is returned.  Asynchronous callbacks get executed after the higher order function, so they can continue their execution at a later time after some other operations are performed. 

#### Synchronous example
```
// higher-order function
function promptForName(callback) { 
    const name = prompt('Enter your name')
    callback(name) // gets executed before the function is returned
}

// callback 
function displayName(name) {
    alert(`Hello ${name}`)
}

promptForName(displayName) // displays Hello with entered name when called  
```
When the function `promptForName()` is invoked with the callback function as its argument it will be executed line by line. The user is first prompted for their name then the callback gets immediately executed when name is entered and the outer function is returned following the callback's invocation. This happens in a synchronous manner meaning code is executed sequentially (top to bottom).

#### Asynchronous example
A good way for demonstrating asynchronous callbacks would be to use the built in Javascript functions [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) and [setTimeout](http://). The addEventListener function waits for a specified event to be triggered before it executes and setTimeout delays code execution until the set time is expired. Both of these functions take in callbacks.
```
// addEventListener example:

const btn = document.querySelector('button')
btn.addEventListener('click', handleClick)

function handleClick(event) {
  alert("I've been clicked!")
}

// setTimeout example:

setTimeout(() => {
    alert('Times up!');
}, 5000);


console.log('Im executed first!') // logs to the console before setTimeouts callback executes
```
The first parameter of the event listener function is just the type of event action it will listen for and the other is a reference to the callback function `handleClick()`. When it is triggered it will invoke its callback function. And for `setTimeout()` it takes two parameters, first its callback function then the set time to delay its execution which is at 5 seconds for this example so the console log statement would be run before the callback is invoked.

## Summary
Callbacks are a common and important tool in the toolbelt of any Javascript developer. They are frequently used in most Javascript applications and are useful for executing code both asynchronously and synchronously. For example listening for events such as a form submmision from a user with an event listener or filtering duplicates out of an array of user data with a [filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)function which takes a callback as its argument are both scenarios where callbacks can be handy.

### Resources 
* [An Introduction to Callbacks and Higher Order Functions](https://www.youtube.com/watch?v=7E8ctomPQJw)
* [Callback function](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function)
* [Callback](https://en.wikipedia.org/wiki/Callback_(computer_programming))












