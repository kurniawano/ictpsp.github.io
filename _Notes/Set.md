---
title: Set
permalink: /notes/set
key: notes-set
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

## What is a Set?

After tuple, list and dictionary, you may be wondering why we need to learn another data type called **set**. Set is a useful data type following set theory in mathematics. Some operations can be performed faster as a set instead of other data type. We will look on some operations that is unique to set.

First, it is important to define what is a set data type. A set is a collection of **unique** objects. What differentiate a set from a list and a tuple is that it requires its members to be unique. This means that non item in a set is the same. 

There are some similarity between a set and a dictionary. Recall that dictionary's keys must be unique. In a way, you can think of a set as a kind of dictionary that only contains *keys* and *no values* attached to the keys. In fact, to create a set, we use the same curly braces as we use to create a dictionary. 

Let's say, we want to record the dates in January that we exercise. We can create a set in the way shown below.

```python
>>> january_exercise_dates: set[int] = {1, 3, 4, 5, 31}
>>> type(january_exercise_dates)
<class 'set'>
```

Notice the curly braces to create the set. Remember that each element of the set must be unique. This means that we have two items that are the same, a set will keep only one of them. This consistency helps a lot for certain type of application and checking. See example below when we recorded date 5th of January two times.

```python
>>> january_exercise_dates: set[int] = {1, 3, 4, 5, 5, 31}
>>> january_exercise_dates
{1, 3, 4, 5, 31}
```

We can also convert other collection data type into a set using `set()` function. This is useful when we want to apply some set operations to these data. For example, we can create the dates in January as another set using the `range()` function and the conversion function `set()`. 

```python
>>> january_dates: set[int] = set(range(1,32))
>>> january_dates
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 
11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 
21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 
31}
```

Now, we know what a set is, let's take a look at some operations that makes the set is very useful. 

## Basic Set Operations

### Adding Item Into a Set

The first common basic operation is to add an item into a collection. Python has a method called `add()` for a set object to add an item. It is not called `append()` because set too is not ordered and there is no sequence in a set. 

For example, we can add another date when the user exercise in January, say on the 25th.

```python
>>> january_exercise_dates.add(25)
>>> january_exercise_dates
{1, 3, 4, 5, 25, 31}
```

### Removing an Item From a Set

We can also remove an item from a set. If we just want to remove one item, Python provides `remove()` method.

```python
>>> january_exercise_dates
{1, 3, 4, 5, 25, 31}
>>> january_exercise_dates.remove(25)
>>> january_exercise_dates
{1, 3, 4, 5, 31}
```

Notice that since you can add and remove elements, a set is a mutable data type.

### Checking if an Item is a Member of a Set

We can also check if an item is a member of a set using the familiar `in` operator.

```python
>>> january_exercise_dates
{1, 3, 4, 5, 31}
>>> 31 in january_exercise_dates
True
>>> 25 in january_exercise_dates
False
```

With the above code, we can quickly check if the user did exercise on a particular date. 

### Getting the Length of a Set

Another common thing to do is to find the number of items in a set. We can use again the same function `len()` for a set.

```python
>>> len(january_dates)
31
>>> len(january_exercise_dates)
5
```
### Common Set Operations

#### Difference

But set is useful because of its set operations which was based on set theory in mathematics. The first one is to get a difference between two sets. For example, we want to know the dates that the user do not exercise. What we can do is to take the difference between the dates in the month of January and the dates that the user exercises.

```python
>> january_dates
{1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 
11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 
21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 
31}
>>> january_exercise_dates
{1, 3, 4, 5, 31}
>>> january_dates - january_exercise_dates
{2, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 
16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 
26, 27, 28, 29, 30}
```

We have used the `-` operator to get this difference. The difference operator can be visualize using the Venn diagram.

INSERT IMAGE VENN

Notice, that we can swap the operands when taking a difference. Let's see what happens if we swap the above operands.

```python
>>> january_exercise_dates - january_dates
set()
```

The result is an empty set. The reason is that january_exercise_dates is smaller than january_dates. In fact, january_exercise_dates is what we call a subset of january_dates.

If the set is not a subset the difference operation will not return an empty set. Let's take a look at another example. Let's say we have two users who use our exercise cycling app. These are the dates the two users exercise in January.

```python
>>> john_january: set[int] = {1, 4, 6, 9, 10}
>>> mary_january: set[int] = {4, 9, 11, 12, 31}
```

We can take the dates that John exercised but Mary did not as follows.

```python
>>> john_january - mary_january
{1, 10, 6}
```

And we can take the dates that Mary exercised but John did not using the code below.

```python
>>> mary_january - john_january
{11, 12, 31}
```

In fact, we can take a **symmetric difference** of the two sets. 

```python
>>> john_january ^ mary_january
{1, 6, 10, 11, 12, 31}
>>> mary_january ^ john_january
{1, 6, 10, 11, 12, 31}
```

These are the dates that John and Mary exercise without the other. 

