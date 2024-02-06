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



## Decompose Problems with Nested Loops