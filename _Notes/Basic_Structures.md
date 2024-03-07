---
title: Basic Control Structures
permalink: /notes/basic-structures
key: notes-basic-structures
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

## Basic Control Structures

We will introduce some basic control structures in this section. You will find these structures throughout many computer codes and programming exercises. In fact, we can actually reduce the control structure of all programming code into only a few control structure. The image below show the three basic control structure.

// put image of sequential and branch and iterative

The first one on the left is **sequential** and we have been using this structure throughout our previous codes. We claim that computer codes are executed sequentially from top to bottom. This is the most basic and fundamental structure of all computer codes.

In this lesson and the next lesson, we are going to introduce the second structure which is a **branch** structure as shown in the middle of the above image. A branch structure adds an extremely important features in programming becauses it allows you to execute a certain code instead of another. Branch structure allows you to change the flow of the code based on some conditions. 

Lastly, we will introduce briefly the **iterative** structure as shown on the right in the above image. Iterative structure is based on the branch structure because it uses the branch structure to determine whether to continue or to stop the iteration. In the above image, if the condition is true, the computer will continue to the next iteration. On the other hand, if the condition is false, the computer will stop the iteration and execute the next block of the code.

Notice that both branch and iterative structure relies on sequential structure for each of the block that they will execute. Sequential structure remains the fundamental control flow of a computer code. Branch structure adds on the possibility of changing this sequential flow based on some conditions and Iterative structure allows you to repeat a block of code as long as the condition is true.

## Sequential Structure

An example of sequential structure is what you have seen previously. Let's put the code and draw a **flow chart** of the code. 

```python
import math
def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> float:
  '''
  Calculates the speed from the given bike parameters and cadence.

  Parameters:
    cadence (int): Cadence in rpm.
    diameter (float): Diameter of the wheel in mm. Default value = 685.8 mm.
    tire_size (float): Size of tire in mm. Default value = 38.1 mm.
    chainring (int): Teeth of the front gears. Default value = 50.
    cog (int): Teeth of the rear gears. Default value = 14.

  Returns:
    speed_kmh (float): cycling speed in km/h 
  '''
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmph: float = speed * 60 / 1_000_000
  return speed_kmph 
```

We can draw a flow chart of the above code as shown below.

<img src="/assets/images/lesson3/sequential1.png" height=500>

As you can easily see from the flowchart, the computation flows from top to bottom. The sequence is important because we need to compute the `gear_ratio` before we can compute the `speed`. Similarly, we need to compute the `speed` before we can compute the `speed_kmph`.

In the image, we have put a rounded rectangle as the starting point of the flowchart. We also indicated the input arguments into the start process. On the other hand, all the computation processes use a normal rectangle. The flow ends with the return statement and we indicate the return value in the end terminal symbol which is also a rounded rectangle. 

// put image of terminal and process flowchart symbol

Let's compare this with another code that you have previously written as well and draw the flow chart as well.

```python
import math
from typing import Tuple 

Speed = Tuple[float, float]

def calculate_speed(cadence: int, 
                    diameter: float = 685.8, 
                    tire_size: float = 38.1, 
                    chainring: int = 50, 
                    cog: int = 14) -> Speed:
  gear_ratio: float = chainring / cog
  speed: float = math.pi * (diameter + (2 * tire_size)) \
          * gear_ratio * cadence
  speed_kmph: float = speed * 60 / 1_000_000
  speed_mph: float = speed * 60 / 1.609e6
  return speed_kmph, speed_mph
```

<img src="/assets/images/lesson3/sequential2.png" height=500>

The above code is similar to the previous one. The only difference is that we compute both `speed_kmph` and `speed_mph` in this code. At the same time, you may have noticed that we don't put a separate process box for the `speed_mph` and `speed_kmph`. The reason is that these two computations does not depend on each other and can be computed as long as `speed` has been computed. This means that the two computations are at the same dependencies with respect to the `speed` process block. 

## Branch Structures

Let's say, now, we want to train at a consistent rate of cadence and we have a specific target to hit, we can monitor our performance whether we hit the target or not using a branch structure. For example, if our target for cycling cadence is 60 RPM, then we can have the following flow chart.

