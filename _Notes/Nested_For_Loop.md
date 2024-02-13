---
title: Nested For Loops
permalink: /notes/nested-for
key: notes-nested-for
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

## Traversing a Nested List

In the previous lesson, we introduced the idea that a collection data type like a list can have elements that are also lists. This introduces us to nested data type. There are times that we may need to visit every element in our nested list which require us to use a nested loop. One simple example that requires us to do is, let's say, we want to represent our data differently. In our previous lesson, we have `month_steps` where we store the steps of every day in a week and every week in a month. It was represented as below.

```python
month_steps_week: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                     [54, 56, 47, 62, 61, 46, 61],
                                     [52, 56, 63, 58, 62, 66, 62],
                                     [57, 58, 46, 71, 63, 76, 63]]
```

Notice, that this list is easy to access if we are interested in the *weekly* data. It's easy to get the steps in the first week or the second week or the third and so on. However, as shown in the previous lesson, it is not easy if we wish to access the data from particular *day*. For example, if we want to display what is my number of steps every Wednesday, we have to slice the data using our previous function that we developped in the last lesson. But what if we represent the data where each *sub-list* is a particular day. This means that the rows are the days and the column and the week. It will be easy to get the steps data for every Wednesday on that month. 

```python
month_steps_day: List[List[int]] = [[40, 54, 52, 57],
                                    [51, 56, 56, 58],
                                    [43, 47, 63, 46],
                                    [55, 62, 58, 71],
                                    [67, 61, 62, 63],
                                    [56, 46, 66, 76],
                                    [60, 61, 62, 63]]
```

We still have the same data but now the first row is the number of steps on Sundays. The first Sunday was 40 steps, the second Sunday was 54 steps and so on. Similarly, the second row now is the number of steps on Mondays. In this case, it is simple to get the data on Wednesdays which is on index 3. 

```python
>>> month_steps_day[3]
[55, 62, 58, 71]
```

What we did was what is called as a *transpose* operation. In a transpose operation, the data in the rows become the columns and the columns become the rows. In order to do this transpose operation, we will need to visit every element in the nested list and, therefore, require a nested for-loop. Let's see how we can do this transpose operation using a nested for-loop.

### Traversing the Sub-List

Let's recall how we can use a for-loop to traverse a list. If we only have a single iterable, we can get the element of that iterable using the following syntax.

```python
for var in iterable:
  # block A
  do_something()
```

In this way, we can get the sublist of our `month_steps_week` using the following code.

```python
for week_list in month_steps_week:
  print(week_list)
```

The output is as follows.

```
[40, 50, 43, 55, 67, 56, 60]
[54, 56, 47, 62, 61, 46, 61]
[52, 56, 63, 58, 62, 66, 62]
[57, 58, 46, 71, 63, 76, 63]
```

We can see that each list is printed in a separate line. We can also get the index and the item at the same time using `enumerate()` function.

```python
for row_idx, week_list in enumerate(month_steps_week):
    print(f'row: {row_idx}, element: {week_list}')
```

The output is shown below.

```
row: 0, element: [40, 50, 43, 55, 67, 56, 60]
row: 1, element: [54, 56, 47, 62, 61, 46, 61]
row: 2, element: [52, 56, 63, 58, 62, 66, 62]
row: 3, element: [57, 58, 46, 71, 63, 76, 63]
```

### Traversing the Element of the Sub-List

Now, if we want to get every element in the row, we can iterate over the `week_list` and print the element of that list.

```python
for row_idx, week_list in enumerate(month_steps_week):
    print("---")
    for col_idx, element in enumerate(week_list):
        print(f'row: {row_idx}, col: {col_idx}, element: {element}')
```

The output is shown below.

