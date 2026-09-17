# VILLAR-PA-4
### Made by : Vance Q. Villar | 2ECE-C

This repository contains Experiment 4: DATA WRANGLING AND DATA
VISUALIZATION

# **A. Visayas Communication DataFrame**

Load the `board2.xlsx` file into a DataFrame named `board`. Create `VisComm` containing students from `Visayas` who are under the `Communication` track. From this subset, display only the columns `Name`, `Gender`, `Math`, `Electronics`, and `Average` (where `Average` is computed across all four subjects). Output the resulting DataFrame and determine the total number of rows.

The following Pandas functions and methods were used in this problem:

• `pd.read_excel('board2.xlsx')` - loads the Excel dataset into a Pandas DataFrame.

• `board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` - calculates the row-wise mean score across all four subject columns to form the `Average` column.

• `board.loc[(board['Hometown']=='Visayas') & (board['Track']=='Communication'), ...]` - applies multi-condition Boolean logic using the bitwise AND (`&`) operator to slice specified rows and restrict output columns.

• `len(VisComm)` - calculates and outputs the total number of rows present in the filtered DataFrame.

```python
import pandas as pd


board = pd.read_excel('board2.xlsx')
board['Average'] = board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

VisComm = board.loc[(board['Hometown'] == 'Visayas') & (board['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm

print("Number of rows:", len(VisComm))
```

# **B. Visayas Female DataFrame**

Create a DataFrame named `VisFemale` containing all `Female` students from `Visayas`. Retain only the columns `Name`, `Track`, `GEAS`, `Electronics`, and `Average`. Display `VisFemale`, and then display a separate view of `VisFemale` where `Average` is greater than or equal to 60 without altering the original subset.

The following functions and methods were used in this problem:

• `pd.read_excel('board2.xlsx')` - loads the Excel dataset into a Pandas DataFrame.

• `board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` - calculates the row-wise mean score across all four subject columns to form the `Average` column.

• `board.loc[(board['Hometown']=='Visayas') & (board['Gender']=='Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]` - filters rows using Boolean indexing based on categorical values in `Hometown` and `Gender` while selecting specified columns.

• `VisFemale.loc[VisFemale['Average'] >= 60]` - performs a conditional filtering operation on `VisFemale` to display only students with an average score of 60 or higher.

```python
import pandas as pd


board = pd.read_excel('board2.xlsx')
board['Average'] = board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

VisFemale = board.loc[(board['Hometown'] == 'Visayas') & (board['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale

VisFemale.loc[VisFemale['Average'] >= 60]
```

# **C. Category-Average Visualization**

Analyze how student performance (`Average`) varies across different categories (`Track`, `Gender`, and `Hometown`). Compute group averages for each category, display the summary statistics, and visualize the comparisons using bar graphs generated with `matplotlib.pyplot`.

The following functions and methods were used in this problem:

• `pd.read_excel('board2.xlsx')` - loads the Excel dataset into a Pandas DataFrame.

• `board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` - calculates the row-wise mean score across all four subject columns to form the `Average` column.

• `board.groupby('Category')['Average'].mean()` - groups the dataset by specified categorical columns and calculates the arithmetic mean of overall average scores for each group.

• `plt.subplots(1, 3, figsize=(16, 5), sharey=True)` - sets up a grid layout of three side-by-side subplots sharing a consistent y-axis scale.

• `axes[i].bar(...)` - creates vertical bar charts to compare mean performance across `Track`, `Gender`, and `Hometown`.

• `plt.tight_layout()` - optimizes plot spacing to eliminate layout overlap between subplots.

```python
import pandas as pd
import matplotlib.pyplot as plt


board = pd.read_excel('board2.xlsx')
board['Average'] = board[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

track_mean = board.groupby('Track')['Average'].mean().reset_index()
gender_mean = board.groupby('Gender')['Average'].mean().reset_index()
hometown_mean = board.groupby('Hometown')['Average'].mean().reset_index()

("Track Average:\n", track_mean)
("\nGender Average:\n", gender_mean)
("\nHometown Average:\n", hometown_mean)

fig, axes = plt.subplots(1, 3, figsize=(16, 5), sharey=True)

axes[0].bar(track_mean['Track'], track_mean['Average'], color='steelblue', edgecolor='black')
axes[0].set_title('Mean Average by Track')
axes[0].set_xlabel('Track')
axes[0].set_ylabel('Mean Score')
axes[0].set_ylim(0, 100)

axes[1].bar(gender_mean['Gender'], gender_mean['Average'], color='sandybrown', edgecolor='black')
axes[1].set_title('Mean Average by Gender')
axes[1].set_xlabel('Gender')

axes[2].bar(hometown_mean['Hometown'], hometown_mean['Average'], color='mediumseagreen', edgecolor='black')
axes[2].set_title('Mean Average by Hometown')
axes[2].set_xlabel('Hometown')

plt.tight_layout()
plt.show()
```