// insert flow chart if-else here.

In the above flowchart we have introduced a diamond symbol which is used to indicate a **decision** process. A Decision process allows a branch to more than one process. Inside that decision, a condition has to be specified. If the condition is true, a certain process will be executed (block A). Otherwise, another process will be executed. In our example here, if the cadence is below 60 RPM, then the user does not hit the target. Otherwise, the user hits the target. 

// insert diamond symbol for flowchart

In the above flowchart, we show that we will display "You are below target" if the cadence is less than 60 RPM. On the other hand, we display "You hit your cadence target of 60RPM" if the cadence is 60 or above.

// insert input / output symbol for flowchart

Notice that we use the parallelogram to indicate the process of displaying an output. This symbol is used for both **input** and **output** process. An input process may be something like getting the data from the user through a keyboard. An output process can be something like what we did here which is to display some data into the screen. 

We can modify the branch structure to be more complicated than the above. The above structure only allow the program to flow into either two options depending on the condition. If the condition is true, it will do one thing, otherwise, it will do another thing. What if we have more than two things to choose? For example, let's say if we want to categorize the user's cadence into the following table.

| cadence    | category  |
|------------|-----------|
| <70        |       low |
| 70 to <90  | moderate  |
| 90 to <100 |      high |
| 100 to 120 | very high |

In this case, we can draw the flowchart as shown below.

// put flowchart for table

Notice that in the above flowchart, we choose to start from the very high category and move down. You can see the substructure of the flowchart is basically just a simple branch structure that is nested in a process when the condition is false. 

Can we choose the other way around starting from the low category?


<img src="/assets/images/lesson3/branch2.png" height=500>

Notice that if the condition `100 <= cadence <= 120` is true, we display "very high". However, if this condition is false, we do not display anything and there is no process associated to it. Though, we can write a code for this, it is easier to read if we start from the "very high" category and move down such that all the other cases when the cadence is lower than 70 is attributed to "low". This example, illustrates that though we can choose how we want to nest and sequence our conditions, certain way of writing is easier to read.

## Iterative Structures

Another common structure that we often find in computing is called **iterative** structure or **loops**. Iterative structure is based on the *branch* structure because it requires the sequence of the code to be altered based on some conditions. The only difference is that for iterative structure one of the branches will loop back to the top to repeat some codes in the body of the loop.

Let's take a look at an example how iterative structure can appear in our cycling chatbot. For example, let's say we want the user to enter the number of steps to calculate the cadence. Some users may enter non-valid data such as a word instead of a number or other non-relevant information. What would the chatbot do? The chatbot can repeat the question until the user enters a valid data. 

Let's recall how we can get input from the user using Python's `input()` function.

```python
steps_inp: str = input("how many push did you do on the pedal within 30 seconds? ")
```

How can we repeat this as long as the user did not enter a valid response? Below is a flowchart on how you can do so.

<img src="/assets/images/lesson3/iterative1.png" height=500>

A few notes on the flowchart diagram above. Notice that we use the parallelogram for the `input()` function to get the users' input. We do this two times: the first one is the initial prompt and the second one is when the user did not enter a valid input. We modified the prompt to the user to indicate that the input entered is not valid and give some valid input example. 

Every time the user enters the input, it will be directed to the decision diamon box where it will check if the input is valid or not. If it is not valid, it will repeat the blocks that requests the user to enter it again. On the other hand, if the input is valid, it will exit the loop and continue to the next part of the code. 

The iterative structure is very common and can be found in many different cases. Another example could be when we want to average the cadence values for the past three days. We can create three variables to store the three days cadence values. Another way is to store it in a **collection** data type such as a list. We will cover list in future lessons. For now, you can see a list data structure as just a list of data. You can name this list `cadence` for example. If you want to store only the past three days, the list can have three elements. On the other hand if you want to store for the past one week, the list can contain seven elements. List is very flexible and very useful in programming. 

Let's go back to our problem in calculating the average cadence for the past `n` days. Below is the flowchart that we can draw to compute the average.

// put flowchart for average

In the above flowchart, notice where the loop structure is. Notice also that we always have some part of the flowchart that is sequential. Recall that we mention that the sequential structure is the most basic structure. In general, any iterative structure *usually* have the following structure.

