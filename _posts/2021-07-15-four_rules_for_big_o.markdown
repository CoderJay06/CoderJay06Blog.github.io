---
layout: post
title:      "Four Rules for Big O"
date:       2021-07-16 03:23:23 +0000
permalink:  four_rules_for_big_o
---


## Worst case
When calculating for the Big O of algorithms we're supposed to assume the worst case. This is our first rule. For example, say you have a function that contains a for loop that iterates through a list of users until it finds the name of the user passed in.
```
const users = ["Jack", "Bob", "Jill", "Sam", "Jay", "Nemo"];

function findUser(name) {
    // find user by name
    for (let i = 0; i < users.length; i++) {
        if (users[i] === name) {
            console.log(`Found ${name}!`);
            return;
        }
    }
    console.log(`${name} not found :(`);
    return;
}

findUser("Nemo") // found Nemo!
```
How long will it take to find our user? Well we are iterating over an array of length n. In this case we're checking the entire users array because our name is contained at the last index, so we're making n - 1 iterations. This gives us linear time or *O(n)*. But what if in our example we passed in the name Jack instead? Since Jack is the first name in the users array technically this would equate to *O(1)* or constant time right? Right! But only for this specific case which would be our best case. When it comes to big o we only care about our worst case so this would remain an *O(n)* algorithm. We must always prepare for the worst!  

## Remove constants
The second rule of Big O is to remove the constants. When your're measuring for the runtime of you're algorithm all of those less time consuming statements become insignificant. Let's go over an example where we're executing several constant time statements and a couple of loops just to explain this further.
```
const array = [1, 2, "Hello", 3, 4, "World"];

function pointlessProcedures(array) {
    let first = array[0]; // O(1)
    let middle = Math.floor(array.length / 2); // O(1)
    
    console.log(first); // O(1)
    
    let count = 0; // O(1)
    while (count < middle) { // O(n/2)
        console.log(count);
        count++;
    }

    for (let idx = 0; idx < array.length; idx++) { // O(n)
        console.log(array[idx]);
    }
}
```
So if we were to include every statement from this example in our final runtime we would end up with something like this *O(1 + 1 + 1 + 1 + n/2 + n)*. *As you can see it's not the prettiest looking thing*. What we do here is drop the constants as they will not add up to enough to affect our overall runtime. We can break this down further to something like *O(n/2 + n)* . And even further to *O(n + n)* . And finally we'd end up with *O(n)* linear time, dropping all unecessary constants.
## Different inputs different variables
Our third rule for Big O is to provide differently named variables for seperate inputs. This can be a bit more tricky than the other rules. It's something I didn't realize I should do when I first started learning big o. Let's use an example where we have a function that takes in two separate arrays as arguments.
```
function sortAndSquareNumsInArr1WithArr2(arr1, arr2) {
    const sortedArr1 = arr1.sort((a, b) => a - b);
    const sortedArr2 = arr2.sort((a, b) => a -b);
    const sortedAndSquared = []
		
    for (let i = 0; i < sortedArr1.length; i++) {
        for (let j = 0; j < sortedArr2.length; j++) {
            sortedAndSquared.push(sortedArr1[i] * sortedArr2[j]);
        }
    }
    
    return sortedAndSquared;
}
```
At first glance, you might think that this function's big o would evaluate to something like *O(n^2)*. But here we have two separate array inputs to be taken as our arguments, we don't know if they're of the same or different lengths. This would call for two differently named variables for our big o. Instead, we'd say something like O(a * b). Or any name you want to plug in to describe your variables will do, just as long as they are different.
## Drop the non dominant terms
Our last rule for Big O is to drop all the terms that are not dominant to your algorithm. In other words if you're including a term that isn't relevant enough to affect the overall time and space complexity of your entire algorithm than you should get rid of it. Let's use the following function as an example.
```
function logItemsAndSort(items) {
    
    items.forEach(item => console.log(item)); // O(n)
    
    // bubble sort O(n^2)
    for (let i = 0; i < items.length; i++) {
        for (let j = i + 1; j < items.length; j++) {
            if (items[i] > items[j]) {
                let temp = items[i];
                items[i] = items[j];
                items[j] = temp;
            }
        }
    }
}
```
Our first operation in `logItemsAndSort() ` is performing a linear time iteration logging each item to the console while the other is using a nested for loop to perform a bubble sort algorithm. So what is the big o of this function? You might say something like *O(n + n^2)* but in this case the n can be dropped. This is because it's not going to make enough of a difference on the big o when we have an operation as slow as bubble sort's *n^2* algorithm included in the overal time.
