---
title: For Loop
permalink: /notes/for-loop
key: notes-for-loop
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

## Implementing Iterative Structure Using For Loop

In the previous section, we have discussed in detail how to implement the branch structure. The last basic control flow stucture is the iterative structure. In this lesson and the next, we will show you how to implement iterative structure using Python. 

Iterative structure is common when you deal with collection-like data type. We will deal with more collection-like data type in future lessons. However, for now, we can explore iterative structure using `string` data. Recall that string can be thought of like a collection of characters in some sequence. We can process each character using iterative structure. Similar processing can be done when we deal with other collection-like data such as list and dictionary. 

So how do we implement the iterative structure using Python? Python has two ways of implementing iterative structure. The first one is using **for-in** statement and the second one using **while-loop** statement. In this lesson, we will explore using the **for-in** statement.

The general syntax for the for-in statement is as follows.

```python
for element in iterable:
  # code block A
  # which will be repeated for every element in iterable
```

The right hand side of the `in` operator in the for-in statement must be an **iterable**. An iterable is any Python objects that can be iterated. This is basically saying that it must be collection-like data type where you can iterate over its element. String data is one of them. All these iterables supports the method `__iter__()` which will return the next element in the collection at every iteration. That next element is assigned to the `element` variable which is the left hand side of the `in` operator in the for-in statement. 

Therefore in a for-in statement, we iterate or repeate the code block A as many as the number of items in the iterable. If there are 11 items in the iterable, the code block A will be repeated 11 times. Each time, Python will assign the element of the iterable to the variable `element` which we can use to process the element. If we don't need the `element` in our code block A, we can choose to ignore it as follows.

```python
for _ in iterable:
  # code block A
  # which will be repeated for the number of items in iterable
```

// put flow chart for for-in statement

Let's take a look at some examples how to use that syntax. Let's say, we want to print every character in a name. We can write the following code.


```python
name = "John Wick"
for char in name:
  print(char)
```
In the above code, the `iterable` is the variable `name` which is a string. Remember that `string` is one of the iterables in Python. At every iteration, an element in the string will be assigned to `char`. 

The output of that code is shown below using Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20char%20in%20name%3A%0A%20%20print%28char%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, the instruction that is repeated for every element (code block A) is the `print(char)` statement. In this case, we are instructing Python to print the element of the iterable. 

One common mistakes that many novice programmers tend to do is processing the collection as a whole when what they wanted is processing the element. An example of this logic error is printing the whole name repetitively instead of printing the characters.

```python
name = "John Wick"
for char in name:
  print(name)
```

In this code, what we print is the string and not the characters. See the output below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20char%20in%20name%3A%0A%20%20print%28name%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that instead of printing each character on every line, what the code does is printing the whole string on every line.

Sometimes, you just want to repeat based on the number of element in the collection. In that case, you don't really use the element in the collection. As mentioned previously, you can ignore the element using an underscore, i.e. `_`. The code below print asterisks as many as the number of characters in the password.

```python
password = "D0n't us3 simpl3 passw0rd#"
for _ in password:
  print('*', end='')
```

In the above code we use the option `end=''` to replace the default new line character that is always added by the print statement. By default the ending character of a line is a new line character, i.e. `\n`. This is why the next print statement is displayed in the line below. By changing the ending character to an empty string, we can display the next string in the same line. See the output using Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=password%20%3D%20%22D0n't%20us3%20simpl3%20passw0rd%23%22%0Afor%20_%20in%20password%3A%0A%20%20print%28'*',%20end%3D''%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## Enumerating a Collection

There are times when it is useful to work with both the element and the index of a collection-like data. For example, we can get both the character and its index from a string. To do this, Python provides `enumerate()` function that returns a tuple of `(index, element)`. 

