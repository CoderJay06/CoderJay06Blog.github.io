---
layout: post
title:      "An Overview of Programming Paradigms"
date:       2021-05-18 01:46:48 +0000
permalink:  an_overview_of_programming_paradigms
---


A programming paradigm is a style or pattern in which we choose to follow for how to structure and approach our programs and applications. There are many different paradigms that most of us are probably not familiar with. Paradigms like [Stack-oriented](http://progopedia.com/paradigm/stack-oriented/) or [Concatenative](http://progopedia.com/paradigm/concatenative/) just to name a few. The more common paradigms that are generally in use today are the ones that you've most likely implemented yourself at some point, Procedural, Object-oriented, and Functional. Each of these can be considered a subset of one of the more broad types of paradigms, imperative or declarative.
## Imperative
The imperative programming approach can be described as, following a series of steps in a sequential order to complete a task. Programming imperatively is telling the computer exactly how to do something. It's similar to writing out a recipe step by step or following a morning routine like making coffee.
```
let morningRoutine = ""
let tired = true
let isWorkDay = true
let timeToCode = true

if (tired && isWorkDay && !timeToCode) {
  morningRoutine = "Make 1 cup of coffee"
} else if (tired && timeToCode && isWorkDay) {
  morningRoutine = "Make two cups of coffee"
} else {
  morningRoutine = "Go back to sleep"
}
```
## Declarative
As opposed to imperative, declarative programming can be defined as telling the computer what to do instead of exactly how to do it. It's a way to abstract away the detailed steps of an algorithm and focus on describing the logic to get the result. An example of a language that implements declarative programming is SQL.
```
SELECT * FROM languages 
WHERE name = "SQL"
OR name = "Javascript";
```

## Procedural
The procedural paradigm is the one most programmers including myself start out with. It implements the simpler approach to managing your programs state by using global variables and uses loops to iterate over data. When programming in this paradigm you're usually creating some sort of routines and subroutines that will eventually be called. Procedural code is evaluated in a top to bottom manner and is of the imperative type. A good example of a procedural language is C.
```
char languages[4][10] = {"C", "Cobol", "Basic", "Fortran"};

for (int i = 0; i < 5; i++) {
  printf("\n%s", languages[i]);
}
```

## Object Oriented
The object-oriented paradigm is the one that is most widely in use today in modern Software Development. It focuses on utilizing objects, classes, and methods to store, manage, and manipulate data. The main characteristics of this paradigm that make it so applicable are the concepts of encapsulation, inheritance, abstraction, and polymorphism. This paradigm gives us a way to model our code based on the real world. It can produce applications with good scalability and security. There are many examples of object-oriented based languages. Some of the more popular ones to name are Ruby, C++, Java, and Python. Even Javascript was created originally as an object-oriented language.
```
class Car 
    attr_accessor :model, :year, :color, :price

    def initialize(model, year, color,  price)
        @model =model 
        @year = year 
        @color = color 
        @price = price 
    end

    def getInfo
        puts "Model: #{model}"
        puts "Year: #{year}"
        puts "Color: #{color}"
        puts "Price: $#{price}"
    end
end 

tesla = Car.new("Tesla","2021", "Red", 40000.00)
tesla.getInfo
```
## Functional
Another paradigm that is quickly gaining popularity in the industry is the functional one. This paradigm is all about maintaining the application's original state and keeping your code predictable. The core concepts of Functional programming are pure functions and immutability. Pure functions are simply functions without side effects; they don't deliver any unexpected results. Immutability is not being able to change. Immutable values are unchangeable once they're assigned. These characteristics of the functional paradigm make it capable of producing highly reusable, testable, safe, and efficient code. One purely functional language is Haskel. Other multiparadigm languages like Javascript also use Functional programming.
```
const list = [1, 2, 3, 4, 5];

function executePureFunctions(list) {
    const reverse = 
        (l) => l.map((num, idx, arr) => 
            arr[arr.length - 1] - idx);

    const odds = 
        (l) => l.filter(num => num % 2 === 1);

    console.log(reverse(list)); // [5, 4, 3, 2, 1]
    console.log(odds(list)); // [1, 3, 5]
}

executePureFunctions(list);
console.log(list); // [1, 2, 3, 4, 5]
```
## Summary
Selecting which paradigm to use usually depends upon the task at hand and what problem you're trying to solve, as they all have their use cases. The imperative style might make more sense for you if you're only looking to write a small program and you're not too worried about changing the program's state. The object-oriented approach could be a good choice for larger applications that change over time. The functional paradigm might be a better solution if you're prioritizing testing, security, and keeping the application's state intact. Or even a combination of all of these paradigms could be a better solution.

### Helpful resources
* [Paradigms](https://cs.lmu.edu/~ray/notes/paradigms/)
* [Introduction to paradigms](https://digitalfellows.commons.gc.cuny.edu/2018/03/12/an-introduction-to-programming-paradigms/#orgheadline1)
* [4 Programming Paradigms In 40 Minutes](https://www.youtube.com/watch?v=cgVVZMfLjEI&t=1467s)
* [Programming Paradigms - Computerphile](https://www.youtube.com/watch?v=sqV3pL5x8PI)
