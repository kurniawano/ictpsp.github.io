---
title: Computational Thinking and Programming
permalink: /notes/intro-programming
key: notes-intro-programming
layout: article
nav_key: Notes
sidebar:
  nav: Notes
license: false
aside:
  toc: true
show_edit_on_github: false
show_date: false
---

## What is Programming?

We have previously talked on what is computational thinking and how it is related to programming. But what is programming and how it helps our computational thinking skills. 

When you use computers for your work or study, you will naturally use some software or applications. These software or applications are also called *programs*. The activity that creates these *programs* or software is called *programming*. The result of a programming activity is what we call as *computer codes*. Computer codes are a series of instructions that can be run on the computer to do some particular task. For example, a web browser was created by writing computer codes that takes in a web address from the address bar, make a request to the internet and displays the website in the browser. Every web browser uses a web browser engine that interpret the returned response from a website to the browser. One example of a web browser engine is WebKit and you can see its *codes* online [^1]. 

To create these computer codes, one usually choose a *programming language* to work with. Every computer code is written in some specific programming language. How then computer processes these codes? There are two main ways: interpreter and compiler. 

In using an interpreter, the computer processes every *statement* or *expression* written in the codes and executes it immediately. For example, let's take a look at a Python code below.

```python
weight = 60
height = 170
bmi = weight / (height * height)
print(bmi)
```

The above Python *code* has four lines. Python is an interpreted programming language which means that every statement will be evaluated and executed before the next one. In the code above, a Python interpretter will read the first line, i.e. `weight = 60` and do something. What does Python interpreter do? We will go into more details in future lessons but for now it is sufficient to say that Python creates an integer data and assign it to variable called `weight` in its environment. Python interpreter does this before it executes the next line, i.e. `height = 170`. 

The second way is done some some *compiled* programming languages such as C and C++. These programming languages have  *compilers* that translates the computer codes into some object files which contain the machine level instructions to the CPU (computer processing unit). Most of the time a *linker* is used to link various object files to a *binary* files that is executable by the computer. 

// image of interpreter process

Since compilers take in the whole source code, they are able to do optimisation and checking on the codes. Optimisations improve the performance of the codes while checking may reduce errors before the codes is being executed. For example, variables that are not used nor initialized may produces errors or warnings during compilation time. Loops can be optimised and memory allocation can be saved by compilers too. Interpreters on the other hand do not have these advantages since the codes are executed one statement at a time. Some interpreted programming languages try to create a Just-in-time compilers to increase the performance.

// image of compilation and linking


## Skills Needed in Programming

[^1]: https://github.com/WebKit/WebKit 