```
---
row: 0, col: 0, element: 40
row: 0, col: 1, element: 50
row: 0, col: 2, element: 43
row: 0, col: 3, element: 55
row: 0, col: 4, element: 67
row: 0, col: 5, element: 56
row: 0, col: 6, element: 60
---
row: 1, col: 0, element: 54
row: 1, col: 1, element: 56
row: 1, col: 2, element: 47
row: 1, col: 3, element: 62
row: 1, col: 4, element: 61
row: 1, col: 5, element: 46
row: 1, col: 6, element: 61
---
row: 2, col: 0, element: 52
row: 2, col: 1, element: 56
row: 2, col: 2, element: 63
row: 2, col: 3, element: 58
row: 2, col: 4, element: 62
row: 2, col: 5, element: 66
row: 2, col: 6, element: 62
---
row: 3, col: 0, element: 57
row: 3, col: 1, element: 58
row: 3, col: 2, element: 46
row: 3, col: 3, element: 71
row: 3, col: 4, element: 63
row: 3, col: 5, element: 76
row: 3, col: 6, element: 63
```

We have printed every element in our nested list. 

It's worth to relook at our code and examine it closely. 

```python
for row_idx, week_list in enumerate(month_steps_week):
    # Beginning of Block A for "outer-loop"
    print("---")
    for col_idx, element in enumerate(week_list):
        print(f'row: {row_idx}, col: {col_idx}, element: {element}')
    # Ending of Block A for "outer-loop"
```

Recall that block A is a block of Code inside the for-loop that is repeated for every element in the iterable. We have put a comment above to indicate all the codes below the first `for` statement is actually a block of code that is repeated for every item in our `month_steps_week`. We call our first for-loop in the first line as our "outer-loop". Since we have four weeks, this block A for the "outer-loop" will be repeated four times. There are two lines of code to be executed. The first is to print a three dash line and the second one is another for loop. We will call this for loop our "inner-loop" since it is inside the other for-loop. Notice that since we repeat block A four times for our "outer-loop", Python executes our `print('---')` four times as well. This can be observed in the output above. You will see there are only four `---` in the output. 

The second `for` statement is what we call as our "inner-loop". This second `for` statement is part of block A of the "outer-loop". This means that this "inner-loop" will be repeated four times. Each time, Python will go through ever element in the "inner-loop". In this "inner-loop" we go through `week_list` which is our sub-list in every row. There are seven days in each week and so the "inner-loop" will repeat for seven times. We can observe this in our output for the printed text between the two `---` lines. 

```
---
row: 0, col: 0, element: 40
row: 0, col: 1, element: 50
row: 0, col: 2, element: 43
row: 0, col: 3, element: 55
row: 0, col: 4, element: 67
row: 0, col: 5, element: 56
row: 0, col: 6, element: 60
---
... more output below
```

Notice that there are seven elements being printed from col 0 to col 6. All these elements are from row 0. We can see similar output for row 1 with another seven elements being printed. 

The *second* `print()` statement, where we print out the row, col and the element, is located inside block A of the "inner-loop". This means that this print statement is repeated seven times by the inner loop. And since the inner-loop is repeated four times, we have a total of $4\times 7 = 28$ print out in the screen due to this second print statement.

```python
for row_idx, week_list in enumerate(month_steps_week):
    # Beginning of Block A for "outer-loop"
    print("---")
    for col_idx, element in enumerate(week_list):
        ## Beginning of Block A for "inner-loop"
        print(f'row: {row_idx}, col: {col_idx}, element: {element}')
        ## Ending of Block A for "inner-loop"
    # Ending of Block A for "outer-loop"
```

