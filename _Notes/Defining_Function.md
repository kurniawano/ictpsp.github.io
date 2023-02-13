---
title: Defining a Function
permalink: /notes/defining-function
key: notes-defining-function
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

## Defining Your Own Function

In our previous lessons, we have been using some built-in functions such as `print()`, `int()` and `input()`. We also have started using other functions provided by `math` library, particularly the `sqrt()` function. There are many other functions provided in the `math` library. However, our focus now is on how can we create our own user-defined function or our own custom function. Let's say, what if you want to create a function to compute the cadence of your cycling app. Recall previously, that we wrote the following code in our cycling chatbot.

```python
steps_inp: str = input("how many push you did on the pedal within 30 seconds? ")

steps: int = int(steps_inp)
cadence: int = steps * 2

print("Your cadence is ", cadence)
```

Now, some other people may wonder why you multiply steps by 2. Wouldn't it be more easier to understand if you replace that line with the following?

```python
cadence: int = compute_cadence_for_30sec(steps)
```

How cadence is computed does not matter at the moment for others to understand your code. See the overall code now.

```python
steps_inp: str = input("how many push you did on the pedal within 30 seconds? ")

steps: int = int(steps_inp)
cadence: int = compute_cadence_for_30sec(steps)

print("Your cadence is ", cadence)
```

This new function `compute_cadence_for_30sec()` serves several purposes. First, it serves as an abstraction on how to calculate a cadence for 30 sec. People need not know how to actually compute cadence, they just need to call this function and they get the result. Second, by naming the process of computation `steps * 2` as `compute_cadence_for_30sec()`, we actually gives meaning to the overall process. Now calculating cadence is straight forward, but imagine if your calculation takes hundreds of lines. By naming those hundred of lines of code into a single name, we actually simplify code. We provide name and meaning to the overall process with a single name, i.e. the function name.

But now, we need to be able to write our own custom function or user-defined function. Let's learn how to do it for the various possible function combination that you have seen previously.

// put images of blackbox with and without input/output

## Defining Functions With Input Arguments and Return Values

// put image of box with both input and output

We will start with the first function that takes in input argument and return some output (return value). The format to define a new function is as follows.

```python
def function_name(arg1, arg2, ...):
  // body of the function
  return output
```

Our `compute_cadence_for_30sec()` is an example of this kind of function. In this function, we take in the number of steps as our input and it returns the cadence as the output. Let's see how, we can define this function in Python.

```python
def compute_cadence_for_30sec(steps):
  return steps * 2
```

It is always good to ask the question, "What is the input?" and also "What is the output?". This is part of our PCDIT framework of Problem Statement. We can apply that framework to design our user-defined function. In this problem, our input is steps in 30 seconds and the output expected is the cadence. 

In the above code, `steps` is the only input argument. If you have more than one input arguments, you can separate them using a comma. The output of the function is specified using a special keyword `return`. In this case the output is this `steps * 2` which is the cadence. 

In asking the input and output of our problem statement, we must also ask, "What is the data type?" or "What kind of data is this?". The input `steps` is most probably a whole number and so we can use `int` data to represent steps. Similarly, since the cadence calculation is just a multiplication by 2, we would expect that the output is also an `int`.

Python 3.6 onwards allows you to annotate the input and output data type for static type checker to verify. The above function definition can be re-written as follows.

```python
def compute_cadence_for_30sec(steps:int) -> int:
  return steps * 2
```

Similar to declaring the type of a variable, we also declare the input argument's type in the same way using colon `:`, i.e. `steps:int`. As regards the output data type or the return value, we use arrow `-> int` to specify the expected data type. 

To use this function, we have to *invoke* or *call* the function. Let's write the code in a file called `01_cadence_int.py`.

```python
def compute_cadence_for_30sec(steps: int) -> int:
  return steps * 2

print(compute_cadence_for_30sec(25))
```

We can run a static type checker on this file.

```sh
$ mypy 01_cadence_int.py
Success: no issues found in 1 source file
```

Try to change the input argument to other data type such as a float and save it as a new file called `02_cadence_float.py`. 


```python
def compute_cadence_for_30sec(steps: int) -> int:
  return steps * 2

print(compute_cadence_for_30sec(24.5))
```

You can see how `mypy` helps us to check if an incorrect input data type is given.

```sh
$ mypy 02_cadence_float.py 
02_cadence_float.py:4: error: Argument 1 to "compute_cadence_for_30sec" has incompatible type "float"; expected "int"  [arg-type]
Found 1 error in 1 file (checked 1 source file)
```

The error says that argument 1 of the function expected an `int` but it is given a `float`. You may think, what's the big deal of checking the data type. In fact, if it is a float, you still get the answer correctly. Let's run Python on this file.

```sh
$ python 02_cadence_float.py 
49.0
```

The function still computes correctly. But now, let's try what happens if you supply a `string` data into the function. Let's modify into a string and save it into a new file called `03_cadence_str.py`. 

```python
def compute_cadence_for_30sec(steps: int) -> int:
  return steps * 2

print(compute_cadence_for_30sec("25"))
```

In the above code, the input argument provided is a `string` data, i.e `"25"`. Running this code results in the following.

```python
$ python 03_cadence_str.py 
2525
```

The output is puzzling and unexpected. It no longer gives `50` as the cadence as in the previous calculation. The reason is that the `*` operator works differently for different kind of data. For number data such as `int` and `float`, the operator `*` does multiplication. However, for `string` data, the operator `*` does a *duplication* of the string. In the above code, what happens is that the string `25` is duplicated *two times* when executing `return steps * 2`. 

It is important, therefore, to ask "What is the data type?". Using `mypy` would prevent such error. Notice that Python continues to execute the code without throwing any error. Python does not check the type. This is where running static type checker such as `mypy` helps.

```sh
$ mypy 03_cadence_str.py 
03_cadence_str.py:4: error: Argument 1 to "compute_cadence_for_30sec" has incompatible type "str"; expected "int"  [arg-type]
Found 1 error in 1 file (checked 1 source file)
```

## Returning Multiple Values as a Tuple

## Defining Functions with Optional Arguments

## Specifying Data Types in Arguments and Return Values

## Abstracting a Problem as a Function

## Identifying Input, Output and Process of a Problem