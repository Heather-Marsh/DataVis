# HW 5 - CS 625, Spring 2025


Homework 5: Analyzing Data Using Distribution Charts

Heather Marsh 



Due: Sunday, March 23, 2025 by 11:59pm



# Data and Data Manipulation
I used table 12 for my data. The file was in xls format so I had to make edits to the file. I got rid of the first three rows which were credits, and then I edited the names of the columns to exclude the month (as months are not necessary for this assignment). I also deleted the 2 columns about postal codes and I deleted the 4 rows about the regions of the U.S. along with the row for D.C. as the capitol is excluded from this assignment. Finally I deleted the rows at the end of the document for the symbpol guide and the URLs. 



# Part 1: Create Distribution Charts, Table 12

## Boxplot: Show the distributions of the population of all states in 1970, 1985, 1995, and 2009

![Boxplot](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/Box.png)

Code Snippet

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

years = ['1970', '1985', '1995', '2009']
pop_data = data[['State'] + years]  

pop_melted = pop_data.melt(id_vars=['State'], value_vars=years, var_name='Year', value_name='Population')

pop_melted['Population'] = pd.to_numeric(pop_melted['Population'], errors='coerce')

plt.figure(figsize=(12, 6))
sns.boxplot(x='Year', y='Population', data=pop_melted, color='plum')

plt.ylim(0, pop_melted['Population'].max() * 1.1) 

plt.title('Population Distribution by State for Selected Years (Excluding D.C.)')
plt.xlabel('Year')
plt.ylabel('Population In Thousands')
plt.xticks(rotation=45)
plt.grid(True)

plt.tight_layout()
plt.show()
```

This code is a seaborn implementation of creating a boxplot, where I loaded my dataset from my google drive. I then selected the years that I wanted to see in my visualization. Then I used the melt() function to change the DataFrame format from wide to long to better prepare the data for creating a visualization. Lastly I created the boxplot and selected a color for the visualization. 

With boxplots each represents the interquartile range (IQR) of the population data for each year, indicating where the middle 50% of data lies.The line inside each box represents the median population and the whiskers extend to show the range of the data (excluding outliers). The outliers are plotted as individual points outside the whiskers. 

Advantages
- This Boxplots have provide a concise summary of the dataset by displaying the median, quartiles, and potential outliers, making it easy to grasp the distribution characteristics at a glance.
- It has helped to facilitate comparisons between different categories (in this case, different years), highlighting differences in central tendency and variability.
- This Boxplot has  effectively identified outliers, which can be crucial for understanding anomalies in the data.

Disadvantages
- It does not convey information about the number of data points or the specific values
- In this box plot you cannot clearly tell if outlier points overlap

Some things that I observed were that every year had around 4 outliers, and that the median population did not change very much, but there was a slight incrrease as the years went on. 


## Histogram: Show the distribution of the population of all states in one of the years (2002)

![Hist](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/Hist.png)

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

year = '2002'  
pop_data = data[['State', year]]

pop_data[year] = pd.to_numeric(pop_data[year], errors='coerce')

plt.figure(figsize=(12, 6))
sns.histplot(pop_data[year].dropna(), bins=15, color='plum', kde=True)

# Add titles and labels
plt.title(f'Population Distribution of States in {year} (Excluding D.C.)')
plt.xlabel('Population In Thousands')
plt.ylabel('Number of States')
plt.grid(axis='y')

# Show the plot
plt.tight_layout()
plt.show()
```

The resulting histogram displays the distribution of state populations for the year 2002. X-Axis (Population in Thousands) represents the population of the states, segmented into bins. Y-Axis (Number of States) represents the number of states that fall within each population bin. The histogram visualizes how the populations of the states are distributed, allowing for quick identification of population ranges where most states fall. The overlayed KDE provides a smooth estimate of the population density.

Advantages 
- The histogram effectively displays how state populations are distributed across a range, allowing for quick insights into the overall population distribution.
Exclusion of D.C.:
- By excluding Washington, D.C., the histogram focuses solely on the states, which provides a clearer understanding of state populations without the outlier effect of the capital.
Kernel Density Estimate (KDE):
- The inclusion of a KDE overlay smooths the distribution, helping to highlight underlying trends and patterns.