We have added two comments to indicate the beginning and ending of Block A for the "inner-loop". You should try to run through the code in Python Tutor and verify the steps.

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=month_steps_week%20%3D%20%5B%5B40,%2050,%2043,%2055,%2067,%2056,%2060%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B54,%2056,%2047,%2062,%2061,%2046,%2061%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B52,%2056,%2063,%2058,%2062,%2066,%2062%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B57,%2058,%2046,%2071,%2063,%2076,%2063%5D%5D%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%0Afor%20row_idx,%20week_list%20in%20enumerate%28month_steps_week%29%3A%0A%20%20%20%20%23%20Beginning%20of%20Block%20A%20for%20%22outer-loop%22%0A%20%20%20%20print%28%22---%22%29%0A%20%20%20%20for%20col_idx,%20element%20in%20enumerate%28week_list%29%3A%0A%20%20%20%20%20%20%20%20%23%23%20Beginning%20of%20Block%20A%20for%20%22inner-loop%22%0A%20%20%20%20%20%20%20%20print%28f'row%3A%20%7Brow_idx%7D,%20col%3A%20%7Bcol_idx%7D,%20element%3A%20%7Belement%7D'%29%0A%20%20%20%20%20%20%20%20%23%23%20Ending%20of%20Block%20A%20for%20%22inner-loop%22%0A%20%20%20%20%23%20Ending%20of%20Block%20A%20for%20%22outer-loop%22&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=3&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

Notice that the program counter repeats the inner-loop for four times. This results in the second print statement to be executed 28 times. 

## Using Print to Debug Nested List Code

Dealing with Nested For-Loop and Nested List can be confusing. One simple way to check your way as you code is to print the values of the state of the loop. We can do this by inserting `print()` statement and simply print the variable of the loop. 

```python
for var in iterable:
  # block A
  print(var) # do this to check your loop
  do_something()
```

Inside your block A of your loop, you should immediately print out the `var` of your iterable to check our loop. There are a few things that you can check.
- See if `var` is what you expected to be the element of the iterable. 
- Check the data type of `var`
- See if `var` starts and ends as you expected

Similarly, when there are more than one loops, it is good to continue checking the state of your loop.

```python
for outer_var in outer_iterable:
  # block A of outer loop
  print(outer_var) # do this to check your outer loop
  print("marking")
  for inner_var in inner_iterable:
    # block A of inner loop
    print(inner_var)
    do_something()
```

Sometimes it is useful to print some *marking* to indicate when we are starting the inner loop. This is especially when you have multiple lines of code in both your inner and outer loop. 


With this, we are ready to tacke the problem of transposing our data. 

## Transposing Your List of Lists

Let's apply what we have learnt on traversing nested list to create a transpose of our list of lists. Let's use PCDIT framework to work it out.

### (P)roblem Definition

In this problem, we are given a list of lists and we would like to output another list of lists which is a transpose of the input list. Let's write it down.

```
Input: 
  - array: list of lists: input list of lists to be transposed.
Output:
  - array: list of lists: output list which is a transposed of the input array.
Problem Statement
  Given an input list of lists, the function should return a transposed list of lists. 
  A transposed list of lists has the same data of the input lists,
  where the row data becomes the column and the column data becomes the row data.
```

### Concrete(C)ases

Let's work out some concrete cases. Instead of dealing with `month_steps_week`, we will use a simpler list of lists as shown below.

```python
input_array: List[List[int]] = [[1, 2, 3, 4],
                                [5, 6, 7, 8],
                                [9, 10, 11, 12]]
```

What we would like to have on the output is as follows.

```python
output_array: List[List[int]] = [[1, 5, 9],
                                 [2, 6, 10],
                                 [3, 7, 11],
                                 [4, 8, 12]]
```

Now, we need to work it out how to get the output from the input step by step as if we are the machine. Our plan is to construct the output one at a time. First, we will create the first sub-list, i.e. `[1, 5, 9]`. When this is done, we will insert this sublist into the output list. To begin, we will create an empty list.

```python
output_array = []
```

Next, we need to create another empty list for the first sublist and start filling up the elements.

```python
sublist = []
```

How do we get the element? We need to get it from the `input_array`. This is where we need to traverse the input list of lists to get the element. We need to get the element `1`, `5` and `9`. These three are at different sub-lists in the input array. So let's write down the step and what we get.

