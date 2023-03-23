---
title: Basic Operators
permalink: /notes/basic-operators
key: notes-basic-operators
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

## Operators and Operands in Computation

In our previous lessons, we have done some simple computations. We first computed the cadence and then the speed based on the cadence and the bicycle parameters. In all these we use mathematical **operators** to do our computation. For example, to calculate the cadence from the number of steps, we had the following function definition.

```python
def compute_cadence_for_30sec(steps):
  return steps * 2
```

In the above function definition, we used the **multiplication** operators, i.e. `*`. Multiplication operator is an example of what we call as **binary operator**. The word binary refers to the number of the operands which in this case is two for the multiplication operator. This means that multiplication operator requires *two operands*, that is the left hand side number and the right hand side number which the operator will multiply. Python expects two operands and when there is a lack of operand, Python will throw an exception or an error as in the code below.

```python
>>> cadence = 2 *
  File "<stdin>", line 1
    cadence = 2 *
                ^
SyntaxError: invalid syntax
```

In the above code, the multiplication operator only has the left operand and it gives a `SyntaxError`. 

We can think of operator as another primitive abstraction concept of a computation. Recall that every computation may take in output and produce output. In this case, an operator takes in the operands as its input. Moreover, the operator is evaluated and produces an output value. Python evaluates the expression and produces a value.  For example, in the expression `steps * 2`, Python first evaluates the variable reference `steps` and get its value. This value and a literal integer of `2` are the operands. Python then evaluates the multiplication using these two operands as the input to the multiplication function. In this way, operators are convinient way of expression a computation as compared to having call a function such as the following.

```python
cadence = multiply(steps, 2)
```

Using the `*` multiplication operator is more expressive and readable for human. At the same time, you can still conceptually think operator as a primitive computational unit that takes in input and produces output. 

## Math and Assignment Operators

Python supports the common arithmetic operators as shown in the table below. We added the assignment operator together here in the last row to show that all the math operators will be evaluated first before it is being assigned.

| precedence | operator | remarks                                                                                                                        |
|------------|----------|--------------------------------------------------------------------------------------------------------------------------------|
| 0          |      ()  | Parenthesis is used to evaluate the inside expression to override the precedence of the surrounding operators.                 |
| 1          | **       | Power or exponentiation operator.                                                                                              |
| 2          | * / % // | Multiplication, division, modulus and integer division. They are evaluated from left to right when appearing in a single line. |
| 3          | + -      | Addition and subtraction.                                                                                                      |
| 4          | =        | Assignment operator.                                                                                                           |

You may be familiar with the common arithmetic operators such as:
- `+` for addition
- `-` for subtraction

These two are at the lowest precedence which means that they are evaluated last. Just as in normal arithmetic, the multiplication and division has higher precedence as compared to addition and subtraction.
- `*` for multiplication
- `/` for division

Starting from Python 3, Python uses `/` operator for *true division*. This means that division of two integer numbers results in a `float` data type.

```python
>>> 3 / 2
1.5
>>> 4 / 2
2.0
>>> 
```

Notice that even when `4` is divided by `2` which may output an int, Python `/` operator still outputs a float. If you want to have an *integer division*, you can use the `//` operator.
- `//` for integer division and to get a quotion of from a division
- `%` for modulus to get a remainder from a division

```python
>>> 3 // 2
1
>>> 3 % 2
1
>>> 4 // 2
2
>>> 4 % 2
0
```

Multiplication, division, integer division and modulus have the same precedence. When they appear, Python will evaluate them from left to right. 

Python also supports:
- `**` for power or exponentiation

```python
>>> 2 ** 3
8
```

The above computation gives the output of $2^3$. In the case of multiple exponentiation, they are evaluated from right to left. 

```python
>>> 2 ** 2 ** 3
256
>>> 2 ** (2 ** 3)
256
>>> (2 ** 2) ** 3
64
```

As the three codes above showed, when we have a multiple of  `**` operators, it will be evaluated from right to left. In this case, $2^{2^3}$ is evaluated as $2^8 = 256$ instead of $4^3 = 64$

