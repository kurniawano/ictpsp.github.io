---
title: Branch Structures
permalink: /notes/branch
key: notes-branch-structures
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

## Implementing Branch Structures

In our previous lesson on [Basic Structures]({{ '/notes/basic-structures' | relative_url}}) we discuss a few flow structures that we will find again and again a computer code. The first one and the most fundamental one is the sequential structure. Everything else is based on this. The second one is the *branch* structure which we will discuss more deeply in this lesson. 

We showed an example of when this branch structure may at play in a real application. For example, in our cycling application, we may want to check if the user hit the set target or not. If the user hits the target, we want to display some congratulatory message. In that lesson we showed how we plan to solve the problem using a flowchart. In this lesson, we will show how we can **I**mplement our design of algorithm using Python. Python statement that allows us to do is is the **if statement**. 

### When Things are Right

Let's start with a simple decision making. Using our cycling app example, let's say if the user hits the set target, we will display `"You hit your cadence target for the week! Well done."`. The flowchart is shown below.

<img src="/ictpsp/assets/images/lesson4/if_true_flowchart.png" width=300>

We can implement the above using the following code.

```python
if cadence >= target:
  print("You hit your cadence target for the week! Well done.")
```

Notice the syntax above. The general syntax is as follows.

```python
if condition:
  # code block A
  # executed when condition is true
```

The condition uses the relational operator `>=` which evaluates to boolean values either `True` or `False`. We have just learnt about boolean values in the previous lesson. If the evaluated value is `True`, the lines of code indented underneath will be executed. We will call this block of code as code block A for now. Basically, code block A will be executed if the condition is true. In our example above, we only have one line of code in block A which is the `print()` statement saying the user hits the target. 

One important thing to note is that the lines of code **must be indented**. This is how Python recognize that those lines of code is part of code block A to be executed.

What if you have some codes not indented as shown below. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%2065%0A%0Aif%20cadence%20%3E%3D%20target%3A%0A%20%20%20%20print%28%22You%20hit%20your%20cadence%20target%20for%20the%20week!%20Well%20done.%22%29%0Aprint%28%22This%20is%20outside%20of%20code%20block%20A%20and%20will%20always%20be%20executed.%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Run the above code till the end and see the output. As you can see that the **unindented** code is no longer part of code block A. In fact, Python consider that as the **next statement after** the if-statement. This means that it will always be executed regardless if the condition is true or false because it is simply the next statement following the sequential nature of the program flow. 

<img src="/ictpsp/assets/images/lesson4/if_true_outside.png" width=300>


This also means that it will be executed when the condition is false. See and run the following code.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%2055%0A%0Aif%20cadence%20%3E%3D%20target%3A%0A%20%20%20%20print%28%22You%20hit%20your%20cadence%20target%20for%20the%20week!%20Well%20done.%22%29%0Aprint%28%22This%20is%20outside%20of%20code%20block%20A%20and%20will%20always%20be%20executed.%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, we change the user's cadence to be lower than the target. Since the condition is false, the print message in code block A is not executed. However, the print statement that is unindented after the if-statement is still executed as seen in the output. 

So for now, we are able to display some message when the user hits the target, but we don't actually display any other message if the user does not hit the target. What can we do about this?

### When It's True and When It's False

The previous code only display message if the user hits the target. Let's say, if the user does not hit the set target, we want to display `"You missed your target but don't give up and try again."`. In this case, we can make use of the **if-else** statement as shown below.

```python
if cadence >= target:
  print("You hit your cadence target for the week! Well done.")
else:
  print("You missed your target but don't give up and try again.")
```

The flowchart is shown here.


<img src="/ictpsp/assets/images/lesson4/if_else_flowchart.png" width=500>

The syntax in general is as follows.

```python
if condition:
  # code block A
  # will be executed when condition is true
else:
  # code block B
  # will be executed when condition is false
```

Let's try this in Python Tutor. The first code is when the condition is true since we set the cadence to be higher than the target (65 > 60). Check the output of the following.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%2065%0A%0Aif%20cadence%20%3E%3D%20target%3A%0A%20%20print%28%22You%20hit%20your%20cadence%20target%20for%20the%20week!%20Well%20done.%22%29%0Aelse%3A%0A%20%20print%28%22You%20missed%20your%20target%20but%20don't%20give%20up%20and%20try%20again.%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

