# ECE-2112-PA-4

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

Problem A: Visayas Communicataion Dataframe
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

```
To narrow down the data to needed requirements we can use `.loc` on `board2` of which the hometown must be in `Visayas`. Their gender must be `Female` and only display `Name`, `Track`, `Math`, `Electronics` and their `average`.
```python
VisFemale = BeforeavgVisFemale.loc[(board2['average'] >= 60)]

```
For the final requirement of which their average must be above 60, we can use `.loc` again and use a `>=` operand to only select the averages above 60.

Problem B: Visayas Female Dataframe Function:
```python
board2
BeforeavgVisFemale = board2.loc[(board2['Hometown'] == 'Visayas') & (board2['Gender'] == 'Female'), ['Name', 'Track', 'Math', 'Electronics', 'average']]
VisFemale = BeforeavgVisFemale.loc[(board2['average'] >= 60)]
```

## CATEGORY-AVERAGE VISUALIZATION
> Examine how the recorded Average differs across the three categorical features Track, Gender, and Hometown.
a. For each feature, compute the mean of Average for every category using Pandas.
b. Display the three summary tables.
c. Create one figure containing three bar charts: mean Average by Track, by Gender, and by
Hometown.
d. Below the figure, write three concise statements identifying the category with the highest sample
mean for each feature.

```python
board2
```
First we call on the original data.
```python
track = board2.pivot_table(index='Track', values='average').reset_index()
gender = board2.pivot_table(index='Gender', values='average').reset_index()
hometown = board2.pivot_table(index='Hometown', values='average').reset_index()
```
To assign the new data to the graph, we must first use `[name].pivot_table` of which we assign the indexes to the average column generated before. To reset the index we can also use `.reset_index()` so that the new index will start at 0
```python
TopTrack = track.loc[track['average'].idxmax()]
TopGender = gender.loc[gender['average'].idxmax()]
TopHometown = hometown.loc[hometown['average'].idxmax()
```
To locate the maximum average of each new dataframe we first need to use `.loc` and then use `.idxmax` to locate said maximum value after which we can assign to the a new variable name.


```python
graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(20, 10))
axes[0].bar(track['Track'], track['average'], color='red')
axes[0].set(title='Mean average by Track', xlabel='Track', ylabel='Mean average')

axes[1].bar(gender['Gender'], gender['average'], color='green')
axes[1].set(title='Mean average by Gender', xlabel='Gender', ylabel='Mean average')

axes[2].bar(hometown['Hometown'], hometown['average'], color='blue')
axes[2].set(title='Mean average by Hometown', xlabel='Hometown', ylabel='Mean average')

graph.text(0.35,0.02, 'Summary of Results:')
graph.text(0.35,-0.01, 'For Mean average by Track, Communications leads with highest mean average of (67.975)')
graph.text(0.35,-0.04, 'For Mean average by Gender, Male leads with highest mean average of (67.183333)')
graph.text(0.35,-0.07, 'For Mean average by Hometown, Luzon leads with the highest mean average of (68.083333) ')
```
To generate the needed graph we must first know how many rows and columns we are going to use and configure. We can use `nrows` and `ncols` as well as `figsize` to generate the graph with the number of rows and columns with the needed size that we want. Using `axes[0].bar()` allows us to generate the bar while `axes[0].set` will "set" the bar for us such as the title and x or y labels. `Graph.Text(x,y)` will allow us to write text in the graph so that we can summarize the results without the use of comments.


Problem C: Category-Average Visualization Function
```python
board2

track = board2.pivot_table(index='Track', values='average').reset_index()
gender = board2.c(index='Gender', values='average').reset_index()
hometown = board2.pivot_table(index='Hometown', values='average').reset_index()

TopTrack = track.loc[track['average'].idxmax()]
TopGender = gender.loc[gender['average'].idxmax()]
TopHometown = hometown.loc[hometown['average'].idxmax()

graph, axes = plt.subplots(nrows=1, ncols=3, figsize=(20, 10))
axes[0].bar(track['Track'], track['average'], color='red')
axes[0].set(title='Mean average by Track', xlabel='Track', ylabel='Mean average')

axes[1].bar(gender['Gender'], gender['average'], color='green')
axes[1].set(title='Mean average by Gender', xlabel='Gender', ylabel='Mean average')

axes[2].bar(hometown['Hometown'], hometown['average'], color='blue')
axes[2].set(title='Mean average by Hometown', xlabel='Hometown', ylabel='Mean average')

graph.text(0.35,0.02, 'Summary of Results:')
graph.text(0.35,-0.01, 'For Mean average by Track, Communications leads with highest mean average of (67.975)')
graph.text(0.35,-0.04, 'For Mean average by Gender, Male leads with highest mean average of (67.183333)')
graph.text(0.35,-0.07, 'For Mean average by Hometown, Luzon leads with the highest mean average of (68.083333) ')


```



## History 
- September 13, 2026 - Created README.md File
- September 16, 2026 - Uploaded PA4 Solutions
- September 17, 2026 - Updated README.md File, Updated PA4 Solutions 