Notice that we actually have used the parenthesis `()` to enforce our precedence. This can be used also for example, if we want to do the lower precedence operators such as addition and subtraction before multiplication or division. For example, to evaluate $(2+3)*4$, we use the parenthesis to evaluate the addition first.

```python
>>> (2 + 3) * 4
20
```

In the table above, we added the assignment operator `=` at the bottom of the table to show that all the previous operators are evaluated first and only at the last that the assignment operator will be executed. 

```python
>>> x = (2 + 3) * 4
```

In the above code, first the parenthesis will enforce the addition operator to be executed first. Second, the multiplication operator will be evaluated. On then, the assignment operator will be executed. 

Assignment operator is also a binary operator but it does different thing to the left and the right hand side of the operator. Python evaluates the *right hand side* of the assignment operators and bind the value to the name in the *left hand side* of the assignment operator. This direction cannot be interchanged. The followign code gives an error in Python.

```python
>>> (2 + 3) * 4 = x
  File "<stdin>", line 1
SyntaxError: cannot assign to operator
```

Python only allows assignment to *names*. 

## Compound Operators

Python also supports some compound operators. The reason is that certain operators are pretty common and it is convenient to write a shorter expression of it. For example, in an iterative structure, we commonly have a counter that we increase. The following computation is common in iterative structure.

```python
x = x + 1
```

The above expression simply adds the value of `x` by `1` and assign it back to the variable `x`. Remember that the right hand side of the assignment operator will be evaluated first, which in this case is `x + 1`. The assignment operator assign the value produced in the right hand side to the name in the left hand side.

Since the above expression is so common, Python provides a shorter version of it.

```python
x += 1
```

You can try the following code.

```python
>>> x = 0
>>> x = x + 1
>>> x += 2
>>> x
3
```
In the above code, the value of `x` was 0 initially. It was then increment by `1` using the `+` operator and increment another time by `2` using the compound `+=` operator. At the end, the value of `x` is `3`. 

Python has several other compound operators for the various math operators: 
- `x -= 3` is the same as `x = x - 3`
- `x *= 3` is the same as `x = x * 3`
- `x /= 3` is the same as `x = x / 3`
- `x //= 3` is the same as `x = x // 3`
- `x %= 3` is the same as `x = x % 3`
- `x **= 3` is the same as `x = x ** 3`

In all these compound operators, the right hand side can be any other Python's expressions. For example, you can have something like the following.

```python
x += calculate_speed(25)
```

In the above code, the right hand side is a function call to `calculate_speed()`. 


## String Operators

We have discussed how we can use some of the common arithmetic operators to do mathematical computations. These are done mainly on numeric data such as `int` and `float`. The other basic data type is `string`. String data type have their own unique operations and yet they may use a similar symbol for its operators. Let's look at some of them.

In arithmetic, a `+` operator is used for addition of two numbers. In string data, however, it is used to **concatenate** or join two strings. 

```python
>>> str1 = "Hello"
>>> str2 = "World"
>>> combined = str1 + str2
>>> print(combined)
HelloWorld
```

Notice that the same operator `+` behaves differently depending on the data type. This is one of the main reason is important for us to ask, "What kind of data is this?". What happens if we try to add two different kinds of data like a string and a number? 

```python
>>> "Hello" + 2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate str (not "int") to str
```

The error says that we can only concatenate string to string and not to an integer. It is important, therefore, to know what kind of data we are working on to ensure that we do the right computation. 

Some string operators actually can work with numeric data. An example of this is the `*` operator. In arithmetic, this operator is used for multiplication. In a string data, however, it is used to duplicate and join the string together. 

```python
>>> "Hello" * 3
'HelloHelloHello'
```

This operator `*` in fact requires one of the operand to be an integer. It won't work if we use either `float` or another `str`.

```python
>>> "Hello" * 3.5
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can't multiply sequence by non-int of type 'float'
>>> "Hello" * "a"
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can't multiply sequence by non-int of type 'str
```

