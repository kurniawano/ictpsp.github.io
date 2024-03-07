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
name:str = "John Wick"
for char in name:
  print(char)
```

How can we write this code using `while` statement. First, we need the code for initialzing the condition and think what that condition would be. We can use a variable to index each of the character in name and we can stop the iteration when the index exceed the last character in the string.

```python
name: str = "John Wick"
# code to initialize for the while loop condition
# we will use index to access the character in a string
idx: int = 0 

# while loop statement with condition
while idx < len(name):
  # block A
  char: str = name[idx]
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
item: int = 10

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
username: str = 'user1'
password: str = 'password4user1'
# code to initialize
username_inp: str = input("Username: ")
password_inp: str = input("Password: ")

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

Another example for iterative structure that best implemented using the `while` statement is for **loop with sentinel value**. Sentinel value refers to some value that indicate to the program that it is time to end the iteration. In other words, it is the value used as a condition for termination. An example of a sentinel value could be the End Of File character or EOF. The software, let's say a word processor, can continue reading the characters and display them until it reaches the end of file character. 

In the example below, we will show you another simple example in playing games where using while loops is more intuitive as compared to for loop. For example, you have a chatbot that can play guessing game with you. At the end of the game, the chatbot will ask if you want to play another game. If you say yes, it will generate a new guessing game. If you say no, however, it will end the game playing. We can have something like this.

```python
continue_playing: bool = True
while continue_playing:
  play_guessing_game()
  continue_playing = ask_user_to_continue()
```

In the above code, we have a function call `play_guessing_game()` which may be defined somewhere else. That function will start the guessing game. After the game ends, it will return to this while loop and continue to call `ask_user_to_continue()` function. This function should return either `True` or `False`. If the return value is `False`, the loop ends. However, if the return value is `True`, it will go into the next iteration and call `play_guessing_game()` again. 

Notice that even in the above code, we have the similar structure. First, we initialize `continue_playing` to `True`. Second, we have the while statement that makes use of this variable `continue_playing`. Third, we have the code to be repeated which is a function call to `play_guessing_game()`. Lastly, we have the code that modify `continue_playing` to ensure potential termination of the loop. 


## Premature Loop Termination
In both while loop and for loop, Python allows you to terminate the loop early using the `break` statement. This is useful when you want to terminate the loop immediately without executing the rest of the code. A simple example would be a program for the robot to continue scanning until it finds the object that he is searching. 

```python
while True:
  found = find_object()
  if found:
    break
  move_to_next_location()
```

In the above code, we have an infinite loop since the condition is always `True`. The code that is repeated contains two function calls. The first function call is `find_object()`. The second one is `move_to_next_locatioN()`. In our code, when the `find_object()` function returns `True`, it will terminate the loop without executing `move_to_next_location()`. 

The `break` statement allows you to terminate the loop even if the program counter has not reach back to the `while` condition checking. This also allows the code to have multiple conditions at various places in the body of the loop where it can terminate the loop. Without break, the program must reach the `while` condition before it can terminate the loop. Moreover, all the conditions of the termination has to be placed in that `while` condition. 

The `break` statement can be used also inside a for-loop. A simple example is when you want to search for a particular element in a list or a particular character in a string. 

## Using Print to Debug While Loop

Let's end this section with a simple example where we can apply our problem solving and debugging skills. Let's say, we have to write a code to read a long string and display all the character positions of  a given search keywords.  For example, let's say we have the following passage which is taken from Sherlock Holmes' "The Adventure of the Speckled Band".

```python
"Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let the county police know what has happened."
```

And the code is to display the position of all the commas in the first sentence. The sentence is ended with a full stop in that passage. Let's write down our **P**roblem Statement.

```
Input => Some passage: string
Output => None
Process => display into the screen all the position of the commas in the first sentence.
```

We can then now do our **C**oncrete Cases. Using the above passage as the input, we find the following:
- a comma after "does"
- a comma after "truth"
- a comma after "violent"
- a fullstop after "another"

Once we found a fullstop, we can stop our search. 

Counting from left to right, we can output the following display.

