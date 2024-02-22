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

Let's look into some example where we can use dictionary and apply some problem solving framework. Let's say, our app can plan a cycling path and we would like to find the path we should take from one place to another place. See example image below of an example map. What are the path we should take from point A to point F?

INSERT IMAGE HERE

The first question we may ask is how should we represent the map in our data. How should we represent the connection between one place to another place?

One useful abstract data type is what we call a **graph**. A graph consists of vertices or nodes. These nodes are connected by edges. In our example here, we can represent each place and junction as a vertex and the connection between two junctions as an edge. Therefore, the above map can be represented as the following graph.

INSERT IMAGE HERE

How can we represent this graph as our data? We can use a dictionary for this. In using the dictionary, we should ask ourselves what are the keys and the values. We can choose the vertices as the keys. Every graph has vertices and these vertices can be the keys in our dictionary. Moreover, each vertex can have some neighbouring vertices. These neighbours can the values for each key. We can then represent the the above graph as follows.

```python
cycling_map: dict[str, list[str]] = {"A": ["B", "D"],
                                     "B": ["A", "C"],
                                     "C": ["B", "D", "F"],
                                     "D": ["A", "C", "E"],
                                     "E": ["D", "F"],
                                     "F": ["C", "E"]}
```

Given the above data, the problem now becomes finding the path from A to F. Usually, we want to find the shortest path and the longest path. So the shortest path is assumed in this problem. We will also make another assumption to simplify our problem. We will assume that it takes the same effort to travel from one point to another. This assumption may not be true and there are ways to represent this in our dictionary. But for now, to simplify our problem, we will assume that it takes the same effort to travel from one point to another and we are only interested to find the shortest path from point A to F. 

### (P)roblem Definition

We will start with our problem definition and try to identify the input, output and summarize the problem into a statement.

```
Input: 
  - map: dictionary[key: string, value: list of string]
  - start point: string
  - end point: string

Output:
  - path: list of string in the map that gives the shortest path

Problem Statement:
  Given a map, starting point and ending point in the dictionary,
  the function should return a shortest path from starting point
  to ending point in the map.
```

How should we approach this problem? Let's start working on this concrete case step by step and generalize the algorithm.

### Concrete (C)ases

Let's start with our input. We have three inputs. The first one is the map and it is represented by the dictionary as follows.

```python
cycling_map: dict[str, list[str]] = {"A": ["B", "D"],
                                     "B": ["A", "C"],
                                     "C": ["B", "D", "F"],
                                     "D": ["A", "C", "E"],
                                     "E": ["D", "F"],
                                     "F": ["C", "E"]}
```

The second input is our starting point. In this case, let's choose a path from A. The last input is our ending point. Let's choose the point F as our destination. We can see that we have a few paths from A to F.

```
path 1: A -> B -> C -> F
path 2: A -> B -> C -> D -> E -> F
path 3: A -> D -> E -> F
```

With our assumptions, we can either choose path 1 or path 3 as our solutions as it has shorter path or smaller number of points. How do we come to these paths?

We start with the second input which is the starting vertex, i.e. A. What we can do now is too look into the neighbours of A. We can get A's neihbours from the dictionary. A has two neighbours, i.e. `["B", "D"]`. What we do is that we can put these to vertices into a list to visit.

```python
to_explore: List[str] = ["B", "D"]
```
The sequence may matter in this case. In the above, we choose to put into list alphabetically. This means that we put B first ahead of D. But we can choose otherwise. What do we do with this list? We can take out the item from the list and do the same thing as we did with A. 

This means that we take out B from the list and find the neighbours of B. Looking into our dictionary, we notice that B has two neighbours, i.e `["A", "C"]`. However, we have visited A and we don't want to go back to A. So we must keep track of those vertices we have visited. Moreover, we also don't want to explore B and D again since we have done that. So we should keep track all these vertices that we have visited. What's the strategy? Well, we can put all those we put into the `to_explore` list into another list called `visited`. We didn't really put A into the `to_explore` list. But we can do this actually. In the beginning, we can add A into the `to_explore` list and `visited` list. Then we take out A from the `to_explore` list to get its neighbours. Let's create a new list for all those vertices we have visited. By now, it should contain A, B and D.

