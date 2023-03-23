---
title: Basic Data Types
permalink: /ictpsp/notes/basic-data-types
key: notes-basic-data-types
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

## What Kind of Data is This?

It is important to ask the question, "what kind of data is this?". One of the challenges of novice programmers is that Python does not require you to declare the *data type*. So many novice programmers do not think on this question, "what kind of data is this?". However, it is essential on every part of the problem solving steps, to continue asking the question, what kind of data we are dealing with.

In the first step `P` for Problem statement, we are asking what is the input, output and the process. In answering these questions, we have to ask what *kind* of data is the input and what *kind* of data is the output. The kinds of data is what we call as *data type*. 

In our first problem, we want to display `Hello World!` into the screen. We should ask, what kind of data is this?

## Two Basic Data Types

Now, we will introduce two basic data types:
- text
- numbers

In our first problem, our data is not numbers but rather text. We call this data of a `string` data type. In some other programming language, they have a character data type where it only consists of a single character. Python does not have a character data type. To create a character, you basically create a string with only one character.  

If you recall about our chatbot, a name will be a string data. But let's say if you create a chatbot to calculate your cadence related to your fitness activity, some of those data may not be a string. For example, the chatbot can ask on the number of steps and the duration of your walk or your cycling period. In calculating your cadence, the app has to work with numbers to do the mathematical manipulation. 

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

## Creating a String Data

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

If the above code looks foreign to you, do not worry. We will discuss about the `for-in` statement, the `range()` function and the role of variables in subsequent lessons. But I hope you can at least identify there are two data types in the above code. The first one is the `int` data which we create using `1_000_000` to represent the number of worlds we have (assuming we only have 1 million worlds). The second one is the `string` data which we create using the double quotes in `"Hello World no. "`. Thinking about "what kind of data is this?" is very important. Knowing what data that is helps us to know what we can do about it. Different data has different operations and ways to manipulate.

## Running Python Code as a Script

We have been running our code in a Python shell. We enter the shell by first typing:
```sh
python
```

in our terminal. 

The second way of running our Python's code is as a *Script*. To do this, create a new *text file* called `01_hello.py`. You may want to use code editor like Visual Studio Code, Atom, Sublime Text, etc, to do this. You can write your code and paste it into your new text file.

```python
print("Hello World no. ", 1)
print("Hello World no. ", 2)
print("Hello World no. ", 3)
```

After you save your text file, you can run this code by running the following command in your terminal or command prompt.

```sh
python 01_hello.py
```

You will see an output that looks like this.

```sh
Hello World no.  1
Hello World no.  2
Hello World no.  3
```

The above command assumes you are in the same location as where you save your `01_hello.py`. For example, if you save your `01_hello.py` in your `/Users/my_user/Downloads`, then you need to go into that folder first. The terminal command to go to a particular location is `cd` which means change directory.

```sh
cd ~/Downloads
```

In Unix-based OS, the character `~` is used to indicate the home user's directory, which is the same as `/Users/my_user/`.

If you use Windows operating system, you may store it in something like `C:\Users\my_user\Downloads`. Similarly, you can open your command prompt and type the following

```dos
cd $HOME\Downloads
```

In Windows, `$HOME` stores the location to the user's home directory. 


## Sequence Matters

In programming, sequence matters. In fact, this is the first pattern that you will continue to see recurring again in all computer codes. Computer codes in general execute the instruction in sequence **from top to bottom**. When you run your code as a script, the sequence matters because different sequence may create a different output. For example, run the below code which is the same as in the previous one using Python Tutor to visualize the sequence. You can click the "next" button to step through the execution of the code. However, we want you to note the two arrows. The green and the red arrows. The green light arrow indicates the instruction that has *just been executed*. On the other hand, the dark red arrow indicates the instruction that is *about to be executed*. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=print%28%22Hello%20World%20no.%20%22,%201%29%0Aprint%28%22Hello%20World%20no.%20%22,%202%29%0Aprint%28%22Hello%20World%20no.%20%22,%203%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The output is different from the following one.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=print%28%22Hello%20World%20no.%20%22,%203%29%0Aprint%28%22Hello%20World%20no.%20%22,%201%29%0Aprint%28%22Hello%20World%20no.%20%22,%202%29%0A&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The reason that the output is different because the sequence of the instruction is different. In the second one, the hello to world number 3 is executed first before the other two instructions. 

Besides noting that the sequence matters, it is important to understand the concept of **program counter**. The red arrow in the two embedded code above shows the program counter. A program counter **points to the next instruction to be executed**. In most cases, the program counter moves from **top to bottom** in a linear sequence. We will learn ways to alter this behaviour in the subsequent lessons. But for now, it is important to remember that program counter moves in sequence from top to bottom. The program counter indicates which instruction to be executed next. 

