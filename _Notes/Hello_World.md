---
title: Hello World
permalink: /notes/hello-world
key: notes-hello-world
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

## Your First Problem

Instead of starting with the first computer code, we would like to start with the first *problem*. Computing centres around data and the first problem is the following: *How to display data into your computer screen?*

Whenever you work with computer, you notice that there are a few components:
- input devices
- output devices
- compute devices

A computer comprises of all these three and you will see that any problem statement tend to comprise the following:
- what is the input?
- what is the output
- what is the computation or the process?


Here's the revised version with corrections highlighted:

So, we have actually introduced the first step in the PCDIT problem-solving framework. In this framework, the first step is to specify the problem statement. In specifying the problem statement, we need to answer the three questions above: the input, the output, and the process.

So, we can rewrite our first problem and make it more specific. What kind of data are we referring to? We have identified that the process is to display this data on the output device, which is your computer screen. But what should be displayed? In many programming lessons, the first thing that programmers usually display is the following data: "Hello, World!".

Maybe we should stop and ask what kind of data "Hello, World!" is. But before we go deeper, let's give a teaser of the solution to this problem written in Python. We will dig deeper into this simple solution in the following sections. For now, here is how to display "Hello, World!" on your computer screen.

```python
print("Hello World!")
```

That's it! But how to run this code?

## Running a Python Code

We have written our first computer code in Python. But recall that what we have created is only the *source* code. The source code does not do anything by itself. The code has to be executed for the computer to do what you ask it to do. Recall that there are two kinds of programming languages: interpreted and compiled. Python is an interpreted language. This means that we need a Python interpreter to execute the code and make the computer do what we ask it to do.

There are two main different ways of executing a Python code and they are listed here:
- Python Shell
- Python Script

If you have installed Python in your computer, you can go to your computer terminal or command prompt and type the following:
```sh
python
```

Some operating system who keeps Python 2 and Python 3 version may require you to specify the version. For example, in Ubuntu Linux OS, you run the Python shell for Python version 3 using the following.

```sh
python3
```

Once you run the Python interpreter, you will see the Python shell where you can type in your Python code into the prompt. It looks like the following:

```sh
Python 3.11 (default, April 4 2021, 09:25:04)
[GCC 10.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The version and the other details maybe different from your Python installation. However, at the end of the shell, you will see the Python shell's prompt `>>>`.

If you type in the code above into this shell (don't forget to press the ENTER key at the end), you will see that the computer is producing the output into the screen immediately below it.

```sh
>>> print("Hello World!")
Hello World!
>>> 
```

We'll show you how to run Python's Script but for the next few section you can just type your code into the Python's shell. 

## Human Language and Programming Language

At this point, it is important to note that there is a significant difference between our human language and a programming language. The reason for this difference is that a computer is not as smart as a human being in resolving ambiguity within the message. A computer requires a more exact instruction that is non-ambiguous to execute your commands. On the other hand, humans are much better at resolving ambiguities by reading the context, body language, and other clues. Humans can also verify if their understanding is correct or not. A computer requires exact and non-ambiguous instructions.

This means that your *source code* has to be written with certain rules. We call this *syntax*. For example, if you miss one single character, the Python interpreter may complain. Try to remove the last parenthesis and type it again into the shell. You will see the following behaviour:



```sh
>>> print("Hello World!"
... 
... 
... 
```

In the above situation, the Python interpreter expects you to have a closing parenthesis, and when there is no closing parenthesis, the Python interpreter will wait for you to close it. To end the above misery, just type in the closing parenthesis `)` and press Enter in the shell.

Why do you need a closing parenthesis? We will talk about functions in more detail, but for now, it is sufficient to say that `print()` is one of Python's built-in *functions*. To *invoke* or *call* a function, you need to specify the function name (in this case, `print`) and use parentheses (opening and closing round brackets, `()`) after the function name. So, `print()` is the *syntax* to invoke the print function. You can guess that the `print()` function's job is to display or print data to the standard output of your computer, which, in most cases, is the screen. What data is to be displayed is the argument of the function and is put between the parentheses. This is why Python expects an opening and closing parenthesis to determine when the function call ends.
You can also try to remove the last double quotes after the exclamation mark. This is the output.

```sh
>>> print("Hello World!)
  File "<stdin>", line 1
    print("Hello World!)
                       ^
SyntaxError: EOL while scanning string literal
>>> 
```

The above shows our first error message. Sometimes it's easier to read from the bottom to the top when dealing with error message. The last line mentioned that the error is the following.

```
SyntaxError: EOL while scanning string literal
```

This indicates that the type of error is a `SyntaxError`. The message after this is saying that the Python interpreter finds `EOL`, which stands for *end of line*, while scanning the string literal "Hello World!. What happens is that the Python interpreter sees the first double quotes before the letter H and recognises that you are trying to create a string literal. However, the Python interpreter cannot find the ending of this string literal before it encounters the end of the line. To fix this error, you need to put back the closing double quotes after the exclamation mark.



## From a Hello World to a ChatBot

You may get bored with saying "Hello, World!" to the multiverse. But if you have played with any chatbot, that may be the first thing a chatbot does. A chatbot can show a message to greet you. 

Let's create our first chat bot greeting then. 

```python
print("Hello Jane! Welcome to the multiverse.")
```

If your name is not Jane, you may be disappointed. In the next lesson, we will learn how to take in your name so that the chatbot can greet you using your name. But before that, we need to ask: what kind of data is it? What kind of data is a name? As we build our chatbot, we will involve more and more data.