Disadvantages
- Due to the nature of histograms data is aggregated into bins,  which means that individual variations within those bins are not visible. This could mask important insights.
- Viewers might misinterpret the distribution if they are not aware of the effects of binning and KDE smoothing, leading to incorrect assumptions about the data's underlying distribution.
- While the KDE adds useful information, it could also create confusion if the audience misinterprets it as a distinct data series rather than a smoothed estimate of the histogram.
- This histogram represents only the year 2002. It doesn’t allow for comparisons across multiple years or an understanding of population trends over time, limiting its analytical depth.

I observed that around 18 states have populations clustered around the first bin which is between 4 million and 5 million people. This means they have a population of between 4 and 5 million people or less. I observed that this is a rightly skewed distribution. A right-skewed distribution often indicates the presence of outliers or extreme values on the high end of the scale, but there was also a collection of states in the middle bins. 


## eCDF: Show the distributions of the population of all states in two of the years (1985 & 2005)

![eCDF](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/eCDF.png)

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

population_1985 = pd.to_numeric(data['1985'], errors='coerce').dropna()
population_2005 = pd.to_numeric(data['2005'], errors='coerce').dropna()

plt.figure(figsize=(10, 6))

sns.ecdfplot(population_1985, label='1985', color='turquoise', linewidth=2)

sns.ecdfplot(population_2005, label='2005', color='tomato', linewidth=2)

plt.title('Empirical Cumulative Distribution Function (eCDF) of State Populations (Excluding D.C.)')
plt.xlabel('Population In Thousands')
plt.ylabel('ECDF')
plt.legend(loc='upper left')
plt.grid(True)

plt.tight_layout()
plt.show()
```

The code visualizes the cumulative distribution of state populations for the years 1985 and 2005 using eCDF plots. The eCDF shows a clear comparisons of population distributions over time and provides insights into how the population landscape of the states has evolved, all while excluding Washington, D.C. for the years 1985 and 2005. X-Axis (Population In Thousands) represents the population size of states while Y-Axis (ECDF), represents the cumulative proportion of states that have populations less than or equal to the values on the x-axis.

Advantages:
- This eCDF plot shows the cumulative proportion of states with populations below a certain value, making it easy to understand the distribution of populations at a glance.
- By displaying eCDFs for both 1985 and 2005, the plot allows for straightforward comparisons between the two years, helping to highlight changes in population distributions over time.
  
Disadvantages:
- While this eCDFs provide cumulative proportions, it does not show individual data points or the specific number of states within certain population ranges. This can mask important details about the data distribution.
- This eCDFs does convey information about the spread or variability of the data within each population range, unlike histograms or boxplots.

One thing that I observed was that that about around overr 85% of the states in both 1985 and 2005 are have a population of 10 million or less people. 


# Part 2: Further Analysis

## What states population were the outliers in 1970, 1985, 1995 and 2009?

![50Bar](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/50Bar.png)

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

years = ['1970', '1985', '1995', '2009']
pop_data = data[['State'] + years]  

pop_melted = pop_data.melt(id_vars=['State'], value_vars=years, var_name='Year', value_name='Population')

pop_melted['Population'] = pd.to_numeric(pop_melted['Population'], errors='coerce')

plt.figure(figsize=(12, 6))

sns.barplot(pop_melted, x="State", y="Population", hue="Year")

# Add titles and labels
plt.title(f'Population Distribution of States in {year} (Excluding D.C.)')
plt.xlabel('Population In Thousands')
plt.ylabel('Number of States')
plt.xticks(rotation=90)
plt.grid(axis='y')

# Show the plot
plt.tight_layout()
plt.show()
```

I noticed that overall four states had the highest population and were most likely the outliers that I saw on the boxplots. Those four states were, California, Florida, New York and Texas. However in 1970 the outliers were California, Illinois, New York, Pennsylvania, Ohio and Texas. In 1985 the outliers were California, New York and Texas. In 19995 the outliers were California, Florida, New York and Texas. Lastly in 2009 the outliers were once again California, Florida, New York and Texas. I also noticed that in 1970 there were actually six outliers but due to the nature of the boxplot it was difficult to see all of the points. 

