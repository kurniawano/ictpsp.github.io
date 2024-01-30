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

Similar to a single list, you can also slice a nested list. What you need to remember is that they are just *a list where the *. This means that you need to decide how the list is to be sliced. Let's start with the simplest task of slicing the weeks in `month_steps`. Let's say, we only want to get the first two weeks. We can type the following.

```python
>>> month_steps: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                    [54, 56, 47, 62, 61, 46, 61],
                                    [52, 56, 63, 58, 62, 66, 62],
                                    [57, 58, 46, 71, 63, 76, 63]]
>>> month_steps[:2]
[[40, 50, 43, 55, 67, 56, 60], 
 [54, 56, 47, 62, 61, 46, 61]]
```

Recall that `month_steps` has four elements where each element is a list. In order for us to get the first two lists, we slice `month_steps[:2]`. We can also get the second week to the fourth week in the following way.

```python
>>> month_steps[1:]
[[54, 56, 47, 62, 61, 46, 61], 
 [52, 56, 63, 58, 62, 66, 62], 
 [57, 58, 46, 71, 63, 76, 63]]
```

What is not possible is to get the steps in the middle of the weeks for all the weeks. There are ways of doing this using `numpy` library when the data type is a numpy array.  We can slice the rows easily because each row is just an element in a list. The columns, however, is different. They are list in a list. There is no easy and simple ways of slicing the *columns*. We will come back to this problem and create a function to solve this at the end of the lesson. 


### Adding and Removing Elements

Similarly, adding and removing can be done if we recall that nested list is just a list inside a list. For example, we can add another week into the list. 

```python
>>> month_steps.append([53, 52, 51, 56, 67, 45, 47])
>>> month_steps
[[40, 50, 43, 55, 67, 56, 60], 
 [54, 56, 47, 62, 61, 46, 61], 
 [52, 56, 63, 58, 62, 66, 62], 
 [57, 58, 46, 71, 63, 76, 63], 
 [53, 52, 51, 56, 67, 45, 47]]
```

Notice that the data type of the item in the `append()` argument is a **list**.  What if you append an integer instead of a list?

```python
>>> month_steps.append(100)
>>> month_steps
[[40, 50, 43, 55, 67, 56, 60], 
 [54, 56, 47, 62, 61, 46, 61], 
 [52, 56, 63, 58, 62, 66, 62], 
 [57, 58, 46, 71, 63, 76, 63], 
 [53, 52, 51, 56, 67, 45, 47], 
 100]
```

Python will basically just add the `int` item as the last element in the list. Recall that Python allows multiple data types in a single list. However, when you run this code using `mypy`, it will throw an error. The reason is that previously, we annotated `month_steps` as `List[List[int]]`. Try running the file `month_steps_error.py` inside `lesson08` folder with `mypy` and check the error message.

```
$ mypy month_steps_error.py
month_steps_error.py:9: error: Argument 1 to "append" of "list" has incompatible type "int"; expected "List[int]"  [arg-type]
Found 1 error in 1 file (checked 1 source file)
```

We can remove or delete the element in the usual way either using `pop()` or the `del` operator. 

```python
>>> del month_steps[-1]
>>> month_steps
[[40, 50, 43, 55, 67, 56, 60], 
 [54, 56, 47, 62, 61, 46, 61], 
 [52, 56, 63, 58, 62, 66, 62], 
 [57, 58, 46, 71, 63, 76, 63], 
 [53, 52, 51, 56, 67, 45, 47]]
```

Notice that the `100` item has been deleted from the list. Adding something as another row in the list is easy because it is just another item in the `month_steps` list. However, adding something in a *column* is not straight forward. If we just want to add or remove an item in one of the sub-list, we just need to access that sub-list first and use the `list` operations to add the item.  Let's say, we want to remove the last element in week 1.

We can either use `del` on the first sub-list. We access the first sub-list using `month_steps[0]`. 
```python
>>> del month_steps[0][-1]
```

Or, we can also pop that item out from the first sub-list.

```python
>>> month_steps[0].pop()
60
```

We can add the item back in using `append()`.

```python
>>> month_steps[0].append(60)
```

Notice that in all these operations, the key idea is to access the *sub-list* `month_steps[0]`. 

## Copying Nested List and Aliasing Issue

Another important aspect of nested list is the effect of aliasing. Let's recreate `month_steps` using four lists as follows.

