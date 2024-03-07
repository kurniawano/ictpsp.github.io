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
name: str = "John Wick"
for char in name:
  print(char)
```
In the above code, the `iterable` is the variable `name` which is a string. Remember that `string` is one of the iterables in Python. At every iteration, an element in the string will be assigned to `char`. 

The output of that code is shown below using Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20char%20in%20name%3A%0A%20%20print%28char%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, the instruction that is repeated for every element (code block A) is the `print(char)` statement. In this case, we are instructing Python to print the element of the iterable. 

One common mistakes that many novice programmers tend to do is processing the collection as a whole when what they wanted is processing the element. An example of this logic error is printing the whole name repetitively instead of printing the characters.

```python
name: str = "John Wick"
for char in name:
  print(name)
```

In this code, what we print is the string and not the characters. See the output below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20char%20in%20name%3A%0A%20%20print%28name%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that instead of printing each character on every line, what the code does is printing the whole string on every line.

Sometimes, you just want to repeat based on the number of element in the collection. In that case, you don't really use the element in the collection. As mentioned previously, you can ignore the element using an underscore, i.e. `_`. The code below print asterisks as many as the number of characters in the password.

```python
password: str = "D0n't us3 simpl3 passw0rd#"
for _ in password:
  print('*', end='')
```

In the above code we use the option `end=''` to replace the default new line character that is always added by the print statement. By default the ending character of a line is a new line character, i.e. `\n`. This is why the next print statement is displayed in the line below. By changing the ending character to an empty string, we can display the next string in the same line. See the output using Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=password%20%3D%20%22D0n't%20us3%20simpl3%20passw0rd%23%22%0Afor%20_%20in%20password%3A%0A%20%20print%28'*',%20end%3D''%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## Enumerating a Collection

There are times when it is useful to work with both the element and the index of a collection-like data. For example, we can get both the character and its index from a string. To do this, Python provides `enumerate()` function that returns a tuple of `(index, element)`. 

```python
name: str = "John Wick"
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
name: str = "John Wick"
for idx in range(len(name)):
  char: str = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

You can check that the output the same by running it in Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=name%20%3D%20%22John%20Wick%22%0Afor%20idx%20in%20range%28len%28name%29%29%3A%0A%20%20char%20%3D%20name%5Bidx%5D%0A%20%20print%28f%22Character%20%7Bchar%7D%20is%20at%20position%3A%20%7Bidx%20%2B%201%7D%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


## Using Print to Debug For Loop

Iterative structure can be complicated, especially when you have a number of computation inside the body of the loop (code block A) which is repeated. The reason is that you need to keep track at which iteration you are at and what is the state of the variables at that iteration. In this section, we will share little tips on how to keep track iterative structure using table and `print()` statement. 

Let's start with our last code.

```python
name: str = "John Wick"
for idx in range(len(name)):
  char: str = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

First, we can note that `range(len(name))` will be evaluated from the inside to the outside as what we have learned previously in [Calling a Function]({ "/notes/calling-function" | relative_url }). This means that `len(name)` will be evaluated to `9` and then Python will evaluate `range(9)`. This function calls produces a range from 0 to 8. These values will be put into the variable `idx` at every iteration. 

It is useful then, to use print statement to print `idx` values at each iteration. 

```python
name: str = "John Wick"
for idx in range(len(name)):
  print(idx)
```

We can setup a table to keep track the variable state at each iteration as follows.
1. Evaluate the iterable and identify the variable that is iterated at each iteration. We have done this step just now where we identify `idx` to be a range of numbers from 0 to 8. 
1. Write a table where the left column is the iterated values.
1. Write the different column to be all the expression we want to keep track. 
For example, in the above code, we can construct the following table.

| idx | name[idx] | char | idx + 1 | print output | 
|-----|-----------|------|---------|--------------|
| 0   |           |      |         |              |
| 1   |           |      |         |              |
| 2   |           |      |         |              |
| 3   |           |      |         |              |
| 4   |           |      |         |              |
| 5   |           |      |         |              |
| 6   |           |      |         |              |
| 7   |           |      |         |              |
| 8   |           |      |         |              |

What we have put in the columns are the various expression in the body of the loop. Looking at the code below, we identified three others besides `idx`:
- `name[idx]`
- `char`
- `idx + 1`

```python
name: str = "John Wick"
for idx in range(len(name)):
  char: str = name[idx]
  print(f"Character {char} is at position: {idx + 1}")
