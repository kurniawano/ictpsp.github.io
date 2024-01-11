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

### Accessing an Element in a List

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

### Getting the Number of Elements in a List

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

### Adding an Element Into a List

Another basic operations is to add elements into a list. There are multiple ways of adding an element into a list. The first one is to add an element at the **back** of the list. This is called **appending**. Since list is an *ordered* linear data structure, there is a sequence in the element. We can talk about the first item and the last item in a list. Appending is adding the item at the end of the list as the last item of the list. As the name suggest, the method to do this is `list.append(item)`. 

```python
>>> my_steps = [40, 50, 43]
>>> my_steps.append(52)
>>> my_steps
[40, 50, 43, 52]
```

In the above code, we add 52 at the end of the list. What if we want to add item at the first position in the list? In this case, we can use the `list.insert(pos, item)` method.

```python
>>> my_steps
[40, 50, 43, 52]
>>> my_steps.insert(0, 45)
>>> my_steps
[45, 40, 50, 43, 52]
```

The method `insert()` has two arguments. The first argument specifies at which position you want to insert the element and the second argument is the element you want to insert. In the above example, we inserted 45 into position 0, which is the first position in the list. We can insert element into the other position as well. 

```python
TypeError: 'list' object is not callable
>>> my_steps
[45, 40, 50, 43, 52]
>>> my_steps.insert(2, 65)
>>> my_steps
[45, 40, 65, 50, 43, 52]
```

In the above code, we inserted 65 into the third position (index 2). 

One important thing to note is that both `.append()` and `.insert()` does not return any value. These methods modify the list object that is attached to these methods. Notice that we call the method in this way.

```python
object_name.append(item)
```

In our case above, the object name was `my_steps`. We then use the "dot" operator to access the method `append()` of this object. In this case, this method is attached to a list object called `my_steps`. The dot operator in `my_steps.append(52)` can be read as follows: "call the append() method OF my_steps object with an input argument 52". The append() belongs to a list object `my_steps`. In fact, every list object that you create has this `append()` method. What this method does is simply appending an item to the object it belongs to which in this case is `my_steps`. However, this method has no return value. We can check that it has no return value by storing the output of this method to a variable and print the variable value as shown below.

```python
>>> output = my_steps.append(70)
>>> print(output)
None
>>> print(my_steps)
[45, 40, 65, 50, 43, 52, 70]
```

We can see that the output of `print(output)` is `None`. However, when you print the list object `my_steps`, you can see that it has been modified with the new element at the end.

Another way of adding elements into a list is by concatenating two lists or extending a list with another list. The operator for concatenating two objects is the `+` operator which we have used for concatenating two strings. We can use the same operator for concatenating two lists.

```python
>>> week1_steps = [40, 45, 50]
>>> week2_steps = [55, 52, 60]
>>> week1_and_2 = week1_steps + week2_steps
>>> week1_and_2
[40, 45, 50, 55, 52, 60]
```

We can also use the `list1.extend(list2)` method to extend a list with another list. The second list is extended to the back of the first list.

```python
>>> week1_steps
[40, 45, 50]
>>> week2_steps
[55, 52, 60]
>>> week1_steps.extend(week2_steps)
>>> week1_steps
[40, 45, 50, 55, 52, 60]
```

There is a subtle difference between using `+` operator and `.extend()` method. When using the `+` operator, a new list containing both lists are created. This new concatenated list is different from both the first and the second list. However, when we use the `.extend()` method. This method is similar to `.append()` and `.insert()` in the sense that it modifies the object that is attached to it through the dot operator and does not return any other value. We can see from the above example that the list object `week1_steps` is changed to contain the second list. 

### Removing an Element From a List

We have shown how to access an element in a list and how to add elements into the list. Now, we can show how to remove elements from a list. The common operator to remove elements from a list is the `del` operator. We use it in this way.

```python
del list[index]
```
where the index is the position of the item we want to remove. For example, we can remove the second element of a list using the following.

```python
>>> my_steps
[45, 40, 65, 50, 43, 52, 70]
>>> del my_steps[1]
>>> my_steps
[45, 65, 50, 43, 52, 70]
```

Notice that the second element, which is indexed by 1, has been removed from the list, i.e. 40. However, there are times that we know the item value that we want to remove rather than its index. A convinient method to remove an item in this case is to use the `list.remove(item)` method. For example, if we want to remove 43 from the list above, we can type the following.

