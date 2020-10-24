---
layout: post
title:      "Method Overloading"
date:       2020-10-24 07:11:18 -0400
permalink:  method_overloading
---


In programming, **method overloading** is the ability to use multiple methods of the same name or identifier but with a different parameter list to execute separate tasks. Method overloading is not available to every programming language but a few of the most popular languages use method overloading like C++, C#, and Java. For the examples in this blog, I'll be using the C# language. To relate method overloading to the real world an example might be when you use a self-checkout machine at the store you choose from several different payment options say cash, credit card, or debit card. Whichever payment option you choose it is still processed by the method called the payment transaction. One of the most common built-in methods used in C# called  `WriteLine()`  is an overloaded method. It can either be called with or without any arguments:
```
WriteLine(); // Outputs a new line
WriteLine("Hello World!"); // Outputs passed in string
```
When overloaded methods are called the compiler automatically determines which one to use by checking the arguments that are passed in. For example say you have a program containing a method that accepts payments and you want the user to be able to enter their pay amount in both double and string format:
```
using static System.Console;
using System;
public class Pay
{
 static void Main()
 {
	 string strPay;
	 double numPay;
		
	 Write("Enter payment >> ");
	 strPay = ReadLine();
		
	 // Determine input type and pass it to overloaded method
	 if (double.TryParse(strPay, out numPay) )
	 {
		 AcceptPayment(numPay);
	 }
	 else
	 {
		 AcceptPayment(strPay);
	 }
  }
	
    public static void AcceptPayment(string pay)
    {
	  double convertedPay;
     // Check if user entered the correct format and display output
	  if (pay.Substring(0, 1) == "$" && double.TryParse(pay.Substring(1), out convertedPay) )
	  {
		  WriteLine($"You payed {convertedPay} dollars");
	   }
	  else
	  {
		  WriteLine("Invalid format entered, use a $ and a decimal number");
	  }
	}

    public static void AcceptPayment(double pay)
    {
        WriteLine($"You payed ${pay} dollars");
    }
}
```
<br>
*Pay program output:*
```
Enter payment >> $100.00
You payed $100.00 dollars
Enter payment >> 100.00
You payed $100.00 dollars
Enter payment >> $Hello World
Invalid format entered, use a $ and a decimal number
```
As you can see, either way the user enters their input the correct overloaded method will be called and their result will be output. 
## Overload Resolution
When you have an overloaded method call that could execute multiple versions, the method with the best match will be executed. In C# this is known as **overload resolution**. Say you have the following methods:
```
public static void OverloadedMethod(double number)
{
   WriteLine("You entered a double: {0}", number);
}

public static void OverloadedMethod(int number)
{
   WriteLine("You entered an int: {0}", number);
}
```
If you call the method with an int argument both methods are able to accept it because an int would be automatically converted to a double type, but the method with the int parameter would be used over the other. In C# this is called betterness rules (rules that determmine which version of the method to call).
```
// Method called with an int number
OverloadedMethod(125); 

// The method with an int type parameter is executed
You entered an int: 125

// Method called with a double number
OverloadedMethod(12.55); 

// The method with a double type parameter is executed
You entered a double: 12.55
```
## Ambiguous Methods
When you use overloaded methods there's a chance you unintentionally create **ambiguous methods** which is when the compiler cannot figure out which method to execute and an error message is returned. For example assume the program below with two methods:
```
using static System.Console;
using System;
public class AmbiguousExample
{
  static void Main()
  {
     AmbiguousMethod(2, 2.5); // Matches first method
     AmbiguousMethod(4.5, 2); // Matches second method
     AmbiguousMethod(2, 2); // Ambiguous error message
  }

  public static void AmbiguousMethod(int num1, double num2) 
  {
     WriteLine($"My parameters are int: {num1} and double: {num2}");
  }
	 
  public static void AmbiguousMethod(double num1, int num2)
  {
     WriteLine($"My parameters are double: {num1} and int: {num2}");
  }
}
```

The first two method calls would work but when we attempt to execute the third method call the compiler will not be able to determine a best match for it by both arguments being integers. This is because although the integer could be converted to a double it will not know which method to choose as there is not an exact match for the method call. After running this program the following error message is generated:
```
main.cs(9,9): error CS0121:  The call is ambiguous between the following methods or properties: `AmbiguousExample.AmbiguousMethod(int, double)' and `AmbiguousExample.AmbiguousMethod(double, int)'
```
This is considered an ambigous situation created by the programmer as the overloaded method would not be determined to be ambigous by itself, only once the programmer has made it that way. 
## Conclusion
To implement method overloading the methods first need to have the same name/identifier and then either of the following:
* different parameter data types
* different number of parameters
* order of parameter lists differing

When used correctly method overloading can improve your codes readablity and maintainability but it is not always necessary and can actually cause more harm than good when used incorrectly. Therefore in most situations it should only be used if needed.

### Additional Method Overloading resouces:
* [https://en.wikipedia.org/wiki/Function_overloading](https://en.wikipedia.org/wiki/Function_overloading)
* [https://app.pluralsight.com/guides/overload-methods-invoking-overload-methods-csharp](https://app.pluralsight.com/guides/overload-methods-invoking-overload-methods-csharp)









