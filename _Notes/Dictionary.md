---
title: Dictionary
permalink: /notes/dictionary
key: notes-dictionary
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

## Why Another Data Type?

We started introducing data types in the early lessons of this book. We started with primitive data types such as integer, float, string and boolean values. When we discussed about string data type, we noted that this data type can be tought of as a collection of characters. We then introduced another collection data type such as tuple and list. List seems useful enough for many cases and we may wonder why we need another data type.

Though it is true that list can be tought of as a kind of universal collection data type, there are many cases when it is inconvenient to use list. One of the best use of list is when we have a collection where the *sequence* of the items matters. This sequence is represented by the *index* of the item. This index is linear from 0 to $n-1$ where $n$ is the number of item in the list. However, there are many data where what matters is not the sequence of the items. We then need a more general data collection data type. 

Before we introduce this more general data type, it's useful to see a simple problem with the sequence in a list data.

Previously, we represent the number of steps that our app user in a list of list. 

```python
month_steps: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                [54, 56, 47, 62, 61, 46, 61],
                                [52, 56, 63, 58, 62, 66, 62],
                                [57, 58, 46, 71, 63, 76, 63]]
```

In this case, the first row represents the steps in the first week and the second row represents the steps in the second week and so on. However, we also showed that there are times, when it is more profitable to represent the data in its transposed. 

```python
month_steps: List[List[int]] = [[40, 54, 52, 57],
                                [51, 56, 56, 58],
                                [43, 47, 63, 46],
                                [55, 62, 58, 71],
                                [67, 61, 62, 63],
                                [56, 46, 66, 76],
                                [60, 61, 62, 63]]
```

In this second representation, the first row is for all the steps on Sundays from week 1 to week 4 and the second row is for all the steps on Mondays and so on. The problem with this list representation is that we have to *remember* that the first row is for Sundays and assumes that it is intuitive for people to know that the first day is Sunday and not Monday. But for some people, they would think that the first day is Monday rather than Sunday. The above representation does not make it easy for people to know out front whether the first row represent Sunday or Monday. 

Another example where we may need more than just a list is a codebook. Let's say your app has a feature to send encrypted message where each letter will be encrypted to another letter or emoji. Shifting the letter by the same amount is the simplest but this suffers from frequency analysis attack. Another simple way is to keep a codebook how to translate each letter to another letter. Let's say, we have the following codebook for the vocals.

```python
codebook: List[Tuple[str, str]] = [('a', 'p'), 
                                   ('e', 'f'), 
                                   ('i', 'j'), 
                                   ('o', 'c'), 
                                   ('u', 'l')]
```

The above codebook translates 'a' to 'p', 'e' to 'f' and so on. So if we have the word "hello", it will be translated to "hfllc". So what's the problem with this codebook representation. The problem is that to find what is the translated letter, we have to scan through the list one by one until we find the right pair that we need. This is not an issue for vocals such as the one above. But if we have a larger list where it has millions of pairings, we have to search for the right pairing before we can get the data that we want. The reason that we have to search one by one is that the pairings are stored in a list and we access the list based on its sequence. In our codebook case, the sequence is not important but the pairing is more important. Therefore, we need another data type that is more efficient than list for our purpose. This is what Dictionary data type comes into play.

## What is a Dictionary?

Dictionary is another collection data type that stores *key-value* pairs. In Dictionary, what matters is the pairing or the relationship between the keys and the values. The sequence of the pairs does not matter. It turns out that this data can be used for many things and is more general than list. 

Let's think for a list of numbers. Recall that we can represent the number of steps in a week in the following way.

```python
week1_steps: list[int] = [40, 50, 43, 55, 67, 56, 60]
```

We can actually represent the same data using Dictionary as follows.

```python
week1_steps: dict[int, int] = {0: 40, 1: 50, 2: 43, 3: 55, 4: 67, 5: 56, 6: 60}
```

In the above Dictionary, we have the keys from 0 to 6 which is the indices of the items in our previous list. At the same time, each of this key is paired with a value. The basic syntax to create a Dictionary is shown below.

```python
var: dict[key_type, val_type] = {key_1: value_1, key_2: value_2, ...}
```