```
A comma at position 14.
A comma at position 24.
A comma at position 49.
```

Notice that we count our position from 1 instead of 0 in the above output. Moreover, the way we get the position is to point to the character one by one. Let's call this position pointer as our *arrow*. We start with the first character and put our arrow to point to position 1. We can then check if that character is a comma or not. If it is not, we move to the next character and increase our arrow's position. We repeat the check whether it is a comma or not until we find a fullstop. When it is a fullstop, we can exit and terminate the code.

Now, we can write our **D**esign of Algorithm. You may have noticed in the previous paragraph some iterative structure when we say:
   We repeat the check whether it is a comma or not until we find a fullstop. 

We can also spot the branch structure when we hear "check" or "if" or "whether". In the above paragraph, we found the following:
   We can then check if that character is a comma or not. 

Let's write down our first draft of the steps.

```
1. put arrow to point to the first character 
2. check if the character pointed by the arrow is a comma or not.
3. if it is a comma, then
  3.1 print the position
4. move the arrow to point to the next character
5. repeat steps 2 to 4 until we find the fullstop
```

That's roughly the steps. Now, we can refine our **D**esign of algorithm in a few ways.
- We can make more specific what it means to point to the first character. Since Python's indexing starts from 0, the first character is at index 0.
- We can move the condition to repeat to the top instead at step 5. The reason is that Python do not have do-while or repeat-until statement. Python only has while-loop. 
- Printing the position is not accurate because Python index starts from 0 while we count our position from 1. So we need to add by one when printing the position.

Let's rewrite our algorithm.

```
1. initialize arrow to index 0.
2. initialize a boolean variable found_fullstop to be False.
3. as long as we have not found a fullstop
  3.1 check if the character pointed by the arrow is a comma or not.
    3.1.1 if it is a comma, display the index added by one.
  3.2 Check if the character is a fullstop
    3.2.1 if it is a full stop, set found_fullstop to be True.
  3.3 add arrow position by one.
```

We have modified our algorithm in a few significant ways. First we use index 0 to assign to arrow. Next, we have a boolean variable as our while condition. We have moved the condition checking to step 3 with `as long as we have not found a fullstop`. Next, we also have added a check if the character is a fullstop or not. This ensures that the while condition will terminate when it encounters a fullstop. 

Let's start our **I**mplement step and **T**esting step together.  We will write the code step by step and  print the values along the way to check our code. 

```python
data: str = """Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let county police know what has happened."""

arrow: int = 0
# initialize condition
found_fullstop: bool = False
```

In the above, we have done the initialize variable `found_fullstop` that would be used in the `while` condition. We have initialized `arrow` as well. You can choose to print the value of the `arrow` but we will skip it here as we know it will be 0. Our next step is to write the while condition. It is important to write a print statement once we write our loop. However, in order to ensure that our loop terminates, we need to write our block B which is the code to ensure loop termination. The question is what should be this code? Since the condition of the while loop termination is whether we find the fullstop or not, we need some code to check if the character is a fullstop, if it is, then we should change the variable to indicate that we have found the full stop. Let's write all these below.

```python
data: str = """Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let county police know what has happened."""

arrow: int = 0
# initialize condition
found_fullstop: bool = False
# while statement
while  not found_fullstop:
  # block A
  char: str = data[arrow]
  print(char)
  # block B
  if char == '.':
    found_fullstop = True
```
  
You can run the above code using Python Tutor and it will display the first sentence with each character on each line.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=data%20%3D%20%22%22%22Violence%20does,%20in%20truth,%20recoil%20upon%20the%20violent,%20and%20the%20schemer%20falls%20into%20the%20pit%20which%20he%20digs%20for%20another.%20Let%20us%20thrust%20this%20creature%20back%20into%20its%20den,%20and%20we%20can%20then%20remove%20Miss%20Stoner%20to%20some%20place%20of%20shelter%20and%20let%20county%20police%20know%20what%20has%20happened.%22%22%22%0A%0Aarrow%20%3D%200%0A%23%20initialize%20condition%0Afound_fullstop%20%3D%20False%0A%23%20while%20statement%0Awhile%20%20not%20found_fullstop%3A%0A%20%20%23%20block%20A%0A%20%20char%20%3D%20data%5Barrow%5D%0A%20%20print%28char%29%0A%20%20%23%20block%20B%0A%20%20if%20char%20%3D%3D%20'.'%3A%0A%20%20%20%20found_fullstop%20%3D%20True&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