```python
visited: List[str] = ["A", "B", "D"]
```

Now, what we do is that before we add anything to the list `to_explore`, we will check if the vertex is already inside `visited` list. If  the vertex is not the `visited` list, we can add that vertex to the list `to_explore`. In this case, only C will be added.


```python
to_explore: List[str] = ["D", "C"]
visited: List[str] = ["A", "B", "D", "C"]
```

Since we add all the neighbours of B, we can visit the neighbours of the next vertex in the list `to_explore`. Now, D is next. So we take out D from the list and find its neighbours. The neighbours of D are `["A", "C", "E"]`. But A and C are already in the `visited` list. So this leaves us only with E. 


```python
to_explore: List[str] = ["C", "E"]
visited: List[str] = ["A", "B", "D", "C", "E"]
```

We will do the same steps. You can see that there is iteration structure here as we do the same steps again and again. We take out C from the list `to_explore` and get its neighbours, i.e. `["B", "D", "F"]`. Out of these three, B and D are in the `visited` list. Therefore, we will not add these two and only add F. But F is actually our destination and we have found our destination!

But how do we get a path? In the above examples, our path is `A -> B -> C -> F`. How can we return a list describing the sequence points in this path? We can do that if we keep track how we visit one vertex to another and how do we get to our destination vertex.

How can we keep track? Everytime we explore a vertex from another vertex, we can keep track which vertex is the previous vertex of the new vertex we visited. For example, when we start from A and visit B and D at the beginning, we can create a new dictionary indicating, who is the parent of B and D. The word parent here refers to the previous vertex from which B and D were visited.

```python
parent: dict[str, str] = {"B": "A",
                          "D": "A"}
```

In the above dictionary, we take not that the parent of B is A and the parent of D is also A. Similarly, when we visit C from B, we will add this into our `parent` dictionary.

```python
parent: dict[str, str] = {"B": "A",
                          "D": "A",
                          "C": "B"}
```

Next, we actually explore D to visit C. So now we have the following.

```python
parent: dict[str, str] = {"B": "A",
                          "D": "A",
                          "C": "B",
                          "E": "D"}
```

After we explore D, we explore C. From C we visit F and found our destination. So our final dictionary is the following.

```python
parent: dict[str, str] = {"B": "A",
                          "D": "A",
                          "C": "B",
                          "E": "D",
                          "F": "C"}
```

How, can then we generate the sequence of points in the path? This time, we will start with our destination F. We add this to our output path list.

```python
path: list[str] = ["F"]
```

From F we find the parent from our dictionary and get C. So we add C into the list.

```python
path: list[str] = ["C", "F"]
```

Notice that we have to add C to the front of F in the sequence. Then we check the parent of C and find B. We add this again to our list.

```python
path: list[str] = ["B", "C", "F"]
```

Lastly, from B's parent, we get A and add this to our list.

```python
path: list[str] = ["A", "B", "C", "F"]
```

We can stop now because A has no parent and A is our starting point. Now we are able to generate our output from our three inputs. Let's generalize these steps in our Design of Algorithm step.

### (D)esign of Algorithm

There are a lot of steps in the previous section. It is useful to reread these section again whenever you get lost in this part here. What we do as our first step is to initialize a few list and dictionary.

```
1. Create an empty list for *visited* and *to_explore*. 
   Create an empty dictionary for *parent*.
```

Next, we can start from our starting point and add this into our `to_explore` list.

```
1. Create an empty list for *visited* and *to_explore*. 
   Create an empty dictionary for *parent*.
2. Add start vertex to *to_explore* list.
```

Reading the Concrete (C)ases section again reveals that once we reach this point, we started to repeat a few steps again and again. What are the steps that we repeat?

```
1. Take out the next vertex to explore from the *to_explore* list.
2. Get the neighbours of this vertex.
```

What do we do with the neighbours of the vertex we want to explore? We do a few things. First we check if this neighbouring vertex is our destination vertex or not. If it is, then we are done. If it is not, we will add into our list to explore. But we only want to add those vertices that we have not visited. So let's write down the steps.

