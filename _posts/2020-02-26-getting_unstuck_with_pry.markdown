---
layout: post
title:      "Getting Unstuck (with pry)"
date:       2020-02-27 04:14:54 +0000
permalink:  getting_unstuck_with_pry
---


One of the most difficult yet common aspects of programming is getting stuck on a problem. Especially as a beginner getting stuck on coding problems tends to happen frequently and getting 'unstuck' can feel like an impossible task in the moment.

![](https://media.giphy.com/media/10SAlsUFbyl5Dy/giphy.gif)


As a beginner programmer, I think trying to develop some kind of process for debugging and problem solving is important. When trying to identify a problem I first always make sure to thoroughly read the error message. Also taking steps like commenting out lines of code to locate the line with the error and using print or puts to see exactly what is getting output.

**Binding your way out**

In Ruby, one of my favorite tools to use for debugging a problem or even just to get a better understanding of my code is called Pry. Pry is a Ruby REPL (REPL stands for read-eval-print loop). It gives you an interactive programming enviornment just like the IRB (Interactive Ruby Shell) except it has added functionality. It lets you get inside your program and test out your code without having to copy and paste it into the shell like you would with IRB. Just install the pry gem, require 'pry' and place a binding.pry inside one of your methods. This lets you dig deeper into your code and check things like what the return values are or the parameters being passed into your method. 


![](https://josh.works/images/2019-09-20-pry-01.jpg)


*blog sources:* https://josh.works/images/2019-09-20-pry-01.jpg, https://learn.co/tracks/full-stack-web-development-v8/module-5-procedural-ruby/section-2-variables-and-methods/debugging-with-pry
