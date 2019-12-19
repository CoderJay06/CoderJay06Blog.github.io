---
layout: post
title:      "Object Accessors "
date:       2019-12-19 22:30:20 +0000
permalink:  object_accessors
---

In Object Oriented Ruby  an object's instance variables are variables that are declared inside of a class and are bound to an instance of that class. These can be set and returned with object or attribute accessors. We use what are called a setter(aka writer) method and a getter(aka reader) method. The reader returns the value of the instance variable and the writer sets it. These can be implemented manually as the following : 
 
```
class Car 
 
 def model=(model) # Writer
  @model = model 
 end   
		 
 def model # Reader 
  @model 
 end

end 
```   

Though in Ruby there is a much more convenient option for your setter and getter or reader and writer methods called macros. When implementing macros they are followed by the attribute name they are being used on. You can sort of think of these as methods that create the definitions of other methods.  These are written as follows: 
```
class Car 
  attr_writer :model 
  attr_reader :model 
	
end
```
Or for both the reader and writer methods in one you can use the attr_accessor macro as a way to both read and write to the same attribute: 
```
class Car 
 attr_accessor :model 
end 
```

Macros are generally preferred over the manual method of writing out your reader and writer methods every time you need to make a new attribute. If you don't need to manually customize something within your method then macros should usually be used over the alternative. In object oriented Ruby sometimes *less is more! *  

![](https://mixandgo.com/assets/learn/ruby_attr-b35cf32a02d67bf2788359a77ebf92fb3da96a2afa8652d2e58e6a5de34379a3.png)
