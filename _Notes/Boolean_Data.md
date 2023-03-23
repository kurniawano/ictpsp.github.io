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
In our previous lessons, we mentioned that the branch structure is the one that gives a computer program flexibility as it allows us to do various things depending on some conditions. This also means that the branch structure depends on being able to check those conditions. 

Recall in our cadence target example in the previous lesson that we want to determine what the chatbot should do depending on whether the average cadence hits the target that the user has set or not. Whether the user hits the target or not is what we call as **Boolean** data. 

Boolean data only has two values, either it is **True** or **False**. In our example, it is whether the user hits the target (true) or it does not hit the target (false). The word Boolean comes from a Mathematician with the name [George Boole](https://en.wikipedia.org/wiki/George_Boole) who devised the boolean algebra. 

As with any other data type, you should ask, "how do we create this data?". Similarly, we should ask, how we can create Boolean data. Since Boolean data is either True or False, we usually create them through some operators. There are two kind of operators that we use to create boolean data: relational operators and logical operators.

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

We can use the equality operator to compare two strings. However, this comparison is case sensitive. In fact, string comparison takes into acount the whitespaces in the string. See the following comparison.

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

All the evaluated results are false in the three comparison above. The reason is that the way Python compares two strings is by comparing its ASCII numbering of the characters. You can see a list of ASCII numbering for different characters in [this website](https://www.asciitable.com). But notice that small letter `a` has an ASCII number of 97 while the capital letter `A` has an ASCII number er of 65. In fact, all the capital letters has a lower ASCII numberings than the small letters. That's the reason why all the above comparisons result in False.

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

On top of that Python is able to convert all its other built-in data type into Boolean data. This means that certain values are considered as False while the rest is considered as True. Let's see some of them. We are going to use the `bool()` function to convert these other data to boolean data.


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

## Evaluating Boolean Expressions

