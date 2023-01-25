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

So we have actually introduced the first step in PCDIT problem solving framework. In this framework, the first step is to specify the problem statement. In specifying the problem statement, we need to answer the three questions above: the input, the output and the process. 

So we can rewrite our first problem and make it more specific. What kind of data are we referring to? We have identified the process is to display this data into the output device, which is your computer screen. But what to be displayed? In many programming lessons, the first thing that programmers usually display is the following data: "Hello World!". 

Maybe, we should stop and ask what kind of data is "Hello World!". But before we go deeper, let's give a teaser to the solution of this problem written in Python. We will dig in deeper into this simple solution in the following sections. For now, here is how to display "Hello World!" into your computer screen. 

```python
print("Hello World!")
```

That's it! But how to run this code?

## Running a Python Code

We have written our first computer code in Python. But recall that what we have created is only the *source code*. The source code does not do anything. The code has to be executed for the computer to do what you ask the computer to do. Recall that there are two kinds of programming language: interpreter and compiler. Python is an interpreted language. This means that we need a Python interpreter to execute the code and make the computer to do what we ask it to do.

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

## Human Language and Programming Language

At this point it is important to note that there is a significant different between our human language and a programming language. The reason for this difference is that computer is not as smart as human in resolving ambiguity in the message. Computer requires a more exact instruction that is non-ambiguous to execute your instruction. On the other hand, human is much better at resolving ambiguities by reading the context, body language and other clues. Human also can verify if his understanding is correct or not. Computer requires exact and non-ambiguous instruction. 

This means that your *source code* has to be written with a certain rules. We call this *syntax*. For example, if you missed out one single character, Python interpreter may complain. Try to remove the last paranthesis and type it again into the shell. You will see the following behaviour. 

```sh
>>> print("Hello World!"
... 
... 
... 
```

In the above situation, Python interpreter expects you to have a closing parenthesis and when there is no closing parenthesis, the Python interpreter will wait for you to close it. To end the above misery just type in the closing parenthesis `)` and press enter in the shell. 

Why do you need a closing parenthesis? We will talk about **function** in more detail, but for now, it is sufficient to say that `print()` is one of Python built-in *functions*. To *invoke* or *call* a function, you need to specify the function name (in this case is `print`) and use parenthesis (opening and closing round bracket `()`) after the function name. So `print()` is the *syntax* to invoke the `print` function. You can guess that `print()` function's job is to display or print data into the standard output of your computer, which in most cases is the screen. What data to be displayed is the *argument* of the function and is put in between the parenthesis. This is why Python expect an opening and closing parenthesis to know when is the end of the function call. 

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

This indicates that the type of error is a `SyntaxError`. The message after this is saying that Python interpreter finds `EOL` which stands for *end of line* while scannign the string literal `"Hello World!`. What happens is that Python interpreter sees the first double quotes before the letter `H` and recognize that you are trying to create a string literal. However, Python interpreter cannot find the ending of this string literal before it encounters the end of line. To fix this error, you need to put back the closing double quotes after the exclamation mark. 

## What Kind of Data is This?

It is important to ask the question, "what kind of data is this?". One of the challenges of novice programmers is that Python does not require you to declare the *data type*. So many novice programmers do not think on this question, "what kind of data is this?". However, it is essential on every part of the problem solving steps, to continue asking the question, what kind of data we are dealing with.

In the first step `P` for Problem statement, we are asking what is the input, output and the process. In answering these questions, we have to ask what *kind* of data is the input and what *kind* of data is the output. The kinds of data is what we call as *data type*. 

In our first problem, we want to display `Hello World!` into the screen. We should ask, what kind of data is this?

## Two Basic Data Types

Now, we will introduce two basic data types:
- text
- numbers

In our first problem, our data is not numbers but rather text. We call this data of a `string` data type. In some other programming language, they have a character data type where it only consists of a single character. Python does not have a character data type. To create a character, you basically create a string with only one character.  

This `string` data type includes other kinds that may not so obviously a text such as:
- new line character
- tab and other whitespaces