```

Notice that the table is similar to the output of the code when it is at the following state.

```python
name: str = "John Wick"
for idx in range(len(name)):
  print(idx)
```

We can use both paper and `print()` statement to debug our code when we implement our solutions. Recall that **T**esting should be done together with the **I**mplementation.  Printing the elements of the iterable is the first thing we always advise novice programmers to do. This is to ensure that we know what is the elements being iterated.

We also put into the tables a few other values to keep track such as `name[id]`, `char` and `idx + 1`. We start from the first row and fill up the table. Recall that `name` is assigned to `John Wick`. 

| idx | name[idx] | char | idx + 1 | print output                  |
|-----|-----------|------|---------|-------------------------------|
| 0   | J         | J    | 1       | Character J is at position: 1 |
| 1   | o         | o    | 2       | Character o is at position: 2 |
| 2   | h         | h    | 3       | Character h is at position: 3 |
| 3   | n         | n    | 4       | Character n is at position: 4 |
| 4   |           |      | 5       | Character   is at position: 5 |
| 5   | W         | W    | 6       | Character W is at position: 6 |
| 6   | i         | i    | 7       | Character i is at position: 7 |
| 7   | c         | c    | 8       | Character c is at position: 8 |
| 8   | k         | k    | 9       | Character k is at position: 9 |

We can also use print statements to verify the expected output by displaying the expressions in the columns of the above table.

## Identifying Iterative Structure in a Problem

Iterative structure is easy to identify. Whenever you have some steps or calculation that you repeat, there you have the iterative structure. In our **D**esign of algorithm step, we can write a few drafts of the algorithm from a very raw into some pseudocode that is closer to programming language. In these earlier drafts we can try to spot if there is any steps that are being repeated. 

Let's see this by looking at an example. Given a message, we want to encrypt the message using a fibonacci sequence. Let's say we have a message as follows.

```python
message: str = """Let us cycle tomorrow at 4pm starting from City Hall"""
```

We would like, for some reason, to encrypt that message using a [Caesar Cipher](https://www.cryptomuseum.com/crypto/caesar/cipher.htm). The encryption and decryption is simple. Each letter of the plaintext is shifted down by 3 position. Here is a table of characters and its encrypted letters after shift.

| A | X |
|---|---|
| B | Y |
| C | Z |
| **D** | **A** |
| E | B |
| F | C |
| G | D |
| H | E |
| I | F |
| J | G |
| K | H |
| L | I |
| M | J |
| N | K |
| O | L |
| P | M |
| Q | N |
| R | O |
| S | P |
| T | Q |
| U | R |
| V | S |
| W | T |
| X | U |
| Y | V |
| Z | W |

Let us define our **P**roblem Statement.
- Input: A message, data type is string.
- Output: An encrypted message, data type is string.
- Process: Encrypt the input message using Caesar Cipher to produce the encrypted output message.

We can then work on our **C**oncrete Cases. Let's take in the input message as given above.

```
input: Let us cycle tomorrow at 4pm starting from City Hall
```

We are expecting an output of something like the following below.

```

