---
title: Boolean Data
permalink: /notes/boolean-data
key: notes-boolean-data
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

## True or False?
In our previous lessons, we mentioned that the branch structure is the one that gives a computer program flexibility, as it allows us to do various things depending on some conditions. This also means that the branch structure depends on being able to check those conditions.

Recall in our cadence target example from the previous lesson that we want to determine what the chatbot should do depending on whether the average cadence hits the target that the user has set or not. Whether the user hits the target or not is what we call **Boolean** data.

Boolean data only has two values: either it is **True** or **False**. In our example, it is whether the user hits the target (True) or does not hit the target (False). The word Boolean comes from a mathematician named George Boole (https://en.wikipedia.org/wiki/George_Boole), who devised Boolean algebra.

As with any other data type, you should ask, "How do we create this data?" Similarly, we should ask how we can create Boolean data. Since Boolean data is either True or False, we usually create it through some operators. There are two kinds of operators that we use to create Boolean data: relational operators and logical operators.

## Relational Operators

Relational operators relates two values and results in a boolean value indicating whether the relation is True or False. Below is a table of some of the common relational operators.

| operator | checking                           |
|----------|------------------------------------|
| a == b   | if a is equal to b                 |
| a != b   | if a is not equal to b             |
| a < b    | if a is less than b                |
| a <= b   | if a is less than or equal to b    |
| a > b    | if a is greater than b             |
| a >= b   | if a is greater than or equal to b |

Notice that the operator to check equality is `==` and not `=`. Recall that `=` is the assignment operator. Notice also that for checking if two values are not equal it uses `!=`. You will see the `!` operator in the logical operator again but it will have a different meaning. 

But now, let's see how we can generate boolean data from these operators. Below are some examples.

```python
>>> 3 == 4
False
>>> 4 == 4
True
>>> 3 != 4
True
>>> 4 != 4
False
>>> 3 < 4
True
>>> 4 <= 4
True
>>> 3 > 4
False
>>> 4 >= 4
True
```

You can use this relational operator not only with integer but also with float. You can also do so with string data. However, string data comparison is rather tricky. Let's see a few example.

```python
>>> 'hello' == 'hello'
True
>>> 'Hello' == 'hello'
False
```

We can use the equality operator to compare two strings. However, this comparison is case-sensitive. In fact, string comparison takes into account the whitespaces in the string. See the following comparison.


```python
>>> 'abc' == ' abc '
False
```

We will discuss on future lessons on what we should do to process string before we compare them. But for now, you need to remember that string comparison is:
- case sensitive
- takes into account the non-visible character such as whitespaces

The relational operator such as less than or greater than is also tricky. Below is a few example of what we can expect when comparing a single character string.

```python
>>> 'a' < 'b'
True
>>> 'b' < 'c'
True
>>> 'a' < 'z'
True
```

However, the below comparison may surprise some of you.

```python
>>> 'a' < 'A'
False
>>> 'a' < 'B'
False
>>> 'a' < 'Z'
False
```

All the evaluated results are False in the three comparisons above. The reason is that the way Python compares two strings is by comparing the ASCII numbering of the characters. You can see a list of ASCII numbering for different characters on this website: https://www.asciitable.com. Notice that the lowercase letter `a` has an ASCII number of 97, while the uppercase letter `A` has an ASCII number of 65. In fact, all the uppercase letters have lower ASCII numbers than the lowercase letters. That's the reason why all the above comparisons result in False.

How about comparing two strings that has more than one letter? Let's see a few results below.

```python
>>> 'abc' < 'aab'
False
>>> 'abc' < 'abd'
True
>>> 'abc' < 'abcd'
True
>>> 'abd' < 'abcd'
False
```

What can we say about those results?
- Python compares the two strings using the ASCII numbering of the characters.
- Python compares the two strings character by character from left to right. For example, `'abc' < 'aab'` because the second character comparison is false, i.e. `'b' > 'a'`. You can see this also from the second example when `'d' > 'c'`. 
- When the substring of the prefix of the string are the same, the longer string has a greater value. Most probably because a NULL character has an ASCII number of 0. You can see this from the third example where `'abc' < 'abcd'`. In this case all the first three characters are the same. The first string only has three characters but the second string has an additional character `d`. In this way, it is like comparing the ASCII of `NULL < 'd'` which results in True. 
- Since Python compares the two strings character by character from left to right, once one of the character is greater than the other, it will produce False. This is seen in the last example `'abd' < 'abcd'`. In this case, the first two characters are the same. However, the third comparisons check if `'d' < 'c'`. The result of this is False and it will stop comparing the rest of the characters. 

Python supports relational operators for all its built-in data types. This means that you can actually use the relational operators to Boolean data as well. Again some of this result may be intuitive and some may not.

```python
>>> True == True
True
>>> True < True
False
>>> True < False
False
>>> False < True
True
```

The first two results are intuitive enough. True is equal to True and since they are equal, they cannot be less than the other. The last two may not be so intuitive. Here, we have `True < False` which results in False and `False < True` which results in True. How can we understand this? 

One way to remember this is that Python encodes `False` to an integer `0` and `True` to an integer `1`. You can verify this.

```python
>>> 0 == False
True
>>> 1 == True
True
```

On top of that, Python is able to convert all its other built-in data types into Boolean data. This means that certain values are considered as False, while the rest are considered as True. Let's see some of them. We are going to use the `bool()` function to convert these other data to Boolean data.


```python
>>> bool(0)
False
>>> bool(1)
True
>>> bool(2)
True
>>> bool(-1)
True
>>> bool(0.0)
False
>>> bool(0.1)
True
>>> bool('')
False
>>> bool('False')
True
```

Notice that for integer values, 0 is considered as `False` and all other integers are considered as `True`. Similarly, for float, `0.` is considered as `False` and all other float values is considered as `True`. As about string data, an empty string `''` is considered as `False` and all other non-empty string is considered as `True`. 

Notice, however, that though empty string is considered as a False value, it is not equal to False. Only 0 and 0. is equal to False. 

```python
>>> '' == False
False
```

## Logical Operators

On top of relational operators, logical operators also evaluate to boolean data. There are three common logical operators as shown in the table below.

| operator | remarks                                                      |
|----------|--------------------------------------------------------------|
| a and b  | true if both a and b are true                                |
| a or b   | true if at least one of the operands (either a or b) is true |
| not a    | true if a is false and false if a is true                    |

In the above table, `a` and `b` can be any other expressions that can be evaluated to boolean data. This means that we can put some relational operators in either `a` and `b`.  Let's see some examples below.

```python
>>> 3 < 4 or 3 > 5
True
>>> 3 < 4 and 3 > 5
False
```

The first one is `True` because `3 < 4` evaluates to `True`. And for `or` operator to return `True` it only requires at least one of the operands to be `True`. On the other hand `and` operator requires both operands to be `True` to result in a `True` value.


```python
>>> 3 == 3 and 3 < 4
True
```

Python actuall supports using to relational operators at the same time assuming it is related by the `and` operator. See below example.

```python
>>> 2 < 3 and 3 < 4
True
>>> 2 < 3 < 4
True
```

The two expressions above are the same.

The last logical operator always invert the boolean values. 

```python
>>> not True
False
>>> not False
True
>>> not 0
True
>>> not 1
False
```

You can combine all the relational and logical operators together. It is recommended to use parentheses to clarify which order we want the operations to be evaluated.

```python
>>> (3 < 4) or (5 < 1) and True
True
>>> not( (3 < 4) or (5 < 1) and True)
False
```

## Evaluating Boolean Expressions

As with the arithmetic operators, relational and logical operators also have their precedence. This determines which operator is evaluated first. It is important to know this, as it may help us greatly in debugging our code.

Consider the below example.

```python
>>> (1 < 5) or (3 > 4) and False
True
```

At first glance, it may not be obvious why the result is True. 
- `1 < 5` results in `True`
- `3 > 4` results in `False`

The question now is whether we evaluate the `or` operator first or the `and` operator first.

If we evaluate the `or` operator first, we will get `True or False` which results in `True`. Then we evaluate the `True and False` when evaluating the `and` operator which results in `False`. 

However, what happens is that `and` has a higher precedence than `or` and Python evaluates `(3 > 4) and False` first which results in `False`. Only then, Python evaluates the `or` operator: `(1 < 5) or False` which evaluates to `True or False` resulting in a `True` value. 

Similarly, we need to know whether `not` operator has a higher precedence as compared to `and` and `or` operator. Let's figure it out using some of these examples.

```python
>>> not False or False
True
```

As can be seen above, `not` has higher precedence as compared to `or`. The reason is that `not False` is evaluated first which results in a `True` value. Only then Python evaluates `True or False` which results in a `True`. How about with regards to `and` operator?

```python
>>> not False and True
True
```

Similarly, `not` operator is evaluated first than the `and` operator in the above example which results in evaluating `True and True`. 

How about between the relational and logical operators? Which is evaluated first?

```python
>>> 3 < 0 and True
False
>>> 3 < 0 or 4 > 1
True
```

In the first example, `3 < 0` is evaluated first which results in `False`. Then Python evaluates `False and True` to produce `False` as the output. In the second example, we also evaluate the relational operators first to produce `False or True` which results in `True`. 

Let's add on these precedence to our previous table. We now have the following.

| precedence | operator | remarks                                                                                                                        |
|------------|----------|--------------------------------------------------------------------------------------------------------------------------------|
| 0          |      ()  | Parenthesis is used to evaluate the inside expression to override the precedence of the surrounding operators.                 |
| 1          | **       | Power or exponentiation operator.                                                                                              |
| 2          | * / % // | Multiplication, division, modulus and integer division. They are evaluated from left to right when appearing in a single line. |
| 3          | + -      | Addition and subtraction.                                                                                                      |
| 4          | =        | Assignment operator.                                                                                                           |
| 5          | <, <=, >, >=, !=, ==        | Relational operators.                                                                                                           |
| 6          | not      | Boolean NOT operator.                                                                                                           |
| 7          | and      | Boolean AND operator.                                                                                                           |
| 8          | or       | Boolean OR operator.                                                                                                           |

Now, we know how to evaluate boolean data. We are not ready to use it in our program especially in the *branch* and *iterative* structure. Before we move on to the *branch* structure. There is one simple useful use of boolean data in programming and that is to **T**est. This is the last part of the PCDIT framework and the way we do it is to write test and implementation in small bites repetitively. 

## Testing Using Assert

One simple way to test your code is to use the `assert` statement in Python. This is the general syntax to use `assert`.

```python
assert condition
```

The way it works is that if the `condition` is `True`, Python will continue to the next line without complaining. However, if the `condition` is `False`, Python will throw an exception or an error. This is useful when writing code because we can fill in our code with assert statements to test it, and our program will continue running as it is, as long as all those conditions are fulfilled. Only when there is an error will Python stop and tell us at which `assert` statement our test fails. Let's take a look at how we can make use of it in our PCDIT framework.

Let's look at some of the functions we have created in the past lessons. One of the first functions we created was compute_cadence_for_30sec(steps). When we are trying to write this function, instead of starting with some implementation, we can start with some **expectation**. This can be written as a series of tests. These expectations can be written based on our specifications for that problem. For example, in the function above, we expect that this function will calculate the cadence given the number of steps. We can write a few expected outputs before we write any implementation.

```python
assert compute_cadence_for_30sec(10) == 20
assert compute_cadence_for_30sec(21) == 42
assert compute_cadence_for_30sec(25) == 50
assert compute_cadence_for_30sec(31) == 62
```

Notice that the expression on the right of the `assert` statement is a Boolean expression that makes use of the relational operator `==`. We wrote those expected output of the function based on our problem spefications and even our **C**oncrete Cases that we did during our PCDIT steps. From the above expectations, which is our **T**est, we can start writing our **I**mplementation. 

```python
def compute_cadence_for_30sec(steps):
  return steps * 2

assert compute_cadence_for_30sec(10) == 20
assert compute_cadence_for_30sec(21) == 42
assert compute_cadence_for_30sec(25) == 50
assert compute_cadence_for_30sec(31) == 62
```

When you run the above code with `mypy` and `python`, you will see no complain thrown out.

```sh
$ mypy 01_compute_cadence.py 
Success: no issues found in 1 source file
$ python 01_compute_cadence.py 
$
```

You can try the above code in Python Tutor shown below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compute_cadence_for_30sec%28steps%29%3A%0A%20%20return%20steps%20*%202%0A%0Aassert%20compute_cadence_for_30sec%2810%29%20%3D%3D%2020%0Aassert%20compute_cadence_for_30sec%2821%29%20%3D%3D%2042%0Aassert%20compute_cadence_for_30sec%2825%29%20%3D%3D%2050%0Aassert%20compute_cadence_for_30sec%2831%29%20%3D%3D%2062&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that Python does not produce any output in the standard output since we do not have any `print()` statement. However, the program finishes without error. The reason that the program finishes is because our **i**mplementation fulfills all the `assert` statements, which is our expectation. 

To see what happens if we have a wrong **I**mplementation, let's try changing our implementation purposely to introduce a wrong one. Let's use `**` instead of `*` in our calculation. 

```python
def compute_cadence_for_30sec(steps: int) -> int:
  return steps ** 2

assert compute_cadence_for_30sec(10) == 20
assert compute_cadence_for_30sec(21) == 42
assert compute_cadence_for_30sec(25) == 50
assert compute_cadence_for_30sec(31) == 62
```

You can run the file `02_compute_cadence_error.py` with `mypy`.

```sh
$ mypy 02_compute_cadence_error.py 
Success: no issues found in 1 source file
```

Note that `mypy` does not complain as it does not find any error from the static check. However, running Python will throw an error.

```sh
$ python 02_compute_cadence_error.py 
Traceback (most recent call last):
  File "02_compute_cadence_error.py", line 4, in <module>
    assert compute_cadence_for_30sec(10) == 20
AssertionError
```

The error is of `AssertionError` and Python actually points out that it fails on the first `assert` statement as the output of the function is not equal to 20. 

You can also try it in Python Tutor and it will stop on the first `assert` statement.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20compute_cadence_for_30sec%28steps%29%3A%0A%20%20return%20steps%20**%202%0A%0Aassert%20compute_cadence_for_30sec%2810%29%20%3D%3D%2020%0Aassert%20compute_cadence_for_30sec%2821%29%20%3D%3D%2042%0Aassert%20compute_cadence_for_30sec%2825%29%20%3D%3D%2050%0Aassert%20compute_cadence_for_30sec%2831%29%20%3D%3D%2062&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The `assert` statement is useful in driving our implementation. As shown in the above example, we can immediately know there is a bug in our implementation since our test fails. This is part of **Test Driven Development** (TDD). In TDD, we write our test before we write any implementation. As we go along these lessons, we will share more on how to write test that drives implementation. But for now, we can see how boolean data can be used for testing our implementation. 
