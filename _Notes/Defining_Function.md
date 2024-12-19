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
In our previous lessons, we have been using some built-in functions such as `print()`, `int()` and `input()`. We have also started using other functions provided by the math library, particularly the `sqrt()` function. There are many other functions available in the math library. However, our focus now is on how we can create our own user-defined function or custom function. Let us consider a scenario where you want to create a function to compute the cadence for your cycling app. Recall that we previously wrote the following code in our cycling chatbot.


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
This new function `compute_cadence_for_30sec()` serves several purposes. First, it acts as an abstraction for calculating `cadence` over 30 seconds. Users do not need to understand how cadence is computed; they simply call this function and receive the result. Secondly, by naming the computation process `steps * 2` as `compute_cadence_for_30sec()`, we give meaning to the overall process. Calculating cadence may seem straightforward, but imagine if the computation required hundreds of lines of code. By encapsulating those hundreds of lines into a single function name, we simplify the code. This provides both clarity and meaning to the overall process through the use of a single name—the function name.

But now, we need to be able to write our own custom function or user-defined function. Let's learn how to do it for the various possible function combination that you have seen previously.

<img src="/ictpsp/assets/images/lesson2/functions.png" width=600>

## Defining a User-Defined Function With Input Arguments and Return Values

<img src="/ictpsp/assets/images/lesson2/functions_i_o.png">

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

It is always beneficial to ask the questions, "What is the input?" and "What is the output?" This aligns with the PCDIT framework of Problem Statement. We can utilise this framework to design our user-defined function. In this case, the input is the number of steps in 30 seconds, and the expected output is the cadence.

In the code above, `steps` is the only input argument. If there are multiple input arguments, they can be separated using commas. The output of the function is specified using the special keyword return. In this instance, the output is `steps * 2`, which represents the cadence.

When considering the input and output of our problem statement, it is also important to ask, "What is the data type?" or "What kind of data is this?" The input steps is likely to be a whole number, so we can represent it using the int data type. Similarly, as the cadence calculation involves simply multiplying by 2, we would expect the output to also be an `int`.



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

```sh
$ python 03_cadence_str.py 
2525
```

The output is puzzling and unexpected. It no longer produces `50` as the cadence, as seen in the previous calculation. The reason for this behaviour lies in how the `*` operator functions with different types of data. For numerical data types such as int and float, the operator `*` performs multiplication. However, for string data, the operator `*` performs a duplication of the string. In the code above, the string `25` is duplicated two times when executing return `steps * 2`.

This example highlights the importance of asking, "What is the data type?" Using a static type checker like mypy can help prevent such errors. Notice that Python continues to execute the code without raising an error, as it does not enforce type checking at runtime. A tool like `mypy` allows you to detect such type mismatches before running the code, making it invaluable for catching these kinds of issues.

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
    diameter (float): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) * gear_ratio * cadence
  return speed * 60 / 1_000_000