```

The question we are interested in **C**oncrete Cases is how do we actually do it step by step computationally. To simplify our case, we will convert our message to all capital letters. That will be our first step.

```
input: "LET US CYCLE TOMORROW AT 4PM STARTING FROM CITY HALL"
```

After this, we will go through every letter from left to right and use the table to get the encrypted message. 

The first letter is `L`. This will be changed to the letter `I`. Then, we go to the second letter and get `E`. This is changed to the letter `B`. Then, we go to the third letter to get `T`. This is changed to the letter `Q`. And we can repeat these steps until the last letter `L` which will be changed to `I`.

Notice, that we have spot our iterative structure here. In the previous paragraph, we mentioned that we will repeate the steps until the last character. Whenever we spot some steps that is to be repeated, we find an iterative structure. 

| iteration | message | encrypted |
|-----------|---------|-----------|
| 1         | L       | I         |
| 2         | E       | B         |
| 3         | T       | Q         |
| 4         |         |           |
| 5         | U       | R         |
| 6         | S       | P         |
| 7         |         |           |
| ...       | ...     | ...       |
| 52        | L       | I         |

Now we can write our **D**esign of Algorithm.
1. Convert the input message to all capital letters.
2. Take the first character
3. Shift down the letter by 3
4. Take the second character
5. Shift down the letter by 3
6. Take the third character
7. Shift down the letter by 3
8. repeat the two steps above until the last character
9. Combine all the encrypted characters into one single string.

Here, we can identify the repetition and its iterative structure. Steps 3 to 4 is repeated from the first character to the last character. Another thing that we want to modify is step number 9. From our lesson on String, we have learnt that in Python, string data type is immutable. It means that we cannot change a string once it is created. However, we can concatenate the string. String concatenation is one of the common operations performed on string data. With this in mind, we can revise our **D**esign of Algorithm to the following.

```
input: message -> string data type
output: encrypted message -> string data type
1. Create an empty string for output, name it as *result*.
2. Convert *message* to all capital letters, name it as *message_in_caps*.
3. For each character in *message_in_caps*
   3.1 Get the character
   3.2 Shift down the character by three letters
   3.3 Concatenate the shifted letter to *result*
```

We have revised our algorithm one time. We can refine it again by looking at how we want to implement it. For example, step 1 can be done using the `upper()` method of string objects. However, how should we do step 3.2? One way to do this is to convert the character to an ASCII number and use subtraction and convert back the number to character. We have `ord()` function to change a character to its ASCII number and `chr()` to change a number to its character. 

```
input: message -> string data type
output: encrypted message -> string data type
1. Create an empty string for output, name it as *result*.
2. Convert *message* to all capital letters, name it as *message_in_caps*.
3. For each character in *message_in_caps*
   3.1 Get the character
   3.2 Change the character to ASCII number
   3.3 Subtract the ASCII number by 3
   3.4 Change the number back to character, and
   3.5 Concatenate the character to *result*
```

I hope you notice that PCDIT framework is not linear. We go back and forth even between **D**esign of Algorithm and **I**mplementation. We need to know some implementation in the programming language that we choose in order to refine our **D**esign of Algorithm. But more importantly, we also refine our **D**esign of Algorithm by identifying its repetitive structure. Now, we can do the **I**mplementation and **T** at the same time. We will write the code step by step using `print()` function in between to test the expected output. 

Let's start with a simple test code and a function definition.

```python
def encrypt(message: str) -> str:
  result: str = ""
  # your code here
  return result

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

In the function definition, we specify that our input argument is a string and this function will return the encrypted string. On top of that, we have done step 1 which is to create an empty string to store our output result.

The first thing we may want to do is simply to print the input arguments and see what kind of value and data type it is.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20print%28message%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

If you run the code to the end, you will see the input message displayed and `None`. The output `None` comes from the `print(output)`. The reason is that our function does not return anything and so by default Python returns a `None` object. This is the one displayed by `print(output)`. 

Now, let us do step 1.

```python
def encrypt(message: str) -> str:
  result: str = ""
  message_in_caps: str = message.upper()
  print(message_in_caps)
  return result

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20print%28message_in_caps%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We can observe that now we have `message_in_caps` with the message in all capital letters. Now, we are ready to start encrypting the letters. 

Now, we are going to iterate every character in `message_in_caps`. We are going to a few things for each character that will be repeated again and again. These are:

```
...
3. For each character in *message_in_caps*
   3.1 Get the character
   3.2 Change the character to ASCII number
   3.3 Subtract the ASCII number by 3
   3.4 Change the number back to character, and
   3.5 Concatenate the character to *result*
```

Let's implement this iteration using the `for-in` statement. The variable on the left-hand side of the `in` operator captures the character for each iteration. 

```python
def encrypt(message: str) -> str:
  result: str = ""
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    print(char)

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20print%28char%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In order to change the character to ASCII number as in step 3.2, we can use `ord()` function. Similarly, we can use the `chr()` function to change from ASCII to character to do step 3.4. 

```python
def encrypt(message: str) -> str:
  result: str = ""
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    print(ord(char))

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20print%28ord%28char%29%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

So we can implement steps 3.2 to 3.5 in a single line as follows.

```python
def encrypt(message: str):
  result: str = ""
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    result += chr(ord(char) - 3)
    print(result)

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20result%20%2B%3D%20chr%28ord%28char%29%20-%203%29%0A%20%20%20%20print%28result%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

