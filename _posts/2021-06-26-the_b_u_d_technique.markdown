---
layout: post
title:      "The B.U.D Technique"
date:       2021-06-26 18:25:54 -0400
permalink:  the_b_u_d_technique
---

Optimizing your algorithms is an important skill for new Software Engineers to develop, especially when it comes to technical interviewing. It's a skill I'm still very much trying to learn and progress at. Lately I've been reading the book Cracking the Coding Interview *by Gayle Laakmann McDowell*. I came across some usefull techniques that are mentioned by the author. One such technique that caught my eye was B.U.D which stands for:

* **B**ottlenecks
* **U**nnecessary Work
* **D**uplicated Work

The basic gist of what these are for is that they represent the three most common tasks that an inefficent solution is wasting time with. An approach would be to walk through you're brute force algorithm checking for each of these. Then focus on fixing it until it can be improved. So let's break down the specifics of each of these and explain how identifying them in your algorithm using the BUD technique can help to optimize your solution.
## Bottlenecks
The bottleneck is the part of your algorithm that considerably slows down its runtime. For an example say we have the following problem to solve:

**Problem**: *You have two arrays with distinct elements in common. How would you compute the number of elements in common.*

**Brute force approach**: Take each element in array A, walk it through array B and check if it contains the current element.

This would roughly add up to an O(A * B) runtime. The bottleneck in this case is B. We're checking for each element of A to see if it contains any of the elements in B, the contains operation is O(B). This sort of repetition negeatively effects our runtime. After recognizing this bottleneck we should think about what's a more optimal way to perform this same type of operation. How about a hash look up. 

**Optimizing for bottleneck**: Add every element in array B into a hash table. Then for each element in A check if it exists in the hash table.

This would bring our runtime down to O(A + B), getting rid of the bottleneck.
## Unnecessary Work
For unnecessary work we'll basically restructure the algorithm by finding the other uneeded operations being done and make small changes to adjust for better optimization. Let's take the following example problem from the Cracking the Coding Interview book:

**Problem**: *Print all positive integer solutions to the equation a^3 + b^3 = c^3 + d^3 where a, b, c and d are integers between 1 and 1000. - Cracking the Coding Interview*

**Brute force approach**: Just use multiple nested for loops like the following Javascript example:
```
for (let a = 1; 1 < 1000; a++) {
    for (let b = 1; 1 < 1000; b++) {
        for (let c = 1; 1 < 1000; c++) {
            for (let d = 1; d < 1000; d++) {
                if (Math.pow(a, 3) + Math.pow(b, 3) == Math.pow(c, 3) + Math.pow(d, 3)) {
                    console.log(' a:', a, ' b:',  b, ' c:', c, ' d:', d)
                }
			}
		}
	}
}
// Note: I don't suggest running this code in you're console
```
This code solves our problem but it uses an unnecassary amount of work. To optimize we could break from the loop as soon as we find our solution. In this case we'll break out of the inner loop of d.

**Optimize for unnecessary work**:
```
for (let a = 1; 1 < 1000; a++) {
    for (let b = 1; 1 < 1000; b++) {
        for (let c = 1; 1 < 1000; c++) {
            for (let d = 1; d < 1000; d++) {
                if (Math.pow(a, 3) + Math.pow(b, 3) == Math.pow(c, 3) + Math.pow(d, 3)) {
                    console.log(' a:', a, ' b:',  b, ' c:', c, ' d:', d)
                    break // solution found, break from loop 
                }
            }
        }
    }
}
```
This may be a very small optimization that does little to improve our code but if you continue to make small adjustments like this it may be able to effect the overall runtime of you're algorithm.
## Duplicated Work

Here we'll look for any duplicated work using the same example as before.

**Problem**: *Print all positive integer solutions to the equation a^3 + b^3 = c^3 + d^3 where a, b, c and d are integeers between 1 and 1000. - Cracking the Coding Interview*

**Optimize for duplicated work**: Once again this is a problem where a hash table can be used to optimize. Add all c, d pairs to an array. Then store it as the value in the hash map.
```
const map = {}
for (let c = 1; c < 1000; c++) {
    for (let d = 1; d < 1000; d++) {
        let result = Math.pow(c, 3) + Math.pow(d, 3)
        map[result] = [c, d]
    }
}

for (let a = 1; a < 1000; a++) {
    for (let b = 1; b < 1000; b++) {
        let result = Math.pow(a, 3) + Math.pow(b, 3)
        let list = map[result]
        for (const pair of list) {
            console.log(a, b, pair)
        }
    }
}
```
We realized that we were duplicating our work by performing multiple nested for loop iterations. So to solve for this we split up our work into two separated nested loops. The first nested loop calculates the result of c^3 + d^3 then mapping this to the c,d pairs array in a hash map. The second nested loop does the same calculations but for a, b pairs then we're simply printing the results. This would bring our runtime down to O(n^2) from the previous O(n^4).
### Resources
* [3 Algorithm Strategies](https://www.youtube.com/watch?v=84UYVCluClQ&list=PLI1t_8YX-ApvFsH-DaFmAmdJboAnbg08P&index=2&t=296s)
* [Cracking the Coding Interview book](https://www.amazon.com/Cracking-Coding-Interview-Programming-Questions-dp-0984782850/dp/0984782850/ref=dp_ob_image_bk)
* [Cracking The Coding Interview](https://www.crackingthecodinginterview.com/)






















