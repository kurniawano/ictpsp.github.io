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

// put image of flow chart of calculate speed.

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

// Draw flowchart

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

// put flowchart from the low category

Notice that if the condition `100 <= cadence <= 120` is true, we display "very high". However, if this condition is false, we do not display anything and there is no process associated to it. Though, we can write a code for this, it is easier to read if we start from the "very high" category and move down such that all the other cases when the cadence is lower than 70 is attributed to "low". This example, illustrates that though we can choose how we want to nest and sequence our conditions, certain way of writing is easier to read.

## Iterative Structures

Another common structure that we often find in computing is called **iterative** structure or **loops**. Iterative structure is based on the *branch* structure because it requires the sequence of the code to be altered based on some conditions. The only difference is that for iterative structure one of the branches will loop back to the top to repeat some codes in the body of the loop.

Let's take a look at an example how iterative structure can appear in our cycling chatbot. For example, let's say we want the user to enter the number of steps to calculate the cadence. Some users may enter non-valid data such as a word instead of a number or other non-relevant information. What would the chatbot do? The chatbot can repeat the question until the user enters a valid data. 

Let's recall how we can get input from the user using Python's `input()` function.

```python
steps_inp: str = input("how many push did you do on the pedal within 30 seconds? ")
```

How can we repeat this as long as the user did not enter a valid response? Below is a flowchart on how you can do so.

// put image flowchart loop

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

How about the output? There is no particular output that this code will return. The program, however, will end up in several possible states.
- state 1: The user hits the target and the chatbot displays some compliment and reward user with some bonus point.
- state 2: The user does not hit the average target by less than 10 RPM difference. In this case, the chatbot will display some words to encourage the user to hit the target. 
- state 3: the user does not hit the average target by more than 10 RPM difference. In this case, the chatbot will offer the user whether he or she wants to modify the target with a lower target at first. 

What we have described in the previous paragraph is part of the computation process that we need to perform. In order to arrive at one of those states, the program has compute the average cadence first. We can summarize the problem statement as follows.

```
Input: 
  - cadence_list: list of cadence for the past seven days. The element of the list is an integer.

Output:
  - None

Process:
  - Compute average cadence from the list
  - From the average, set the state of the chatbot one of the three states in the table. 
```

### Concrete Cases

In concrete cases steps, we try to think of specific values for the input and work out the computation step by step. The important part is take note and observe how we do the computation. This step leads to the **D**esign of Algorithm step. 

To do this, let's create some concrete cases for the input. For example, we can start with the following input list for the cadence in the past seven days.

```python
cadence_list = [45, 57, 62, 58, 55, 66, 63]
```

In the above, we use the square bracket `[]` to indicate a list of data. Notice that we put only integers inside the list. This is part of what we have already indicated in our problem statement. PCDIT framework is not meant to be linear. In the case that we realize that some of the elements are not integer, we should go back to the **P**roblem statement step and revise it.

In **C**oncrete Cases, we walk through the computation as if we are the computers. This is an important exercise of computational thinking. This means that we have to think like a computing agent in doing this step. Let's do it.

The first step is to compute the average. In order to compute the average from the input, we need to get two things: the sum of all the elements and the number of elements in the list. 