## Introducing Variables

In many cases, we want to **work** with data. This means that our data may change over time. We may also re-use some of the data we have created in other places in our computation and manipulate it. Computers are good to work with numbers but human works better with labels. In most programming language, we are able to create a **variable** that binds a label or a name with a value or data. For example, in the previous problem of saying hello to our multiverse, we can actually store our world's index or number into a variable. For example,

```python
world_index = 1
print("Hello World no. ", world_index)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=world_index%20%3D%201%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

When you click "next" for the first time, Python interpreter will execute the first line `world_index = 1`.  The effect of this execution  was not apparent as there is no output produced. However, Python Tutor displays that there are three things happening in the **Global frame** which is the memory environment used by Python to execute the code.
- a label or a name called `world_index` was created
- an `int` literal was created with the value `1`. 
- the name `world_index` was binded with the literal data `1`.

When you click the "next" button the second time, Python interpreter executes the `print()` statement and displays the text into the standard output. Note that in displaying this output, Python interpreter encounters a **name** called `world_index`. Python interpreter then tries to find what is the meaning of this name. Python could not find it in any of its built-in keywords and functions and, therefore, check whether `world_index` is **defined** in the *global frame*. When Python interpreter finds the name `world_index` in the global frame and recognize that it is a variable, it evaluates its value, which is `1`. Thus, the above code is evaluated similar to the following code.

```python
print("Hello World no. ", 1)
```

A variable is just a name that is binded to some value. You can change this binding to a different value. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=world_index%20%3D%201%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29%0Aworld_index%20%3D%202%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29%0Aworld_index%20%3D%203%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, when Python interpreter executes line number 3 `world_index = 2`, it does the following:
- Python creates an `int` literal with value `2`.
- Python binds this new literal to the name `world_index`.

We can see that the value in the *global frame* for `world_index` changes to `2` after executing line 3. 

You may have noticed that we use the equal sign, i.e. `=` in the above code. This **operator** is called the **assignment operator**. It is called the assignment operator because it assigns the literal to a label or a name. 

Note that this assignment is from **right to left**. We cannot swap the sequence. Writing the below code produces an error. 

```python
>>> 1 = world_index
  File "<stdin>", line 1
SyntaxError: cannot assign to literal
```

The error says that you cannot assign something to a literal. Recall that `1` is an `int` type literal and the assignment is from right to left

The error says that you cannot assign something to a literal. Recall that `1` is an `int` type literal and the assignment is from right to left. With the above code, you are telling python to assign the value associated with the name `world_index` to the literal `1` and Python does not allow this. 

## Checking Data Type

Python makes it easy for programmers to create variables. But this comes at a cost that programmers do not ask the question, "What kind of data is this?". When you create a variable, binds the data dynamically and does not require you to specify the type of the data. However, Python 3.6 onwards allows programmers to specify the data type as a kind of **annotation** to be checked by other programs. You can specify the previous variable as follows.

```python
world_index: int = 1
```

However, what Python does is just to create an annotation and does not enforce it. For example, you can still make mistakes assigning a wrong data type and Python interpreter will still executes fine. Run the following code step by step observing the data created in the memory.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=world_index%3Aint%20%3D%201%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29%0Aworld_index%20%3D%20%222%22%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29%0Aworld_index%20%3D%203.0%0Aprint%28%22Hello%20World%20no.%20%22,%20world_index%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

As you can see that `world_index` is neither `str` nor `float` and yet Python continues to executes the code. The annotation is useful if you use other checker to check your code. The most common one is called [mypy](https://github.com/python/mypy). 

To install mypy, do the following from the terminal.

```sh
python -m pip install -U mypy
```

You can then run `mypy` on your script. To create your script. Create a text file called `02_wrong_type_hello.py` and type in the following code.

```python
world_index:int = 1
print("Hello World no. ", world_index)
world_index:str = 2
print("Hello World no. ", world_index)
world_index:float = 3
print("Hello World no. ", world_index)
```

Running `mypy` on the text file results in the following.

```sh
$ mypy 02_wrong_type_hello.py
02_wrong_type_hello.py:3: error: Incompatible types in assignment (expression has type "str", variable has type "int")  [assignment]
02_wrong_type_hello.py:5: error: Incompatible types in assignment (expression has type "float", variable has type "int")  [assignment]
Found 2 errors in 1 file (checked 1 source file)
```

To fix this error, you need change the data back to `int` type. Create a new text file with the corrected code with the name `03_correct_type_hello.py`. 

```python
world_index:int = 1
print("Hello World no. ", world_index)
world_index = 2
print("Hello World no. ", world_index)
world_index = 3
print("Hello World no. ", world_index)
```

And run `mypy` again.

```sh
$ mypy 03_correct_type_hello.py
Success: no issues found in 1 source file
```

Notice that `mypy` does not actually runs the code but only checks if there is any issues by doing static type checking on the code. We will use `mypy` to improve our code.

As a programmer, you can actually check what is the data type of a variable using the `type()` function. 

```python
world_index = 1
print(type(world_index))
world_index = "2"
print(type(world_index))
world_index = 3.0
print(type(world_index))
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=world_index%20%3D%201%0Aprint%28type%28world_index%29%29%0Aworld_index%20%3D%20%222%22%0Aprint%28type%28world_index%29%29%0Aworld_index%20%3D%203.0%0Aprint%28type%28world_index%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Try clicking the "next" button and see how the code works. I think it is important to explain the following line.

