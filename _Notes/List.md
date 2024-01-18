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

Once we know how to create a List, we can now show some of the common basic operations with List data type. The most basic one is to access the element in a list. The way we do it is exactly the same as accessing an element in a Tuple. We use the get item operator which is a square bracket operator with an index.

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

### Modifying an Element in a List

The get item operator can be used together with the assignment operator `=` to change an element in the list. 

```python
>>> my_steps = [40, 50, 43]
>>> print(my_steps[0])
40
>>> my_steps[0] = 65
>>> print(my_steps[0])
65
```

In the above code, we modify the first element (index 0) from 40 to 65. 

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

The third argument in the get item operator for list slicing is the step size. We can specify the step size other than the default value 1. For example, let's day we want to get the data every two days. We can do so using the code below.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
every_other_days: list[int] = my_steps[::2]
print(every_other_days)
```

The output is shown below.

```python
[40, 43, 67, 60]
```

Notice that since we did not specify the `start` and `end` index, Python takes their default values 0 and 7 for these two arguments. The resulting slice starts from the first element to the last but with a step of 2. We can also specify a negative step size. This is useful for example if we want to get a new list with a reverse order. Let's say, we can get the last three days starting from the last day to the earlier day using the code below.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
reverse_last_three_days: list[int] = my_steps[-1:-4:-1]
print(reverse_last_three_days)
```
The output is shown below.

```python
[60, 56, 67]
```

In the above slicing code, the `start` index was -1 which is the index of the last element using the negative indexing. The `end` index was -4 which is exclusive. Getting the difference between these two indices tells us that the resulting list will have 3 elements. The step size is specified as -1 because we start our indexing from the back and end it at the front.

## Aliasing a List

One important concept about list data structure in Python is the concept of alias. This has implication on how list is copied and when it is passed on to a function. To start with, let's recall the concept of variable in a primitive data type like an integer.

```python
a: int = 4
b: int = a
```

In Python, variable names are just label that is binded to some value. In this case, the integer value 4 is binded to a name `a`. When we do assignment such as `b = a` as in the code above, Python evaluates the value of `a` and get `4`. This value is then binded to the name `b`. In this way, changing `b` will not affect `a`.

```python
a: int = 4
b: int = a
b = -3
print(a)
print(b)
```

The output is shown below.

```python
4
-3
```

We can see the environment diagram from Python Tutor below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=a%3A%20int%20%3D%204%0Ab%3A%20int%20%3D%20a%0Ab%20%3D%20-3%0Aprint%28a%29%0Aprint%28b%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=5&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

This is different in the case of list data type. 

```python
my_steps: list[int] = [40, 50, 40, 50]
copy_steps: list[int] = my_steps
copy_steps[0] = 75
print(my_steps)
print(copy_steps)
```

The output is shown below.

```python
[75, 50, 40, 50]
[75, 50, 40, 50]
```

Notice that both `my_steps` and `copy_steps` first elements are modified to 75. It's important to pause here and ponder what happens. In our code above, we created a list called `my_steps`. We then create another variable called `copy_steps` and assign `my_steps` to this variable. Unlike integer, the value that is binded to the new name `copy_steps` is a **reference** to the list **object**. This reference can be represented as an **arrow** in the environment diagram. Compare the environment diagram below with that for the integer case.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=my_steps%20%3D%20%5B40,%2050,%2040,%2050%5D%0Acopy_steps%20%3D%20my_steps%0Acopy_steps%5B0%5D%20%3D%2075%0Aprint%28my_steps%29%0Aprint%28copy_steps%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=5&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice the arrow in that environment diagram that points to the same list object. Because the two names point to the same object, modifying one of them causes modification on the other name. The reason of this is that `b` is an **alias** to `a` and so points to the same object as `a`. This is different from that when we deal with integer data type. For the case of integer data type, the integer object is duplicated and `b` points to a different integer object (Python has some optimisation for small integers but that's for another story). 

The environment diagram before `b` is modified in the case of integer data type is shown below when the program counter is at line 3.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=a%3A%20int%20%3D%204%0Ab%3A%20int%20%3D%20a%0Ab%20%3D%20-3%0Aprint%28a%29%0Aprint%28b%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=2&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


This aliasing effect of list data type becomes important when we pass list data into a function as one of the input arguments.

## Passing a List into a Function as Input

In the previous section, we mentioned that list behaves differently than integer data type when we assign a variable to an existing data. In the case of integer data type, the integer object is duplicated when we assign a different name. However, in the case of list, the list object is not duplicated but rather the two names point to the same object. What happens for these two data types when we pass them into a function as input arguments?

Let's start again with an integer data type. We can pass an integer as an argument as shown below.

```python
def compute_cadence_for_30sec(steps: int) -> int:
  return steps * 2

my_step: int = 40
cadence = compute_cadence_for_30sec(my_step)
```