// put flowchart for iterative in general

The init block is used to initialize the data which will be used to decide whether we will enter into the loop or not. This data is checked with some conditions in the diamond decision block. Depending on the condition, we either enter the **body** of the loop or **terminate** the loop. It is possible that we may never enter the body of the loop for some cases. The condition simply determines whether to do the body of the loop or not. The body of the loop consists of two parts, the first part is the main code to be executed repeatedly. The second part is the code to modify the data in such a way that the condition at some points in time will *terminate* the loop. If we do not have this block that modifies the conditions, the loop will run forever and we will end up in an **infinite** loop. The program will hang and will never continues. 

## Identifying Structural Patterns in a Problem

We will see the three basic structures again and again. It is important for us to be able to identify which structure may be present in a given problem that we are solving. As a basic rule, the sequential structure is present throughout and is the most basic structure. All computation is fundamentally sequential. This means that the sequence matters and we compute from the top to the bottom. Therefore, in this section, we are more interested in identifying if we can spot the *branch* structure and the *iterative* structure in a given problem statement.

The way we will do this is to introduce the next part of our problem solving framework, which is the **C**oncrete cases and the **D**esign of Algorithm steps. Previously, we have discussed the **P**roblem statement step in identifying the input, output, the computation process that is needed. We also shared that we need to ask the question, "What kind of data is this?" at every step of our PCDIT framework. 

These two steps in PCDIT is best illustrated with an example. Let's start with a problem. Let's say we want to train cycling cadence to hit a certain target average for the past one week. If the user hit the target, the chatbot would like to compliment the user for achieving the target and maybe give some bonus points through its gamification features. IF the user does not hit the target, the chatbot may encourage the user to try harder or maybe to set a lower target. Whether the chatbot requests the user to set a lower target or simply encourage him to try harder will be based on the difference that the user's cadence average with the target. If the difference is greater than 10 RPM, then the chatbot will ask the user to have a lower target. How should we start? Let's apply the PCDIT framework and in the process, we will identify if there is any *branch* structure or *iterative* structure.

### Problem Statement

We will start with the problem statement. In this step, we will ask what is the input, output and the computation process. We are also interested in the kind of data of the input and output. 

Let's say for our case, the input is a list of cadence of the user for the past seven days. This input is a collection data type. In such collection data type, we want to ask further what is the data type of the element of the list. In our case, the cadence is of `int` type in RPM (rotation per minute). 

There is another input in our case. This is the target cadence average the user wants to hit. Since this is a cycling training app, the user may want to hit a certain target cadence for the past one week. This target value is an input to this computation. What's the data type? This can be another integer. 

How about the output? There is no particular output that this code will return. The program, however, will end up in several possible states.
- state 1: The user hits the target and the chatbot displays some compliment and reward user with some bonus point.
- state 2: The user does not hit the average target by less than 10 RPM difference. In this case, the chatbot will display some words to encourage the user to hit the target. 
- state 3: the user does not hit the average target by more than 10 RPM difference. In this case, the chatbot will offer the user whether he or she wants to modify the target with a lower target at first. 

What we have described in the previous paragraph is part of the computation process that we need to perform. In order to arrive at one of those states, the program has compute the average cadence first. We can summarize the problem statement as follows.

```
Input: 
  - cadence_list: list of cadence for the past seven days. The element of the list is an integer.
  - target_cadence: the target value for the cadence average to hit.

Output:
  - None

Process:
  - Compute average cadence from the list
  - From the average, set the state of the chatbot one of the three states in the table. 
```

### Concrete Cases

In concrete cases steps, we try to think of specific values for the input and work out the computation step by step. The important part is take note and observe how we do the computation. This step leads to the **D**esign of Algorithm step. 

To do this, let's create some concrete cases for the input. For example, we can start with the following input list for the cadence in the past seven days and some target value.

```python
cadence_list = [45, 57, 62, 58, 55, 66, 63]
target_cadence = 60
```