However, the program actually displays "V" and it enters into an infinite loop. What happens? As you can observe, "V" is the first character and it seems that the program never moves to the next character. The reason is that we have not implemented step 3.3 to increase the arrow position. Let's fix that.

```python
data: str = """Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let county police know what has happened."""

arrow: int = 0
# initialize condition
found_fullstop: bool = False
# while statement
while  not found_fullstop:
  # block A
  char: str = data[arrow]
  print(char)
  # block B
  if char == '.':
    found_fullstop = True
  arrow += 1
```

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=data%20%3D%20%22%22%22Violence%20does,%20in%20truth,%20recoil%20upon%20the%20violent,%20and%20the%20schemer%20falls%20into%20the%20pit%20which%20he%20digs%20for%20another.%20Let%20us%20thrust%20this%20creature%20back%20into%20its%20den,%20and%20we%20can%20then%20remove%20Miss%20Stoner%20to%20some%20place%20of%20shelter%20and%20let%20county%20police%20know%20what%20has%20happened.%22%22%22%0A%0Aarrow%20%3D%200%0A%23%20initialize%20condition%0Afound_fullstop%20%3D%20False%0A%23%20while%20statement%0Awhile%20%20not%20found_fullstop%3A%0A%20%20%23%20block%20A%0A%20%20char%20%3D%20data%5Barrow%5D%0A%20%20print%28char%29%0A%20%20%23%20block%20B%0A%20%20if%20char%20%3D%3D%20'.'%3A%0A%20%20%20%20found_fullstop%20%3D%20True%0A%20%20arrow%20%2B%3D%201&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Now, the code does print the first sentence. So we have created our while-loop structure. Notice, that we use the `print()` function as part of block A just to make sure we have the correct while-loop structure first. Now, we can fill in block A code with our actual algorithm.

Our next step is to check if the character is a comma or not. If it is, then we will print out the position. As you can see from the "check" keyword, it is a branch structure and we will use *if-statement* to implement this.

```python
data: str = """Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let county police know what has happened."""

arrow: int = 0
# initialize condition
found_fullstop: bool = False
# while statement
while  not found_fullstop:
  # block A
  char: str = data[arrow]
  if char == ',':
    print(f"A comma at position {arrow + 1}.")
  # block B
  if char == '.':
    found_fullstop = True
  arrow += 1
```

In the above code, we have removed our earlier `print()` function and replaced it with our branch structure using if-statement. Our check if whether `char == ','`. If it is, it will print the sentence "A comma at position X.". Notice that we use string interpolation here and we have added `arrow` by one to get the position. 


The result is the following output. Which is what we expected from our **C**oncrete Cases above. 

```
A comma at position 14.
A comma at position 24.
A comma at position 49.
```

Try running the code step by step using Python Tutor.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=data%20%3D%20%22%22%22Violence%20does,%20in%20truth,%20recoil%20upon%20the%20violent,%20and%20the%20schemer%20falls%20into%20the%20pit%20which%20he%20digs%20for%20another.%20Let%20us%20thrust%20this%20creature%20back%20into%20its%20den,%20and%20we%20can%20then%20remove%20Miss%20Stoner%20to%20some%20place%20of%20shelter%20and%20let%20county%20police%20know%20what%20has%20happened.%22%22%22%0A%0Aarrow%20%3D%200%0A%23%20initialize%20condition%0Afound_fullstop%20%3D%20False%0A%23%20while%20statement%0Awhile%20%20not%20found_fullstop%3A%0A%20%20%23%20block%20A%0A%20%20char%20%3D%20data%5Barrow%5D%0A%20%20if%20char%20%3D%3D%20','%3A%0A%20%20%20%20print%28f%22A%20comma%20at%20position%20%7Barrow%20%2B%201%7D.%22%29%0A%20%20%23%20block%20B%0A%20%20if%20char%20%3D%3D%20'.'%3A%0A%20%20%20%20found_fullstop%20%3D%20True%0A%20%20arrow%20%2B%3D%201&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>