Notice that we use curly braces to create Dictionary literal. The key-value pairs are separated using comma as usual and marked with a colon (:). 

The great thing about Dictionary is that the key is not limited to an integer sequence. We can actually represent our data in a more intuitive way.

```python
week1_steps: dict[int, int] = {"Sunday": 40, "Monday": 50, "Tuesday": 43, 
                               "Wednesday": 55, "Thursday": 67, "Friday": 56, 
                               "Saturday": 60}
```

There are some requirement for the data type of the *keys*. These are the requirements:
- unique
- hashable

The keys must be unique makes much sense similar to indices of items in a list. In a list, every item has a unique index. No two items have the same index. Similarly, in a Dictionary, no two pairings can have the same keys. Every key must be unique. 

The second requirement sounds rather fancy but this is the key why Dictionary is much better for the case of our codebook example. The keys must be *hashable*. This means that Python must be able to *hash* the keys. The word *hash* is a technical term in computing. A hash is a function that converts a data into a hash value.   Python has a built-in `hash()` function where you can try to hash some values.

```python
>>> hash("Monday")
-5612247997379553688
>>> hash("Saturday")
4116785229157965906
```
We will not go into detail of hash and hash function. What is important to remember is that Dictonary stores the keys as hash values and computer has a very efficient and fast way of finding them. This means that given a key, Python can compute the hash values and retrieve the data paired to this key in a very efficient way. This retrieval does not depend on the number of keys in the Dictionary unlike list. In a list, we have to go through one item in the list one by one and find the data we want. In a Dictionary, on the other hand, given a key, we can get our data immediately. 

In order for Python to hash the keys, the data type of the key must be of certain primitive data types which is called immutable. Here are some immutable data type in Python which you can use for Dictionary keys:
- int
- float
- string
- tuple

Notice that list is not included there since list is a mutable data type. 

With this in mind, we can now represent our steps data using Dictionary.

```python
month_steps_day: dict[str, list[int]] = {'Sunday': [40, 54, 52, 57],
                                         'Monday': [51, 56, 56, 58],
                                         'Tuesday': [43, 47, 63, 46],
                                         'Wednesday': [55, 62, 58, 71],
                                         'Thursday': [67, 61, 62, 63],
                                         'Friday': [56, 46, 66, 76],
                                         'Saturday': [60, 61, 62, 63]}
```

There are no requirements for the *value* of a key. It can be of any data type. Previously, we have integer as the value and now we have a list of integer as the value for each key. 

Another example where it is more appropriate to use Dictionary instead of a list is a profile data. Let's say your app has a profile data, you can group them in this way.

```python
profile: dict = {"name": "John Wick",
                 "email": "john@wick.ed",
                 "phone": "+6591234567",
                 "birth-year": 1980}
```

Here, we see that the values of the dictionary need not even have the same type. Name, email and phone is represented as string data while birth-year is represented as integer number. The reason why birth-year is an integer is is that we can automatically compute the age if we know the birth-year of the user. 

## Basic Operations with Dictionary Data

Now, we know what is a dictionary and how to create a Dictionary literal. In the subsequent sections, we will see how we can operate on Dictionary data. There are some common operations similar to other collection data type.

### Getting Data from Dictionary

To read data from a dictionary, we use the "get item" operator or the square bracket operator. This is similar to list. In a list, we put the index inside the square bracket. In the case of Dictionary, we put in the *key*.

```python
>>> profile['name']
'John Wick'
>>> profile['birth-year']
1980
```

Similarly, we can get the data from our month-steps dictionary.

```python
>>> month_steps_day['Wednesday']
[55, 62, 58, 71]
```

or the data from our `week1_steps`.

```python
>>> week1_steps['Wednesday']
55
```

The key in a Dictionary is analogous to the index in the list data type. What happens if you try to access a non-existing key? The answer is an error.

```python
>>> week1_steps['February']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'February'
```

The error says `KeyError` because `February` is not one of the keys in `week1_steps` dictionary. Python provides a method `get()` where we can supply a default value if the key does not exist. 

```python
>>> week1_steps.get('Wednesday')
55
>>> week1_steps.get('February', 'Error')
'Error'
```

