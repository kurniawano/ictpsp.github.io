---
title: Computational Thinking and Programming
permalink: /ictpsp/notes/intro-programming
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

We have previously talked on what is computational thinking and how it is related to programming. But what is programming and how it may help our computational thinking skills. 

When you use computers for your work or study, you will naturally use some softwares or applications. These softwares or applications are also called *programs*. The activity that creates these *programs* or softwares is called *programming*. The result of a programming activity is what we call as *computer codes*. Computer codes are a series of instruction that can be run on the computer to do some particular tasks. 

For example, a web browser software is created by writing computer codes that takes in a web address from the address bar, makes a request to the internet and displays the website in the browser. Every web browser uses a web browser engine that interpret the returned response from a website to the browser. One example of a web browser engine is WebKit and you can see its *codes* online[^1]. 

[^1]: https://github.com/WebKit/WebKit 

To create these computer codes, one usually choose a *programming language* to work with. Every computer code is written in some specific programming language. How then computer processes these codes? There are two main ways: using an interpreter or a compiler. 

In using an interpreter, the computer processes every *statement* or *expression* written in the codes and executes it immediately. For example, let's take a look at a Python code below to calculate a Body Mass Index.

```python
weight = 60
height = 170
bmi = weight / (height * height)
print(bmi)
```

The above Python *code* has four lines. Python is an interpreted programming language which means that every statement will be evaluated and executed before the next one. In the code above, a Python interpretter will read the first line, i.e. `weight = 60` and do something. What does Python interpreter do? We will go into more details in future lessons but for now it is sufficient to say that Python creates an integer data and assign it to variable called `weight` in its environment. Python interpreter does this before it executes the next line, i.e. `height = 170`. 

// image of interpreter process

The second way is in using some *compiled* programming languages such as C and C++. These programming languages have  *compilers* that translates the computer codes into some object files which contain the machine level instructions to the CPU (computer processing unit). Most of the time a *linker* is used to link various object files to a *binary* files that is executable by the computer. A similar code written in C is shown below.

```c
int main(void){
  int weight = 60;
  int height = 160;
  float bmi = weight / (height * height);
  printf(bmi);
}
```

Unlike interpreted language, where the instructions are executed line by line, the whole source code is *compiled* into an object file which is then linked into an executable file. Only then the computer executes the program.

// image of compilation and linking

Since compilers take in the whole source code, they are able to do optimisation and checking on the codes. Optimisations improve the performance of the codes while checking may reduce errors before the codes is being executed. For example, variables that are not used nor initialized may produces errors or warnings during compilation time. Moreover, loops can be optimised and memory allocation can be saved by compilers too. Interpreters on the other hand do not have these advantages since the codes are executed one statement at a time. Some interpreted programming languages try to create a Just-in-time compilers to increase the performance.


The important things to note is that the result of a programming activity is a source code which is used to produce instructions for the computer to execute. 


## Skills Needed in Programming

Programming, however, is not an easy task. This is especially true for novice programmers. The reason for this is that programming requires a number of different skill sets. Here we list down four of them which is common in most programming activities.
- Familiarity with the programming language
- Problem solving skills
- Familiarity with the development environment tools
- Analytical thinking and debugging skills

// insert image of skills needed in programming

Each of this different skill is required for programmers to perform a single task of programming. Familiarity with a programming language used is analogous to learning a new foreign language. At the same time, knowing programmng language does not guarantee a person to be able to write a computer code. The reason is that the programming language itself is just a tool to solve some problems at hand. Therefore, problem solving skill is also needed in programming. It is common for novice programmers to learn the programming language without being able to write the code to solve certain problems. 

Moreover, programmers usually use certain development tools such as Integrated Development Environment (IDE) or other softwares to write the computer codes, debug, test and executes them. This means that a novice programmers must learn how to use these tools. In some occasions, the installation and operation of these software tools are not easy. This means that novice programmers must juggle to learn how to use the softwares on top of the new programming language and the problem solving skills they need to acquire. One simple example is that many novice programmers do not know how to use the debugging features of their IDE. This makes it difficult for them to fix their code when they encounter some errors.

Speaking about fixing codes, this is another skill that is different from problem solving and learning a new language. There are two kinds of errors that programmers may encounter. The first one is a syntax error where the compiler or the interpreter is unable to execute the command that the programmer writes due to some mistakes in the way the code is written. Usually the compiler or the interpreter is able to highlight what kind of syntax error occurrs and which line of the code that it fails. Unfortunately, many novice programmers are not able to understand the error message that the compiler or the interpreter gives. Some of these error messages produce a whole stack of information that is useful for expert programmers but may confuse a novice programmer. 

The second kind of error is what is called semantic errors or logical errors. These errors are not caught by the compiler or the interpreter because the codes are written in a valid syntax or instruction for the machine to execute. However, these are called semantic or logical errors because they produce a different output than what is expected. Being able to trace where the logical errors are requires  some analytical skills. 

The various skills that is needed by programmers to do programming may seem overwhelming for novice programmers. At the same time, this is the reason why programming activities are helpful for a person's growth in their thinking and work skills. When someone learn programming, he or she picks up these various skills such as those needed by someone learning a new foreign language, or like those engineers who are able to solve various problems, or even like those detectives who are able to use their analytical skills to form conclusions from the given evidences. In short, programming is a challenging yet rewarding activities. 
