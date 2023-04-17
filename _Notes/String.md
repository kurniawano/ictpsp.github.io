---
title: String
permalink: /notes/string
key: notes-string
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

## Recap: String Data

In our lesson [Basic Data Types]({{ "/notes/basic-data-types" | relative_url }}), we have introduced `string` data to represent text. In a way, `string` data is different from numbers like `int` and `float` because it consists of a sequence of **characters**. Though numbers can be thought of like a sequence of digits, however, we tend to manipulate and treat numbers as a whole. On the other hand, string is rather different. There are many occasions that we want to manipulate some of the substrings in a particular string or even some of its characters. For example, in many text processing, we want to remove the leading and trailing whitespaces in the string as they may not be meaningful for our data processing. Those whitespaces are part of a string. Therefore, it is important to be able to manipulate not only the string as a whole but also its substrings and characters inside the string. In this way, a string is like a **collection** of characters which we want to process. We will introduce another *collection* data type in the future, but for now, string is a good way to introduce how computing processes these kind of collection-like data. 

Let's recap again on how we can create `string` data. We can create string data using either a single quote or a single double quote.

```python
str1 = 'This is a string data.'
str2 = "This is another string data."
```

We have also discussed on why Python have these two kinds of string delimiters. Other programming language may only have one way of creating a string data. For Python, it is one simply way to create a string whenenver there is an apostrophe or quotes inside that string. See example, below.

```python
print("How're you?")
print('The actor exclaimed, "To be or not to be"')
```

In the the first example, we have a single apostrophe in the string. Therefore, we use the double quotes as the string delimiter. It's the other way around for the second example which contains quotes in the string data. 

We can create multi-line string data using **triple** single quotes or **triple** double quotes. 

```python
data = '''
Two roads diverged in a yellow wood,
And sorry I could not travel both
And be one traveler, long I stood
And looked down one as far as I could
To where it bent in the undergrowth;

Then took the other, as just as fair,
And having perhaps the better claim,
Because it was grassy and wanted wear;
Though as for that the passing there
Had worn them really about the same,

And both that morning equally lay
In leaves no step had trodden black.
Oh, I kept the first for another day!
Yet knowing how way leads on to way,
I doubted if I should ever come back.

I shall be telling this with a sigh
Somewhere ages and ages hence:
Two roads diverged in a wood, and I—
I took the one less traveled by,
And that has made all the difference.

-- by Robert Frost
'''
```

We can do the same with a triple double quotes.
```python
data = """
“Hope” is the thing with feathers -
That perches in the soul -
And sings the tune without the words -
And never stops - at all -

And sweetest - in the Gale - is heard -
And sore must be the storm -
That could abash the little Bird
That kept so many warm -

I’ve heard it in the chillest land -
And on the strangest Sea -
Yet - never - in Extremity,
It asked a crumb - of me.

-- by Emily Dickinson
"""
```

Notice that in the above data, it contains both double quotes in the first line and a single quote in `I've heard...`. So triple quotes can handle those in a single string without any issue. 

## Basic String Operations

