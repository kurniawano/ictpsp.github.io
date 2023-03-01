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

Since the input arguments are all in mm and the cadence is in rotation per *minute*, the variable `speed` has a unit  of mm/min. In order to change this unit to km/h, we multiply by 60 (to convert from minute to hour) and divide by 1,000,000 (to convert from mm to km). Notice that we expect the `gear_ratio` to be a float after dividing `chainring` by `cog`. Similarly, `speed` is expected to be a `float`. 

The nice thing about Python docstring is that we can access this documentation. To do that, type in the above code into the Python shell and press enter for Python to execute the function definition. In order to access the documentation, you can type `calculate_speed.__doc__`. 

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
def calculate_speed(diameter: float, tire_size: float, 
                    chainring: int, cog: int, 
                    cadence: int) -> Tuple[float, float]:
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
      speed_kmh (float): cycling speed in km/h 
      speed_mph (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmh: float = speed * 60 / 1_000_000
  speed_mph: float = speed * 60 / 1.609e6
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

## Local Frame and Local Variables

At this point it is instructive to see the difference between a global and local variables as this may affect the way we define our functions. Let's run the above functions on Python Tutor.

<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adef%20calculate_speed%28diameter%3A%20float,%20tire_size%3A%20float,%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int,%20cog%3A%20int,%20%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cadence%3A%20int%29%20-%3E%20Speed%3A%0A%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmh%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmh,%20speed_mph%0A%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%28685.8,%2038.1,%2050,%2014,%2025%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


We have added the function call and the print statement at the end of the code. We have also removed the docstring to shorten the code. At the same time, we created an Alias to define the type of the return value of the function.

```python
Speed = Tuple[float, float]
```
In order to use `Tuple[float, float]`, we need to import the name `Tuple` from `typing` library. This makes `Tuple` available in your environment for type hinting. 

```python
from typing import Tuple
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

In subsequent lines, Python does similar things to create several other *local variables*: `speed`, `speed_kmh` and `speed_mph`. 

Those are called **local variables** because they are local to the functin and are **not accessible** anywhere else. To see this, make sure your program counter is back at line 11 or Step 11 of 13. Click "Next" two times to exit the function. Notice that now there is only one single frame, which is the *global* frame. The local frame of `calculate_speed` has been destroyed. Since this frame is destroyed none of those local variables are accessible when we exit the function. 

## Global Variable

Now, you may realize that most of the arguments in the function `calculate_speed` will not change if the bicycle remains the same. Most of these are parameters of the bicycle of the users. As long as the user does not change the bicycle, those parameters will not change. Do we need to keep on entering those numbers such as the diameters and the tire size again every time we want to calculate the speed for a given cadence? The answer is no. In this section we will show two alternatives which uses the global variable and optional arguments. We will discuss its advantage and disadvantage. In the future lessons, we will show some other alternatives such as using your own custom data type through object oriented programming. Object oriented programming will allow you to pass on the bicycle information as one single data.  

Let's start with using the global variables. Since these parameters never (or seldom) change, we may put all these values as a kind of constants and define it outside of the functions. In this way, all these constants are readable by all the functions that we create. How to do this? Let's see the code below in Python Tutor.

<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adiameter%3A%20float%20%3D%20685.8%0Atire_size%3A%20float%20%3D%2038.1%0Achainring%3A%20int%20%3D%2050%0Acog%3A%20int%20%3D%2014%0A%0Adef%20calculate_speed%28cadence%3A%20int%29%20-%3E%20Speed%3A%0A%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmh%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmh,%20speed_mph%0A%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%2825%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


In the code above, we define all the constants the first few lines of the code followed by the function definition. Notice that now the functin definition only takes in `cadence` as the input argument. During function invocation, we also only provide one actual argument, which is for the cadence, i.e. 25. How does the function `calculate_speed` obtains the values from the constants? Click "Next" button until you reach the first line inside the function `calculate_speed`, i.e. Step 11 of 17.

Notice the environment diagram on the right hand side. As expected, when we execute a functin, Python will create a local frame for that function. Here we see there is one local variable which comes from the input argument, i.e. `cadence`. However, note that the global frame has more names associated with it. This time, we not only have `math` but also `diameter`, `tire_size`, `chainring` and `cog`. We also have the name `calculate_speed` (Python needs to know how to execute this function). 

Let's see what happens when you execute line 13:
- At line 13, when we execute `gear_ratio = chainring / cog`, Python recognizes that you are doing assignment from the assignment operator, i.e. `=`. Because of this, Python tries to evaluate the right hand side of the expression.
- At the right hand side, Python sees the binary operator `/` and found two operands with two names `chainring` and `cog`. 
- Python tries to find what these names are. Python cannot find these names in its built-in functions or keywords and so Python check the *local frame*. However, Python cannot find these two names in the local frame as well.
- Since Python, cannot find the names in the local frame, Python goes **up** one level to the **previous** frame. This is the frame where the function `calculate_speed` is called. It happens that this is the same as the *global* frame. At this point, Python finds the two names and evaluates the values and execute the binary operator to perform division. 
- The result is assigned to a new name `gear_ratio` which is part of the *local* frame.

Click Next to see how the environment change in the local frame. 

Similar things happens when we execute line 14 to calculate the `speed`. This time, Python gets the value for `diameter`, `tire_size` from the *global* frame. On the other hand, Python gets the value of `gear_ratio` and `cadence` from the local frame. You may not noticed that actually in this expression, we access the constant `math.pi` even in our earlier version of the code. If you observe carefully, the name `math` is located in the global frame. This is because our `import math` statement is outside of the function. Any code outside of any function is executed in the global frame. This is also the reason why we import the name `math` in the global frame. The reason is that more than one functions may make use of the math functions and constants. If we import the library `math` inside of each function, we have to do multiple import. 

## Variable Shadowing

What happens if you have the same name both in the local and in the global variable? In this case, the name in the local frame takes precedence and you will not be able to access the global variable. Let's look at a simple example to illustrate this. Let's create a variable `diameter` inside the function with some specific constant value.

<iframe width="800" height="700" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Afrom%20typing%20import%20Tuple%0A%0ASpeed%20%3D%20Tuple%5Bfloat,%20float%5D%0A%0Adiameter%3A%20float%20%3D%20685.8%0Atire_size%3A%20float%20%3D%2038.1%0Achainring%3A%20int%20%3D%2050%0Acog%3A%20int%20%3D%2014%0A%0Adef%20calculate_speed%28cadence%3A%20int%29%20-%3E%20Speed%3A%0A%20%20chainring%3A%20int%20%3D%200%0A%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20speed_kmh%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20speed_mph%3A%20float%20%3D%20speed%20*%2060%20/%201.609e6%0A%20%20return%20speed_kmh,%20speed_mph%0A%0Aspeed%3A%20Speed%20%3D%20calculate_speed%2825%29%0Aprint%28speed%5B0%5D,%20speed%5B1%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, we have two variables with the name `chainring`. The first one is at line 8 which is outside of the function and is in the global frame while the second one is at line 12 which is inside the function and is in the local frame. When you run the code and execute line 12 (Step 11 of 18), you notice that now the gear_ratio is 0.0. The reason is that Python takes in the value of `chainring` from the local frame instead of the global frame. Notice in the environment diagram that the value of `chainring` in the local frame is 0. This is why we say that the local variable shadows the global variable when they have the same name. 

If you move the steps to the last step and observe the global frame, notice that the value of the `chainring` remains at 50. The value at the global frame does not change when we have a new definition with the same name in the local frame. If you want to modify the global frame variable's value, you can use the keyword `global` in Python inside the function definition. But modifying global variable from inside a function is creating a side effect. This will make it hard for programmers to debug as the value can be modified from any function and we will find a hard time where or how the value is modified. The best way to modify a value in the global variable is by returning the output of the function and assigning it back to the global variable. 

In summary, avoid using the global variable to modify information. If you want to pass on information to the function, pass it through the input arguments. On the other hand, if you want the function to modify some variables, modify by assigning the output of that function to that variable. In short, we want to have no side effects from a function as much as possible. Side effects make it hard for us to debug our code. On the other hand, if we use input arguments and return values, we know what data coming in and out of the functions and it will be easier to debug. 


## Defining Functions with Optional Arguments

The other alternative instead of using a global variable is to use optional arguments with default values. Python allows some arguments to be optional, which means that you do not need to supply the actual argument during the function call. However, to ensure that the function can still compute the output, you need to provide the default values for these optional arguments. To declare optional arguments, you just need to use the assignment operators in the function header and provide its default values. Let's use it for our `calculate_speed()` function.

```python
import math
from typing import Tuple 

Speed = Tuple[float, float]

def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> Speed:
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmh: float = speed * 60 / 1_000_000
  speed_mph: float = speed * 60 / 1.609e6
  return speed_kmh, speed_mph
```

In the above function, note that we provided the default values for `diameter`, `tire_size`, `chainring` and `cog`. Because Python has values for these arguments, if there are no actual arguments provided, Python will use these default values to compute. Thus, you can call this function as follows.

```python
speed: Speed = calculate_speed(25)
```

In the case if any of the bicycle parameters change, you can modify the value using the argument name as the keyword. For example, if the `chainring` is 56 instead of 50, you can call the function as follows.

```python
speed: Speed = calculate_speed(25, chainring=56)
```

Here we follow PEP8 guidelines of not putting space in the keyword arguments. But notice that you do not need to follow the sequence of the arguments anymore when you provide the name of the argument. Python will match the name of the arguments. This also implies that you can only put the optional arguments at the back of the compulsory arguments. Notice that we have change the sequence of the arguments by putting `cadence` to the first argument in our function definition. This is needed because for Python will supply the actual arguments based on its position in the function header. In our case, 25 is the first argument and Python will feed into the first argument in the function header, which is `cadence`. On the other hand, since the rest of the arguments are optionals, they need not be supplied with any actual arguments. You can supply only the arguments that you know is different from the default values. But now, Python does not know which optional arguments you are supplying, so in this case, you need to give the name of the argument. This why it is also called as keyword arguments. 

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