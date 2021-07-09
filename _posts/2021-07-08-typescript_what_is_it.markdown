---
layout: post
title:      "Typescript. What is it?"
date:       2021-07-09 01:49:00 +0000
permalink:  typescript_what_is_it
---

Typescript is an open-source statically typed programming language that was developed by Microsoft. At a high level, it is basically just a superset of Javascript. It gives you the ability to add optional strict typing to your Javascript code. The main focus of Typescript is to make Javascript more scaleable and reliable by adding static type safety.
## Why do we need it?
Since Javascript is naturally a dynamically typed language it does not require explicit declaring of variable data types before they are used. It performs its type checking at runtime meaning it will run the program regardless of whether it contains errors that stop it from running correctly. This differs from statically typed languages which type check at compile time. Typescript gets rid of the cons of dynamically typed languages. It helps you catch errors in your program before they become a problem.
## Types
Typescript has all of the basic data types from Javascript such as boolean, number, string, and more!
```
// boolean
let isBoolean: boolean = true

// number
let bigNumber: number = 100000000

// string
let greeting: string = "Hello World"

// array
let numArray: number[] = [1,2,3,4,5]
let strArray: string[] = ["Javascript", "Typescript"]

// tuple
let tup: [string, number] // declare tuple
tup = ["tuple string", 10] // initialize
tup = [10, "string"] // error! Must be in same order as when declared
```
## An example
```
function greetGenerator(greet: string) {
    console.log(greet);
}

const exampleGreet = "Hello World"
greetGenerator(exampleGreet);
```
## Summary
Typescript offers all of the same things as Javascript but also adds its type system on top of it. Typescript helps to prevent scalability problems with Javascript applications. It supports compile-time error checking, Object Orientation, and strong static-type checking.
## Resources
* [Typescript Docs](https://www.typescriptlang.org/)
* [Typescript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