```
- Go to the first sublist
- Get the first element
- Add this to the sublist 

->[1, 2, 3, 4]
   ^
   |
```

Notice in the above, we have two arrays. The "horizontal" arrow and the "vertical" arrow. The horizontal arrow is pointing to the first sublist. In this sublist pointed by the horizontal arrow, we have the second arrow pointing to which element we want to get, which is the vertical arrow. At the moment it points to the first element.

After these steps, we get the following for our sublist.

```python
sublist = [1]
```

Once we get `1`, we need to go to the second sub-list to get `5`. To do this, we move our "horizontal" arrow down to the second sub-list. We can keep the position of the "vertical" arrow since `5` is still located at the first element. 

```
- Go to the second sublist
- Get the first element
- Add this to the sublist 

  [1, 2, 3, 4]
->[5, 6, 7, 8]
   ^
   |
```

After we add `5` to the sublist, we have the following.

```python
sublist = [1, 5]
```

Now, we do the same by going to the third sublist.

```
- Go to the third sublist
- Get the first element
- Add this to the sublist 

  [1, 2, 3, 4]
  [5, 6, 7, 8]
->[9, 10, 11, 12]
   ^
   |
```

and after we add `9`, we get the following.

```python
sublist = [1, 5, 9]
```

We are done in getting the first sublist in the `output_array`. So we can add this sublist into the output list.

```python
output_array = [[1, 5, 9]]
```

Notice, that `output_array` is a list of one element. This one element, however, is a list with three elements. It is a list of lists. 

We have finished with the first row in the output. Let's construct the second row to get `[2, 6, 10]`. To do this, we need to move the "vertical" arrow to the **second** element in the sublist. We also need to reset the "horizontal" arrow back to the first sublist. 

```
- Go to the *first* sublist
- Get the *second* element
- Add this to the sublist 

->[1, 2, 3, 4]
      ^
      |
  [5, 6, 7, 8]
  [9, 10, 11, 12]
```

With  this, we get `2` and add it into our sublist. Recall that we want to construct a new row, so we need to create a new sublist for the new row.

```python
sublist = [2]
```

We can then move to the second row to get `6`.

```
- Go to the *first* sublist
- Get the *second* element
- Add this to the sublist 

  [1, 2, 3, 4]
->[5, 6, 7, 8]
      ^
      |
  [9, 10, 11, 12]
```

And we add this to sublist.

```python
sublist = [2, 6]
```

Lastly, we do the same with the third row.

```
- Go to the *first* sublist
- Get the *second* element
- Add this to the sublist 

  [1, 2, 3, 4]
  [5, 6, 7, 8]
->[9, 10, 11, 12]
      ^
      |
```

And we end up in the following sublist.

```python
sublist = [2, 6, 10]
```

We are then ready to insert this into the `output_array`.

```python
output_array = [[1, 5, 9],
                [2, 6, 10]]
```

I hope by now, you can see the pattern of how we are goint to get the final output. This pattern is important as we will write it down in the next (D)esign of Algorithm step. What we will do is to move the "vertical" arrow to the third position and reset the "horizontal" arrow back to the first row in the input list. We will then repeat the same steps. As you can see by now that we are doing a few steps that are being repeated again and again. This structure is our **iterative** structure. Let's write down a general steps in the next section.

### (D)esign of Algorithm

Let's try to generalize the steps in the previous Concrete (C)ases. One thing we have identified is that we need to repeat some steps again and again. This involves iterative structure. How many times do we need to repeat them? For each output row, we need to move the "horizontal" arrow down three times which is the number of row in the input list. Moreover, we need to keep on adding the element to the `sublist` four times. We did this by moving the "vertical" arrow to the right four times which is the number of column in the input list of lists.

Let's start by creating an empty output array.

```
1. create an empty output_array
```

After this step, we actually have to add the sublist into this `output_array` four times, which is the number we move the "vertical" arrow. This is also the number of columns in the input list of lists. Let's write the big steps in the following way.