Notice the environment diagram as we enter the function `compute_cadence_for_30sec`. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compute_cadence_for_30sec%28steps%3A%20int%29%20-%3E%20int%3A%0A%20%20return%20steps%20*%202%0A%0Amy_step%3A%20int%20%3D%2040%0Acadence%20%3D%20compute_cadence_for_30sec%28my_step%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=3&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the environment diagram shown above, the argument `steps` is a variable in the local frame of the function `compute_cadence_for_30sec`. This `steps` has a value of 40 and is different from that of the variable `my_steps` in the *global* frame. The value 40 is duplicated and passed into the function. 

As you can guess, the behaviour is different in the case when we pass a list data type into a function. Let's modify the function to take in a list.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compute_cadence_for_30sec%28steps%29%3A%0A%20%20return%20steps%20*%202%0A%0Adef%20compute_cadence_for_list%28list_of_steps%29%3A%0A%20%20output%20%3D%20%5B%5D%0A%20%20for%20step%20in%20list_of_steps%3A%0A%20%20%20%20cadence%20%3D%20compute_cadence_for_30sec%28step%29%0A%20%20%20%20output.append%28cadence%29%0A%20%20return%20output%0A%0Amy_step%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%0Alist_cadence%20%3D%20compute_cadence_for_list%28my_step%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=4&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We purposely stop the step in Python Tutor at line 4 where we just entered the function after the function call. Notice the environment diagram on the right. We can see that both `my_steps` and `list_steps` point to the same list object. 

See if you can understand the above code and what it does. We will show in the following section how to traverse a list. But for now, our interest is to show that when we pass a list as an input argument to a function, what is being passed on is the **reference** to this list. This means that you may **modify** the list inside the function. We should avoid this as it may be harder to debug your code. The reason is that when you modify the list inside the function, the list in the global frame is also modified. See the code below for an example.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compute_cadence_for_30sec%28steps%29%3A%0A%20%20return%20steps%20*%202%0A%0Adef%20correct_first_day%28list_of_steps%29%3A%0A%20%20corrected_steps%20%3D%20list_of_steps%0A%20%20corrected_steps%5B0%5D%20%2B%3D%2010%0A%20%20return%20corrected_steps%0A%0Amy_steps%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%0Acorrected_steps%20%3D%20correct_first_day%28my_steps%29%0Aprint%28my_steps%29%0Aprint%28corrected_steps%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=11&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We have modified the code just to illustrate this aliasing effect inside a functin. Let's say you have a code to correct one of the element of the list. In the code above, we added the first step by 10. Notice that at the end of the code, both `my_steps` and `corrected_steps` have the same value on the first element, i.e. it was changed from 40 to 50. We do expect `corrected_steps` to be changed but not `my_steps`. To avoid this aliasing effect, we should have copied the list as shown below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=import%20copy%0Adef%20compute_cadence_for_30sec%28steps%29%3A%0A%20%20return%20steps%20*%202%0A%0Adef%20correct_first_day%28list_of_steps%29%3A%0A%20%20output%20%3D%20copy.copy%28list_of_steps%29%20%23%20or%20output%20%3D%20list_of_steps%5B%3A%5D%0A%20%20output%5B0%5D%20%2B%3D%2010%0A%20%20return%20output%0A%0Amy_step%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%0Acorrected_step%20%3D%20correct_first_day%28my_step%29%0Aprint%28my_step%29%0Aprint%28corrected_step%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=12&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice, in this case now `my_steps` and `corrected_steps` are two different list and we did not modify `my_steps` in the process. 

## Mutable and Immutable Data Type

By now, you may wonder how do we know whether an object is duplicated or only its reference. It turns out that Python's data type falls into either **mutable** or **immutable** data type. Mutable means that it can be changed (Remember the mutant in X-men?). Immutable means that it cannot be changed. The following table list down the mutable and immutable data types.

| immutable | mutable             |
|-----------|---------------------|
| int       | list                |
| float     | dictionary          |
| str       | set                 |
| tuple     | user-defined object |

You may be surprised to see that integer and float as immutable as it seems that we can actually modify integer as in the code below.

```python
a: int = 4
a = 5
```

However, we **didn't** change the integer object `4`. What happens is that we create a new integer object `5` and bind it to the same name `a`. The integer object `4` itself is immutable. This is more obvious in a string when you try to modify one of the character in a string. Recall that we can access a character in a string using the get item operator.

```python
name: str = "John Wick"
print(name[0])
```

This outputs `J`. However, we are not able to modify this element.

```python
name: str = "John Wick"
name[0] = "B"
```