```python
name = "John Wick"
for (idx, char) in enumerate(name):
  print(f"Character {char} is at position: {idx + 1})
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20%28idx,%20char%29%20in%20enumerate%28name%29%3A%0A%20%20print%28f%22Character%20%7Bchar%7D%20is%20at%20position%3A%20%7Bidx%20%2B%201%7D%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We can see that the `enumerate()` function returns an iterable. Each element of this iterable contains two things. The first one is the index of that element and the second one is the element itself. In our code block A which is repeated, we make use of both the index and the element to print both the position, which is `idx + 1` and the character itself. 


## Range Function and Iteration Using Index

Previously, we mentioned that the right hand side of the `in` operator in `for-in` syntax must be an *iterable*. One simple way to create an iterable that can be used for indexing the elements in a collection data type is `range()` function. This function `range()` produces an iterable which element is a sequence of integers. 

```python
>>> range(10)
range(0, 10)
>>> for item in range(10):
...     print(item)
... 
0
1
2
3
4
5
6
7
8
9
```

In the above code, `range(10)` produces a range of values from `0` to `9`. Notice that it does not include `10`. This similar convention can be found when we slice a string in the previous lesson. In slicing, the ending index is excluded. Similarly with `range()` function. By default the starting index is 0, but you can modify it following this syntax below.

```python
range(start, end, step)
```

For example, you can have something like the following.

```python
>>> for item in range(10,100,10):
...     print(item)
... 
10
20
30
40
50
60
70
80
90
```

Notice again that `100` is excluded. In that range function, we put our starting number to be 10 and a step of 10. 

Range function is useful when we need an index of each character or element of a collection data type. We can rewrite our previous code where we used `enumerate()` in a different way using `range()` function. See below.

```python
name = "John Wick"
for idx in range(len(name)):
  char = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

You can check that the output the same by running it in Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20idx%20in%20range%28len%28name%29%29%3A%0A%20%20char%20%3D%20name%5Bidx%5D%0A%20%20print%28f%22Character%20%7Bchar%7D%20is%20at%20position%3A%20%7Bidx%20%2B%201%7D%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


## Using Print to Debug For Loop

Iterative structure can be complicated, especially when you have a number of computation inside the body of the loop (code block A) which is repeated. The reason is that you need to keep track at which iteration you are at and what is the state of the variables at that iteration. In this section, we will share little tips on how to keep track iterative structure using table and `print()` statement. 

Let's start with our last code.

```python
name = "John Wick"
for idx in range(len(name)):
  char = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

First, we can note that `range(len(name))` will be evaluated from the inside to the outside as what we have learned previously in [Calling a Function]({ "/notes/calling-function" | relative_url }). This means that `len(name)` will be evaluated to `9` and then Python will evaluate `range(9)`. This function calls produces a range from 0 to 8. These values will be put into the variable `idx` at every iteration. 

It is useful then, to use print statement to print `idx` values at each iteration. 

```python
name = "John Wick"
for idx in range(len(name)):
  print(idx)
```

We can setup a table to keep track the variable state at each iteration as follows.
1. Evaluate the iterable and identify the variable that is iterated at each iteration. We have done this step just now where we identify `idx` to be a range of numbers from 0 to 8. 
1. Write a table where the left column is the iterated values.
1. Write the different column to be all the expression we want to keep track. 

For example, in the above code, we can construct the following table.

| idx | name[idx] | char | idx + 1 |
|-----|-----------|------|---------|
| 0   |           |      |         |
| 1   |           |      |         |
| 2   |           |      |         |
| 3   |           |      |         |
| 4   |           |      |         |
| 5   |           |      |         |
| 6   |           |      |         |
| 7   |           |      |         |
| 8   |           |      |         |

What we have put in the columns are the various expression in the body of the loop. Looking at the code below, we identified three others besides `idx`:
- `name[idx]`
- `char`
- `idx + 1`

```python
name = "John Wick"
for idx in range(len(name)):
  char = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

Notice that the table is similar to the output of the code when it is at the following state.

```python
name = "John Wick"
for idx in range(len(name)):
  print(idx)
```

We can use both paper and `print()` statement to debug our code when we implement our solutions. Recall that **T**esting should be done together with the **I**mplementation.  Printing the elements of the iterable is the first thing we always advise novice programmers to do. This is to ensure that we know what is the elements being iterated.





## Identifying Iterative Structure in a Problem

## Decomposing Problems With Iterative Structures