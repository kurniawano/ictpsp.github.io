---
title: Calling a Function
permalink: /notes/calling-function
key: notes-calling-function
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

## Functions, Our First Abstraction

In our previous lessons, we have used a few built-in functions:
- `print()` to display data into the standard output, which in most cases is your computer screen.
- `int()` to convert a value into an `int` data type.
- `input()` to get a value entered through a standard input device, which in most cases is your keyboard.

We call these functions as built-in functions because Python provides these functions for our use. At the same time, we want to introduce the concept of abstraction and how functions actually provides that abstraction. For example, in order to display some data into a screen requires not a single instruction in a computer. It actually requires a number of instructions that would include part of the operating system before the data is displayed into the computer screen. However, Python **abstract** all those instruction into a single function called `print()`. 

In a way, a *function* encapsulates some computation. Every computation may or may not have some input. It may or may not have some output. Similarly, every function does some computation. Some function may or may not have some input. Some functions may or may not have some output. We can draw a function like a blackbox as shown in the diagram below. 

// Put image of function as black box with various combination of input and output

In the above diagrams, we have drawn various possible combination with regards to the input and output of a function. Let's discuss some of these in the sections below.

## How to Call a Function

The first important thing about function is to know how to **execute** a function. We have a term for this executing a function. We call it **calling** a function or **invoking** a function. Basically, when we call a function, we execute a whole set of instructions encapsulated by that function. We do not need to know how to display a character into a computer screen, we just need to know how to *call* the `print()` function. To call a function in Python, you need to specify using the following format.

```python
function_name(input_arguments)
```

We have to specify the name of the function followed by a round bracket or parenthesis. Inside the paranthesis, we need to provide the input data required by the function to perform. For example, 

```python
print("Hello World")
int("5")
input("How many steps?")
```

In the above, example, `print`, `int` and `input` are the function names. You can see that all three has the parenthesis following the function name. Inside these paranthesis are the input data needed by the function to perform its computation. We call this input data as **input arguments**. So `"Hello World"`, `"5"`, and `"How many steps?"` are input argument to the respective function calls above. 

Not all functions have input arguments but the above three functions are example of functions with input arguments. Similarly, not all functions have outputs. In fact, one of those three function does not have an output. Let's see which one.

## Output of a Function Versus Side Effects

Input arguments are data that the function **takes in** in order to do its computation. The **output** of a function is the data that the function **throws out** as a result of some computation inside the function. In our three built-in examples, only `int()` and `input()` throws some output. The `print()` function does not throw an output. 

// Put diagram for function that throws output and no output.

You may wonder why `print()` function does not throw an output though you can see something on the computer screen. Doesn't displaying data on a screen can be considered as an output? 

Again, let's repeat our definition of an output of a function. The output of a function is the data thrown out by the function as a result of some computation inside the function. Therefore, one way to check if a function has an output or not is to check what data is coming out from that function. We can store data into some variables as we saw in our previous lessons. For example,

```python
cadence: int = 25
```

In the above line, we create variable called `cadence` which is an integer and assign a value `25`. Since the literal `25` is interpreted by Python as an `int` data, cadence is binded to an `int` data `25`. We can consider this assignment as *storing* the value `25` into the variable `cadence`. See image below.

// PUt image of storing a literal to a variable.

Now, we can see if a function throws any output data by storing that output data into a variable. We will use the same **assignment** operator to assign the output of the function to the variable.

```python
out_print = print("Hello World")
print(out_print)

out_int = int("5")
print(out_int)

out_input = input("What's your steps?")
print(out_input)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=out_print%20%3D%20print%28%22Hello%20World%22%29%0Aprint%28out_print%29%0A%0Aout_int%20%3D%20int%28%225%22%29%0Aprint%28out_int%29%0A%0Aout_input%20%3D%20input%28%22What's%20your%20steps%3F%22%29%0Aprint%28out_input%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Try the above code and enter `25` as your number of steps. You will get something like the following output.

```
Hello World
None
5
What's your steps? 25
25
```

The first line displays `Hello World` and this is due to the print function where the input argument is that string data to be displayed. However, the next line contains `None`. This line is due to the `print(out_print)` statement. As we can see that the `out_print` variable stores the output of the `print()` function in the first line. The data is displayed in the second line of the standard output as `None`. The reason of this is that `print()` function does not throw any output data. Python, by default, returns a `None` object when it does not have any return output data. 

The third line of the output, however, displays `5`. This is the result of `print(out_int)`. So we know that `int()` function throws an output data, i.e. `5`. The second last line, we see the prompt being displayed into the standard output, `What's your step?`. In the last line, we see the output data thrown out by the `input()` function, i.e. `25` (assuming you enter 25 when prompted "What's your steps?"). 

