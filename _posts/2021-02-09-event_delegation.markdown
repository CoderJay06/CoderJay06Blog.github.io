---
layout: post
title:      "Event Delegation"
date:       2021-02-10 02:38:33 +0000
permalink:  event_delegation
---


## What is Event Delegation
In simple terms event delegation is just a way to add one event listener to listen for multiple child elements on the dom. Instead of having to attatch a listener to each element and running the risk of slowing down your application or breaking something when you need to add to your code event delegation prevents this. It supports event listeneing using a single common parent element.

## An example
Say you have a shopping list as an unordered list element. Each item in the shopping list is contained in a li tag with a remove button next to each item. 
```
<ul id="shopping-list">
  <li class="item">Milk<button class="remove">X</button></li>
  <li class="item">Bread<button class="remove">X</button></li>
  <li class="item">Eggs<button class="remove">X</button></li>
</ul>
```
If you wanted a specific item to be deleted when the remove button is clicked you'd want to listen for the click event somehow. Your first instinct might be to iterate over each element and attatch an event listener to it.
```
const removeBtns = Array.from(document.getElementsByClassName('remove'))
removeBtns.forEach(btn => {
  btn.addEventListener('click', (e) => {
    e.target.parentElement.remove()
  })
});
```
While this would work and is a okay for a small list of elements like our shopping list it is not the most optimal solution. Using this iteration solution if you wanted to add many more items to your list than as it grows the performance would decrease and begin to slow down your application. This is because having an event handler on a large number of similar elements would begin to take up more memory resulting in poor performance. A better way would be to use the event delegation pattern.
```
const shoppingList = document.querySelector('#shopping-list');
shoppingList.addEventListener('click', (e) => {

  // Check if remove button clicked
  if (e.target.className === 'remove') {
    e.target.closest('.item').remove() // Remove item
  }
});
```
In this example we're first grabbing the shopping list container element which is the parent of all child elements containing our items we want to be able to delete. We then attatch the event listener to it. In the body of the event listener we are checking to see if the remove button was clicked and removing the specified item from the list if so. This solution uses two important event features called [bubbling and target](https://javascript.info/bubbling-and-capturing). When an event is triggered it first runs the handler on that inner element then the event bubbles up to all parent elements until reaching the document object, this is event bubbling. The event target is the most nested element that initiated the event and it gives us the details of that element. 


## Summary 
Event delgation can be very useful especially when working with a large collection of similar elements that need to be handled. I also find it to be a more simple solution to implement vs having to iterate over a bunch of elements and attatch listeners to them.

## Resources
* [JavaScript Event Capture, Propagation and Bubbling ](https://www.youtube.com/watch?v=F1anRyL37lE&t=4s)
* [javascript.info event-delgation](https://javascript.info/event-delegation)
* [Intro to events MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)