It will output the following error message.

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
```

String object is immutable and so it does not support item assignment. Similarly with tuple.

```python
contact_info: tuple = ("John Wick", 81234567, "john@wick.com")
contact_info[1] = 91234567
```

This also gives an error as shown below.

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

This is not the case for mutable data type such as list.  We have shown that we can actually modify an element in a list.

```python
my_steps = [40, 50, 43]
my_steps[0] = 65
```

The above code does not produce error and it actually modifies the first element to 65. 

We will discuss the other data type such as dictionary and set on the subsequent sections. One important thing to note for now is that these mutable data type binds its *reference* to its object to a variable name. This is the arrow that we have been seeing in the Python Tutor visualisation previously. When we copy this arrow to a new name, the arrow still points to the same list object. This is what happens when we create an **alias**. To avoid aliasing, you need to copy the list. We have shown above on how you can create a copy of a list. 


## Traversing a List

One of the common operations when we deal with a list data type is to **traverse** the list. This means that we would like to visit every element of the list and process it in some way. The previous section has shown one simple way to traverse a list. The syntax is shown below.

```python
for element in iterable:
  # block A for code to be repeated
  # do something with element
```

This syntax is similar when we traverse every character of a string. Recall the following code.

```python
name = "John Wick"
for char in name:
  print(char)
```

List is also an *iterable* just like string data type. Because of this, we can actually traverse the list in a similar way.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60] 
output = []
for step in my_steps:
  cadence = compute_cadence_for_30sec(step)
  output.append(cadence)
```

In the above code `my_steps` is our list which is an iterable. The variable `step` takes in the element of `my_steps` at *every iteration*. We can see the value of `step` by adding the `print()` statement after the for statement as shown below. Click the "next" button to step through the iteration in the for loop.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=my_steps%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20%0Aoutput%20%3D%20%5B%5D%0Afor%20step%20in%20my_steps%3A%0A%20%20print%28step%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We can also use the `enumerate()` function to count the element and get the element at the same time. For example, we can use the code below to display the day and the steps.

```python
my_steps = [40, 50, 43, 55, 67, 56, 60] 
output = []
for index, step in enumerate(my_steps):
  print('Day ', (index + 1), ', steps: ', step)
```

Recall that enumerate returns an iterable where each element is a tuple. The first element of the tuple is the index and the second element of that tuple is the list element that we are enumerating. To capture this tuple, we set the variable between `for` and `in` as the following: `index, step`. Since the enumeration starts from 0 and we want to count the day from 1, we use `index + 1` inside our `print()` statement. Use the below Python Tutor to step through the code and observe the output. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=my_steps%20%3D%20%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D%20%0Aoutput%20%3D%20%5B%5D%0Afor%20index,%20step%20in%20enumerate%28my_steps%29%3A%0A%20%20print%28'Day%20',%20%28index%20%2B%201%29,%20',%20steps%3A%20',%20step%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Lastly, we can also traverse the list by creating the index and traversing the range of the indices. 

```python
my_steps = [40, 50, 43, 55, 67, 56, 60] 
output = []
for index in range(len(my_steps)):
  print('Day ', (index + 1), ', steps: ', my_step[index])
```

Notice that the argument for `range()` function is an integer and not a list. In this case, we specify `len(my_steps)` as the input to `range()` function. The length of the list is 7 and so it calls `range(7)` which results in an iterable from 0 to 6 (exclusive of the ending) for the variable `index`. To retrieve the element of the list, we use the get item operator (square bracket), i.e. `my_step[index]`.

## Identifying When to Use a Tuple or a List

List looks a lot like tuple that we learned in the previous lesson. So when do we use tuple and when do we use list? One main difference between tuple and list that we have discussed is that tuple is immutable while list is mutable. This means that we use tuple when there is no need to change the element of the tuple. On the other hand, if our solution requires change of the elements of the collection data, it would be preferable to use list instead.

Another common practice when programmers use tuple is when we just want to group a collection of data which maybe related but rather different. In the example above, for example, we use tuple for contact info. 

```python
contact_info: tuple = ("John Wick", 81234567, "john@wick.com")
```

Notice that though these three data are related since they are all information of the same person, they are different kinds of data. The first one is a string since it is the name of the person. The second one is a number for the contact. The last one is the email address. Tuple is a convenient way to group them together. There are better ways which we will explore in subsequent lesson such as using dictionary. However, list is usually used to group items that is very look a like. In this lesson, we used it to group the steps of various days.

```python
my_steps: list[int] = [40, 50, 43, 55, 67, 56, 60] 
```

Notice that all these data are integers and they are all `steps`. The only thing that differentiate them is which day the step belongs to. This comes to the other characteristics of list data. List data naturally suits those that have a sequence. In this case, the first data is the step on the first day, the second data is the step on the second day and so on. This suits list since each element is placed with a fixed index. The indices in a list data type is useful when the data has a certain order or sequence. Data at index of higher value is at a later sequence as compared to data at a lower value index. 

Because of this, usually list is used when the data is of the same type. Though Python allows a mixed data type in a list, it is common to apply list for those collections that have the same data type. On the other hand, it is common to use tuple for those collections that have various data type in their elements.