First, we handle the case when we found the destination vertex.

```
1. For every vertex in the neighbouring vertex, do
   1.1 if this neighbouring vertex is our destination vertex, do
       1.1.1 Add this neighbouring vertex to the *parent* dictionary
       1.1.2 Exit the search
```
If the neighbouring vertex is not the destination vertex we will add them into the list to explore.

```
1. For every vertex in the neighbouring vertex, do
   1.1 If this neighbouring vertex is our destination vertex, do
       1.1.1 Add this neighbouring vertex to the *parent* dictionary
       1.1.2 Exit the search
   1.2 Otherwise, if the neighbouring vertex is not in the *visited* list, do
       1.2.1 Add the neighbouring vertex to the *visited* list
       1.2.2 Add the neighbouring vertex to the *to_explore* list
```

We can now embed the above steps into our steps after we get the neighbours of our vertex to explore. 

```
1. Take out the next vertex to explore from the *to_explore* list.
2. Get the neighbours of this vertex.
3. For every vertex in the neighbouring vertex, do
   3.1 If this neighbouring vertex is our destination vertex, do
       3.1.1 Add this neighbouring vertex to the *parent* dictionary
       3.1.2 Exit the search
   3.2 Otherwise, if the neighbouring vertex is not in the *visited* list, do
       3.2.1 Add the neighbouring vertex to the *visited* list
       3.2.2 Add the neighbouring vertex to the *to_explore* list
```

Previously, we mentioned that we need to repeat these steps again and again. The question now is until what condition do we repeat the steps above? We can continue doing this as long as there is a vertex in the `to_explore` list. If there is no more, we can stop exploring. So let's add the iterative structure into the above steps. 

```
1. As long as there is an item in *to_explore* list
   1.1 Take out the next vertex to explore from the *to_explore* list.
   1.2 Get the neighbours of this vertex.
   1.3 For every vertex in the neighbouring vertex, do
       1.3.1 If this neighbouring vertex is our destination vertex, do
             1.3.1.1 Add this neighbouring vertex to the *parent* dictionary
             1.3.1.2 Exit the search
       1.3.2 Otherwise, if the neighbouring vertex is not in the *visited* list, do
             1.3.2.1 Add the neighbouring vertex to the *visited* list
             1.3.2.2 Add the neighbouring vertex to the *to_explore* list
```

We can then combine these iterative structure into our overall steps.

```
1. Create an empty list for *visited* and *to_explore*. 
   Create an empty dictionary for *parent*.
2. Add start vertex to *to_explore* list.
3. As long as there is an item in *to_explore* list
   3.1 Take out the next vertex to explore from the *to_explore* list.
   3.2 Get the neighbours of this vertex.
   3.3 For every vertex in the neighbouring vertex, do
       3.3.1 If this neighbouring vertex is our destination vertex, do
             3.3.1.1 Add this neighbouring vertex to the *parent* dictionary
             3.3.1.2 Exit the search
       3.3.2 Otherwise, if the neighbouring vertex is not in the *visited* list, do
             3.3.2.1 Add the neighbouring vertex to the *visited* list
             3.3.2.2 Add the neighbouring vertex to the *to_explore* list
```

These are the steps up to the point we find the destination point. But we have not come up with the steps to get the sequence of points in the path. What we did was to `exit the search` in step 3.3.1.2 when we find the destination vertex. Let's write down the steps to get the sequence of points in the path. 

In order to do this, we need to have the `parent` dictionary. Given the `parent` dictinary, the starting point and the destination point, we can craft steps to get the sequence as described in the Concrete (C)ases section. 

We start by adding the destination vertex into our output path.

```
1. Add destination vertex into output list.
```

The next few steps are repeated again and again until we reach starting vertex. So we can write the following iterative structure.

```
1. Add destination vertex into output list.
2. Get the parent of the current vertex.
3. As long as the parent is not the starting vertex, do
   3.1
```

What do we do in step 3? we simply make this parent vertex as our current vertex and get its parent from the dictionary again. We also add these vertices into our output path into the *first* position (refer to the Concrete Cases in case you forget why we insert into the first position). 


