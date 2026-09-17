# VILLAR-PA-4
### Made by : Vance Q. Villar | 2ECE-C

This repository contains Experiment 4: DATA WRANGLING AND DATA
VISUALIZATION

# **A. Visayas Communication DataFrame**

Create a DataFrame named `VisComm` containing students from `Visayas` who are under the `Communication` track. From this subset, display only the columns `Name`, `Gender`, `Math`, `Electronics`, and `Average`. Output the resulting DataFrame and determine the total number of rows.

The following functions and methods were used in this problem:

• `pd.read_excel('board2.xlsx')` - loads the Excel dataset into a Pandas DataFrame.

• `df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)` - calculates the row-wise mean score across all four subject columns to form the `Average` column.

• `df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ...]` - applies multi-condition Boolean logic using the bitwise AND (`&`) operator to slice specified rows and restrict output columns.

• `len(VisComm)` - calculates and outputs the total number of rows present in the filtered DataFrame.

```python
import pandas as pd


df = pd.read_excel('board2.xlsx')
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']]
VisComm

len(VisComm)
```

# **B. Visayas Female DataFrame**

Create a DataFrame named `VisFemale` containing all `Female` students from `Visayas`. Retain only the columns `Name`, `Track`, `GEAS`, `Electronics`, and `Average`. Display `VisFemale`, and then display a separate view of `VisFemale` where `Average` is greater than or equal to 60 without altering the original subset.

The following functions and methods were used in this problem:

• `df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ...]` - filters rows using Boolean indexing based on categorical values in `Hometown` and `Gender` while selecting specified output columns.

• `VisFemale.loc[VisFemale['Average'] >= 60]` - performs a conditional filtering operation on `VisFemale` to display only students with an overall average score of 60 or higher.

```python
VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']]
VisFemale

VisFemale.loc[VisFemale['Average'] >= 60]
```

# **C. Category-Average Visualization**

Analyze how student performance (`Average`) varies across different categories (`Track`, `Gender`, and `Hometown`). Compute group averages for each category, display the summary statistics, and visualize the comparisons using bar graphs generated with `matplotlib.pyplot` along with annotated interpretations.

The following functions and methods were used in this problem:

• `df.groupby('Category')['Average'].mean()` - groups the DataFrame by specified categorical columns (`Track`, `Gender`, `Hometown`) and calculates the arithmetic mean of overall average scores.

• `plt.figure(figsize=(15, 4))` - initializes a plot figure with custom dimensions.

• `plt.subplot(1, 3, i)` - creates individual subplots within a 1-row by 3-column grid layout.

• `plt.bar(Series.index, Series.values)` - generates vertical bar charts using categorical series index labels for the x-axis and computed mean scores for bar heights.

• `fig.text(...)` - appends custom multi-line text annotations to the figure layout to detail the statistical interpretations.

```python
import pandas as pd
import matplotlib.pyplot as plt


df = pd.read_excel('board2.xlsx')
df['Average'] = df[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1)

track_mean = df.groupby('Track')['Average'].mean()
track_mean
gender_mean = df.groupby('Gender')['Average'].mean()
gender_mean
hometown_mean = df.groupby('Hometown')['Average'].mean()
hometown_mean

fig = plt.figure(figsize=(15, 4))

plt.subplot(1, 3, 1)
plt.bar(track_mean.index, track_mean.values)
plt.title('Mean Average by Track')

plt.subplot(1, 3, 2)
plt.bar(gender_mean.index, gender_mean.values)
plt.title('Mean Average by Gender')

plt.subplot(1, 3, 3)
plt.bar(hometown_mean.index, hometown_mean.values)
plt.title('Mean Average by Hometown')

plt.tight_layout()
fig.text(0, -0.2, 'Interpretation\n\n1. Communication has the highest sample mean average in the Track category.\n2. Male has the highest sample mean average in the Gender category.\n3. Luzon has the highest sample mean average in the Hometown category.')
plt.show()
```


September 17, 2026- update README output uploaded
