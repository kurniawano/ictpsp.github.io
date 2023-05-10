---
title: Tuple Data
permalink: /notes/tuple
key: notes-tuple
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

## What is a Tuple?

This lesson and the next focuses on data structure that is available in Python. More importantly, we will introduce you to collection-like data structure. In the previous lesson, we have been dealing with only basic data structure such as `int`, `float`, `bool` and `string`. When we are dealing with `string`, we noted that we can think of `string` as a sequence of characters. We can then process each character by iterating over the string. Computer is very efficient when working with this kind of data when it has do the same computation again and again. All programming languages have some ways to implement iterative structure as it is one of the ways that makes programming to be powerful. 

In this section and the next, we will begin to work with more collection-like data type. In this section, we will introduce `tuple`. On the other hand, the next section will deal with `list`. 

You may not realize it, but you have actually dealt with tuple when we discuss about function that returns multiple output. Let's put the function again here for us to recall.

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

Notice that the function returns two things, i.e. `speed_kmph` and `speed_mph`. Moreover, we actuall can store these two output into two different variables.

```python
speed_kmph, speed_mph = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed_kmph, speed_mph)
```

If you just assign it to a single variable, you can still access it using the square bracket and the index.

```python
speed = calculate_speed(685.8, 38.1, 50, 14, 25)
print(speed[0], speed[1])
```

In the code above, `speed` is of the type `tuple`. You can actually check by using the code below.

```python
print(type(speed))
```

It will output the following.

```python
<class 'tuple'>
```

In Python, a `tuple` is simply a collection of objects and it is immutable. In our example above, the return value of the function `calculate_speed()` is a collection of two floats. Tuple can consists of objects of different type. The one thing that differentiates it with `list` is that tuple is **immutable**. This means that you cannot modify the element of a tuple. 


## Creating a Tuple Data Type

We create a tuple simply by grouping them using a comma.

```python
>>> my_output = 12.8, 7.97
>>> print(my_output)
(12.8, 7.97)
>>> print(type(my_output))
<class 'tuple'>
```

The parenthesis is not a requirement, but often times, it is clearer if you put a parenthesis over the tuple.

```python
>>> my_output = (12.8, 7.97)
```

We can create a tuple made of objects of different data types as in the example below here.

```python
>>> various_types_tuple = 3, 3.14, '3.14', True
>>> print(various_types_tuple)
(3, 3.14, '3.14', True)
```

Once we know how to create tuple, now we can discuss on what we can do with tuple data type.

## Basic Operations with Tuple Data

The simplest basic operation of tuple data is to access its elements. We access element of a tuple in a similar way as we access a character from a string, i.e. using a square bracket (`[]`) or the get item operator.

```python
>>> various_types_tuple = 3, 3.14, '3.14', True
>>> print(various_types_tuple)
(3, 3.14, '3.14', True)
>>> various_types_tuple[0]
3
>>> various_types_tuple[-1]
True
```

In the code above, we access the first and the last element using index 0 and -1 respectively. You can also use slicing operator with tuple similar to string. This can be done using the square bracket operator with colon.

```python
>>> various_types_tuple
(3, 3.14, '3.14', True)
>>> various_types_tuple[1:]
(3.14, '3.14', True)
>>> various_types_tuple[2:]
('3.14', True)
```

In the above code, we slice the tuple from the second element (index 1) to the end and then from the third element (index 2) to the end. You can specify the ending and the step also in the slicing as in the example below.

```python
>>> various_types_tuple[1:-1:2]
(3.14,)
```

In the code above, we start from the second element (index 1) up to but not including the last element (index -1) with a step of 2. Since we only have four elements, the second element is 3.14 and the next element two steps away is already the last element. Since we do not include the last element, the slicing returns only one element in the tuple, i.e. `(3.14,)`. Notice that the output is still a tuple though there is only a single element. A single element tuple has a comma in it without any other element. 

Recall also that tuple is immutable and this is what differentiates a tuple with a list. Immutable simply means that you cannot change the element of a tuple. An exception will be thrown if you try to modify the value of a tuple.

```python
>>> various_types_tuple[0] = False
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>> various_types_tuple
(3, 3.14, '3.14', True)
```

In the code above, we tried to modify the value of the first element (index 0) from integer 3 to a boolean `False`. However, Python throws a `TypeError` exception saying that `tuple` object does not support item assignment. Basically it is saying that you cannot modify the element of a tuple. It is immutable.