```python
print(type(world_index))
```

When Python interpreter sees this, 
- it sees a name `print` and recognize that you are *invoking* a function due to the opening and closing parenthesis `print()`. 
- Python tries to evaluates the value inside the parenthesis to pass it to the `print()` function. 
- When Python evaluates the value inside the parenthesis, it finds another name `type` and recognize that it is another of its built-in function.
- Python also sees that you are invoking `type()` because of the opening and closing parenthesis. In order to execute this function, Python tries to evaluate the value inside this *inner* parenthesis.
- When evaluating the inner parenthesis, Python finds another name `world_index`. This time, Python cannot recognize this name from any of its built-in keywords or function and tries to find it in the global frame.
- Python finds the name `world_index` in the global frame and obtains the value, which is `1`.
- Python pass this value `1` to the function `type()` and executes `type()`. This functions evaluates to a data that describes Python's `type`. You can actually try to type the following in a Python shell to see: `type(type(1))`. You will get `<class 'type'>`. 
- Python then pass this output of `type()` function to `print()` function. In order to print it, Python will convert this data into a string so that it can displays it into the standard output.
- Python finally displays `<class 'int'>` into the screen.

Now, that's a lot of things going on with just a simple code. But it is important to note that Python **evaluates from inside to outside of the parenthesis** when it invokes a function such as `print()` and `type()`. We will learn more about function in the next lesson. 

## Environment Diagram

Python Tutor allows you to see the memory environment of your code. On the right hand side of your code you see two panels, the first one at the top right is the print of your standard output. This panel shows you whatever that you display to the standard output through the `print()` function. The second one is on the right side just below the print output panel. This shows you what is happening in the memory environment of your code. At the beginning, you only see the labels:
- Frames
- Objects

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=world_index%20%3D%201%0Aprint%28type%28world_index%29%29%0Aworld_index%20%3D%20%222%22%0Aprint%28type%28world_index%29%29%0Aworld_index%20%3D%203.0%0Aprint%28type%28world_index%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Try clicking the "next" button and you will see that the first frame created is called the **global frame**. Later on, when you learn to create your own user defined function, you will see that each function has its own local frame. But for now, we will only deal with the global frame. All the variables are created in this global frame. Currently, we only have one variable called `world_index`. As we introduce more data and more different kinds of data, you will see more things in this environment diagram.

## Identifying Data Type in a Problem

The first step of PCDIT is Problem Statement. In this step, we need to identify the input, output and process of the problem. In identifying the input and the output, we need to ask, "what kind of data is this?". 

Let's try to identify the input and output of our chatbot. Let's say, our chatbot is able to advise us on our fitness activity and would like to calculate your cadence from your previous cycling period. So the chatbot will do a conversation like the following.

```
Hi, Jane! How as your last cycling?

> nice

Did you count how many push you did on the pedal within 30 seconds?

> 25

Thanks. Your cadence is 50. That's rather low, you may want to try to increase it.
```

Now, we should ask, what the input and the output of this program is. The input to the chatbot is all the data that you give to the program. In this case, they are text data as you type into the chatbot. This means that the data is a string data. On the other hand, the chatbot displays a string data as well into the app screen. So both input and output are string. 

You may ask why the input is not a number since `25` looks like a number. The answer is that the data that you key in is considered as a string because it is entered into a kind of text field. This is why it is important to ask what kind of data it is. 

However, in order to calculate the cadence, you cannot manipulate a string data and therefore you need to transform your data into a number-like data. Since steps tend to be generally whole number, we can convert that string data into an `int`. So now we can roughly design our algorithm to calculate your cycling cadence.
1. Request for number of steps within 30 seconds
1. Convert the number of steps from string into integer
1. Multiply number of steps by 2 to get the cadence

