---
layout: post
title:      "Big O Notation"
date:       2020-10-14 21:27:28 -0400
permalink:  big_o_notation
---



## What is Big O?
Big O notation is a mathmatical tool commonly used in Computer Science for measuring the runtimes of computer algorithms and describing their complexity. It's often used to determine what the efficency of a particular approach to a problem will be. More specifically, Big O determines what the "worst case scenerio" is for an algorithm's runtime and space as the input size grows.


## Time Complexity
Instead of measuring the actual time of an algorithm, we use time complexity which is the method of determining how many times an algorithm's statements will run. 

### Most common time complexities<br>
*The n in O() represnts the input size.*<br>

**O(1)** - Constant runtime. This means the code executes instantly. No matter what the input size it executes in the same exact time. For example if a group of programmers all decide to say hello world at the same time it would cost the same amount of time as only one programmer saying hello world. The following code executes in constant time:<br>
```
public void greet() {
  System.out.println("Hello World!");
}
```
<br>
**O(n)** - Linear runtime. Linear means to execute n amount of times. For example if you can  picture a long line of programmers standing in line for a job interview. Say you need to find out all of their names. You would go and ask each programmer their name indivdually. The following code executes in linear time:
```
public void askNames(int numNames) {
   
   for (int i = 0; i < numNames; i++) {
	  System.out.println("What's your name?");    
   }
}
```
<br>
**O(n^2)** - Quadratic time. Quadratic means the runtime number of executions increases in relation to the square root of n. This is not an ideal runtime as it will only grow as the input size increases. An example in code would be a nested for loop as follows:
```

public void printNamePairs(String[] names) {
  for (int first = 0; first < names.length; first++) {
	 for (int last = 0; last < names.length; last++) {
		System.out.println(names[first] + ", " + names[last]);
	 }
  }
}
```

<br>
**O(log n)** - Logarithmic time. Means the runtime will increase in relation to the logarithm of n (the input size). A real world example of this runtime would be searching a phonebook for a specific number. You open the phonebook halfway then if you dont find it, repeat the process of halving the pages of only the section that needs to be checked until you eventually find the number you're looking for. This would be considered [binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm), which is a common algorthm that runs in logarithmic time. *Learn more about logarithms [here](https://www.khanacademy.org/math/algebra2/x2ec2f6f830c9fb89:logs)*
```
public static int binarySearch(int [] phoneBook, int number) {
      int mid, low, high;

      low = 0;
      high = phoneBook.length - 1;

      while (high >= low) {
          mid = (high + low) / 2;
          if (phoneBook[mid] < number) {
              low = mid + 1;
          }
          else if (phoneBook[mid] > number) {
              high = mid - 1;
          }
          else {
              return mid;
          }
      }
			return -1; // If not found
  }
```
*Binary Search*
<br>
<br>

### Drop the Constants and Non-Dominant Terms<br>
When determining a Big O notation runtime, the constants should be dropped. For example if you have a specific runtime expression *O(n + 1 + 1 + 1)* this would be boiled down to *O(n)* because Big O only describes the worst case and including the constants wouldn't make a big enough difference. Also non-dominant terms should be dropped from the expression, for example *O(n^2 + n)* would become *O(n^2)*
## Space Complexity
In Big O space complexity describes the total amount of memory space used by an algorithm determined by its input size n. This is also expressed the same as time complexity for example an array of size n elements would be expressed as *O(n)* space.

### Analyzing Space Complexity<br>


```
public double calculateAverage(int[] array) {

  int sum = 0;
  double average;
  for (int i = 0; i < array.length; i++) {
	 sum += array[i];
  }
  average = sum / array.length;
	 
  return average;
}
```



To determine the space complexity of this code, we can list the size in bytes of the variables used.<br>
*int = 4 bytes, double = 8 bytes*
* array - 4n bytes
* sum - 4 bytes
* average - 8 bytes
* i - 4 bytes

The space for this example code would be mesured by 4n + 4 + 8 + 4. Since n is the dominant this would evaluate to O(n) space. *Read more about Space Complexity [here](https://www.baeldung.com/cs/space-complexity)*
<br>
<br>
<br>
<br>
#### Additional Big O Resources
* [Big O notation](https://en.wikipedia.org/wiki/Big_O_notation)
* [What is Big O Notation Explained: Space and Time Complexity](https://www.freecodecamp.org/news/big-o-notation-why-it-matters-and-why-it-doesnt-1674cfa8a23c/)
* [Understanding Time Complexity with Simple Examples](https://www.geeksforgeeks.org/understanding-time-complexity-simple-examples/)