Some string operations are totally different from arithmetic comptutations. We will go through some string operations in future lessons. 

## Testing and Debugging using Print Statement

As we introduce more things into our code, it is best to start the habit of **debugging** our code. No programmers can ever written a code without debugging it (Okay, maybe we can write a print Hello World code without debugging it). Most code as it grows in complexity requires programmers to test its code and check whether the code runs as what it is expected it to do. Instead of testing the code at the end of writing a long lines of code, programmers do test their code in bite-size. 

In this section, we want to introduce a little habit which should be part and puzzle of every novice programmers when writing code. This habit is to test their code after one or few lines of code to see whether it performs what it is expected to do. One simple way is to use the `print()` function to test two things:
- the expected value of computation
- the data type of some value

Let's revisit our `calculate_speed()` function. We will put here the final version, but we will describe how a novice programmers can write it step by step with the print statement to test it. 


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
    speed_kmh (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmh: float = speed * 60 / 1_000_000
  return speed_kmh 
```

So how do we start writing the above code and test it step by step. The *first step* is to write the functin header and immediately create a function call with some actual arguments. In our PCDIT framework, the **C**oncrete Cases can provide some of the actual arguments to be used. In our example, we can start with the following code.

```python
def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> float:
    pass

print(calculate_speed(25))
# print(calculate_speed(25, 600, 30, chainring=60, cog=16))
# print(calculate_speed(25, diameter=600, tire_size=30, chainring=60, cog=16))
# print(calculate_speed(25, diameter=600))
```

We have written down our function header starting from the `def` keyword using the information that we have from our **P**roblem Statement step. In this step, we know what are our input to our computations and we know the output. We also ask what kind of data they are, both for the input and the output. 

Outside of the function definition, we have four (4) function calls to test different way the function may be called. We can write more, but for simplicity we only list four of them here. 

```python
print(calculate_speed(25))
```

This function call test if we supply the required input argument for `cadence` and use the default values for the rest of the input arguments.

```python
# print(calculate_speed(25, 600, 30, chainring=60, cog=16))
# print(calculate_speed(25, diameter=600, tire_size=30, chainring=60, cog=16))
# print(calculate_speed(25, diameter=600))
```

In these few other function calls, we put comments  for subsequent tests. But we will start with that first one call first to test. We have also put Python keywords `pass` as the body of the function. This keyword does not do anything but it is useful when we want to leave the body of the function empty. Without putting this keyword, the functin will give an error. The error is caused because Python expect some indented code after the function header. In fact, after every statement that ends with the colon `:`, it expects some indented block. 

We can save the above code into a file `01_calculate_speed_1.py` and run both `mypy` and `python`.

```sh
$ mypy 01_calculate_speed_1.py 
01_calculate_speed_1.py:1: error: Missing return statement  [empty-body]
Found 1 error in 1 file (checked 1 source file)
```

In this first run of `mypy`, it detects that our function has a `float` output from the functin header but we do not have any `return` statement. So it throws an error. This is a good reminder. Let's fix our code to return something and run `mypy` again.

```python
def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> float:
   return speed 

print(calculate_speed(25))
```

In the above code, we have removed the other function calls for simplicity but we added the `return speed`. The output of running `mypy` on the above code is shown below.

```sh
$ mypy 02_calculate_speed_2.py 
02_calculate_speed_2.py:6: error: Name "speed" is not defined  [name-defined]
Found 1 error in 1 file (checked 1 source file)
```

Now, `mypy` complains that `speed` has not been defined. Python simply doesn't know what `speed` is. To fix this, we can tell Python that `speed` is our output variable, but since, we have not done any computation yet, we can assign it to `0.0` object for now.

```sh
$ mypy 03_calculate_speed_3.py
Success: no issues found in 1 source file
```

Now `mypy` has no complain. Notice that we assign `speed` to `0.0` instead of `0`. You can try assigning it to `0` but `mypy` will complain that the output is expected to be a `float` instead of an `int`. Anyway, we will compute `speed` and hopefully it will be `float` data at the end.

So now, we can run `python` to execute the code. Python will register the function definition and do a function call. However, it will currently output `0.0`. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20calculate_speed%28cadence%3A%20int,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20diameter%3A%20float%20%3D%20685.8,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20tire_size%3A%20float%20%3D%2038.1,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int%20%3D%2050,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cog%3A%20int%20%3D%2014%29%20-%3E%20float%3A%0A%20%20%20%20speed%20%3D%200.0%0A%20%20%20%20return%20speed%0A%0Aprint%28calculate_speed%2825%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Now, we can start writing our code. One of the useful thing to do is actually to check that you have the input you expected it. So we can start using our `print()` function to test this. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20calculate_speed%28cadence%3A%20int,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20diameter%3A%20float%20%3D%20685.8,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20tire_size%3A%20float%20%3D%2038.1,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int%20%3D%2050,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cog%3A%20int%20%3D%2014%29%20-%3E%20float%3A%0A%20%20%20%20speed%20%3D%200.0%0A%20%20%20%20print%28cadence%29%0A%20%20%20%20print%28type%28cadence%29%29%0A%20%20%20%20return%20speed%0A%0Aprint%28calculate_speed%2825%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the code above, we print both the value of `cadence` and its type. If you annotate your input arguments, this may not be necessary as `mypy` would have checked that for you. However, type annotation is optional in Python and we just want to show you that it is useful to check the type of your input as well. You can also print all the other values of the input arguments such as `diameter`, `tire_size`, etc. 

Now, we can calculate the gear ratio from the given `chainring` and `cog`. Let's add the code and print the values.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20calculate_speed%28cadence%3A%20int,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20diameter%3A%20float%20%3D%20685.8,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20tire_size%3A%20float%20%3D%2038.1,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int%20%3D%2050,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cog%3A%20int%20%3D%2014%29%20-%3E%20float%3A%0A%20%20%20%20speed%20%3D%200.0%0A%20%20%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20%20%20print%28gear_ratio,%20type%28gear_ratio%29%29%0A%20%20%20%20return%20speed%0A%0Aprint%28calculate_speed%2825%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We printed both the value and the type. Since we expected the value of the gear ratio to be a float, we added a type annotation for `gear_ratio` as `float`. The output is given as shown below.

```sh
3.5714285714285716 <class 'float'>
0.0
```
The first line comes from the print statement for the `gear_ratio`. The second line comes from the print statement in line 11 which is the output of the function call `calculate_speed(25)`. Recall that `speed` is still assigned to `0.0`. Notice also that we have removed the print statement for the `speed`. These print statements are used for us to quickly test our code and we can always remove it when it is not neeeded.

Now, we are ready to calculate the speed. Let's put in the expression using the mathematical operators we have discussed. 

```python
def calculate_speed(cadence: int,
                    diameter: float = 685.8,
                    tire_size: float = 38.1,
                    chainring: int = 50,
                    cog: int = 14) -> float:
    speed = 0.0
    gear_ratio: float = chainring / cog
    speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
    print(speed)
    return speed

print(calculate_speed(25))
```

This is what happens when we run `mypy`.

```sh
$ mypy 04_calculate_speed_4.py 
04_calculate_speed_4.py:8: error: Name "speed" already defined on line 6  [no-redef]
04_calculate_speed_4.py:8: error: Name "math" is not defined  [name-defined]
Found 2 errors in 1 file (checked 1 source file)
```

There are two issues here. 
- The first one is that the name `speed` is defined two times. There is nothing wrong in Python to redefine a variable name, but it is best to keep the definition to be the same. Otherwise, it will be hard to debug our code if the value or its type can change over the execution of the code.
- The second error is that `math` is not defined. Python does know what `math` is and so we can simply fix it by importing the `math` library. This happens because we make use of the `math.pi` constant in our equation.

To fix it, let's remove `speed = 0.0` and import `math` to our code.

```python
import math
def calculate_speed(cadence: int,
                    diameter: float = 685.8,
                    tire_size: float = 38.1,
                    chainring: int = 50,
                    cog: int = 14) -> float:
    
    gear_ratio: float = chainring / cog
    speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
    print(speed)
    return speed

print(calculate_speed(25))
```

Now, `mypy` will report no errors.

```sh
$ mypy 05_calculate_speed_5.py 
Success: no issues found in 1 source file
```

The output when running `python` is as follows.

```sh
python 05_calculate_speed_5.py 
213740.50018173413
213740.50018173413
```

Now we got two values that are the same because we have two print statements. The first print statement is inside the function definition which is just before the `return` statement. The second print statement is in the function call at line 14. You can also run the code in this Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Adef%20calculate_speed%28cadence%3A%20int,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20diameter%3A%20float%20%3D%20685.8,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20tire_size%3A%20float%20%3D%2038.1,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int%20%3D%2050,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cog%3A%20int%20%3D%2014%29%20-%3E%20float%3A%0A%20%20%20%20%0A%20%20%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20%20%20print%28speed%29%0A%20%20%20%20return%20speed%0A%0Aprint%28calculate_speed%2825%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

But this is not the value that we expected. We expected the speed to be about 12.8 km/h. The reason is that the units are wrong. This is why it is useful to print the value value of our computation. Though there are no longer syntactical errors, our code may not produce the correct output. To convert to km/h, we can add the conversion calculation. 

```python
import math
def calculate_speed(cadence: int,
                    diameter: float = 685.8,
                    tire_size: float = 38.1,
                    chainring: int = 50,
                    cog: int = 14) -> float:
    
    gear_ratio: float = chainring / cog
    speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
    speed_kmh: float = speed * 60 / 1_000_000
    print(speed_kmh)
    return speed

print(calculate_speed(25))
```

In this code, we replaced printing `speed` to printing `speed_kmh` which is our speed in km/h. Running this code using `mypy` produces no errors.

```sh
$ mypy 06_calculate_speed_6.py 
Success: no issues found in 1 source file
```

However, it produces two outputs.

```sh
$ python 06_calculate_speed_6.py 
12.824430010904047
213740.50018173413
```

The reason is that the return value still returning `speed` instead of `speed_kmh`. We can fix this by changing the return variable to `speed_kmh`. 

```python
```

Now, we get the output that we expected.

```sh
$ mypy 06_calculate_speed_6.py 
Success: no issues found in 1 source file

$ python 06_calculate_speed_6.py 
12.824430010904047
```

You can also run in in Python Tutor below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20math%0Adef%20calculate_speed%28cadence%3A%20int,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20diameter%3A%20float%20%3D%20685.8,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20tire_size%3A%20float%20%3D%2038.1,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20chainring%3A%20int%20%3D%2050,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20cog%3A%20int%20%3D%2014%29%20-%3E%20float%3A%0A%20%20%20%20%0A%20%20%20%20gear_ratio%3A%20float%20%3D%20chainring%20/%20cog%0A%20%20%20%20speed%3A%20float%20%3D%20math.pi%20*%20%28diameter%20%2B%20%282%20*%20tire_size%29%29%20%5C%0A%20%20%20%20%20%20%20%20%20%20*%20gear_ratio%20*%20cadence%0A%20%20%20%20speed_kmh%3A%20float%20%3D%20speed%20*%2060%20/%201_000_000%0A%20%20%20%20return%20speed_kmh%0A%0Aprint%28calculate_speed%2825%29%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Previously, we have commented the other function calls with different values of input arguments. You can remove the comment now and test. You may need to calculate it using your calculator just to make sure that it outputs the right speed using the equation when the input arguments are different.

We will show how to test for the various input arguments and using the `assert` statement in future lessons. For now, we just want to show that you can use `print()` statement in stages to test your code in bite-size and ensure that it produces what you expected. We have made use of `mypy` as well to do some of the checking on our behalf. 