The second code is when the condition is false. We set the cadence to be lower (55 < 65). 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%2055%0A%0Aif%20cadence%20%3E%3D%20target%3A%0A%20%20print%28%22You%20hit%20your%20cadence%20target%20for%20the%20week!%20Well%20done.%22%29%0Aelse%3A%0A%20%20print%28%22You%20missed%20your%20target%20but%20don't%20give%20up%20and%20try%20again.%22%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Again, any unindented code is considered as the **next statement** after the if-statement and will be executed regardless if the condition is true or false. See the flowchart below.

<img src="/ictpsp/assets/images/lesson4/if_else_next.png" width=500>

### When There are More Than Two

So far, we have only considered the case when the condition is true and when the condition is false. But what if we have more than one condition and we want to do several things. An example would be in our cycling app when we want to categorize the user's cadence.

| cadence    | category  |
|------------|-----------|
| <70        |       low |
| 70 to <90  | moderate  |
| 90 to <100 |      high |
| 100 to 120 | very high |

We can implement the above table in Python as follows.

```python
if 100 <= cadence and cadence <= 120:
  category = 'very high'
elif 90 <= cadence and cadence < 100:
  category = 'high'
elif 70 <= cadence and cadence < 90:
  category = 'moderate'
else:
  category = 'low'
```

The general syntax for **if-elif-else** statement is as follows.

```python
if condition_1:
  # code block A 
  # will be executed when condition_1 is true
elif condition_2:
  # code block B
  # will be executed when condition_1 is false
  #  and condition_2 is true
elif condition_3:
  # code block C
  # will be executed when condition_1 and 2 are false
  #  and condition_3 is true
.
.
.
else: 
  # code block D
  # will be executed when all the previous conditions are false
```

One important note is that the **conditions are checked sequentially from the top to the bottom**. This is described in the following flowchart.

// put flowchart if-elif-else block

It is imperative for us to compare the above structure with the following structure.

```python
if condition_1:
  # do action 1
if condition_2:
  # do action 2
if condition_3:
  # do action 3
else:
  # do action 4
```

First, notice the difference in the keyword that we use. In the previous code, we use **if** and **elif**. On the other hand, this code uses **if** and **if** for the various conditions. The flowchart below shows what it looks like for the if-if codes.

// flowchart for if-if code

Basically, the next if-statement for condition_2 and condition_3 are just the next statement after the previous if-statement. This means that each of this conditions will be checked regardless whether condition_1 is true or false. On the other hand, the if-elif statement does something different. If the earlier condition is true, it will execute the block and immediately go to the end and execute the next statement. See flowchart for the if-elif and notice the flow when condition_1 is true. It does not go and check condition_2 at all.

// flowchart for if-elif again

We can show this difference using the following code examples. Let's start with the if-elif statements.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%20105%0A%0Aif%20100%20%3C%3D%20cadence%20and%20cadence%20%3C%3D%20120%3A%0A%20%20category%20%3D%20'very%20high'%0Aelif%2090%20%3C%3D%20cadence%20and%20cadence%20%3C%20100%3A%0A%20%20category%20%3D%20'high'%0Aelif%2070%20%3C%3D%20cadence%20and%20cadence%20%3C%2090%3A%0A%20%20category%20%3D%20'moderate'%0Aelse%3A%0A%20%20category%20%3D%20'low'%0Aprint%28category%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

In the above code, we set the user cadence to be 105. This falls under the 'very high' category. If you run the code to the last step, you will see the output `very high`. Now, what happens if we use if-if structure?

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=target%20%3D%2060%0Acadence%20%3D%20105%0A%0Aif%20100%20%3C%3D%20cadence%20and%20cadence%20%3C%3D%20120%3A%0A%20%20category%20%3D%20'very%20high'%0Aif%2090%20%3C%3D%20cadence%20and%20cadence%20%3C%20100%3A%0A%20%20category%20%3D%20'high'%0Aif%2070%20%3C%3D%20cadence%20and%20cadence%20%3C%2090%3A%0A%20%20category%20%3D%20'moderate'%0Aelse%3A%0A%20%20category%20%3D%20'low'%0Aprint%28category%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

