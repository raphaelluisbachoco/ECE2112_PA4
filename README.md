# ECE-2112-PA-3

Created by: Raphael Luis L. Bachoco | 2ECE-D

This repository contains content that pertains to Programming Assignment 4 of ECE 2112: Advanced Computer Programming and Algorithms, SY: 2026-2027

## A. VISAYAS COMMUNICATION DATAFRAME
> Create a DataFrame named VisComm containing students whose Hometown is Visayas and whose Trackis Communication. Retain only these columns, in the stated order: Name, Gender, Math, Electronics, Average. Display the resulting DataFrame and its number of rows. Both filtering conditions must be applied to
the source dataset before the columns are selected.

```python
import pandas as pd
import matplotlib.pyplot as plt
```
First we must import both pandas and matplotlib.pyplot as `pd` and `plt` respectively. This is done so that when we call both library, we can shorten them as the given name such as `pd` or `plt`.


```python
board2 = pd.read_excel('board2.xlsx')

```
Next we must import the needed data from the excel file named board2. We can assign a variable name to the excel file of which we choose `board2`.

```python
board2['average'] = (board2['Math'] + board2['Electronics'] + board2['GEAS'] + board2['Communication'])/4
```
To add the needed average column from the given data set we must first add the columns of `Math`, `Electronics`, `GEAS` and `Communication respectively. After which we can divide by 4 to to get the total average of each row in which the new average column will be the right most column.

```python
VisComm = board2.loc[(board2['Hometown'] == 'Visayas') & (board2['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'average']]
```
To narrow down the data to only people with the hometown of Visayas and is in the track of Communication we can use `.loc` on both while narrowing it down to `Name`, `Gender`, `Math`, `Electronics`, `average`.

Problem A : Visayas Communicataion Dataframe
```python
import pandas as pd
import matplotlib.pyplot as plt
board2 = pd.read_excel('board2.xlsx')
board2['average'] = (board2['Math'] + board2['Electronics'] + board2['GEAS'] + board2['Communication'])/4
VisComm = board2.loc[(board2['Hometown'] == 'Visayas') & (board2['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'average']]
```


## VISAYAS FEMALE DATAFRAME
> Create a second DataFrame named VisFemale containing students whose Hometown is Visayas and whose Gender is Female. Retain only: Name, Track, GEAS, Electronics, Average Display VisFemale. Then display only the rows of VisFemale whose Average is at least 60. Do not overwrite VisFemale when performing this second filter.


```python
board2
```
First we call the original data again.


```python
BeforeavgVisFemale = board2.loc[(board2['Hometown'] == 'Visayas') & (board2['Gender'] == 'Female'), ['Name', 'Track', 'Math', 'Electronics', 'average']]
BeforeavgVisFemale
```
To narrow down the data to needed requirements we can use `.loc` on `board2` of which the hometown must be in `Visayas`. Their gender must be `Female` and only display `Name`, `Track`, `Math`, `Electronics` and their `average`.
```python
VisFemale = BeforeavgVisFemale.loc[(board2['average'] >= 60)]
VisFemale
```
For the final requirement of which their average must be above 60, we can use
```python

```






## CATEGORY-AVERAGE VISUALIZATION
> Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.
a. For each feature, compute the mean of Average for every category using Pandas.
b. Display the three summary tables.
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.
d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.








## History 
- September 13, 2026 - Created README.md File
- September 16, 2026 - Uploaded PA4 Solutions