The first argument for `get()` method is the key. The second argument which is optional is the default value if the key does not exist. 

### Modifying and Adding Dictionary Data

On top of reading the data, we can modify an existing values in Dictionary using the same get-item operator and the assignment operator. For example, we can change the name in our profile data as follows.

```python
>>> profile['name'] = "John Nice"
>>> profile
{'name': 'John Nice', 'email': 'john@wick.ed', 'phone': '+6591234567', 'birth-year': 1980}
```

In the code above, we have changed the name from "John Wick" to "John Nice". 

Now, this is where Dictionary is different from List. In a list we have a few methods to add data into the list. We have `append()` to add to the end of the list. We have `insert()` to add to a particular position in a list and we have `extend()` to extend a list with another list. Appending and inserting operations make sense in list because list has a sequence. In a sequence, it makes sense to talk about the end of a list or inserting at a particular position in a list. However, dictionary has no sequence and order. We call dictionary **unordered collection** data type. This means that there is no sequence and Python does not guarantee the sequence of the key-value pairs. Because of this, Dictionary does not have any appending and inserting operation. What Dictionary has is simpply **adding a key-value pair** into ta dictionary. 

To add a key-value pair, we use the same get-item operator and assignment operator. The only thing we have to take note is that the *key* must be some value that is not present in the existing list of keys in the dictionary. For example, we can add address into our profile data.

```python
>>> profile['address'] = "Somewhere out there."
>>> profile
{'name': 'John Nice', 'email': 'john@wick.ed', 'phone': '+6591234567', 'birth-year': 1980, 'address': 'Somewhere out there.'}
```

### Removing Data from Dictionary

To remove data from a dictionary, we can use the `del` operator and the get-item operator. This is similar to delete an item from a list. In a list, we specify `del list_name[index]`. We can do the same with dictionary keeping in mind that we need to supply the key instead of the index.

```python
>>> del profile['address']
>>> profile
{'name': 'John Nice', 'email': 'john@wick.ed', 'phone': '+6591234567', 'birth-year': 1980}
```

Once we delete the key-value pair we cannot access it again. If we try to delete it again, it will give a `KeyError` error.

```python
>>> del profile['address']
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'address'
```

This is because `address` key has been removed in the previous command. 

### Getting the Keys and the Values

There are times when it is useful to get only the keys or the values or the pairs of key-value in a dictionary. To do this, Python provides a few methods. To get all the keys, we can use `keys()` method of a dictionary.

```python
>>> profile.keys()
dict_keys(['name', 'email', 'phone', 'birth-year'])
```

Notice that this is not a list and if we need to process this data, it is helpful to convert it into a list using the conversion function.

```python
>>> list(profile.keys())
['name', 'email', 'phone', 'birth-year']
```

Similarly, we can get the values in a dictionary using `values()`.

```python
>>> profile.values()
dict_values(['John Nice', 'john@wick.ed', '+6591234567', 1980])
>>> list(profile.values())
['John Nice', 'john@wick.ed', '+6591234567', 1980]
```

We can also get the key-value pairs using `items()` method. 

```python
>>> profile.items()
dict_items([('name', 'John Nice'), ('email', 'john@wick.ed'), ('phone', '+6591234567'), ('birth-year', 1980)])
>>> list(profile.items())
[('name', 'John Nice'), ('email', 'john@wick.ed'), ('phone', '+6591234567'), ('birth-year', 1980)]
```

We can see that `items()` method gives us a sequence of key-value pairs as a tuple, i.e. `(key, value)`. 

### Traversing a Dictionary

As in any other collection data types, one of the most common operation is on how we can traverse the elements of the collections. The usual `for-in` syntax is commonly used to traverse dictionary data as well. Recall the format for `for-in` syntax in Python.

```python
for var in iterable:
  # Block A : code to repeat
  do_something_here()
```

Since dictionary is iterable, we can actually put the dictionary name as the `iterable` in the above syntax.

```python
for key in profile:
  print(key)
```

The output is shown below.

```
name
email
phone
birth-year
```

Notice that the variable `key` is not a keyword but just a variable name to capture what is thrown by the iterable at every iteration. When putting the dictionary's name, Python throws out the dictionary **keys** at every iteration. We can access the value for every key-valu pair using the get-item operator as usual.

