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

## Identifying Structural Patterns in a Problem