#### Union and Intersection

But we can find more interesting results using set operations. Let's say we want to know which dates that Mary and John exercise on the same dates. We can use **intersection** operator.

```python
>>> mary_january & john_january
{9, 4}
>>> john_january & mary_january
{9, 4}
>>> 
```

Maybe the app can arrange the two to exercise together next time? 

We can also get the dates when both Mary and John exercise using **union** operation.

```python
>>> mary_january | john_january
{1, 4, 6, 9, 10, 11, 12, 31}
```

This lists all the dates that both Mary and John exercise. 

#### Subset and Superset

As shown in the previous section, it is useful to know if a set is a subset of another set. To check if a set is a subset of another set, we use `<=` operator.

```python
>>> january_exercise_dates <= january_dates
True
```

We can see that january_exercise_dates is a subset of january_dates. This is why when we substract `january_exercise_dates` with `january_dates` we get an empty set. We can also check if a set is a **proper subset** of another set using `<` operator.

```python
>>> january_exercise_dates < january_dates
True
>>> january_exercise_dates < january_exercise_dates
False
```

A set is a proper subset of another set if it is a subset of the other set and *not* the same as the other set. In the second code above, the result is `False` because the two sets are the same. 

Similarly, we can check if a set is a superset of another set using the opposite operator.

```python
>>> january_exercise_dates > january_dates
False
>>> january_dates > january_exercise_dates
True
```

Here we use the **proper superset** operator but we can also check the usual superset using `>=` operator instead.

## Identifying When to Use Set

So when should we use a set? We should use it when we want to use some of the set operations described above such as union, intersection, difference, etc. Most of the times, we may convert another collection data type to a set, perform a set operations and may convert it back to other collection data type. Let's a give an example of this for our cycling app.

Let's say, we have a dictionary of users and where they stay. To make it simpler, we will indicate the regin of where they stay such as west, east, north, north east, or south and central. 

```python
>>> users_region: dict[str, str] = {'John': 'West', 'Jane': 'East',
... 'Mary': 'West', 'Joe': 'North', 'Brad': 'Central',
... 'Nat': 'East', 'Robin': 'North East'}
>>> regions: list[str] = ['West', 'East', 'North', 'North East', 'South', 'Central']
```

Let's say we want to know which are the regions that our app users stay, we can write the following code.

```python
>>> active_region = users_region.values()
>>> active_region
dict_values(['West', 'East', 'West', 'North', 'Central', 'East', 'North East'])
```

But, we may be more interested to see the active region without any duplication. In this way, we can change this to a set.

```python
>>> active_region:set[str] = set(users_region.values())
>>> active_region
{'North East', 'North', 'West', 'Central', 'East'}
```

And we can get the region which has no users using the difference operation.

```python
>>> no_user_region: set[str] = set(regions) - active_region
>>> no_user_region
{'South'}
```

First, we convert the list of all the regions into a set and do a difference set operation. We see here that we do not have any users on the South region. So maybe, the marketing group can target those users in the South.

## Use Case: Matching Users Together

Let's say our app would like to connect users to cycle together. So we would like to create a dictionary with the region as the key and the user as the values of the dictionary. 

Let's first create a function to generate this new dictionary. 

```python
def generate_region_dict(user_dict: dict[str, str]) -> dict[str, list[str]]: 
    output: dict[str, list[str]] = {}
    # our code here
    return output

users_region: dict[str, str] = {'John': 'West', 'Jane': 'East',
'Mary': 'West', 'Joe': 'North', 'Brad': 'Central',
'Nat': 'East', 'Robin': 'North East'}
regions_dict: dict[str, list[str]] = generate_region_dict(users_region)
```

We start with an empty functin and a test. We used our previous user dictionary to drive the test.  Notice also that our output dictionary has a string for its key and a list for its value. 

Running mypy and python on the above code gives us the following output.

```sh
$ mypy matching_users_region.py
Success: no issues found in 1 source file
$ python matching_users_region.py 
{}
```

The output currently is an empty dictionary. We will not go through the PCDIT steps in detail for this function but please work it out yourself and see if you can write this function yourself. We will just show the final function below.

```python
def generate_region_dict(user_dict: dict[str, str]) -> dict[str, list[str]]: 
    output: dict[str, list[str]] = {}
    for user in user_dict:
        region = user_dict[user]
        if region in output:
            output[region].append(user)
        else:
            output[region] = [user]
    return output
```

The output is shown below.

```sh
$ mypy matching_users_region.py  
Success: no issues found in 1 source file
$ python matching_users_region.py
{'West': ['John', 'Mary'], 'East': ['Jane', 'Nat'], 'North': ['Joe'], 'Central': ['Brad'], 'North East': ['Robin']}
```

Since the users are unique and the sequence of the user in a particular region is not significant, it is better to represent this dictionary using a set instead of a list. We can rewrite our function in a different way as follows.