```python
for key in profile:
  print(f"key: {key}, value: {profile[key]}")
```

The output is shown below.

```
key: name, value: John Wick
key: email, value: john@wick.ed
key: phone, value: +6591234567
key: birth-year, value: 1980
```

Notice that in the code above, we get the value using `profile[key]`. However, previously, we learnt that we can actually get both key and value from a dictionary using `.items()` method. Therefore, we can write the following code to get both key and value at every iteration.

```python
for key, value in profile.items():
  print(f"key: {key}, value: {value}")
```

The output is given below.

```
key: name, value: John Wick
key: email, value: john@wick.ed
key: phone, value: +6591234567
key: birth-year, value: 1980
```

We get the same output, but now the variable that is capturing the data at each iteration is a tuple `key, value`. Of course, there are times when we don't need the key-value pairs and maybe only need to iterate over the values. In order to do that, we can use the other methods `.values()` also mentioned in the previous section.

```python
for value in profile.values():
  print(value)
```

The output is given below.

```
John Wick
john@wick.ed
+6591234567
1980
```

Note that we can guarantee the order of the key-value pair in dictionary. 

## Using Dictionary to Implement Branch Structure

Another useful use case for dictionary data is to implement branch structure. Recall the codebook example in the beginning of this section. We want to translate certain vowels into another letter. We can actually write an if-else to do this. 

```python
message: str = "hello"
encrypted: str = ""
for char in message:
  if char == "a":
    encrypted += "p"
  elif char == "e":
    encrypted += "f"
  elif char == "i":
    encrypted += "j"
  elif char == "o":
    encrypted += "c"
  elif char == "u":
    encrypted += "l"
  else:
    encrypted += char
print(f"{message} is encrypted as: {encrypted}")
```

In the above code, we are encrypting the message, which is `"hello"`. We replaced the vowels accordingly as specified in the beginning of this lesson. If it is not a vowel, we just add back the character into the encrypted message. The output of the above code is given below.

```
hello is encrypted as: hfllc
```

However, we can use dictionary to simply the code. We can have a codebook dictionary as follows and write the encryption as shown below.

```python
message: str = "hello"
encrypted: str = ""
codebook: dict[str, str] = {'a': 'p', 
                            'e': 'f', 
                            'i': 'j', 
                            'o': 'c', 
                            'u': 'l'}
for char in message:
    if char in codebook:
        encrypted += codebook[char]
    else:
        encrypted += char
print(f"{message} is encrypted as: {encrypted}")
```

The output is shown below.

```
hello is encrypted as: hfllc
```

We have replaced the `if-else` for the translation into a single line `encrypted += codebook[char]`. We still need the if statement to check if the character is one of the vowels. If it is not, it will just put back the same character from the original message. 

One key limitation is that we can only use dictionary for branch structure where the condition is a single value. In the above example, the character is either `a` or `e` or `i` and so on. We are not able to represent a range of values. Therefore, it is hard to implement the following branch structure using dictionary.

```python
if 10 < average_steps <= 40:
    message = "Try again next month to hit your target."
elif 41 < average_steps <= 60:
    message = "Well done! You hit your target."
elif 60 < average_steps :
    message = "Extraordinary! You break a record."
```

However, for simple if-else, dictionary can make the code cleaner. This is even more so when there are many conditions. Think what would the codebook translation code look like if we also translate the consonants using if-else statement. In the case of dictionary, the code remains the same. We just need to add an extra entry into our dictionary which can be done programmatically using code.

## Graph and Breadth First Search

Let's look into some example where we can use dictionary and apply some problem solving framework. Let's say, we have a train rail network and we would like to find the path we should take from one station to another station. See example image below of an example train network. What are the stations that we have to take from station A to station F?

INSERT IMAGE HERE

The first question we may ask is how should we represent the train network in our data. How should we represent the connection between one station to another station?

One useful abstract data type is what we call a **graph**. A graph consists of vertices or nodes. These nodes are connected by edges. In our example here, we can represent each station as a vertex and the connection between two stations as an edge. Therefore, the above train network can be represented as the following graph.

INSERT IMAGE HERE