Depending on the cadence we may want to decide whether to prompt the user to increase their cycling cadence or not. But in order to display different messages, we will need to learn on the control structure in the subsequent lesson. For now, we can implement the cadence calculation.

In order to get data, you need to learn a function to take in data from the keyboard. In Python, you can use `input()` function where the argument is the prompt you want to display to the user. This function returns you the string that the user enters through the keyboard. 


```python
steps_inp: str = input("how many push did you do on the pedal within 30 seconds? ")

steps: int = int(steps_inp)
cadence: int = steps * 2

print("Your cadence is ", cadence)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=steps_inp%3A%20str%20%3D%20input%28%22how%20many%20push%20you%20did%20on%20the%20pedal%20within%2030%20seconds%3F%20%22%29%0A%0Asteps%3A%20int%20%3D%20int%28steps_inp%29%0Acadence%3A%20int%20%3D%20steps%20*%202%0A%0Aprint%28%22Your%20cadence%20is%20%22,%20cadence%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=1&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%2225%22%5D&textReferences=false"> </iframe>


Try clicking the "next" button step by step. When Python Tutor loads, you will see a prompt to enter the number of steps. In the embedded Python Tutor, a value of 25 was already entered. If you want to see the prompt and enter it yourself, you can click [this link](https://pythontutor.com/visualize.html#code=steps_inp%3A%20str%20%3D%20input%28%22how%20many%20push%20you%20did%20on%20the%20pedal%20within%2030%20seconds%3F%20%22%29%0A%0Asteps%3A%20int%20%3D%20int%28steps_inp%29%0Acadence%3A%20int%20%3D%20steps%20*%202%0A%0Aprint%28%22Your%20cadence%20is%20%22,%20cadence%29&cumulative=false&curInstr=0&heapPrimitives=nevernest&mode=display&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false). Now you see the variable `steps_inp` was created in the global frame with a value `"25"`. You can note that the data type is a string. 

The next instruction is to convert the data into an `int` using the `int()` function. Notice the common way of calling the function using the parenthesis. The output is stored in a new variable called `steps`. After you click "next" you see that the value of `steps` and `steps_inp` are different. One is an `int` while the other is a `string`. 

In the next instruction, we calculate the `cadence` by multiplying the number of push within 30 seconds. And lastly, this number is printed into the standard output. 

You can try running the above Python code as a script. To do that, create a new file, say with the name `04_cadence_bot.py`. Paste the code into this text file. You can run the code then by typing the following into the terminal.

```sh
python 04_cadence_bot.py
```

The output and interaction may look like something of the following.

```sh
$ python 04_cadence_bot.py 
how many push you did on the pedal within 30 seconds? 23
Your cadence is  46
```

In the above code, the output cadence is also an `int` but then we display this value into the standard output. In later lessons, we will learn on Python's string formatting so that we can format any data as a string to display them in the standard output in a better way.

## Summary

In this two lessons, you have learnt how to write your first code. The first important pattern that we introduce here is what we call as **sequential**. In general, Python code is executed in sequence from the top to the bottom. We will learn how to change this sequence to allow variation of code to be executed depending on different conditions. 

We also learn our first built-in function, which is `print()`. We learn how to call a function using the parenthesis and supplying the input data to the `print()` function through its argument. We will create our own custom function in the next lesson. We also made use of `int()` function to convert a string data into an `int` data type.

How would we know that we need to use `int()` function in our last example of cadence chat bot? The answer is because we were asking the question, "What kind of data is this?". In our use of `input()` function (the other built-in function that we use), the output of this function is a `string` data. Because it is a string data it cannot be used with any other mathematical operators to calculate any new data. But an `int` data is a numeric data that can be manipulated using mathematical operators. So we convert it to an `int` first before we calculate the cadence. Asking what kind of data that we are dealing with is a necessary components in PCDIT framework. So in this P (problem statement) step, we also ask that question. That helps us to know that we need a step to convert the data from one type to another type.

We have introduced a few basic data types, `string`, `int` and `float`. These are the basic data and it allows us to do a simple chatbot example to calculate cadence when you cycle. In subsequent lessons, we will introduce more data and when you learn about object oriented, you will be able to create your own custom data. 

In the next lesson, we will dive in into **functions**, which is our first lesson on abstraction. Remember that abstraction is one of the big element in computational thinking. You will see abstraction every where in learning how to code and creating a function is one of the first example of abstraction that we will introduce. 