## Outlier Analysis

![Grate](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/Grate.png)

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

data['State'] = data['State'].str.strip()

years = ['1970', '1985', '1995', '2009']
pop_data = data[['State'] + years]

pop_melted = pop_data.melt(id_vars=['State'], value_vars=years, var_name='Year', value_name='Population')

pop_melted['Population'] = pd.to_numeric(pop_melted['Population'], errors='coerce')

selected_states = pop_melted[pop_melted['State'].isin(['California','Florida', 'New York', 'Texas'])]

pivot_data = selected_states.pivot(index='Year', columns='State', values='Population')

growth_rates = pivot_data.pct_change()
growth_rates = growth_rates.dropna() 

plt.figure(figsize=(12, 6))
growth_rates.plot(kind='bar', color=['lightblue', 'orange', 'plum', 'lightgreen'], alpha=0.7)

plt.title('Average Growth Rate of Population (in %) for California, Florida, Texas, and New York')
plt.xlabel('Year')
plt.ylabel('Growth Rate (%)')
plt.xticks(rotation=0)
plt.grid(axis='y')

plt.tight_layout()
plt.legend(title='State')
plt.show()
```

In this graph I saw that in 1985 Florida had the highest growth rate and New York actually had a population decline. I also noticed that in 1985 All of the states besides New York had higher percentages of average growth rate then they would in 1995 and 2009. 1995 and 2009 were both significantly smaller years than 1985 but in these two years New York did experience growth instead of a population decline. Overall Flordia actually had the highest growth rate on aberage followed then by Texas. 




![PopGrow](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW5/PopGrow.png)

```
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW5/Tab12.csv')

data['State'] = data['State'].str.strip()

years = ['1970', '1985', '1995', '2009']
pop_data = data[['State'] + years]

pop_melted = pop_data.melt(id_vars=['State'], value_vars=years, var_name='Year', value_name='Population')

pop_melted['Population'] = pd.to_numeric(pop_melted['Population'], errors='coerce')

pop_melted = pop_melted[pop_melted['State'] != 'District of Columbia']

selected_states = pop_melted[pop_melted['State'].isin(['California','Florida', 'New York', 'Texas'])]

pivot_data = selected_states.pivot(index='Year', columns='State', values='Population')

growth_rates = pivot_data.pct_change() 
growth_rates = growth_rates.dropna()  

average_growth = growth_rates.mean()

print("Average Percentage Growth from 1985 to 2009:")
for state in average_growth.index:
    print(f"{state}: {average_growth[state]:.2f}%")

plt.figure(figsize=(8, 5))
average_growth.plot(kind='bar', color=['lightblue', 'orange', 'plum', 'lightgreen'], alpha=0.7)

plt.title('Average Percentage Growth of Population (1985-2009)')
plt.xlabel('State')
plt.ylabel('Average Growth Rate (%)')
plt.xticks(rotation=0)
plt.grid(axis='y')

plt.tight_layout()
plt.show()
```

From this chart I saw that the average percentage growth from 1985 to 2009 for California was 0.23%, for Florida it was 0.41%, for New York it was 0.02% and lastly for Texas it was 0.31%. THis supports the observations I had perrviosly made by stating that Florida had the highest growth followed by Texas and that New York had the smallest growth but was still an outlier for 1985 to 2009. 



## References
* Reference 1, https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
* Reference 2, https://www.census.gov/library/publications/2010/compendia/statab/130ed/population.html
* Reference 3, https://www.datacamp.com/tutorial/seaborn-barplot
* Reference 4, https://seaborn.pydata.org/generated/seaborn.barplot.html
* Reference 5, https://matplotlib.org/stable/users/explain/colors/colors.html#sphx-glr-users-explain-colors-colors-py
* Reference 6, https://pandas.pydata.org/docs/dev/getting_started/intro_tutorials/03_subset_data.html
* Reference 7, https://www.digitalocean.com/community/tutorials/pandas-melt-unmelt-pivot-function
* Reference 8, https://colab.research.google.com/drive/18_Ph5qr2oT26OV7WLCLoSulNu6UJZo1P?usp=sharing





















