---
layout: post
title:      "Single Responsibility in OOP"
date:       2020-05-03 21:30:49 -0400
permalink:  single_responsibility_in_oop
---


Single responsibility is an import concept in object-oriented programming. It is the first of the [SOLID](https://en.wikipedia.org/wiki/SOLID)(Single responsibility, Open-closed, Liskov substitution, Interface segregation,  Dependency inversion) principles which were first introduced by [Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin) and named by Michael Feathers. It was created to make software design understandable, flexible, and maintainable. Single responsibility's  definition is defined as follows, *'A class should have only a single responsibility, changes to just one part of the software's specification should be able to affect the specification of the class'.*

**Designing Classes with a Single Responsibility**

In chapter 2 of the current book I am reading called [POODR](https://www.poodr.com/)(Practical Object-Oriented Design In Ruby) by Sandi Metz the process of designing classes with a single responsibility is nicely broken down for the reader to understand. The author states that when first designing your application the goal is to model it using classes, such that it does what it's supposed to do and is easy to change later on. *Design is more the art of preserving changeability than it is the act of achieving perfection. - Sandi Metz*

**Organizing Code to Allow for Easy Changes**

Still following with chapter 2 of the POODR book Sandi Metz suggests writing code with the following TRUE(Transparent, Reasonable, Usable, Exemplary) qualities:

**T**ransparent - It should be easy to determine the effects of changing code and the effects on code that relies on it.

**R**easonable - The cost of change should align with the  benefits of the change.

**U**sable - The current code should be flexible such that it can be used in new and unexpected circumstances.

**E**xemplary - The code should influence whoever changes it to follow these qualities.

The first step in achieving these qualities is to implement your classes such that they have a Single Responsibility.


**Enforcing Single Responsibility**

Like classes, methods should also implement single responsibility for all the same reasons.

An example of a method not utilizing single responsibility:
```
def calculate_bmi
  people.collect {|person| (person.weight * 703) / person.height }
end
```
This method clearly has two responsibilities, it iterates over people and calculates a person's BMI(Body Mass Index).
The following is a refactoring of this method so to implement single responsibility:
```
# first iterate over the array
def all_people
  people.collect {|person| calculate_bmi(person) }
end 

# second - calculate BMI of one person
def calculate_bmi(person)
  (person.weight * 703) / person.height
end
```

The effects of just one refactoring like this is small but the positive effect of implementing this coding style throughout your program is big. The benefits of methods that have a single responsibility are the following:

**.** Exposes previously hidden qualities

**.** Avoids the need for comments 

**.** Encourages reuse 

**.** Are easy to move to another class


**Summary**

*The path to changeable and maintainable object-oriented software begins with classes that have a single responsibility. Classes that do one thing isolate that thing from the rest of your application. This isolation allows change without consequence and reuse without duplication* - Sandi Metz