```python
>>> my_steps
[45, 65, 50, 43, 52, 70]
>>> my_steps.remove(43)
>>> my_steps
[45, 65, 50, 52, 70]
```

This `.remove()` method is similar to the other list methods in the sense that it does not return any value. However, these methods modify the existing list which in this case is `my_steps`. We can see that `my_steps` no longer contains 43 after calling `my_steps.remove(43)`. 

Just as it is common to add items from the back of the list, it is also common to remove items from the back of the list. This is typically true when list is used as stack data structure. We will discuss stack at some other lessons but for now we can think of stack data structure similar to a stack of books on a table where we can put book at the top of the stack and remove the book only from the top of the stack. Python provides `list.pop()` method for this.

```python
>>> my_steps
[45, 65, 50, 52, 70]
>>> out = my_steps.pop()
>>> print(out)
70
>>> my_steps
[45, 65, 50, 52]
```

Notice above that `pop()` method does two things:
* first, it returns the last element as the output of the `pop()` method.
* second, it removes the last element from the list and thereby changing the list itself.

In the above example, 70 was removed from `my_steps` and it is returned by `pop()` to be assigned to `out` variable. 

What is interesting is that you can change the behaviour of `pop()` by providing an argument. Instead of popping the element from the last item of the list, you can specify which item you want to pop out from the list. For example, let's say if we want to pop out the first item of the list, we can type the following code.

```python
>>> my_steps
[45, 65, 50, 52]
>>> out = my_steps.pop(0)
>>> print(out)
45
>>> print(my_steps)
[65, 50, 52]
```

You can see that 45, which is the first element, is removed from the list and is stored into `out`.  How different `pop()` is with `del` keyword. Both seems to remove the element by providing its index. The difference lies in the fact that `pop()` returns the element that is removed from the list while `del` does not. In fact, if you try to assign to a variable when using `del` it will give an error.

```python
>>> out = del my_steps[0]
  File "<stdin>", line 1
    out = del my_steps[0]
          ^
SyntaxError: invalid syntax
```

The error says it is an invalid syntax because `del` keyword is expected to be the first token in a statement and cannot be used with an assignment operator. 

### Finding the Index of an Element

What if we want to know the position of a particular item in the list? Can we find its index? Python provides `index()` method to find the index of a particular element. 

```python
>>> my_steps
[65, 50, 52]
>>> my_steps.index(52)
2
```
In the above example, `my_steps.index(52)` finds the index of an element 52 in the list `my_steps`. What if there are more than one elements in the list? Can we find its second occurance position? We can still use the same `index()` method by providing the second argument. The second argument specifies from which position you want to start finding the element. See example below. First, we will add another element with the same value 52 and then we will find the two positions in the list.

```python
>>> my_steps
[65, 50, 52]
>>> my_steps.append(52)
>>> my_steps
[65, 50, 52, 52]
>>> first_pos = my_steps.index(52)
>>> first_pos
2
>>> second_pos = my_steps.index(52, first_pos + 1)
>>> second_pos
3
```

In the above code, we first append another 52 into the list `my_steps`. Then, we capture the first position of 52 by using the `index(52)` method. We stored this output into `first_pos` variable. We then used this position to find the second position by providing it into the second argument of `index()`. We put `first_pos + 1` because we want to start find the next 52.

## Creating a New List From an Existing Data

We have learnt how to create a list using what we call as a *list literal*. We used square bracket to create a new list.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
```

We can also create a new list from any existing data. In this section, we will discuss some of a few way to create a new list from an existing data.

### List Conversion Function

Python provides a built-in function `list()` to convert any other data type to a list. This means that we can convert a tuple into a list or a string into a list. See code below.

```python
step_as_tuple: tuple[str, int] = ('John', 50)
step_as_list: list[str, int] = list(step_as_tuple)
print(step_as_list, type(step_as_list))
```

The output displays the following.
```
['John', 50] <class 'list'>
```

Similarly, we can convert a string into a list. In this case, every character will be an individual element in the converted list.

```python
name: str = 'John'
name_as_list: list[str] = list(name)
print(name_as_list)
```

The output is shown below.
```
['J', 'o', 'h', 'n']
```

### Copying a List into a New List

We can also make a copy of an existing list into a new list. To do this, we will use the `copy()` function from the `copy` library.

```python
import copy
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
my_steps_backup: list[int] = copy.copy(my_steps)
print(my_steps, id(my_steps))
print(my_steps_backup, id(my_steps_backup))
```

The output is shown below.

```
[40, 50, 43, 55, 67, 56, 60] 4454460608
[40, 50, 43, 55, 67, 56, 60] 4454499840
```

In the above code, we used `id()` to check the object id in the memory. We can see the output on the second number after the list. Notice that the two ids are different because they are two different objects in the memory. The `copy()` function has created a new object with the same value as the first list `my_steps`. 

### Slicing a List

Another way we can create a new list is by *slicing* the list. Python provides a convenient syntax using the square bracket operator (or the get item operator). The format is the following.

```
list[start:end:step]
```

One thing that we have to remember is that the **end index** is exclusive. This means that it excludes the element pointed by the *end index*. Let's illustrate this with an example. Let's start with our existing list.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
```