```python
from typing import List

week_1: List[int] = [40, 50, 43, 55, 67, 56, 60] 
week_2: List[int] = [54, 56, 47, 62, 61, 46, 61] 
week_3: List[int] = [52, 56, 63, 58, 62, 66, 62] 
week_4: List[int] = [57, 58, 46, 71, 63, 76, 63]

month_steps: List[List[int]] = [week_1, week_2, week_3, week_4]
```

What if we modify one of the sub-list such as `week_2`. Let's say, we remove the last element of `week_2`. What will happen to month_steps?

```python
del week_2[-1]
print(month_steps)
```

The output is shown below.

```
[[40, 50, 43, 55, 67, 56, 60], 
 [54, 56, 47, 62, 61, 46], 
 [52, 56, 63, 58, 62, 66, 62], 
 [57, 58, 46, 71, 63, 76, 63]]
```

Notice that the last element in the second sub-list has been removed. It is important to stop here. Recall that we did not apply `del` on `month_steps` but only on `week_2`. However, when `week_2` is modified, the effect is seen as well on `month_steps`. We can understand this by looking into the environment diagram.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=week_1%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20%0Aweek_2%20%3D%20%5B54,%2056,%2047,%2062,%2061,%2046,%2061%5D%20%0Aweek_3%20%3D%20%5B52,%2056,%2063,%2058,%2062,%2066,%2062%5D%20%0Aweek_4%20%3D%20%5B57,%2058,%2046,%2071,%2063,%2076,%2063%5D%0A%0Amonth_steps%20%3D%20%5Bweek_1,%20week_2,%20week_3,%20week_4%5D%0Adel%20week_2%5B-1%5D%0Aprint%28month_steps%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=7&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that both `month_steps` and `week_2` points to the same list object in the environment. This is why when we modify `week_2`, we also modify `month_steps`. Similarly, when we modify `month_steps`, we will see that `week_2` is modified. Let's add back the element, but this time, we will add `month_steps`.

```python
month_steps[1].append(61)
print(week_2)
```

The output is shown below.

```
[54, 56, 47, 62, 61, 46, 61]
```

Notice that `61` is back into `week_2`. Both `week_2` and `month_steps`'s second sub-list points to the same object. 

This has important consequences when we slice a nested list. Let's say, we create a new list containing the first two weeks.

```python
first_two_weeks: List[List[int]] = month_steps[:2]
```

The environment diagram is shown below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=week_1%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20%0Aweek_2%20%3D%20%5B54,%2056,%2047,%2062,%2061,%2046,%2061%5D%20%0Aweek_3%20%3D%20%5B52,%2056,%2063,%2058,%2062,%2066,%2062%5D%20%0Aweek_4%20%3D%20%5B57,%2058,%2046,%2071,%2063,%2076,%2063%5D%0A%0Amonth_steps%20%3D%20%5Bweek_1,%20week_2,%20week_3,%20week_4%5D%0Afirst_two_weeks%20%3D%20month_steps%5B%3A2%5D&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=6&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that `first_two_weeks` has only two elements. These two elements points to the same objects as the first two sub-lists in `month_steps`, which are the same objects pointed by `week_1` and `week_2` as well. This is what happens when we do a **shallow copy** of a nested list. The first level element of the list is copied but not the deeper levels. Notice that the `first_two_weeks` copied the element of `month_steps`. The two elements copied is the *arrows* pointing to `week_1` and `week_2`. However, it does not make a copy of `week_1` and `week_2`. They still point to the same object. 

What if we want to create a new copy of the deeper level items as well? Python provides a `deepcopy()` function from the `copy` library. 

```python
import copy

first_two_weeks: List[List[int]] = copy.deepcopy(month_steps[:2])
```

The environment diagram is shown below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20copy%0A%0Aweek_1%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20%0Aweek_2%20%3D%20%5B54,%2056,%2047,%2062,%2061,%2046,%2061%5D%20%0Aweek_3%20%3D%20%5B52,%2056,%2063,%2058,%2062,%2066,%2062%5D%20%0Aweek_4%20%3D%20%5B57,%2058,%2046,%2071,%2063,%2076,%2063%5D%0A%0Amonth_steps%20%3D%20%5Bweek_1,%20week_2,%20week_3,%20week_4%5D%0Afirst_two_weeks%20%3D%20copy.deepcopy%28month_steps%5B%3A2%5D%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=7&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that now, `first_two_weeks` list elements do not point to the same objects as `week_1` and `week_2`. They point to two new list objects. The function `deepcopy()` ensures that you do copy all the objects at all levels. 


## Slicing any part of the list