```python
def generate_region_dict(user_dict: dict[str, str]) -> dict[str, set[str]]: 
    output: dict[str, set[str]] = {}
    for user in user_dict:
        region = user_dict[user]
        if region in output:
            output[region].add(user)
        else:
            output[region] = {user}
    return output
```

Notice a few part that changes. First, when a new region is found and it is not in the output dictinary, we created a set instead of a list.

```python
output[region] = {user}
```

Second, instead of using `.append()` when adding a user to a region already existing in the output dictionary, we use `.add()` method which belongs to set object.

```python
output[region].add(user)
```

Lastly, we have changed the type of our returned value. Now, the value of our dictionary is a set. We do this in our function header.

```python
def generate_region_dict(user_dict: dict[str, str]) -> dict[str, set[str]]: 
```

We also modified the initialization when creating the output dictionary.

```python
output: dict[str, set[str]] = {}
```

The output now looks as follows.

```sh
$ python matching_users_region.py 
{'West': {'Mary', 'John'}, 'East': {'Jane', 'Nat'}, 'North': {'Joe'}, 'Central': {'Brad'}, 'North East': {'Robin'}}
```

With this, we can create some useful functions. The first function, we will create is a function to create a new combined region. For example, let's say we want to see who are the users in the North East and East region. We can create a new dictionary entry called "North East - East" with all the users in these two regions. Let's start by writing the test code.

```python
ne_e_regions: dict[str, set[str]] = create_combined_region_dict(regions_dict, 'North East', 'East')
print(ne_e_regions)
```

Notice that we expect this function to return a new dictionary with the same type. The input to this function is `region_dict` which is the output of the previous function `generate_region_dict()`. 

We can start with the function header and initializing a new dictionary by copying the input argument dictionary.

```python
def create_combined_region_dict(region_dict: dict[str, set[str]], r1, r2) -> dict[str, set[str]]:
    output: dict[str, set[str]] = copy.deepcopy(region_dict)
    # your code here
    return output
```

We used `deepcopy` function to make sure that the dictionary with all the values are copied as a separate distinct object. What we will do now is to add a new entry into the dictionary. However, we will do this only if the region `r1` and `r2` exist in the dictionary. Otherwise, we can just return the dictionary as it is.

```python
def create_combined_region_dict(region_dict: dict[str, set[str]], r1, r2) -> dict[str, set[str]]:
    output: dict[str, set[str]] = copy.deepcopy(region_dict)
    if r1 not in region_dict or r2 not in region_dict:
        return output
    return output
```

In the code above, we have added the if-statement to check if the two regions we want to combine exist in the dictionary or not. If one of them does not exist, we will just return the output and exit the function immediately. 

When both regions exists, we can create a new entry. The key will a combined word of the two regions separated by a dash, i.e. `-`. 

```python
output[r1 + ' - ' + r2] = # something
```

And the value will be a union of the two sets, i.e. 

```python
region_dict[r1] | (region_dict[r2])
``` 

So we can write our function as follows.

```python
def create_combined_region_dict(region_dict: dict[str, set[str]], r1, r2) -> dict[str, set[str]]:
    output: dict[str, set[str]] = copy.deepcopy(region_dict)
    if r1 not in region_dict or r2 not in region_dict:
        return output
    output[r1 + ' - ' + r2] = region_dict[r1] | (region_dict[r2])
    return output
```

The output of this function given the previous input is shown below.

```sh
{'West': {'Mary', 'John'}, 'East': {'Jane', 'Nat'}, 'North': {'Joe'}, 
'Central': {'Brad'}, 'North East': {'Robin'}, 
'North East - East': {'Robin', 'Jane', 'Nat'}}
```

Notice that we have a new entry, `North East - East`, in our dictionary. This entry has Robin, Jane and Nat, who are the users in the these two regions. So our app can match these three users to have a cycling activity together. We create any combinations that we want. For example, now we can use the same function to create `North East - East - Central` region.

```python
ne_e_c_regions: dict[str, set[str]] = create_combined_region_dict(ne_e_regions, 'North East - East', 'Central')
print(ne_e_c_regions)
```

In the code above, we feed the previous dictionary containing our first combined region to generate a new region `North East - East - Central`. The output is shown below.

```sh
{'West': {'Mary', 'John'}, 'East': {'Jane', 'Nat'}, 'North': {'Joe'}, 
'Central': {'Brad'}, 'North East': {'Robin'}, 
'North East - East': {'Robin', 'Jane', 'Nat'}, 
'North East - East - Central': {'Robin', 'Jane', 'Brad', 'Nat'}}
```

The best part is that we don't need to create a new function for this. We are able to get all the users in these three regins. Now, Brad from Central region is added into the set.

## Summary

In this section, we cover a new data type called set which is very useful when we are dealing with set operations. The key difference is that all the elmenents in the set are unique. Set data type makes it easy to perform some operations that would take us write lines of codes if we were to do using list. Understanding when a set is suitable is an important step in writing a good code.
