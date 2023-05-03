---
title: While Loop
permalink: /notes/while-loop
key: notes-while-loop
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

## Implementing Iterative Structure using While Loop

In the previous lesson, we have implemented iterative structure using `for-in` statement. The main criteria in using this statement is that we must have an *iterable* to iterate with. There are times, however, when we do not have an iterable data and yet we want to have iterative structure to repeat. A simple example is a login page where the user name and password prompt is repeatedly presented to the users until the user enters the correct username and password. In this case, it is more natural to use the `while` statement instead of the for-in statement. 

In this lesson, we will first repeat what we do with iterables using for-in statement. However, this time, we will use the `while` statement. This is to highlight the similarity and the differences. After this, we will focus on some cases where it is more natural to use the `while` statement to implement the iterative structure.

## Basic Structure of a While Loop

Let's start with the basic syntax for a `while` statement.

```python
# initialization for condition
# while condition 
while condition:
  # block A
  # which is the code to repeat
  # ...

  # block B
  # which is to modify the condition
```

The syntax for the while-loop has four main parts:
1. The first one is the code to initialize the condition of the while loop. This is needed so that the next code does not throw an error when it checks the condition.
1. The next one is the while statement that contains the condition. As long as the condition is true, block A and block B will be executed. When the condition is no longer true, it will exit the loop and move on to the next code after the while-loop.
1. The third part is block A code which contains code that will be repeated. In the example of a login page, this would be to display the username and password prompt and capturing user input to these data.
1. The last part, which is very important, is block B, which has to be present to modify the state of the condition. If the condition never changes, the boolean evaluation will remain true and the loop never stops. This is what we call as infinite loop. Block B code is the code that makes sure the condition will become false at some points when the iteration should stop.

Let's take a look at some example. First, let's redo some of the iterative structure in the previous lesson but this time using the `while` statement. The first code we had previously is like the one below here.

```python
name = "John Wick"
for char in name:
  print(char)
```

How can we write this code using `while` statement. First, we need the code for initialzing the condition and think what that condition would be. We can use a variable to index each of the character in name and we can stop the iteration when the index exceed the last character in the string.

```python
name = "John Wick"
# code to initialize for the while loop condition
# we will use index to access the character in a string
idx = 0 

# while loop statement with condition
while idx < len(name):
  # block A
  char = name[idx]
  print(char)

  # block B
  idx += 1
```

In the above code, we have the first part which is the initialization code that is needed for the condition in the while statement. In our case, we chose to use the index which is the position of the character as our condition. When the index has exceed the last character index, then we can stop the iteration. The code `len(name)` gives us the length of the string, which in this case is 9 characters. Since the index starts from 0, we will repeat block A and block B as long as the index is less than 9. The index of the last character is at index 8. 

Block A is the code that is repeated as long as the condition is `true`. In our case, we just want to print the character of the string `name`. We do that by first accessing the character using the *get item* operator, i.e. square bracket, and providing its index. Once we have the character, we can use the `print()` function to print it. We repeat these code as long as the index is less than 9. 

Block B is the code that is also repeated as long as the condition of the while statement is `true`. However, the purpose of this code is different. The purpose is to modify the condition so that at some point, the condition will be evaluated as `false`. This is to ensure that the loop **terminates**. In this case, our block B is simply to increase the index by one. Since the indices increases, at some point, it will be equal to 9. This means that the condition `idx < len(name)` will no longer be `true`. At this point, the loop terminates.

We can see the same structure for various code when using the `while` statement. Let's take another look of our previous code and try to create the code using `while` statement.

```python
for item in range(10,100,10):
  print(item)
```

How would we write the code above using `while` statement? Let's start with thinking about the condition of the `while` statement. We can continue printing as long as `item` is less than `100`. What is the initial value for `item`? The `range()` function tells us it starts from `10` and it increases by `10`. Let's assemble the code.

```python
# code to initialize
item = 10

# while statement
while item < 100:
  # block A
  print(item)

  # block B
  item += 10
```

In this case, our initialization is simply to set the variable `item` to 10. The condition is as long as `item` is less than 100, we will do two things. The first one is to print the item and the second one is to increase the item by 10. Note that this increment by 10 is part of block B because it changes the condition at every iteration. At some point, the condition will be evaluated as `false`. You can follow the code step by step using Python Tutor below.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=%23%20code%20to%20initialize%0Aitem%20%3D%2010%0A%0A%23%20while%20statement%0Awhile%20item%20%3C%20100%3A%0A%20%20%23%20block%20A%0A%20%20print%28item%29%0A%0A%20%20%23%20block%20B%0A%20%20item%20%2B%3D%2010&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## When to use While Loop Instead of For Loop

In the previous examples, we implemented iterative structure using `while` statement which we convert from the `for-in` statement. The `while` statement is general enough that it can do what `for-in` statement can do. When dealing with *iterable* data types, it is easier and more natural to use `for-in` statement as we iterate for every item in the iterable or in the collection. The `while` statement is used more naturally when there is no obvious iterable data or collection data that we work on. It is also more natural to use the `while` statement when we do not know beforehand how many iteration is needed. An example of this is when users login unsuccessfuly. In this case, the user is presented with the login page repeatedly until he or she enters the right password. Let's write a simple Python code to test this.

```python
username = 'user1'
password = 'password4user1'
# code to initialize
username_inp = input("Username: ")
password_inp = input("Password: ")

# while loop with condition
while (username_inp != username) or (password_inp != password):
  # block A
  print("You have entered a wrong username or password. Please try again.")

  # block B
  username_inp = input("Username: ")
  password_inp = input("Password: ")

print("You have successfuly login!")

```

The output below show an example when you enter the wrong username or password and then the right one.

```sh
$ python 01_login.py 
Username: d
Password: s
You have entered a wrong username or password. Please try again.
Username: user1
Password: password4user1
You have successfuly login!
```

Notice that we have put some comments on the above code to show that we still have a similar structure for while loop. The first part is to initialize the variable that will be used as the condition for the while-loop. The second part is the while condition itself inside the `while` statement. The third part is the block A which is the code to be repeated. In this case, we simply print the error message. Lastly, the fourth part is the block B which is the code that modifies the state of the condition. This is needed to ensure that the condition can terminate. If we do not prompt the user to enter the new user name or password, the evaluated condition will not change and the loop will not terminate. 

In the case above, it is more natural to use the `while` statement instead of the `for-in` statement. The reason is that `for-in` statement requires iterable on the right hand side of the `in` keyword. However, in the example above, there is no obvious iterable that we work on. 

Another example for iterative structure that best implemented using the `while` statement is for **loop with sentinel value**. Sentinel value refers to some value that indicate to the program that it is time to end the iteration. In other words, it is the value used as a condition for termination. 

## Using Print to Debug While Loop


## Early Termination