So we see that both `int()` and `input()` throws some output data but `print()` does not. This *throwing out* output is more commonly called **return an output** in programming languages and you will see later on that Python has a specific keyword if you want to return an output from your user-defined function. We will learn how to create our own user-defined function soon.

But we may ask, so what is the thing that we see on the screen when we call `print()` function? The answer is it is a **side effect**. A function is said to have a side effect if it modifies some state outside of its local environment. This results in some observable effect other than its primary effect of returning a value to the invoker of the function. In our case, displaying a text into a screen is this observable effect. The cause of this observable effect of something appear on the screen is that the `print()` function modifies something outside of its function **not by returning a value to the program that call the print function**. We have seen that the function `print()` does not return any data to `out_print`. Because `print()` modifies something outside of its function not through its **return value**, we say that the `print()` function has a side effect. 

Now, we have differentiate an output of a functin and a side effect. When we call a function, Python evaluates its **return value** as its output. For example,

```python
out_int = int("5")
```

Python interpreter evaluates the return value of invoking `int("5")`. The result of this computation is the output of the function which is an `int` type data that represent `5`. This output is then assigned to the variable.

```python
out_int = 5
```

It is a good practice to annotate your variable to keep track of your data type. In our previous code, we should have written the following.

```python
out: int = int("5")
```

Instead of putting the "int" as part of the variable name, we can use type annotation. The good thing about type annotation is that we can use tools such as `mypy` to do a static check on our code.

// Put diagram

## Importing and Calling Math Functions in Python

We have learnt how to call functions and supplying the input arguments as well as how to retrieve the output returned by the function. Now we can work with more functions. One of the common functions that Python provides is the math library. In order to use the math library, we need to import them into the current environment.

```python
import math
```

You can find a list of math functions [in this link](https://docs.python.org/3/library/math.html). 

For example, if you want to find a square root of a number, you can call the `sqrt()` function from the `math` library. 

```python
import math
x: float = math.sqrt(4)
```

The value of `x` after executing the function is `2`. Notice that we are importing the `math` name into our environment. This `math` name contains a reference to the `math` module that contains a range of functions. In order to access that function inside that module, we use the **dot** operator as in `math.sqrt()`.  Notice also that our `math.sqrt()` function returns a float and not an integer. Because of this, we annotate `x` as a float.

Sometimes, we are too lazy to keep on typing `math` everytime, we want to call a function. In this case, we can rename it using the keyword `as`. 

```python
import math as m
x: float = m.sqrt(4)
```

If we do not prefer to type `m` at all, we can simply import the function itself instead of importing the module into our environment. In this case, we do it as shown below.

```python
from math import sqrt
x: float = sqrt(4)
```

In the last example, what we imported is only the function `sqrt` which we get from the `math` module. If two packages provide a similar function name, your global frame will be populated by only the last name you define or imported. If you prefer to keep separately the two functions for different usage, it is recommended to use the second approach above by renaming the different modules and access the same function name using the dot operator. 

For example, `numpy` also provides a `sqrt` function. We can import both function as follows.

```python
import math as m
import numpy as np
x: float = m.sqrt(4)
y: float = np.sqrt(4)
```

You maybe wondering what's the use of `numpy` package if `math` package already provides the same square root function. Python's `math` library deals with either `int` or `float` data type but not a collection of these data. On the other hand, `numpy` can deal better with array-like data. In later section, we will learn about some collection data like `list` which `numpy` array can handle better. For `math` library, we need to loop over those values in the collection in order to apply the function. There is another way like using the `map` function to do similar thing. For now, our objective is on how to call functions and how to import functions from another library like `math`.


## Summary

In this lesson, you have learnt how to call a function. Some functions require you to supply the input arguments for the function to do its calculation. You also learn how take the return value of the function which we also call as the output of the function. We differentiate the output returned by the function and its side effect. Some functions like `print()` do not have output but creates side effect. We also learn on how you can make use of other functions created by other people such as the various mathematical function in the `math` library. We show the different ways of importing the module into the current environment so that we can call the function using the dot operator. 