```
1. create an empty output_array
2. for the number of columns in the input_array
    2.1 create output sublist from the input_array
    2.2 add sublist into output_array
```

The question is how we create the output sublist. We need to expand step 2.1 into several steps. Let's recall what we did when we create the output sublist.

```
Creating output sublist
1. create an empty sublist
2. for the number of rows in the input_array
    2.1 add the element into the output sublist
```

Recall that we move the horizontal arrow three times which is the number of rows in the input array. Every time we move down the horizontal arrow, we add the element pointed by the arrow into our output sublist. We can then combine and insert these steps into our overall steps.

```
1. create an empty output_array
2. for the number of columns in the input_array
    2.1 create an empty sublist
    2.2 for the number of rows in the input_array
        2.2.1 add the element into the output sublist
    2.3 add sublist into output_array
```

Maybe, we should remind ourselves that we need to move our arrows as well. So, we will add a few steps to remind us to do this. Let's start with the horizontal arrow. The horizontal arrow moves down for the number of rows in the input array. So we will add this after steps 2.2.1.

```
1. create an empty output_array
2. for the number of columns in the input_array
    2.1 create an empty sublist
    2.2 for the number of rows in the input_array
        2.2.1 add the element into the output sublist
        2.2.2 move the horizontal arrow down by one
    2.3 add sublist into output_array
```

On the other hand, the vertical arrow moves to the right after we finish adding the sublist into the output_array. This means that we can add this step after step 2.3.

```
1. create an empty output_array
2. for the number of columns in the input_array
    2.1 create an empty sublist
    2.2 for the number of rows in the input_array
        2.2.1 add the element into the output sublist
        2.2.2 move the horizontal arrow down by one
    2.3 add sublist into output_array
    2.4 move the vertical arrow to the right by one
```

Let's try to implement these steps that we have written.

### (I)mplementation and (T)est

We will create a python script called `transpose.py` to implement and test our steps. Let's start by writing the function header and some code to test it.

```python
from typing import List

def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    return output_array

input_array: List[List[int]] = [[1, 2, 3, 4],
                                [5, 6, 7, 8],
                                [9, 10, 11, 12]]
output: List[List[int]] = transpose(input_array)
print(output)
```

In the code above, we have done step 1 which is to create an empty output array. Currently, the function returns an empty list.

Running mypy and python shows the following output.

```
$ mypy transpose.py
Success: no issues found in 1 source file
$ python transpose.py 
[]
```

Step 2 is to iterate for the number of columns in the input array. We will use the `range()` function so that we can get both the index. On top of that, we will first calculate the number of rows and columns in the input array. In the code below, we remove the other parts of the code and focus only on the function definition.

```python
def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    n_rows: int = len(input_array)
    n_cols: int = len(input_array[0])
    for v_arrow in range(n_cols):
        print(v_arrow)
    return output_array
```

Notice that we added `n_rows` and `n_cols` after creating an empty array. The number of rows is the number of sublist and, therefore, we can get it from `len(input_array)`. On the other hand, the number of columns is the number of element *inside the sublist*. Since all the sublist has the same length, we can get the number of columns using `len(input_array[0])`.

We have also named the index as `v_arrow` which stand for our vertical arrow in the Concrete (C)ases example above. We used the vertical arrow to point to which element in the sublist that we are working at now. The vertical arrow runs over the element across the *column*. Running the script gives the following output.

```
0
1
2
3
[]
```

We can ignore the last empty list since we still return the empty `output_array`. However, we can see that vertical arrow iterates from 0 (most left) to 3 (most right) in the input array. 

With this, it seems we have implemented step 2 and we are ready to implement the steps under this outer iteration. Step 2.1 creates another empty array but this time it is for the rows in the output array. Since the rows in the output array have the same number as the columns in the input array, we iterate four times to create the empty lists. 