Python supports the standard [ASCII characters](https://www.asciitable.com) and [Unicode](https://home.unicode.org) characters.

Even what may seem like numbers can be actually a `string` data type. For example, `1234` can be considered as a string instead of numbers. One example would be a student id data. Since this data is more like a label rather than being used with any mathematical manipulation, it is more likely that such data is represented as a string instead of as a number.

On the other hand, Python supports two kinds of numbers:
- `int`: whole number
- `float`: decimal numbers represented as floating point

An example for `int` data type would be the whole range of whole numbers: 3, 17, 1234, etc. On the other hand, `float` is used to represent numbers with decimal point. In computer, decimal numbers cannot be represented accurately all the time. The reason is that there are some numbers with infinite decimal expansion. For example,
- 1/11 = 0.090909...
- 10/3 = 3.333333...
- 7/4 = 1.74999...
- etc

Since computer stores information in a finite space (or finite *bits*), it is not possible for computer to represent these numbers accurately. Therefore, real numbers are stored in computer using a representation called *floating point numbers* that has some finite precision. When dealing with real numbers in computers, we have to accept that we can never eliminiate floating-point errors. We can only [manage floating-point errors by mitigating them](https://en.wikipedia.org/wiki/Floating-point_error_mitigation). 

## Creating Data  a String Data

Now, we can answer that `Hello World!` is of `string` data type. How can we create `string` data type and use it in our computer programs? There are a few ways of creating a `string` literal in Python.

The first way is to use *single* double quotes as shown in the previous code. 

```python
"Hello World!"
```

You can create this data in the Python shell. When you press enter, it will just display the data you just created.

```python
>>> "Hello World!"
'Hello World!'
>>> 
```

The second way is to use a *single* single quotes. 

```python
'Hello World!'
```

The third way is to use a *tripple* double quotes.
```python
"""Hello World!"""
```

And the last one is to use a *tripple* single quotes.
```python
'''Hello World!'''
```

Notice that you have to use the same opening and closing quotes to create the string. For example, you will see the following error if you try to use different quotes to create a string literal.

```python
>>> "Hello World!'
  File "<stdin>", line 1
    "Hello World!'
                 ^
SyntaxError: EOL while scanning string literal
>>> 
```

Remember to read the error from the bottom.  In the above code, we use a double quote in the beginning but use a single quote at the end. Python produces the same error. The reason is that Python interpreter cannot find the closing double quotes. 

Why does Python allow multiple ways to create strings? One reason is that single quotes and double quotes can be part of a `string` data. For example, you can create the following data.

```python
"Hello World! What's up"
```
Notice that we have a single quote in the text. We can also include a double quote in our text.

```python
'Yoda spoke, "World, Hello"'
```

What is important is that the opening and closing quotes must match. We cannot however, insert a single quote in between like the following.

```python
>>> 'Yoda spoke, 'World, Hello''
  File "<stdin>", line 1
    'Yoda spoke, 'World, Hello''
                  ^
SyntaxError: invalid syntax
```

The reason that the syntax is invalid is because Python finds a closing quotes for the string literal just before `World, Hello'`. Python interpret the `string` data to be: `'Yoda spoke, '`. Python does not understand how to interpret the subsequent characters in `World, Hello'` because there is no operator in between the two tokens of a string `'Yoda spoke, '` and a symbol `World`. Notice that Python does not interpret `World` as a `string` data because it does not have an opening quotes. Therefore, Python try to interpret `World` as a symbol or names instead. 

But how about the triple quotes? What is it used for? Python allows you to create multi-line string data using the triple quotes strings. For example,

```python
"""Hello,
World!"""
```

If you type this into the shell, you can see that it records the new line between the comma and the text `World`. 

```python
>>> """Hello,
... World!"""
'Hello,\nWorld!'
```

The new line is recorded as `\n` character. The backslash is normally used for an escape character in many programming language. 

## Creating Int and Float Data

So we now know that we can create `string` data using the various ways discussed in the previous section. How about numbers? How can we create `int` and `float` data in our code?

To create an `int` data, we just type the literal as it is.

```python
4321
```

When the numbers are long, you can use underscore to make it easier for human to read.  For example, this how you can create the following number $4,321,567,000 in Python.

```python
>>> 4_321_567_000
4321567000
```

On the other hand, to create a `float` data, we must make use of the `.` character to insert the decimal point. For example, to create 4321.0 data, we do either the following.

```python
4321.0
```
or
```python
4321.
```

The `0` is not required but the `.` is required to create a `float`. 

## Saying Hello to the Multiverse

Let's say we have a few worlds which we want to say hello. We can label each world with a number like:
- World no 1
- World no 2
- World no 3
- ...

We can then say hello to each of the world. 

```python
print("Hello World no. 1")
print("Hello World no. 2")
print("Hello World no. 3")
```

Another way of doing the same thing is by typing the following.

```python
print("Hello World no. ", 1)
print("Hello World no. ", 2)
print("Hello World no. ", 3)
```

What is the different between the two codes above? In the first code, we print the world's label 1, 2 and 3 as part of a single `string` data. On the other hand, in the second code, we print two **kinds** of data. The first data `"Hello World no. "` is a `string` data type. The second of data, however, is not. The data that is displayed into the screen, i.e. `1` is an `int` data type. The comma (`,`) in between the two data is just to separate the different objects to be displayed. 

Why this matters, you may ask. Thinking abou the data matters because we work with different data differently. For example, you can add numbers and increase it sequentially. Later, you will be able to write *loops* to do the above. Imagine if you have a million of worlds. You are not going to write `print()` statements a million times. Instead, you can just do the following.

```python
for world in range(1_000_000):
  print("Hello World no. ", world)
```

If the above code looks foreign to you, do not worry. We will discuss about the `for-in` statement, the `range()` function and the role of variables in subsequent lessons. But I hope you can at least identify there are two data types in the above code. The first one is the `int` data which we create using `1_000_000` to represent the number of worlds we have (assuming we only have 1 million worlds). The second one is the `string` data which we create using the double quotes in `"Hello World no. "`. Thinking about "what kind of data is this?" is very important. 


## Sequence Matters