```

Since the input arguments are all in mm and the cadence is in rotations per minute, the variable speed has a unit of mm/min. To convert this unit to km/h, we multiply by 60 (to convert from minutes to hours) and divide by 1,000,000 (to convert from mm to km). Notice that the gear_ratio is expected to be a float after dividing chainring by cog. Similarly, speed is also expected to be a float.

One of the useful features of Python's docstring is that it allows us to access the documentation directly. To do this, type the above code into the Python shell and press enter to execute the function definition. Once defined, you can access the documentation by typing `calculate_speed.__doc__`.

```python
>>> print(calculate_speed.__doc__)

  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (float): diameter of the wheel in mm
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
      diameter (float): diameter of the wheel in mm
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
def calculate_speed(diameter: float, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> float:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (float): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
   speed (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  return speed * 60 / 1_000_000
```

In the above definition, we decided to write the arguments in multiple lines. Python can take this as it understands that the arguments have to be enclosed within the parenthesis.  We have also used the backslash `\` character to write our long math expression into two lines. It is a convention to break *before* the binary operator following [PEP 8](https://peps.python.org/pep-0008/#should-a-line-break-before-or-after-a-binary-operator). 

## Functions Returning Multiple Outputs Using a Tuple

Suppose we want our function to return not only the speed in km/h but also in mph (miles per hour). Python allows functions to return a tuple. A tuple is a collection data type that can contain more than one value. To create a tuple, we simply separate the values using a comma (,). For clarity, we often enclose the tuple in parentheses.

For example, the code below creates a tuple and print its values and its type.

```python
>>> my_output:tuple = 12.8, 7.97
>>> print(my_output)
(12.8, 7.97)
>>> print(type(my_output))
<class 'tuple'>
```

We can then use a tuple to return multiple values out of the function. For example, the first value of the tuple can be the speed in km/h and the second value of the tuple is the speed in mph. We can rewrite our functions as shown below.

```python
import math
def calculate_speed(diameter: float, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> tuple[float, float]:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    diameter (float): diameter of the wheel in mm
    tire_size (float): size of tire in mm
    chainring (int): teeth of the front gears
    cog (int): teeth of the rear gears
    cadence (int): cadence in rpm

  Returns:
    Tuple:
      speed_kmph (float): cycling speed in km/h 
      speed_mph (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmph: float = speed * 60 / 1_000_000
  speed_mph: float = speed * 60 / 1.609e6
  return speed_kmph, speed_mph
```

In our equation above, we created two additional variables to store the speed in km/h and the speed in mph. We use a conversion of 1 mile to be about $1.609\times 10^6 \text{mm}$. 

There are two ways to access the output. First is that, we provide two variables to store the output when calling the function.

```python
speed_kmph, speed_mph = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed_kmph, speed_mph)
```

The other way is to store it in a single variable first which then can be accessed using the bracket operator. 

```python
speed: tuple = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed[0], speed[1])
```

The bracket operator takes in an index which starts from 0. This means that to access the first output, you use index 0. On the other hand, to access the second output, you use index 1 and so on. 

You can access the code above in the file `05_speed_annotated.py` and run `mypy` to do static check on it. 

## Local Frame and Local Variables

At this point it is instructive to see the difference between a global and local variables as this may affect the way we define our functions. Let's run the above functions on Python Tutor.

<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adef%20calculate_speed%28diameter%3A%20float,%20tire_size%3A%20float,%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int,%20cog%3A%20int,%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cadence%3A%20int%29%20-%3E%20Speed%3A%0A%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmph%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmph,%20speed_mph%0A%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%28685.8,%2038.1,%2050,%2014,%2025%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


We have added the function call and the print statement at the end of the code. We have also removed the docstring to shorten the code. At the same time, we created an Alias to define the type of the return value of the function.

```python
Speed = tuple[float, float]
```

We can then define `Speed` as a tuple that consists of two float values. We then use this `Speed` to annotate the return value of the function. 

```python
def calculate_speed(diameter: float, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> Speed:
```

Since `speed` is a tuple, we can access the elements using the square bracket operators. 

```python
speed: Speed = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed[0], speed[1])
```

Click the "Next" button a few times until the program counter reach line number 11, which is step 11 out of 13. 

At this point the image on the right hand side gives a snapshot of what is in the memory before the function exit and returns the two values. A few things which you need to take note. The first one is that there are **two frames** created. The first one is the **global** frame and the second one is the **calculate_speed** frame. The calculate speed frame is created when the function `calculate_speed` is called. This happens on step 6 of 13. You can click the "Prev" button to verify this. Go to step 5 and click "Next" to see when is the `calculate_speed` frame created. In essence the `calculate_speed` frame is a local frame which is called when the function is *invoked* or *executed*. Every function invocation creates a new frame. 

At step 7, the program counter is at the first line of the code in function `calculate_speed`. At this point, the local frame has been populated by the input arguments: `diameter`, `tire_size`, `chainring`, `cog` and `cadence`. When you execute line 6 to arrive at Step 8, a new **local** variable is created, which is `gear_ratio`. When this local variable is created, several things happens:
- Python tries to evaluate the value of the expression on the right.
- On the right hand side of the assignment operator (`=`), Python sees the operator `/` and understood it as a division. Since this is a *binary* operator it requires two operands.
- Python found two **names** for the operands of `/`: `chainring` and `cog`. Python tries to see if these names are any of the built-in names or keywords.
- Since Python cannot find any of these names in its built-in functions or keywords, Python looks into the **local frame**. At this point, Python finds the two names and *evaluates* the values.
- Once Python obtains the two values for the operands, Python executes the division operation on the two operands and assign it to the name on the left hand side of the assignment operators, i.e. `gear_ratio`. 

In subsequent lines, Python does similar things to create several other *local variables*: `speed`, `speed_kmph` and `speed_mph`. 

Those are called **local variables** because they are local to the functin and are **not accessible** anywhere else. To see this, make sure your program counter is back at line 11 or Step 11 of 13. Click "Next" two times to exit the function. Notice that now there is only one single frame, which is the *global* frame. The local frame of `calculate_speed` has been destroyed. Since this frame is destroyed none of those local variables are accessible when we exit the function. 

## Global Variable

Now, you may realise that most of the arguments in the function calculate_speed will not change if the bicycle remains the same. Most of these are parameters specific to the user’s bicycle. As long as the user does not change the bicycle, those parameters will remain constant. Do we need to repeatedly enter those numbers, such as the diameter and the tyre size, each time we calculate the speed for a given cadence? The answer is no.

In this section, we will explore two alternatives: using global variables and optional arguments. We will discuss their respective advantages and disadvantages. In future lessons, we will introduce additional approaches, such as creating custom data types using object-oriented programming. Object-oriented programming allows you to package the bicycle's information as a single unit of data.

Let us start by using global variables. Since these parameters rarely change, we can treat them as constants and define them outside of the functions. This way, all functions we create can access these constants. How do we achieve this? Have a look at the following code in Python Tutor.



<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adiameter%3A%20float%20%3D%20685.8%0Atire_size%3A%20float%20%3D%2038.1%0Achainring%3A%20int%20%3D%2050%0Acog%3A%20int%20%3D%2014%0A%0Adef%20calculate_speed%28cadence%3A%20int%29%20-%3E%20Speed%3A%0A%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmph%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmph,%20speed_mph%0A%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%2825%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


In the code above, we define all the constants in the first few lines of the code, followed by the function definition. Notice that the function definition now takes only cadence as the input argument. During function invocation, we only provide one actual argument—cadence, which in this case is 25. How does the function calculate_speed obtain the values of the constants? Click the "Next" button until you reach the first line inside the function calculate_speed, i.e., Step 11 of 17.

Observe the environment diagram on the right-hand side. As expected, when we execute a function, Python creates a local frame for that function. Here, we see there is one local variable, which comes from the input argument: cadence. However, note that the global frame has more names associated with it. This time, we not only have math, but also diameter, tire_size, chainring, and cog. Additionally, the name calculate_speed is present because Python needs to know how to execute this function.

Now, let us examine what happens when we execute line 13:

At line 13, when we execute gear_ratio = chainring / cog, Python recognises that this is an assignment due to the assignment operator, =. Consequently, Python attempts to evaluate the right-hand side of the expression.
On the right-hand side, Python sees the binary operator / and identifies two operands with the names chainring and cog.
Python checks what these names represent. Since these names are not built-in functions or keywords, Python looks in the local frame. However, it does not find chainring or cog in the local frame.
Since Python cannot locate these names in the *local frame*, it moves **up** one level to the **previous** frame. This happens to be the *global* frame. At this point, Python finds the names and retrieves their values, evaluates the expression, and executes the division operation.

- The result is assigned to a new name `gear_ratio` which is part of the *local* frame.

Click Next to see how the environment change in the local frame. 

Similar things happens when we execute line 14 to calculate the `speed`. This time, Python gets the value for `diameter`, `tire_size` from the *global* frame. On the other hand, Python gets the value of `gear_ratio` and `cadence` from the local frame. You may not noticed that actually in this expression, we access the constant `math.pi` even in our earlier version of the code. If you observe carefully, the name `math` is located in the global frame. This is because our `import math` statement is outside of the function. Any code outside of any function is executed in the global frame. This is also the reason why we import the name `math` in the global frame. The reason is that more than one functions may make use of the math functions and constants. If we import the library `math` inside of each function, we have to do multiple import. 

## Variable Shadowing

What happens if you have the same name both in the local and in the global variable? In this case, the name in the local frame takes precedence and you will not be able to access the global variable. Let's look at a simple example to illustrate this. Let's create a variable `diameter` inside the function with some specific constant value.

<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adiameter%3A%20float%20%3D%20685.8%0Atire_size%3A%20float%20%3D%2038.1%0Achainring%3A%20int%20%3D%2050%0Acog%3A%20int%20%3D%2014%0A%0Adef%20calculate_speed%28cadence%3A%20int%29%20-%3E%20Speed%3A%0A%20%20chainring%3A%20int%20%3D%200%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmph%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmph,%20speed_mph%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%2825%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, we have two variables named chainring. The first one is located at line 8, outside of the function, and is in the global frame. The second one appears at line 12, inside the function, and is in the local frame. When you run the code and execute line 12 (Step 11 of 18), you'll notice that the value of gear_ratio is 0.0. This is because Python takes the value of chainring from the local frame instead of the global frame. In the environment diagram, you can observe that the value of chainring in the local frame is 0. This is why we say the local variable shadows the global variable when they share the same name.

If you proceed to the final step and observe the global frame, you'll see that the value of chainring remains at 50. The value in the global frame does not change when a new definition of chainring is created in the local frame. If you want to modify the global frame variable's value, you can use the global keyword inside the function definition. However, modifying a global variable from inside a function introduces a side effect. This can make it difficult for programmers to debug, as the value can be altered from any function, making it hard to pinpoint where or how the value was modified.

The best practice for modifying a global variable is to return the output from the function and then assign it back to the global variable.

In summary, you should avoid using global variables to modify information. If you need to pass data into a function, do so through input arguments. If you need the function to modify variables, modify them by assigning the output of the function back to the variable. In short, strive for no side effects in your functions as much as possible. Side effects make it harder to debug your code. By using input arguments and return values, you can clearly track the data coming in and out of the functions, which makes the code easier to debug.


## Defining Functions with Optional Arguments

The other alternative instead of using a global variable is to use optional arguments with default values. Python allows some arguments to be optional, which means that you do not need to supply the actual argument during the function call. However, to ensure that the function can still compute the output, you need to provide the default values for these optional arguments. To declare optional arguments, you just need to use the assignment operators in the function header and provide its default values. Let's use it for our `calculate_speed()` function.

```python
import math

Speed = tuple[float, float]

def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> Speed:
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmph: float = speed * 60 / 1_000_000
  speed_mph: float = speed * 60 / 1.609e6
  return speed_kmph, speed_mph
```

In the above function, note that we provided the default values for `diameter`, `tire_size`, `chainring` and `cog`. Because Python has values for these arguments, if there are no actual arguments provided, Python will use these default values to compute. Thus, you can call this function as follows.

```python
speed: Speed = calculate_speed(25)
```

In the case if any of the bicycle parameters change, you can modify the value using the argument name as the keyword. For example, if the `chainring` is 56 instead of 50, you can call the function as follows.

```python
speed: Speed = calculate_speed(25, chainring=56)
```

In the code, we follow PEP8 guidelines by avoiding spaces in keyword arguments. However, notice that you no longer need to follow the sequence of arguments when providing values for them. Python will match the argument names automatically. This also means that optional arguments must appear after compulsory arguments in the function definition.

In our case, we've changed the order of the arguments by placing cadence as the first argument in the function definition. This is necessary because Python assigns actual arguments based on their position in the function header. For example, when we pass 25 as the first argument, Python will assign it to cadence.

On the other hand, since the rest of the arguments are optional, they don't need to be supplied with actual values. You can only provide values for the arguments that differ from their default values. However, since Python can't determine which optional arguments you're supplying, you need to specify their names. This is why they are also called keyword arguments.



## Identifying Input, Output and Process of a Problem

We have discussed how to create our own function in this section. We also say that function is one way we can abstract our computation. In our previous lessons, we mentioned that we can use PCDIT framework to solve problems, design our algorithms and implement it. In the first part of this framework, we need to state the Problem Statement, i.e. P step. We can actually apply PCDIT for every function that we design. 

In the example above, we first ask what is the input to the `calculate_speed` function? We identify a few input:
- `cadence`
- `diameter`
- `tire_size`
- `chainring`
- and `cog`

It is also important to ask what kind of data are these inputs? We then identify:
- `cadence` to be an int
- `diameter` to be a float
- `tire_size` to be a float
- `chainring` and `cog` to be an int

After identifying the input, we also need to identify the output of the problem and in this case is the output of the function. In our `calculate_speed()` function, the output is the speed. However, we actually output two values, one in km/h and the other one in mph. So the kind of output is a tuple of two numbers. We should expect that these two numbers are floats instead of just integers. 

The last part is to identify the computation process of the function. In our case, it is the math equation to calculate speed from the those input arguments. 

$$\text{speed} = \pi \times \left(\text{diameter} + (2 \times \text{tire\_size})\right) \times (\text{chainring}/\text{cog}) \times \text{cadence}$$

So we have identified:
- input
- output
- process

This completes our Problem Statement step. This step must be done at the beginning and we can revise or revisit it again as we move on to the following steps. 

We have put this PCDIT framework discussion at the end instead of the beginning as a kind of reflection how we arrive at the final function. In actual practice, we should do our **P**roblem Statement formulation before we write down any **I**mplementation. 

Let's relook at the problem again. Instead of returning a tuple, let's state that our function only return the speed in km/h. We can then think of another computation that converts speed in km/h to speed in mph. In this new function, let's identify the input, output and the computation process.

The input to this function is speed in km/h. We should then ask, "What kind of data is this?". We can get a hint from our `calculate_speed()` function and note that it is a float data. Similarly, the output is the speed in mph and it is a float data as well. How about the computation process then? Approximately, you can get speed in mph from km/h using by using the following:

$$\text{speed}_{mph} = \text{speed}_{kmph} \times 0.621371192 $$

Now, we have our **P**roblem Statement. We have identified the input, output, and computation process. We can then translate these information into our function defnition. Since the problem is simple enough, we will skip the **C**oncrete Cases and the **D**esign of Algorithm steps. 

```python
def convert_kmph_to_mph(speed_kmph: float) -> float:
  return speed_kmph * 0.621371192
```

We can then test this function by putting in the actual argument in the function call.

```python
speed_mph: float = convert_kmph_to_mph(12.82)
print(speed_mph)
```

You will get about 7.97 mph which is what you saw previously in the second output of `calculate_speed()`. Now, our `calculate_speed()` need not return two values but only the speed in km/h. Let's modify our function again.

```python
import math
def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> float:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    cadence (int): Cadence in rpm.
    diameter (float): Diameter of the wheel in mm. Default value = 685.8 mm.
    tire_size (float): Size of tire in mm. Default value = 38.1 mm.
    chainring (int): Teeth of the front gears. Default value = 50.
    cog (int): Teeth of the rear gears. Default value = 14.

  Returns:
    speed_kmph (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmph: float = speed * 60 / 1_000_000
  return speed_kmph 

def convert_kmph_to_mph(speed_kmph: float) -> float:
  '''
  Calculates the speed in mph from the speed in km/h.

  Parameters:
    speed_kmph (float): speed in km/h

  Returns:
    speed_mph (float): speed in mph
  '''
  return speed_kmph * 0.621371192
```

We can then use these two functions as follows.

```python
speed_kmph: float = calculate_speed(25)
speed_mph: float = convert_kmph_to_mph(speed_kmph)
```

If we are just interested in the speed in mph, we can combine the above code into a single line of code.

```python
speed_mph: float = convert_kmph_to_mph(calculate_speed(25))
print(speed_mph)
```

// insert diagram

Notice that Python first executes the inner function `calculate_speed(25)` and evaluates the return value. This return value is used as an input argument for `convert_kmph_to_mph()` function. See diagram above.

You can run the file `06_speed_convert.py` with `mypy` to check if the code passes the static check. 

```sh
$ mypy 06_speed_convert.py  
Success: no issues found in 1 source file
```

To actually run the code as a script. Execute the following.

```sh
$ python 06_speed_convert.py 
7.968731362596021
```

## Summary


Here’s a revised version with some grammar improvements and added clarity:

In this lesson, we have learned how to create our own user-defined functions. We learned how to declare a new function that takes input arguments and returns output values. We also continued to use type hinting to ensure that our code is well-structured and easy to debug.

A function can be thought of as a small unit of computation, and we can abstract these computation units as separate functions. We have shown how we can solve the same problem in a few different ways. In all these cases, we follow the PCDIT framework, primarily focusing on the Problem Statement, identifying the input and output, and the computational process. As our code becomes more complicated, we will use the other steps of the PCDIT framework as well.

Another important point is the concept of global and local variables. A local variable only exists within the context of the function when it is executed and resides in the local frame. On the other hand, a global variable is accessible from all frames. However, if there is a variable with the same name as a global variable, it will shadow the global variable. A function always accesses the local frame first before searching the global frame.

We also introduced the use of optional arguments in our function definitions. In this case, our function can be made simpler. Additionally, we showed how we can chain function calls and pass the output of one function as the input to another function.
