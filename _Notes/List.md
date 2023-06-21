---
title: List
permalink: /notes/list
key: notes-list
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

## What is List?
In the previous lesson, we introduced an immutable collection data type called Tuple. In this lesson, we will work with List. The main difference between Tuple and List is that List is mutable. This means that you can modify its elements. You can also append, insert or remove the elements of a List which you cannot do with a tuple. However, there are similarities also between a tuple and a list. Both are a collection of items that may have different types. Though List can have elements with different types, it is more common to use list for homogenous element types. Tuple is more frequently used if the elements are of different type. Another similarity is that the elements of both tuple and list can be accessed using an index of integer type. 

List is more commonly used than tuple in many cases because of its mutability. At the same time, there are cases where we need to be aware on how list works especially when we assign list or pass list to a function. We will discuss all this in this lesson. 

## Creating a List

Let's begin by creating a list. Previously, we created a tuple by assigning a number of items into a variable separated by a comma. The use of the parenthesis, i.e. `()`, was optional to create a tuple. List data type is created also by assembling items separated by a comma. However, to indicate to Python that we want to create a list instead of a tuple, we use a **square bracket** when creating a list literal, i.e. `[]`. 

```python
>>> my_pies = [3, 3.14, '3.14']
>>> print(my_pies)
[3, 3.14, '3.14']
>>> type(my_pies)
<class 'list'>
```

As we mentioned in the first section, though List can have elements of different types, it is more common to create list where the elements are of the same type. In this case, we can also use type annotation when creating a list where the elements are of the same type.

```python
from typing import List

my_steps: List[int] = [40, 50, 43]
print(my_steps)
print(type(my_steps))
```

In the above code we annotate `my_steps` as follows

```python
my_steps: List[int] 
```

On Python 3.8 and earlier, the name of the collection type is capitalized, and the type is imported from the 'typing' module. 

## Basic Operations for List

Once we know how to create a List, we can now show some of the common basic operations with List data type. The most basic one is to access the element in a list. The way we do it is exactly the same as accessing an element in a Tuple.

```python
>>> my_steps = [40, 50, 43]
>>> print(my_steps[0])
40
>>> print(my_steps[2])
43
>>> print(my_steps[-2])
50
```

Notice that we can access the first element from index 0 and the last element from size of list minus 1, i.e. `len(my_steps) - 1`. We can also use the negative index where -1 refers to the last element. In the example above, -2 index will refer to the second last element, which is 50. 

We can get the length of a list from the `len()` built-in function and so we can access the last element using this.

```python
>>> my_steps = [40, 50, 43]
>>> print(my_steps[len(my_steps) - 1])
43
```

Notice that the last element is the size of the list minus one. Therefore, if we use the size of the list as an index to access an element, this results in trying to access an element that is outside of the range.

```python
>>> my_steps = [40, 50, 43]
>>> print(my_steps[len(my_steps)])
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

The error message indicates that the list index is out of range. This is because the last index is `len(my_steps) - 1`. 

## Basic Operations with a List Data

## Getting a Sublist from a List

## Aliasing a List

## Environment Diagram of List Data

## List Comprehension

## Traversing a List

## Identifying When to Use a Tuple or a List