```python
def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    n_rows: int = len(input_array)
    n_cols: int = len(input_array[0])
    for v_arrow in range(n_cols):
        output_row: List[int] = []
        print(output_row)
    return output_array
```

We have added the line `output_row` and print it out. Since these two lines are inside the outer iteration loop which is iterated four times, we should expect the empty list to be printed four times.

The output is as follows.

```
[]
[]
[]
[]
[]
```

Note that there are five empty list where the first four comes from the print statement inside the iteration and the last one comes from printing the final output array. 

Now, we can do step 2.2 which is to iterate over all the rows in the input array and get the elements. 

```
2.2 for the number of rows in the input_array
    2.2.1 add the element into the output sublist
    2.2.2 move the horizontal arrow down by one
```

We can implement Step 2.2 including 2.2.2 using the usual `for-in` statement.

```python

def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    n_rows: int = len(input_array)
    n_cols: int = len(input_array[0])
    for v_arrow in range(n_cols):
        output_row: List[int] = []
        for h_arrow in range(n_rows):
            output_row.append(input_array[h_arrow][v_arrow])
            print(output_row)
    return output_array
```

We have named the variable in the inner loop as `h_arrow` which stands for the horizontal arrow in our Concrete (C)ases previously. This arrow points to which row in the input list that we are currently working on. This arrow iterates over the number of rows in the input. This number of rows in the input is the same as the number of columns in the output. This is how we assemble the output array's sublist. We added the elements into the `output_row` list. 

Which element that we add? We add the element from `input_array` pointed by the the two arrows. Recall that the row is pointed by the `h_arrow` and the column is pointed by `v_arrow`. Since every row is a sublist which is the element of the `input_array`, we access each sublist using `input_array[h_arrow]`. This gives us a list in the row. We then need to access the element at a particular column pointed by the `v_arrow`. Therefore, our code to get the element is given by `input_array[h_arrow][v_arrow]`. This element is added into `output_row` using `output_row.append()` method. 

We added a single print statement to show `output_row`. Let's see the output.

```
[1]
[1, 5]
[1, 5, 9]
[2]
[2, 6]
[2, 6, 10]
[3]
[3, 7]
[3, 7, 11]
[4]
[4, 8]
[4, 8, 12]
[]
```

We can see that it first added `1` into the `output_row` and then `5` and then `9`. Once it has three elements, it creates a new list and added `2` for the second row in the output. We repeat these four times which is the number of columns in the input or the number of rows in the output. Comparing these sublist with out Concrete (C)ases example, we can see that we get the output rows correct. Recall the following expected output in Concrete (C)ases.

```python
output_array: List[List[int]] = [[1, 5, 9],
                                 [2, 6, 10],
                                 [3, 7, 11],
                                 [4, 8, 12]]
```

We can see all the rows needed to assemble the output array. Now, what we need to do is to implement step 2.3 which is to add the sublist into the output array. 

```python
def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    n_rows: int = len(input_array)
    n_cols: int = len(input_array[0])
    for v_arrow in range(n_cols):
        output_row: List[int] = []
        for h_arrow in range(n_rows):
            output_row.append(input_array[h_arrow][v_arrow])
        output_array.append(output_row)
        print(output_array)
    return output_array
```

We added step 2.3 in the same indentation as 2.1 and 2.2 code. This is because we want to add the sublist only after we finish adding the elements into the sublist, which is step 2.2 iteration. We added print statement to see how the output array looks like at each iteration. Note that Step 2.3 is still placed under the outer loop and so we should see the print statement to be executed four times which is the number of columns in the input array.