Running `mypy` and `python` output the following.

```sh
$ mypy 02_count_comma.py 
Success: no issues found in 1 source file
$ python 02_count_comma.py 
A comma at position 14.
A comma at position 24.
A comma at position 49.
```

Instead of using a boolean variable `found_fullstop`, the code can be written by looping till the end of the string and end prematurely when it sees a fullstop. See an alternative code below.

```python
data:str = """Violence does, in truth, recoil upon the violent, and the schemer falls into the pit which he digs for another. Let us thrust this creature back into its den, and we can then remove Miss Stoner to some place of shelter and let county police know what has happened."""

# initialize condition
arrow:int = 0

# while statement
while  arrow < len(data):
  # block A
  char:str = data[arrow]
  if char == ',':
    print(f"A comma at position {arrow + 1}.")
  if char == '.':
    break
  # block B
  arrow += 1
```

In the code above, we no longer have our `found_fullstop` boolean variable. Now, our `while` condition is `while arrow < len(data)`. This also changes our initialization block. Now, `arrow` is considered as part of this initialization condition because `arrow` is in the condition to continue or terminate the loop. The other changes that we have in the last if statement. When we sees a fullstop, it executes `break` statement. As mentioned earlier, the `break` statement terminates the loop immediately without executing the other statements such as the `arrow += 1`. This statement now, is no longer part of block B but rather part of block A. The code in block B is simply the line that increases the arrow position. This will ensure that the condition for the loop terminates when it reaches the end of the string. 
<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=data%3Astr%20%3D%20%22%22%22Violence%20does,%20in%20truth,%20recoil%20upon%20the%20violent,%20and%20the%20schemer%20falls%20into%20the%20pit%20which%20he%20digs%20for%20another.%20Let%20us%20thrust%20this%20creature%20back%20into%20its%20den,%20and%20we%20can%20then%20remove%20Miss%20Stoner%20to%20some%20place%20of%20shelter%20and%20let%20county%20police%20know%20what%20has%20happened.%22%22%22%0A%0A%23%20initialize%20condition%0Aarrow%3Aint%20%3D%200%0A%0A%23%20while%20statement%0Awhile%20%20arrow%20%3C%20len%28data%29%3A%0A%20%20%23%20block%20A%0A%20%20char%3Astr%20%3D%20data%5Barrow%5D%0A%20%20if%20char%20%3D%3D%20','%3A%0A%20%20%20%20print%28f%22A%20comma%20at%20position%20%7Barrow%20%2B%201%7D.%22%29%0A%20%20if%20char%20%3D%3D%20'.'%3A%0A%20%20%20%20break%0A%20%20%23%20block%20B%0A%20%20arrow%20%2B%3D%201&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

We can run `mypy` and `python` from the script `03_count_comma.py` as well.

```sh
$ mypy 03_count_comma.py 
Success: no issues found in 1 source file
$ python 03_count_comma.py 
A comma at position 14.
A comma at position 24.
A comma at position 49.
```

## Summary

In this lesson, we  show another way to implement iterative structure using the `while` statement. We first showed that this while loop can implement all those code that uses for loop in our previous lesson. We discuss when it is more appropriate to use for-loop and when it is more appropriate to use while loop. When we are dealing with iterable data, it is simpler to use for-loop. However, while loop can be used when we do not have a predetermined number of iteration. 

We also discussed about the break statement that can be used to terminate the loop prematurely before the while condition actually terminates the loop. We end the lesson by applying PCDIT framework to a simple problem. We first use a boolean variable as a condition to terminate the loop. However, with the break statement, we can actually use the string data as part of the condition to terminate the loop. In this case, actually, we can make use of for-loop to solve the same problem since string data is an iterable data. You may want to try to re-write the solution using for-loop and a break statement. 