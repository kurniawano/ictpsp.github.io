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


## Abstracting a Problem as a Function
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

## Defining a User-Defined Function With Input Arguments and Return Values

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

## Specifying Data Types in Arguments and Return Values

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

## Functions Taking in Multiple Arguments 

If you know your bicycle parameters, you can determine your cycling speed based on your cadence and those parameters. Using the below equation, you can determine the speed. 

$$\text{speed} = \pi \times \left(\text{diameter} + (2 \times \text{tire\_size})\right) \times (\text{chainring}/\text{cog}) \times \text{cadence}$$

In the above equation, we need a few input values in order to determine the speed:
- diameter of the wheel in mm
- tire size  in mm
- chainring and cog values. The ratio between them is called the gear ratio.
- and lastly the cadence.

Now, if we want to compute the speed, we need all these inputs and our functions must be able to take in all these inputs. In Python, we separate the different input arguments using a comma as shown below.

```python
import math
def calculate_speed(diameter, tire_size, chainring, cog, cadence):
  gear_ratio = chainring / cog
  speed = math.pi * (diameter + (2 * tire_size)) * gear_ratio * cadence
  return speed * 60 / 1_000_000
```

Notice that we have imported the `math` library in order to get the value of $\pi$. We have talked about math library in our previous lessons where we imported some functions. This time, instead of a function, we imported a constant from the library.

We also have a few input arguments this time. In fact, we have five of them. It is useful to document what these arguments are. We may need it to describe the unit of these values such as whether they are in milimeters or in inches. Similarly what is the unit of the output. The last line of the above functin is needed to ensure that the output speed has a unit in km/h.

Note that the above code is just a **function definition**. We have not executed the function. To do a function invocation or function call, we need to type in the function name and provide the **actual arguments**. Let's input the following input arguments:
- wheel's diameter to be 685.8 mm or 27 inches
- tire's size to be 38.1 mm or 1.5 inches
- chainring to be 50 teeth
- cog to be 14 teeth
- and lastly the cadence is 25 rpm.

```python
>>> print(calculate_speed(685.8, 38.1, 50, 14, 25))
12.824430010904047
```

The result of the calculation is about 12.8 km/h for the given input arguments.

As you may see that the output calculated depends on the unit of the inputs. For someone to use this function, they need to know what kind of value to be put into the actual arguments. 

The common way to do it is to insert what we call as a docstring. It is a multiline of string just after the function definition which serves to explain about the function. Let's write our docstring describing the input and the output.

```python
import math
def calculate_speed(diameter, tire_size, chainring, cog, cadence):
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (int): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
  '''
  gear_ratio = chainring / cog
  speed = math.pi * (diameter + (2 * tire_size)) * gear_ratio * cadence
  return speed * 60 / 1_000_000
```

Since the input arguments are all in mm and the cadence is in rotation per *minute*, the variable `speed` has a unit  of mm/min. In order to change this unit to km/h, we multiply by 60 (to convert from minute to hour) and divide by 1,000,000 (to convert from mm to km). 

The nice thing about Python docstring is that we can access this documentation. To do that, type in the above code into the Python shell and press enter for Python to execute the function definition. In order to access the documentation, you can type `calculate_speed.__doc__`. 

```python
>>> print(calculate_speed.__doc__)

  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (int): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
```

You can also type `help(calculate_speed)` and it will enter into a help documentation mode in Python.

```
Help on function calculate_speed in module __main__:

calculate_speed(diameter, tire_size, chainring, cog, cadence)
    Calculates the speed from the given bike parameters and cadence.
    
    Parameters:
      diameter (int): diameter of the wheel in mm
      tire_size (float): size of tire in mm
      chainring (int): teeth of the front gears
      cog (int): teeth of the rear gears
      cadence (int): cadence in rpm
    
    Returns:
     speed (float): cycling speed in km/h
```

We can include the data type as part of the annotation into our function definition in order to make it even better. Our final function definition for the `calculate_speed()` is as shown below.

```python
import math
def calculate_speed(diameter: int, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> float:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (int): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
  '''
  gear_ratio = chainring / cog
  speed = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  return speed * 60 / 1_000_000
```

In the above definition, we decided to write the arguments in multiple lines. Python can take this as it understands that the arguments have to be enclosed within the parenthesis.  We have also used the backslash `\` character to write our long math expression into two lines. It is a convention to break *before* the binary operator following [PEP 8](https://peps.python.org/pep-0008/#should-a-line-break-before-or-after-a-binary-operator). 

## Functions Returning Multiple Outputs Using a Tuple

Let's say if we want our function not only to return the speed in km/h but also in mph (miles per hour). Python allows functions to return a *tuple*. A tuple is a collection data type that can contain more than one values. In order to create a tuple, we just need to separate them using a comma (`,`). Most of the time, for clarity purposes, we put a parenthesis around the tuple. 

For example, the code below creates a tuple and print its values and its type.

```python
>>> my_output = 12.8, 7.97
>>> print(my_output)
(12.8, 7.97)
>>> print(type(my_output))
<class 'tuple'>
```

We can then use a tuple to return multiple values out of the function. For example, the first value of the tuple can be the speed in km/h and the second value of the tuple is the speed in mph. We can rewrite our functions as shown below.

```python
import math
def calculate_speed(diameter: int, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> float:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (int): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
  '''
  gear_ratio = chainring / cog
  speed = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmh = speed * 60 / 1_000_000
  speed_mph = speed * 60 / 1.609e6
  return speed_kmh, speed_mph
```

In our equation above, we created two additional variables to store the speed in km/h and the speed in mph. We use a conversion of 1 mile to be about $1.609\times 10^6 \text{mm}$. 

There are two ways to access the output. First is that, we provide two variables to store the output when calling the function.

```python
speed_kmh, speed_mph = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed_kmh, speed_mph)
```

The other way is to store it in a single variable first which then can be accessed using the bracket operator. 

```python
speed = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed[0], speed[1])
```

The bracket operator takes in an index which starts from 0. This means that to access the first output, you use index 0. On the other hand, to access the second output, you use index 1 and so on. 


## Defining Functions with Optional Arguments

## Identifying Input, Output and Process of a Problem