In the above, we use the square bracket `[]` to indicate a list of data. We will talk about list in future lessons. For now, just take not that a list is a collection data type that you can use to group similar data. Notice that we put only integers inside the list. This is part of what we have already indicated in our problem statement. PCDIT framework is not meant to be linear. In the case that we realize that some of the elements are not integer, we should go back to the **P**roblem statement step and revise it.

In **C**oncrete Cases, we walk through the computation as if we are the computers. This is an important exercise of computational thinking. This means that we have to think like a computing agent in doing this step. Let's do it.

The first step is to compute the average. In order to compute the average from the input, we need to get two things: the sum of all the elements and the number of elements in the list. 

Let's do the first step of getting the sum of all the elements first. We will need something to hold the sum, let's name it total.

```
total = 0
```

Now, we go through every element in the list and add them to total. In the first iteration, we will take the value of the first element.

```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                ^
                |
```

The value is `45` and we will add it to total.

```
total = 0 + 45 = 45
```

Then we move to the next element.

```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                    ^
                    |
```

And we add it again to total.

```
total = 45 + 57 = 102
```

Similarly, to the third element. We do this until it reaches the last element.

```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                        ^
                        |
total = 102 + 62 = 164
```
fourth iteration:
```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                            ^
                            |
total = 164 + 58 = 222
```

fifth iteration:
```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                                ^
                                |
total = 222 + 55 = 277
```

sixth iteration:
```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                                    ^
                                    |
total = 277 + 66 = 343
```

seventh iteration:
```
cadence_list = [45, 57, 62, 58, 55, 66, 63]
                                        ^
                                        |
total = 343 + 63 = 406
```

Now, we have reached the last element and get the sum of all the cadence values. We can get the average by dividing this total with the number of elements. There are seven elements and so we have:

```
average_cadence = 406 / 7 = 58
```

Now we have the average cadence, we can *check* whether the average cadence hits the target value or not. 

If `average_cadence` is greater than or equal to the  `target_cadence`, then the chatbot will display `"Good job, you hit your target for the past week cycling."`. Otherwise, we want to check the difference. If the difference is greater or equal to `10`, then we will request the user to adjust the target value. If the difference is less than `10`, we will just display, `"You almost hit your target, try harder in the coming weeks."`. 

In our concrete case here, our average cadence is 58 while the target cadence is 60. So in this case, we do not hit the target. Now, we need to calculate the difference.

```
difference = 60 - 58 = 2
```

Since the difference is less than 10, we will just display `"You almost hit your target, try harder in the coming weeks."`. 

You should try with a different input values. For example, if the target is 70.

```
target_cadence = 70
```

In this case, the difference will be:

```
difference = 70 - 58 = 12
```

Since the difference is greater than 12, the chatbot should request the user to adjust the target.

On the other hand, if the target is 50.

```
target_cadence = 50
```

In this case, our average is greater than the target and we will just display, `"Good job, you hit your target for the past week cycling."`

### Design of Algorithm

Now, we are ready to design our algorithm. The word algorithm refers to the steps of the computation. We can derive the algorithm from the previous **C**oncrete Case steps by **generalizing** the steps we took in our computation. We will do so in two ways. The first one is through a pseudocode and the second one will use a flowchart. 

Let's start with using the pseudocode. A pseudocode is not a computer code. That's where the word *pseudo* comes from. It is meant to be general enough in such a way that it can be implemented by any programming language. The key feature of a pseudocode is to help us to think through about the steps without worrying about the programming language features. In these notes, we will use simple English for our pseudocode which we will then refine to use with certain key words that helps us to identify the structure of steps.

We can divide the steps into few distinct stages:
- calculating the total
- calculating the average
- determining the state output
- displaying the state output

To calculate the total, we start with an empty storage, `total = 0`. We then go through every element in the list and add the value to the `total`. We will write it in two stages. Here is our first draft.

```
1. Initialize *total* to 0. 
2. Go to the first element.
3. Get the value of the first element and add to *total*. Store the result back to *total*. 
4. Go to the second element.
5. Get the value of that element and add to *total*. Store the result back to *total*. 
6. Go to the third element.
7. Get the value of that element and add to *total*. Store the result back to *total*. 
8. Repeat the last two steps up to the last element.
```