Once you create a tuple, you cannot modify it. It has a fixed number of element and it will stay there. You can check the number of element using the `len()` function as usual.

```python
>>> various_types_tuple
(3, 3.14, '3.14', True)
>>> len(various_types_tuple)
4
```

In the above example, the tuple has four elements. Once the tuple is created, we cannot add or remove elements from the tuple. It is immutable. 

What if you really want to change the element of the tuple? You have two options. The first option is not to use tuple but rather a `list` data type. We will cover list in the next lesson. The second option is to create a new tuple. 

For example, if we want to remove the last element, what we can do is to slice the original tuple creating a new tuple with three elements only.

```python
>>> various_types_tuple
(3, 3.14, '3.14', True)
>>> new_tuple = various_types_tuple[:-1]
>>> new_tuple
(3, 3.14, '3.14')
```

We can join two tuples using the `+` operator. See example below.

```python
>>> various_types_tuple
(3, 3.14, '3.14', True)
>>> new_tuple
(3, 3.14, '3.14')
>>> joined_tuple = various_types_tuple + new_tuple
>>> joined_tuple
(3, 3.14, '3.14', True, 3, 3.14, '3.14')
```

We can use this slicing and joining to remove some of the elements in the tuple. For example, let's say we want to remove `True` from the `joined_tuple` variable. We can slice the left up to `True` and joined it with the other tuple starting from after `True`. Notice that `True` is at index 3. We can write the following code.

```python
>>> removed_bool_tuple = joined_tuple[:3] + joined_tuple[4:]
>>> removed_bool_tuple
(3, 3.14, '3.14', 3, 3.14, '3.14')
```

Similar to string, we can also duplicate the element of a tuple using the `*` operator.

```python
>>> new_tuple
(3, 3.14, '3.14')
>>> new_tuple * 3
(3, 3.14, '3.14', 3, 3.14, '3.14', 3, 3.14, '3.14')
```

Notice, however, that if we tend to modify the elements of our collection, it is better to use `list` instead of `tuple`. What is then the advantage of tuple over list? 
- Tuple, because it is immutable, has a better performance. Iterating over a tuple is faster than iterating over a list. 
- Tuple is immutable and so it is safer if you want to have a collection that should not be modified. Programs like `mypy` can help to check your code if you try to modify a tuple. 
- Lastly, tuple can be used as a dictionary keys because it is immutable. We will discuss about dictionary in the future lesson. One thing to note is that dictionary keys must be hashable and so it must be immutable. Since list is mutable, it cannot be used as dictionary keys. But we will come to this point again when we dicuss dictionary data type.

Just a simple example that `mypy` can check if we try to modify a tuple, you can run `mypy` on `01_modify_tuple.py`.

```python
various_types_tuple = 3, 3.14, '3.14', True
various_types_tuple[0] = False
```

and run in the shell.

```sh
$ mypy 01_modify_tuple.py 
01_modify_tuple.py:2: error: Unsupported target for indexed assignment ("Tuple[int, float, str, bool]")  [index]
Found 1 error in 1 file (checked 1 source file)
```

Notice that `mypy` detects an error when we try to assign to a tuple. We can use type annotation when declaring a tuple as follows. In the code below, we put all the basic operations with its type annotation when assigning to a new variable.

```python
from typing import Tuple

various_types_tuple:Tuple[int, float, str, bool] = 3, 3.14, '3.14', True
print(various_types_tuple)

# slicing a tuple
print(various_types_tuple[1:])
print(various_types_tuple[2:])
print(various_types_tuple[1:3])
print(various_types_tuple[1:-1:2])

# creating a new tuple using slicing and joining
new_tuple:Tuple[int, float, str] = various_types_tuple[:-1]
print(new_tuple)
print(various_types_tuple)
joined_tuple:Tuple[int, float, str, bool, int, float, str] = various_types_tuple + new_tuple
print(joined_tuple)
removed_bool_tuple:Tuple[int, float, str, int, float, str] = joined_tuple[:3] + joined_tuple[4:]
print(removed_bool_tuple)

# duplicating a tuple
print(new_tuple * 3)
```

When we run `mypy` on this file `02_tuple_basic_operations.py`, we have the following output.

```sh
$ mypy 02_tuple_basic_operations.py 
Success: no issues found in 1 source file
```

## Traversing a Tuple