Previously, in our lesson [Basic Operators]({{ "/notes/basic-operators | relative_url }}), we have also introduced two simple operators that can be used with string data: the concatenation `+` operator and the duplication `*` operator. Let's review it again here.

We can concatenate two strings using the `+` operator. 

```python
>>> first_name = "John"
>>> last_name = "Wick"
>>> full_name = first_name + last_name
>>> print(full_name)
JohnWick
```

Oops. The concatenated string does not have a space. But we can fix that by concatenating a space in between.

```python
>>> full_name = first_name + " " + last_name
>>> print(full_name)
John Wick
```

This kind of operation is useful in many applications since usually the user profile is stored as first name and last name. You can display the full name in the profile by concatenating the two strings.  Similarly, with data like home address where you need to concatenate the road address, unit number and its postal code. 

We have also introduced the duplication operator `*`. For example, we can create an ASCII artwork as below.

```python
data = 3 * " " + "*" + "\n"
data += 2 * " " + 3 * "*" + "\n"
data += 1 * " " + 5 * "*" + "\n"
data += 3 * " " + "*" + "\n"
data += 3 * " " + "*" + "\n"
print(data)
```

You can see the output by running it in Python Tutor below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=data%20%3D%203%20*%20%22%20%22%20%2B%20%22*%22%20%2B%20%22%5Cn%22%0Adata%20%2B%3D%202%20*%20%22%20%22%20%2B%203%20*%20%22*%22%20%2B%20%22%5Cn%22%0Adata%20%2B%3D%201%20*%20%22%20%22%20%2B%205%20*%20%22*%22%20%2B%20%22%5Cn%22%0Adata%20%2B%3D%203%20*%20%22%20%22%20%2B%20%22*%22%20%2B%20%22%5Cn%22%0Adata%20%2B%3D%203%20*%20%22%20%22%20%2B%20%22*%22%20%2B%20%22%5Cn%22%0Aprint%28data%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We used a few operators here. The most common one is actually the assignment operator `=`. In the first line, we created the first string and assign it to the name `data`. How did we create the first string? We have the following line.

```python
data = 3 * " " + "*" + "\n"
```

In this line of code, we duplicate a single space string `" "` three times and concatenate it with a single asterisk. At the end we added a **newline character**  `"\n"` so that the next string added will be printed into a new line.  The second line added the next line to the string.

```python
data += 2 * " " + 3 * "*" + "\n"
```

In this code, we use the compound operator `+=` which is equivalent to `data = data + something`. That something is the expression on the right hand side. It does a few thing. First it duplicates the space two times and concatenate with the asterisk that is duplicated three times (`***`). Lastly, it is concatenated with a newline character again. By now, you should be able to guess what the other lines do. The result is a simple christmas tree.

```
   *
  ***
 *****
   *
   *
```

On top of that, we also learned that we can compare strings in our lesson [Boolean Data]({{ "/notes/boolean-data" | relative_url }}). We can use the relational operators such as `<`, `<=`, `>`, `>=`, `==`, `!=`. In many cases, we are actually interested to compare if two strings are equal or not equal. A common example is in many website form or login when we want to compare whether the user is in a database.

```python
>>> name_entered = 'John the Wick'
>>> name_in_database = 'John Wick'
>>> print(name_entered == name_in_database)
False
```

## Collection Operators

Now, we will introduce a few new operators that works in a collection-like data type. We mention that though string data can be considered as a collection of characters inside that string. There are some common operations that we usually do with collection-like data.

### Check If Substring is in a String

The first one maybe is simply to check if some item is inside a collection. In the case of `string` data, we may want to check if a character is inside a string or if a substring is inside a string.  In this case we use the `in` operator. This operator evaluates to a boolean data because it is either true, when the substring is inside the  string, or false, when the substring is not inside  string. 

```python
>>> char = 'a'
>>> vowel = 'aiueo'
>>> print(char in vowel)
True
```

Similarly, we can do the same for a substring.

```python
>>> first_name = 'John'
>>> full_name = 'John Wick'
>>> print(first_name in full_name)
True
```

### Getting the Length of the String

It is very useful to know what is the length of a collection. This means like how many items are there in a list. In the case of string data, we are interested to know what is the length of the string or how many characters are there in the string. This is done simply using the `len()` built-in function provided by Python. 

```python
>>> name = "John Wick"
>>> print(len(name))
9
```

You can count manually to verify whether "John Wick" has nine characters. 


### Getting an Element

Another common operation in collection-like data is to get an element from the collection. In our string data, we may want to get the first character or the last character. To do this we will use the **bracket** operator where we specify the **index** inside the bracket. The index starts from 0 in Python. 

| index     | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|-----------|---|---|---|---|---|---|---|---|---|
| character | J | o | h | n |   | W | i | c | k |

We can get the different characters by specifying the index inside the bracket operator. The bracket operator is also called the **Get Item** operator.

```python
>>> name = "John Wick"
>>> print(name[0])
J
>>> print(name[5])
W
>>> print(name[8])
k
```

You can also use **negative indexing** with the bracket operator. 

| index     | -9 | -8 | -7 | -6 | -5 | -4 | -3 | -2 | -1 |
|-----------|----|----|----|----|----|----|----|----|----|
| character | J  | o  | h  | n  |    | W  | i  | c  | k  |

```python
>>> name = "John Wick"
>>> print(name[-9])
J
>>> print(name[-4])
W
>>> print(name[-1])
k
```

Notice that we can get the same characters either using the positive indexing or the negative indexing. It is, however, very convinient to get the last character using the index `-1`. Otherwise, we will need to know the length of the string or the collection.  The last character is always **the length of the string minus one**. 

```python
>>> name = "John Wick"
>>> print(name[len(name) - 1])
k
>>> print(name[-1])
k
```

The reason that the last character is always length of string minus one is that Python starts its indexing from 0. As shown in the table above, the last character has the index of 8 when the length of string is 9. 

### Getting a Substring from a String

Not only we can get a character from a string, we can also slice a substring from a string. This **slicing** operation makes use of the same **Get Item** operator (or the bracket operator). The only difference is that the argument inside the bracket is a slice that contains double colon.

```python
[start:end:step]
```

The only point to take note is that **end index** is excluded from the sliced substring. To illustrate. Let's put back here our table and try a few slicing operations. 

| index     | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|-----------|---|---|---|---|---|---|---|---|---|
| character | J | o | h | n |   | W | i | c | k |

```python
>>> name = "John Wick"
>>> print(name[0:3])
Joh
>>> print(name[3:6])
n W
```

In the first slice, we start with index `0` and end at index `3`. Notice that index 3 refers to the letter `n` in `John`. However, what is printed is only `Joh` without the `n` character. This is to emphasize that the ending index is **excluded** in the slice. 

What's the reason for this? Python developers find it easier to obtain the length of the slice from the two indices. When we have `name[0:3]`, we can immediately subtract the two indices $3-0 = 3$ which gives us the length of the sliced substring `Joh`. 

We can see similar behaviour in `name[3:6]`. In this case, index 3 is on character `n` while index 6 is on character `i` after the letter `W`. However, the output simply prints `n W` which contains three character as you can calculate from the two indices. 

When the slicing starts from the beginning or all the way to the end, you can remove the index from the slice. Python will use those first index and all the way to the last element as default values. See the two examples below.

```python
>>> print(name[:4])
John
>>> print(name[5:])
Wick
```

You can also provide steps in the slicing. So if you would like to get every other characters from the string, you can do something like the following.

```python
>>> name = "John Wick"
>>> print(name[::2])
Jh ik
>>> print(name[1::2])
onWc
```

The first slicing is from the beginning to the end with a step of two characters. Therefore, it starts from the first character (`J`) and then the third character (`h`) and so on. The second example put the starting index as 1 which is the second character. The second output gives you characters from the second to the end with every two steps. 

You can use negative indexing in slicing though it may become rather confusing. Let's see one example here.

```python
>>> print(name[-1:-10:-1])
kciW nhoJ
>>> print(name[::-1])
kciW nhoJ
```

In the first insance, we use the starting index to be -1 which is the last character and all the way to the character position before the first character. See from above table that the first character is at -9 index. Here, we put the ending index to be -10 which is one before the first character. We need to do this because the ending index is excluded. Notice also that we put the step to be -1. In the second example, we do exactly the same without specifying the starting and ending index. Python can figure out that you want to take the whole string and reverse it from the negative index in the step argument. 

Use negative index sparingly and only when it clarifies what you are trying to do. Try to use positive indexing as it is clearer in many cases.

## String is Immutable

Different programming language may implement string data type differently. Python makes its `string` data type to be **immutable**. Immutable means that you cannot change it. Once you create a string, you cannot edit it or change it.

```python
>>> name = "John Wick"
>>> name[0] = 'Z'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'str' object does not support item assignment
>>> 
```

Notice that the error says string data does not support item assignment. The assignment operator does not work with string data because string is immutable. How can you change the string then? The answer is that you cannot. But you can create a new string.

For example, in the above case when we want to change the first character to `'Z'`, we can do the following.

```python
>>> name = 'Z' + name[1:]
>>> print(name)
Zohn Wick
```

Here, we managed to change the name from John Wick to Zohn Wick. What is important here is that `name` variable points to a new string. In order to illustrate this, we will use the built-in function `id()` to check its identity which depends on where it is located in the memory address. 

```python
Zohn Wick
>>> name = "John Wick"
>>> id(name)
140450800593904
>>> name = 'Z' + name[1:]
>>> id(name)
140450800593840
```

Notice that the variable `name` has two different identities number. 

A number data types in Python are actually immutable such as `int` and `float`. You can check it out in the same manners.

```python
>>> a = 1
>>> id(a)
4544481632
>>> a = 2
>>> id(a)
4544481664
>>> b = 3.
>>> id(b)
140450263065232
>>> b = 3.14
>>> id(b)
140450531292976
```

What happens with every assignment is that Python creates a new binding to a new `int` or `float` objects. This is what Python does with `string` object as well. 

## String Formatting

There are several ways to format string data. This is particularly useful when you have a combination of string with other data type to be displayed as string literals. In this lesson, we will introduce Python's formatted string literals to achieve this.

Python's formatted string literals start with `f` or `F` before the string quotes. Inside this string, you can write Python's expression within `{}`. Let's see some example.

```python
>>> name = "John Wick"
>>> greeting = f"Good day, {name}!"
>>> print(greeting)
Good day, John Wick!
```

Notice that we put the variable name as the expression within the `{}`. Not only variables, you can actually put any Python's expression there. For example, we can call the `len()` function inside this formatted string literals.

```python
>>> reply = f"My name, {name}, has {len(name)} characters."
>>> print(reply)
My name, John Wick, has 9 characters.
```

You can format how you want to display the evaluated data inside the `{}` in several ways. For example, you can specify the minimum width. You do this by putting `:X` after the expression where `X` is a number specifying the width.

```python
>>> reply = f"My name, {name:15}, has {len(name):10d} characters."
>>> print(reply)
My name, John Wick, has 9 characters.
>>> print(reply)
My name, John Wick      , has          9 characters.
```

You may notice some extra space in `John Wick      ` at the end of the name and some extra space in `         9` before the number 9. What happens is that Python reserves 15 spaces for `name` and 10 spaces for `len(name)`. You may also notice that for string data it is left-aligned by default while for number data is right-aligned. You can change this using the alignment format specifier, i.e. `<` for left-aligned and `>` for right-aligned.

```python
>>> reply = f"My name, {name:>15}, has {len(name):<10d} characters."
>>> print(reply)
My name,       John Wick, has 9          characters.
```

You may notice there is a `d` in `10d`. That type specification can be used to format various number data type. You can change it to binary, hex, or octal. The complete table is given below.

| Type | Meaning                                                                                                                                                                    |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 'b'  | Binary format. Outputs the number in base 2.                                                                                                                               |
| 'c'  | Character. Converts the integer to the corresponding unicode character before printing.                                                                                    |
| 'd'  | Decimal Integer. Outputs the number in base 10.                                                                                                                            |
| 'o'  | Octal format. Outputs the number in base 8.                                                                                                                                |
| 'x'  | Hex format. Outputs the number in base 16, using lower-case letters for the digits above 9.                                                                                |
| 'X'  | Hex format. Outputs the number in base 16, using upper-case letters for the digits above 9. In case '#' is specified, the prefix '0x' will be upper-cased to '0X' as well. |
| 'n'  | Number. This is the same as 'd', except that it uses the current locale setting to insert the appropriate number separator characters.                                     |
| None | The same as 'd'.                                                                                                                                                           |

You may guess that for floating point number, there are a number of ways you want to display such as the number of decimal points or in a scientific notation instead. In this case the format is `expression:W.dt`, where:
- `expression` is the expression to be displayed in the string literal.
- `W` is the total width including the decimal point and its decimal numbers.
- `d` is the number of decimal point to be displayed.
- and `t` is the format type. 

Below are some examples.

```python
>>> from math import pi
>>> f"Pi number is: {pi}"
'Pi number is: 3.141592653589793'
>>> f"Pi number is: {pi:10.2f}"
'Pi number is:       3.14'
>>> f"Pi number is: {pi:5.2e}"
'Pi number is: 3.14e+00'
```

The table for the floating point type is shown below and was taken from Python's [Format String Syntax documentation](https://docs.python.org/3/library/string.html#formatstrings).

| Type | Meaning                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
|------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 'e'  | Scientific notation. For a given precision p, formats the number in scientific notation with the letter ‘e’ separating the coefficient from the exponent. The coefficient has one digit before and p digits after the decimal point, for a total of p + 1 significant digits. With no precision given, uses a precision of 6 digits after the decimal point for float, and shows all coefficient digits for Decimal. If no digits follow the decimal point, the decimal point is also removed unless the # option is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 'E'  | Scientific notation. Same as 'e' except it uses an upper case ‘E’ as the separator character.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 'f'  | Fixed-point notation. For a given precision p, formats the number as a decimal number with exactly p digits following the decimal point. With no precision given, uses a precision of 6 digits after the decimal point for float, and uses a precision large enough to show all coefficient digits for Decimal. If no digits follow the decimal point, the decimal point is also removed unless the # option is used.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| 'F'  | Fixed-point notation. Same as 'f', but converts nan to NAN and inf to INF.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 'g'  | General format. For a given precision p >= 1, this rounds the number to p significant digits and then formats the result in either fixed-point format or in scientific notation, depending on its magnitude. A precision of 0 is treated as equivalent to a precision of 1. The precise rules are as follows: suppose that the result formatted with presentation type 'e' and precision p-1 would have exponent exp. Then, if m <= exp < p, where m is -4 for floats and -6 for Decimals, the number is formatted with presentation type 'f' and precision p-1-exp. Otherwise, the number is formatted with presentation type 'e' and precision p-1. In both cases insignificant trailing zeros are removed from the significand, and the decimal point is also removed if there are no remaining digits following it, unless the '#' option is used. With no precision given, uses a precision of 6 significant digits for float. For Decimal, the coefficient of the result is formed from the coefficient digits of the value; scientific notation is used for values smaller than 1e-6 in absolute value and values where the place value of the least significant digit is larger than 1, and fixed-point notation is used otherwise. Positive and negative infinity, positive and negative zero, and nans, are formatted as inf, -inf, 0, -0 and nan respectively, regardless of the precision. |
| 'G'  | General format. Same as 'g' except switches to 'E' if the number gets too large. The representations of infinity and NaN are uppercased, too.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| 'n'  | Number. This is the same as 'g', except that it uses the current locale setting to insert the appropriate number separator characters.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| '%'  | Percentage. Multiplies the number by 100 and displays in fixed ('f') format, followed by a percent sign.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| None | For float this is the same as 'g', except that when fixed-point notation is used to format the result, it always includes at least one digit past the decimal point. The precision used is as large as needed to represent the given value faithfully. For Decimal, this is the same as either 'g' or 'G' depending on the value of context.capitals for the current decimal context. The overall effect is to match the output of str() as altered by the other format modifiers.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |


## Summary

In this section, we have dived slightly deeper on `string` data type. We review how to create string literals and some of basic operations that are common to string data. String can be thought of as a collection-like data where we can process the sequence of characters inside this string. In this lesson, we focus more on how to slice some substring from a given string. In the next lesson, we will learn how to iterate over each character. At the end, we emphasise that string is immutable data type in Python. This means that we cannot change it once it is created in the memory. We also showed some simple way to format string using Python's formatted string literals. 