There you go. We basically write what we have done in the **C**oncrete Cases steps. Notice that we repeat some steps again and again. This is an indicator of an **iterative** structure. What we want is to go through some steps **for every element in the list**. We can refine this further by using this keyword *for every element in the list*.

```
1. Initialize *total* = 0. 
2. *for every element in the list*
    2.1. Add the value of that element to *total* and store back the result to *total*.
```

We have shortened our previous steps by using the *iterative* keyword *for every element in the list*.  The steps are still easy to read and understood. Now, we can calculate the average.

```
1. Divide the *total* by the number of element in the list and store it to *average_cadence*.
```

In order to do the above, we need to know the number of element in the list. Let's combine these steps and re-write it.
```
1. Initialize *total* to 0. 
2. Get the number of element in the list and store it to *n*. 
3. *for every element in the list*
    3.1. Add the value of that element to *total* and store back the result to *total*.
4. Divide *total* by *n* and store it to *average_cadence*. 
```

Now, we can proceed to the next two stages that is to determine the state and display it. To determine the state, we can write something like the following.

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

Let's combine all the steps now into one single algorithm.

```
1. Initialize *total* to 0. 
2. Get the number of element in the list and store it to *n*. 
3. *for every element in the list*
    3.1. Add the value of that element to *total* and store back the result to *total*.
4. Divide *total* by *n* and store it to *average_cadence*. 
5. Determine what to display
  5.1 if the *average_cadence* is greater than or equal to *target_cadence*
      5.1 Display "Good job, you hit your target for the past week cycling.".
  5.2 Otherwise,
      5.2.1 calculate difference betwen *average_cadence* and *target_cadence*.
      5.2.2 Determine state depending on the difference
        5.2.2.1 if the difference is less than 10
            5.2.2.1.1 Display, "You almost hit your target, try harder in the coming weeks."
        5.2.2.2 Otherwise,
            5.2.2.2.1 Call *modify_target_cadence* function.
```

Notice a few things:
- In general, the structure is sequential which means the instruction is executed from the top to the bottom. We need to do the earlier steps before the later steps. This is true for all computer codes.
- Starting with the total calculation, we observe there is an iterative structure. We identify this iterative structure because in the previous draft of our design of algorithm we have some repeated steps that we do *for every element in the list*. We then use this keyword *for every element in the list* in our second draft of the design of algorithm.
- The step that is being repeated in this iterative structure is simply to add the element in the list to the total. We indented this step and added a sub numbering to indicate that this step is part of the iterative structure.
- In step 5, we can observe the branch structure. In fact, this branch structure has another branch structure inside it in step 5.2.2. All structure can be nested inside another structure. 

We can also represent the above design of algorithm using a Flowchart. 5.2.2. All structure can be nested inside another structure. 

We can also represent the above design of algorithm using a Flowchart. We can iterate the flowchart from big steps to the smaller steps. For example, we can start with the following basic steps.

// show flowchart for big steps sequential

Notice, that we do not describe in detail on how to get the average. We can expand the process to calculate the average using the following flowchart.

// flowchart for calculate average

Notice that the iterative structure in the above flowchart. We continue adding as long as there is a next element in the list. When there is no more next element, we stop the iteration and calculate the average. 

Similarly, we can draw the flowchart to determine the state of the program after the average cadence calculation as shown below.

// flowchart for state determination

Notice that we also have two decision box in this section showing how the branch structure is actually nested inside another branch structure. 

Finally, we can combine the different part into one single flowchart as shown below.

// flowchart overall.

For smaller problem like the above, we can draw all the parts in a single flowchart. For bigger problems, we may need to modularize and separate the flowchart into different sections and parts. 

## Summary

In this section, we introduced to you the three basic structures, sequential, branch and iterative. The basic structure is sequential. However, the branch structure actually is the one that creates flexibility in our computer programs as it allows us to choose what to do depending on some conditions. In fact, the iterative structure is based on the branch structure as it chooses to repeat certain block of steps depending on some conditions. 

We also introduce how you can write down your **C**oncrete Cases and **D**esign of Algorithm. We showed you how to iterate over your design of algorithm using both pseudocode and flowchart. In subsequent lessons, we will focus on pseudocode to design our algorithm.