```
[[1, 5, 9]]
[[1, 5, 9], [2, 6, 10]]
[[1, 5, 9], [2, 6, 10], [3, 7, 11]]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

We have five lines where the last two lines are the same. The reason is that the last print comes from printing the output array outside of the function definition. In the output above, we can see how the sublists are being added at every iteration. 

We got the final output array correctly and we can remove the print statement inside the function definition. 

```python
def transpose(input_array: List[List[int]]) -> List[List[int]]:
    output_array: List[List[int]] = []
    n_rows: int = len(input_array)
    n_cols: int = len(input_array[0])
    for v_arrow in range(n_cols):
        output_row: List[int] = []
        for h_arrow in range(n_rows):
            output_row.append(input_array[h_arrow][v_arrow])
        output_array.append(output_row)
    return output_array
```

Running mypy and python on the script file now gives the following output.

```
$ mypy transpose.py  
Success: no issues found in 1 source file
$ python transpose.py
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```

You can execute the code step by step in Python Tutor below. We have removed the type annotation to make the environment diagram cleaner. 

<iframe width="800" height="500" frameborder="0" src="https://pythontutor.com/iframe-embed.html#code=%0Adef%20transpose%28input_array%29%3A%0A%20%20%20%20output_array%20%3D%20%5B%5D%0A%20%20%20%20n_rows%20%3D%20len%28input_array%29%0A%20%20%20%20n_cols%20%3D%20len%28input_array%5B0%5D%29%0A%20%20%20%20for%20v_arrow%20in%20range%28n_cols%29%3A%0A%20%20%20%20%20%20%20%20output_row%20%3D%20%5B%5D%0A%20%20%20%20%20%20%20%20for%20h_arrow%20in%20range%28n_rows%29%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20output_row.append%28input_array%5Bh_arrow%5D%5Bv_arrow%5D%29%0A%20%20%20%20%20%20%20%20output_array.append%28output_row%29%0A%20%20%20%20return%20output_array%0A%0Ainput_array%20%3D%20%5B%5B1,%202,%203,%204%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B5,%206,%207,%208%5D,%0A%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%5B9,%2010,%2011,%2012%5D%5D%0Aoutput%20%3D%20transpose%28input_array%29%0Aprint%28output%29&codeDivHeight=400&codeDivWidth=350&cumulative=false&curInstr=0&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe>

## Function Composition Use Case

At the beginning of this lesson, we mentioned that getting the number of steps for every Wednesdays in a week was not easy and we need to use our `slice_2d` function. But if we transpose the data, it is easier to get the Wednesdays' steps data. Let's create a function that takes in `month_steps` and makes use of our transpose function to get the number of steps on a particular day in the month.

We want to be able to pass `month_steps` and get the number of steps for Wednesdays in that month. 

```python
month_steps: List[List[int]] = [[40, 50, 43, 55, 67, 56, 60],
                                [54, 56, 47, 62, 61, 46, 61],
                                [52, 56, 63, 58, 62, 66, 62],
                                [57, 58, 46, 71, 63, 76, 63]]
wednesdays: List[int] = steps_month_for_day(month_steps, 3)
```

We created a function called `steps_month_for_day()` which takes in two arguments. The first is the list of lists containing all the steps in a month. This list has the number of steps for each week in its rows. The second argument is the index of the day we are interested in. In the above code, we put in `3` for Wednesday since we start with Sunday which is index `0`. 

We can then write this function as follows.

```python
def steps_month_for_day(month_steps: List[List[int]], index: int) -> List:
    steps_on_days: List[List[int]] = transpose(month_steps)
    output: List[int] = steps_on_days[index]
    return output
```

In the above code, we first transpose the input array. Once it is transposed, we can get the number of steps on every Wednesday using a simple slicing. 

Running mypy and python on the script gives us the following.

```
$ mypy steps_month_for_day.py  
Success: no issues found in 1 source file
$ python steps_month_for_day.py
[55, 62, 58, 71]
```

## Summary

In this lesson, we showed how we can nest an iteration structure inside another iteration structure. We worked on transpose operation and applied some print statement along the way during the implementation of the code. Nested structure is not limited to only two for-loops. It can be more than two. However, the more nested it is, the more complicated and harder to debug. It is best to keep the loop as shallow as possible for easy debugging. 