When you run the above code till the end, you see that it gives a wrong output, i.e. `low`. The reason is the following.
- at step 3 of 8, the computer checks if the cadence is between 100 and 120. Since the user's cadence is 105, it will execute line 5 and set `category = 'very high'` (step 4 of 8).
- However, since, we do not use `elif` keyword, the program counter does not go to `print(category)`. On the other hand, it simply goes to the next statement which is another if-statement.
- In this if-statement, the computer again checks if the user's cadence is between 90 and 100. Since it is false, it will not set category to high. Line 7 will not be executed. What happens is that the computer goes to the next statement at line 8.
- At line 8 (step 6 of 8), the computer again checks if the user's cadence is between 70 and 90. Since it is false, it will go to the `else` block and set `category = 'low'`. This is the reason why at the end `category` is set to `low`. 

Therefore, we **must always use** if-elif statement when it is the same comparison over several conditions. Using several if-statements for these cases are common mistakes that novice programmers may make.

## Nested If-Else

In our previous discussion on basic structures, we noted that you can actually have a nested structure. The most common one is to have some sequential structure in one of the blocks inside either branch or iterative structure. This means the "code block A" when the condition is True may contain more than one statement but a few and they are all executed sequentially. However, such nested structure is not limited to only sequential structure. We can have a branch structure inside another branch structure. 

Recall our example of our cycling application. In our previous lessons, we drafted the following pseudocode.

```
1. if the *average_cadence* is greater than or equal to *target_cadence*
    1.1 Display "Good job, you hit your target for the past week cycling.".
2. Otherwise,
    2.1 calculate difference betwen *average_cadence* and *target_cadence*.
    2.2 Determine state depending on the difference
      2.2.1 if the difference is less than 10
          2.2.1.1 Display, "You almost hit your target, try harder in the coming weeks."
      2.2.2 Otherwise,
          2.2.2.1 Call *modify_target_cadence* function.
```

Notice in the above pseudocode that we have two branch structure. The first branch structure is based on whether the `average_cadence` is greater than or equla to the `target_cadence`. When the condition is `False`, step 2.1 calculates the difference between the two. Furthermore, step 2.2 actually contains another branch structure that is based on the difference. We can draw the flowchart as below.

// flowchart for nested if-else

Note that the nested branch structure can be either in the true block or in the false block of codes. Where they are located really depends on the logic and the problem we are trying to solve. 

The way we will introduce another branch structure is basically just to include another if-statement at the **right indentation** level. Recall that Python identifies what is block of codes to be executed when it is `True` or `False` depends on the indentation of the code. For example, the above pseudocode or flowchart can be implemented in Python as follows.

```python
if average_cadence >= target_cadence:
  print("Good job, you hit your target for the past week cycling.")
else:
  difference = abs(average_cadence - target_cadence)
  if difference < 10:
    print("You almost hit your target, try harder in the coming weeks.")
  else:
    target_cadence = modify_target_cadence()
```

It is important to take note of the indentation level when reading Python codes. In the above code we have one statement in the True block if `average_cadence >= target_cadence` which is the `print()` statement. On the other hand, there are two statements in the False block when the condition is `False`. In that False block of codes, we have the assignment to calculate the `difference` and another if-statement to check how big the difference is. This is the other branch structure that is nested in the earlier branch structure. If the difference is less than 10, it will call the `print()` function. On the other hand, if the difference is not less than 10, it will call `modify_target_cadence()` function. 

Now you know how to have a nested if-else. But what is more important is to come up with the pseudocode and the algorithm as well as identifying the basic structures. 

In some cases, you can actually reduce the level of the nested if-statements. For example, in our case, above, you can rewrite the nested if-else using if-elif-else statements.

```python
if average_cadence >= target_cadence:
  print("Good job, you hit your target for the past week cycling.")
elif abs(average_cadence - target_cadence) < 10:
    print("You almost hit your target, try harder in the coming weeks.")
else:
    target_cadence = modify_target_cadence()
```

In this case, the elif condition is checked only if `average_cadence` is not greater than or equal to `target_cadence`. This results in the same logic. Which way to write is better? Some times having a nested if-else statement is done for simplicity and clarity of the logic. However, when the nested levels become too deep, it will become harder to read. We should strive to avoid nested code without sacrificing the readability of the code. 

## Identifying Branch Structure in a Problem

How can we identify a branch structure from our **D**esign of algorithm? The answer is simple. Whenever we encounter a step in the algorithm that requires us to take **different actions** depending on some **conditions** we have a branch structure. This requires us to make a **decision** on which course of action to take. This is why the flowchart symbol for a branch structure contains the "Decision" symbol.

<img src="/ictpsp/assets/images/lesson3/decision.png" width=200>