We can create a new list consisting of `[50, 43, 55]` which is the second element to the fourth element in the list above using slicing.
```python
mon_to_wed_steps: list[int] = my_steps[1:4]
print(mon_to_wed_steps)
```

The output is shown below.
```
[50, 43, 55]
```

Notice that the index starts from 0 as shown in the table below.

| positive index | 0  | 1  | 2  | 3  | 4  | 5  | 6  |
|----------------|----|----|----|----|----|----|----|
| element        | 40 | 50 | 43 | 55 | 67 | 56 | 60 |

Notice that we did not specify the steps in the slicing arguments. By default the step size is 1. The `start` and the `end` index also has its default values. By default `start` is 0. This means that you don't need to specify the start index if you want to slice from the first element.

```python
sun_to_wed: list[int] = my_steps[:4]
print(sun_to_wed)
```

The output is shown below.

```
[40, 50, 43, 55]
```

The default for the `end` index, however, is **one plus** the last element's index. In our case, the last element is 6, so the default for the end index is 7. Therefore, these two codes are equivalent.

```python
copy_1: list[int] = my_steps[0:7]
copy_2: list[int] = my_steps[:]
print(copy_1, id(copy_1))
print(copy_2, id(copy_2))
```

The output is shown below.

```
[40, 50, 43, 55, 67, 56, 60] 4405092864
[40, 50, 43, 55, 67, 56, 60] 4405094080
```

Notice that we have just created a duplicate of an existing list using slicing similar to what we do with `copy()`. 

We can also slice the list using a negative index. See table below.

| negative index | -7 | -6 | -5 | -4 | -3 | -2 | -1 |
|----------------|----|----|----|----|----|----|----|
| element        | 40 | 50 | 43 | 55 | 67 | 56 | 60 |

Notice the difference between the positive indexing and the negative index. While the positive indexing starts from 0, the negative indexing starts from -1. This is useful when we want to create a new list counting from the back. For example, let's say we want to get the *last three elements*. 

```python
last_three_days: list[int] = my_steps[-3:]
print(last_three_days)
```

The output is shown below.

```
[67, 56, 60]
```

Notice in the above slicing that we have used the default value for the `end` index. We can get the same results using the following code.

```python
last_three_days: list[int] = my_steps[-3:7]
```

The above example shows that you can actually mixed positive and negative indexing. However, utilising the default values are useful because it is just more intuitive to retrieve the last *three days* with indexing `my_steps[-3:]`. 

We can also get the first three days using the positive indexing and default values as shown below.

```python
first_three_days: list[int] = my_steps[:3]
print(first_three_days)
```

The output is shown below.

```
[40, 50, 43]
```

As can be seen above it is intuitive to get the first three days with slicing index of `my_steps[:3]`. This also explains why Python chose the `end` index is **exclusive**. The reason is that you easily get the number of elements from `start-end`. As in the example of the first three days, you know there are three days because $3-0=3$. Similarly, when we try to get the steps from Monday to Wednesday, the `end` index was 4 rather than 3 because $4-1=3$. This gives us a number of days when slicing `my_steps[1:4]`. 

Another way to see the slice index is to put them at the boundary of the elements as shown in the figure below.

INSERT FIGURE HERE

In the figure above, we can see the `start` and `end` index as the boundary of the sliced elements. For example, when we want to get the steps from the second element to the fourth, we can see that the boundary enclosing those elements is 1 on the left and 4 on the right. The same thing works for the negative index. 




## Aliasing a List

## Environment Diagram of List Data

## List Comprehension

## Traversing a List

## Identifying When to Use a Tuple or a List