However, we noticed that the spacing is not preserved. Let's say, if we want to preserve the spacing in the encrypted message as a spacing as well, we can modify our algorithm as follows.

```
input: message -> string data type
output: encrypted message -> string data type
1. Create an empty string for output, name it as *result*.
2. Convert *message* to all capital letters, name it as *message_in_caps*.
3. For each character in *message_in_caps*
   3.1 Get the character
   3.2 If the character is a space
       3.2.1 Add a space to result
   3.3 Otherwise,
       3.3.1 Change the character to ASCII number
       3.3.2 Subtract the ASCII number by 3
       3.3.3 Change the number back to character, and
       3.3.4 Concatenate the character to *result*
```

Now, we not only see iteration but we see a branch structure inside the iteration. 

```python
def encrypt(message: str):
  result: str = ""
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    if char == " ":
      result += char
    else:
      result += chr(ord(char) - 3)
    print(result)

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20if%20char%20%3D%3D%20%22%20%22%3A%0A%20%20%20%20%20%20result%20%2B%3D%20char%0A%20%20%20%20else%3A%0A%20%20%20%20%20%20result%20%2B%3D%20chr%28ord%28char%29%20-%203%29%0A%20%20%20%20print%28result%29%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Now, we can see some spaces in the encrypted message. This may be easier to break, but that's ok. This encryption, is just for fun and it's good to illustrate how we can have a branch structure inside an iteration structure. 

All this while, we still use print to test our code. Now, we can return `result` as an output of the function when we are sure this is what we want for the `encrypt()` function. The final code looks something like the following.

```python
def encrypt(message: str) -> str:
  result: str = ""
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    if char == " ":
      result += char
    else:
      result += chr(ord(char) - 3)
  return result

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20if%20char%20%3D%3D%20%22%20%22%3A%0A%20%20%20%20%20%20result%20%2B%3D%20char%0A%20%20%20%20else%3A%0A%20%20%20%20%20%20result%20%2B%3D%20chr%28ord%28char%29%20-%203%29%0A%20%20return%20result%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Oops. There is something wrong with the code. Upon checking the output. It seems that `A` is translated to `>`. In our table, above, `A` should be translated as `X`. The reason is that we do not use modular arithmetic to calculate our translation. This means that our character can exceed the range that we have specified. To ensure that the character to be kept within `A-Z`, we can do the following modular arithmetic. 

```python
def encrypt(message: str) -> str:
  result: str = ""
  base: int = ord('A')
  message_in_caps: str = message.upper()
  for char in message_in_caps:
    if char == " ":
      result += char
    else:
      result += chr((((ord(char) - base) - 3) % 26 ) + base)
  return result

input_message: str =  "Let us cycle tomorrow at 4pm starting from City Hall"
output: str = encrypt(input_message)
print(output)
```

What we did is simply set the ASCII number for `A` as the `base`. So we subtract any number by this base. This ensures the numbers are from 0 to 25 for 26 letters. Applying modulus 26 keeps the number within this range when it is subtracted by 3. When we are done, we add back `base` to get the right ASCII number. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=def%20encrypt%28message%29%3A%0A%20%20result%20%3D%20%22%22%0A%20%20base%20%3D%20ord%28'A'%29%0A%20%20message_in_caps%20%3D%20message.upper%28%29%0A%20%20%0A%20%20for%20char%20in%20message_in_caps%3A%0A%20%20%20%20if%20char%20%3D%3D%20%22%20%22%3A%0A%20%20%20%20%20%20result%20%2B%3D%20char%0A%20%20%20%20else%3A%0A%20%20%20%20%20%20result%20%2B%3D%20chr%28%28%28%28ord%28char%29%20-%20base%29%20-%203%29%20%25%2026%20%29%20%2B%20base%29%0A%20%20return%20result%0A%0Ainput_message%20%3D%20%20%22Let%20us%20cycle%20tomorrow%20at%204pm%20starting%20from%20City%20Hall%22%0Aoutput%20%3D%20encrypt%28input_message%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Now, we can see that `A` is translated correctly as `X`. 
