---
title: Nested List
permalink: /notes/nested-list
key: notes-nested-list
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

## Nested Data Structure

So far, we have worked on two kinds of collection data types. The first one is tuple and the second one is a list. In each of those lessons, we showed how to contain various items in a single collection. This collection, however, is linear or one dimensional. In our last example, we have a list of steps in a week.

```python
from typing import List

my_steps: List[int] = [40, 50, 43, 55, 67, 56, 60] 
```

What if we want to contain the list of steps in a month? We can continue adding the items to have a list of 30 or 31 elements. To go to the second or third week, however, we have to calculate what is the starting index of that week. For example, the first week starts from 0 to 6. The second week, on the other hand, will be from 7 to 13. The third week will be from 14 to 20 and so on. This means that when we work on the second or third or fourth week, the index of the maximum step is no longer from 0 to 6 and we are unable to make use of the function `get_name_day()` anymore. We have to transform it to 0 to 6 range before we can use that function. It's not that difficult. But there is another way we can organize our data.

We can organize our data as a list in a list. This is what we call as nested data structure. This means that we have one list to represent the month where each item is to represent each week. This representation for each week can be another list. Let's see how we can create and work on this nested data structure.

## Creating a Nested List

Let's say, we have data for four weeks exercises. Each week is contained in a list.

```python
week_1: List[int] = [40, 50, 43, 55, 67, 56, 60] 
week_2: List[int] = [54, 56, 47, 62, 61, 46, 61] 
week_3: List[int] = [52, 56, 63, 58, 62, 66, 62] 
week_4: List[int] = [57, 58, 46, 71, 63, 76, 63] 
```

We can then store these data in another list for a month.

```python
month_steps: List[List[int]] = [week_1, week_2, week_3, week_4]
```

Notice that this list has **four elements**. Each element is a **list** data type. We can check it's length and type using the normal list operations.

```python
print(type(month_steps), len(month_steps))
print(type(month_steps[0]), len(month_steps[0]))
```

The first line prints the type of the `month_steps` list and its length. The second line prints the type of the first element of `month_steps` which is `week_1` and its type. The output is shown below.

```
<class 'list'> 4
<class 'list'> 7
```

We can see that `month_steps` has four elements which are the four week lists. On the other hand, the first element of `month_steps` is also a list but this list has seven elements which is the number of steps for each day in that week. 

Another thing that we introduced here is the type annotatin for nested list. See that we defined it in the following way.

```python
month_steps: List[List[int]] = [week_1, week_2, week_3, week_4]
```

We used the usual `List[element_type]` for annotating `month_steps`. The only thing is that the element type for this list is another list with `int` elements, i.e. `List[int]`. 

We need not create a variable and directly create a single nested list literal as shown below.

```python
month_steps: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                [54, 56, 47, 62, 61, 46, 61],
                                [52, 56, 63, 58, 62, 66, 62],
                                [57, 58, 46, 71, 63, 76, 63]]
```

The above list creates the same nested list as before. You can actually write everythign in a single line. However, it is easier for us to separate the different week in a separate lines in creating the above list. 

## Environment Diagram of a Nested List

It is important for us to see what the environment diagram looks like for a nested data structure like the above. Previously, we showed the environment diagram of a single list. See below the arrow on the right hand side that points to the list object. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=my_steps%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=1&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that the list object contains the int immutable object. Now compares this with the environment diagram of a nested list.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=month_steps%20%3D%20%5B%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B54,%2056,%2047,%2062,%2061,%2046,%2061%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B52,%2056,%2063,%2058,%2062,%2066,%2062%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B57,%2058,%2046,%2071,%2063,%2076,%2063%5D%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=4&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that we have more *arrows* in this diagram. The name `month_steps` has an arrow pointing to a list of *four* elements. The element of this list is not an integer but rather another *arrow* which points to different list objects. Understanding this environment diagram helps us to understand what happens when we copy or access elements in the array. Let's look at some basic operations of a nested list.

## Basic Operations with Nested Lists

### Accessing an Element

The first basic operation is accessing an element either to read the value or to modify the value. Notice that `month_steps` is a list data type where each element is another list. See the type annotation of this variable.

```python
month_steps: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                [54, 56, 47, 62, 61, 46, 61],
                                [52, 56, 63, 58, 62, 66, 62],
                                [57, 58, 46, 71, 63, 76, 63]]
```

We have also seen the environment diagram in the previous section. The environment diagram shows that `month_steps` is actually just a list of four elements. This means that we can use the usual get item operator or the square bracket operator to get the item of its element.

```python
>>> month_steps[0]
[40, 50, 43, 55, 67, 56, 60]
>>> month_steps[1]
[54, 56, 47, 62, 61, 46, 61]
```

We can also check the type of this element using the `type()` function.

```python
>>> type(month_steps[0])
<class 'list'>
```

In order to get the number of steps in day one of week one, we need to access the list of list. Let's show how to do this in steps.

```python
>>> month_steps[0]
[40, 50, 43, 55, 67, 56, 60]
>>> month_steps[0][0]
40
```

Notice that we used two get item operators here. The first one is to get the element of `month_steps` which is the first week, i.e. `month_steps[0]`. The second get item operator is to get the first element of that week which is the step of day one in week one. To make it clear, you can actually assign the first week to a variable first.

```python
>>> week_1 = month_steps[0]
>>> week_1
[40, 50, 43, 55, 67, 56, 60]
>>> week_1[0]
40
```

Notice that this `week_1[0]` is the same as `month_steps[0][0]` because `week_1 = month_steps[0]`. Similarly, if we wish to access the third day of week four, we can type the following code.

```python
>>> month_steps[3][2]
46
```

Notice that week four is index 3 in the list since our indexing starts from 0. Similarly, our day three is index 2. 

You can also modify the element using the get item operator and the assignment operator as usual. For example, you can modify the value of  third day in the fourth week as follows.

```python
>>> month_steps[3][2]
46
>>> month_steps[3][2] = 57
>>> month_steps[3][2]
57
>>> month_steps
[[40, 50, 43, 55, 67, 56, 60], 
[54, 56, 47, 62, 61, 46, 61], 
[52, 56, 63, 58, 62, 66, 62], 
[57, 58, 57, 71, 63, 76, 63]]
```

### Slicing 

Similar to a single list, you can also slice a nested list. What you need to remember is that they are just *a list where the *. This means that you need to decide how the list is to be sliced.


### Adding and Removing Elements


## Copying Nested List and Aliasing Issue
