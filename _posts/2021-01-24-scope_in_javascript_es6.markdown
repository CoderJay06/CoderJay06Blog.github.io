---
layout: post
title:      "Scope in Javascript (ES6)"
date:       2021-01-24 19:54:37 -0500
permalink:  scope_in_javascript_es6
---


## What's scope?
In Computer Programming scope can be defined as the accessibility and visibility of your code to other parts of your program. When declaring variables, functions, or objects they will have a specific scope depending on how and where they are written.

## Execution Context
Execution context is an abstract concept that just describes the environment that your code is executed in. There are two types, the global & local execution context. The global execution context is the first to get created when your code is run. The local execution context is created when a function is called.

## Global vs Local scope
In Javascript global scope is considered to be the entire area of the program or document you are coding in while the local scope is specific to an individual function or object. There can only be one global scope while there can be many local scopes within your program. A simple analogy to relate this concept to could be the following, consider a  zoo with many different species of animals and a zookeeper. In this analogy each species of animal has its own environment (local scope) which would be the function, the animals inside are the local variables only being accessible within their environment. The zookeeper would be the global variable that has access to the entire zoo (global scope).

```
// Global scope
let zooKeeper = "I'm global!"

function zooAnimalEnivornment() {
  // Local scope
  let zooAnimal = "I'm a local!"
}

console.log(zooKeeper) // I'm global!
console.log(zooAnimal) // Uncaught ReferenceError: zooAnimal is not defined
```

In the above code example we are declaring a globally scoped variable and assigning it a string. Next the function we are declaring `zooAnimalEnivornment()` is declared also in the global scope but it creates its own scope which is local to itself, it is the [function scope](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#function_scope). When we log the global variable `zooKeeper` it outputs to the console without any errors because it is accessible to the whole program but when we try to log the locally scoped variable `zooAnimal `it throws a [Reference Error](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_defined) because it is not visible anywhere besides its own function.

## Block scope
When variables are declared inside a block of code such as a conditional statement or even inside of a for loop they are only accessible to that block's local scope. This is true when declaring with let and const but when using var to declare your variables it would still be accessible outside of the block.
```
if (true) {
  let blockScopedVar = "I'm block scoped!"
  const anotherBlockScopedVar = "I'm also block scoped!"
}
console.log(blockScopedVar) // Uncaught ReferenceError: blockScopedVar is not defined
console.log(anotherBlockScopedVar) // Uncaught ReferenceError: anotherBlockScopedVar is not defined

for (let i = 0; i < 3; i++) {
  console.log(i) // logs: 0 1 2
}
console.log(i) // Uncaught ReferenceError: i is not defined

if (true) {
  var notBlockScopedVar = "I'm not block scoped!"
}
console.log(notBlockScopedVar) // I'm not block scoped!
```


## Lexical scoping (Nested functions)
In Javascript we are able to declare functions inside of other functions. Doing this creates a nested scope or lexical scope as it is called in Javascript. This means any inner functions will have access to all of their outer functions variables but not the other way around. This is true no matter how deep the inner function is nested. A simple example is shown below:
```
function outer() {
    let outerVar = 1
    
    function inner() {
        let innerVar = 2
        
        console.log(outerVar, innerVar) // 1 2
    }
    inner()
}

outer() // 1 2
```
When `outer()` function is called it logs both variable's contents to the console because `inner()` function has access to its own locally scoped variable and the variable assigned in its outer scope. The topic of lexical scoping leads into the concept of [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) which is defined by MDN web docs as *"A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment)."*  You can read more about closures [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures).

## Avoid using var
Before Javascript ES6 (ECMAScript 2015) there was no support for let and const, when creating variables only var was used.  Var is function scoped and allows variables to be reassigned vs let & const which are block scope and don't allow reassignment. So it is best to not use var to avoid the many possible bugs and mistakes that can come from it.


## Conclusion
Scope is an extremely important concept in any programming language. In general terms scope In Javascript is what determines the visibility and accessibility of variables. The two basic types of scope are the global and local scope. For further reading on scope in Javascript check out the links below:

* [Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
* [understanding-scope-in-javascript](https://scotch.io/tutorials/understanding-scope-in-javascript)<br>
* [javascript-fundamentals-scope-context-execution](https://levelup.gitconnected.com/learn-javascript-fundamentals-scope-context-execution-context-9fe8673b3164)