```
1. Add destination vertex into output list.
2. Get the parent of the current vertex.
3. As long as the parent is not the starting vertex, do
   3.1 Make this parent vertex as the current vertex
   3.2 Add the current vertex into the output path at the first position
   3.3 Get the parent of the current vertex from the *parent* dictionary
```

We keep on repeating steps 3.1 to 3.3 as long as this parent vertex is not the starting vertex. If it is, then we are done repating and simply add the last vertex, which is the starting vertex into the output path.

```
1. Add destination vertex into output list.
2. Get the parent of the current vertex.
3. As long as the parent is not the starting vertex, do
   3.1 Make this parent vertex as the current vertex
   3.2 Add the current vertex into the output path at the first position
   3.3 Get the parent of the current vertex from the *parent* dictionary
4. Add the parent of the current vertex into the output path at the first position
```

Let's implement and test these steps. 

### (I)mplement and (T)est

As shown in the previous section, we can actually breakdown our solution into two distinct steps. The first one is to get the parent dictionary. Once we have this parent dictionary, the second step is to get the list of points in our path. So we will create three functions for this. The first one is the overall function which will call the other two functions. 

We start with the following function headers.

```python
def create_path(start: str,
                end: str,
                map: dict[str, list[str]]) -> dict[str, str]:
    parent_tree: dict[str, str] = {}
    # our code here
    return parent_tree

def get_path(start: str,
             end: str,
             parent_tree: dict[str, str]) -> list[str]:
    path: list[str] = []
    # our code here
    return path

def get_cycling_path(start: str, 
                     end: str, 
                     map: dict[str, list[str]]) -> list[str]:
    parent_tree: dict[str, str] = create_path(start, end, map)
    output_path: list[str] = get_path(start, end, parent_tree)
    return output_path
```

We save the above file into `cycling_path.py`. We have also indicated the type hints for the input and output of each function. We can run mypy on this and it should return no error.

```sh
$ mypy cycling_path.py 
Success: no issues found in 1 source file
```

Notice that in `get_cycling_path()` function, we call the other two functions which are `create_path()` and `get_path()`. We will now work on writing test and implementation for each of these two functions. 

Let's start with `create_path()` function. To test it, we need to create our dictionary and provide the input.

```python
cycling_map: dict[str, list[str]] = {"A": ["B", "D"],
                                     "B": ["A", "C"],
                                     "C": ["B", "D", "F"],
                                     "D": ["A", "C", "E"],
                                     "E": ["D", "F"],
                                     "F": ["C", "E"]}
parent_tree: dict[str, str] = create_path("A", "F", cycling_map)
print(parent_tree)
```

We will now only show the code inside `create_path()` using the test code above. Running mypy and python on the file now produces an empty dictionary.

```sh
$ mypy cycling_path.py
Success: no issues found in 1 source file
$ python cycling_path.py 
{}
```

We can start implementing the steps to get the parent dictionary. Let's copy the steps here again for easy reference.

```
1. Create an empty list for *visited* and *to_explore*. 
   Create an empty dictionary for *parent*.
2. Add start vertex to *to_explore* list.
3. As long as there is an item in *to_explore* list
   3.1 Take out the next vertex to explore from the *to_explore* list.
   3.2 Get the neighbours of this vertex.
   3.3 For every vertex in the neighbouring vertex, do
       3.3.1 If this neighbouring vertex is our destination vertex, do
             3.3.1.1 Add this neighbouring vertex to the *parent* dictionary
             3.3.1.2 Exit the search
       3.3.2 Otherwise, if the neighbouring vertex is not in the *visited* list, do
             3.3.2.1 Add the neighbouring vertex to the *visited* list
             3.3.2.2 Add the neighbouring vertex to the *to_explore* list
```

We can start with step 1 and 2. 

```python
def create_path(start: str,
                end: str,
                map: dict[str, list[str]]) -> dict[str, str]:
    parent_tree: dict[str, str] = {}
    visited: list[str] = []
    to_explore: list[str] = [start]
    return parent_tree
```

Note that we have combined step 1 and 2 for `to_explore` list. In the code above, instead of creating an empty list, we immediatelly add the starting vertex to `to_explore` list.