In order for us to easily spot the branch structure it is recommended that we rewrite our **D**esign of algorithm with certain keywords such as the following:
- decide ..., determine ...
- if ...
- otherwise ...

This is an example of our pseudocode for our average cadence.

```
1. if the *average_cadence* is greater than or equal to *target_cadence*
    1.1 Display "Good job, you hit your target for the past week cycling.".
2. Otherwise,
    2.1 calculate difference betwen *average_cadence* and *target_cadence*.
    2.2 Determine state depending on the difference
      2.2.1 if the difference is less than 10
          2.2.1.1 Display, "You almost hit your target, try harder in the coming weeks."
      2.2.2 Otherwise,
          2.2.2.1 Call *modify_target_cadence* function.
```

Notice in the above pseudocode we use the keywords: if ..., otherwise ..., determine ..., etc. This helps us to translate the above pseudocode using the if-statement in Python easily. 


## Abstracting Selection Process as a Function

In some cases, we want to abstract our selection process using a function. Recall that we can use function as an abstraction of some computation such as calculating speed, calculating cadence, etc. Similarly, we can create functions that returns a Boolean data for our selection process. For example, we can create the following functions for our example on average cadence of the week.
- `user_hits_target(user_value, target)` which checks if the user hits the target or not. 
- `has_small_difference(user_value, target)` which checks if the difference is small or not. We can use this to decide whether to modify the target or just display some encouraging message as in step 2.2 in the pseudocode above.

In the two functions above, we need to return a Boolean data as the return value. Let's see how we can define those two functions.

```python
def user_hits_target(user_value, target):
  return user_value >= target
```

We can also write that function using type annotation as follows.

```python

def user_hits_target(user_value: float, target: float) -> bool:
  return user_value >= target
```

Similarly, we can have the following function to check if the difference is large or not.

```python
def has_small_difference(user_value, target):
  return abs(user_value - target) < 10
```
Its type annotated function can be written as follows.

```python
def has_small_difference(user_value: float, target: float) -> bool:
  return abs(user_value - target) < 10
```

With these two functions, we can re-write our if-else statements by calling these two functions.

```python
if user_hits_target(average_cadence, target_cadence):
  print("Good job, you hit your target for the past week cycling.")
elif has_small_difference(average_cadence,  target_cadence):
    print("You almost hit your target, try harder in the coming weeks.")
else:
    target_cadence = modify_target_cadence()
```

You may wonder what's the advantage of abstracting the condition as a function. One advantage is that the if-statement is more readable as it is written in a higher abstraction. It is easier to read a condition that says "if it has small difference" as compared to read something with some mathematical operations in it. The second advantage is that if our definition of small difference changes, we do not need to change our if-statement code. Consider for example, if different user may have different motivation level and for some, a difference of 10 is significant while for others is not significant. What if we want to change when we should modify the target? Let's say if the difference is smaller than 20 instead. If we abstract our conditions as a function, we only need to change our function `has_small_difference()`. This is more significant if there are more than one places where we want to check if the difference is large or not.  

## Decomposing Problems Containing Branch Structures

Another advantage of abstracting those boolean conditions into a function is that it fits nicely to how we think from big problems and decomposing it to smaller problems. For example, in our case above, we can start writing our pseudocode in this manner.

```
1. if the user hits the target
    1.1 Display "Good job, you hit your target for the past week cycling.".
2. Otherwise,
    2.1 calculate difference betwen *average_cadence* and *target_cadence*.
    2.2 Determine state depending on whether it has a small difference between the user and the target
```

We can then expand 2.2 into the following.

```
      2.2.1 if it has a small difference
          2.2.1.1 Display, "You almost hit your target, try harder in the coming weeks."
      2.2.2 Otherwise,
          2.2.2.1 Call *modify_target_cadence* function.
```

As you can see that we try to think in terms of the big picture with big steps that may contain smaller steps. Step 2.2 for example may be broken down into 2.2.1 and 2.2.2. Moreover, we can decompose the step `if the user hits the target` into the following:

```
if the average_cadence is greater than or equal to target_cadence
```

In this case, the second statement is more concrete while the original one is more abstract. 

Similarly, we can drill down step 2.2.1 `if it has small difference` into the following.

```
if the difference is less than 10
```

We should not be afraid of revising our **D**esign of algorithm at various level of abstraction. In fact, that is one of important lesson in computational thinking. To be able to think through some abstraction and at different level of abstraction is one of the key element of computational thinking. 