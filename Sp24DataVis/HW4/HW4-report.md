# HW 4 - CS 625, Spring 2025


Homework 4: Arrange Tables

Heather Marsh 



Due: Sunday, March 16, 2025 by 11:59pm


## Dataset 1
Table 346 - Land and Water Area Of States and Other Entities: 2008

# Q1: For each state, show the relationship between the state's land area and its total water area. Consider only the 50 US states (Alabama - Wyoming), ignore DC and the territories. Highlight any interesting outliers.

![D1.1](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW4/D1.1.png)

 Idiom: Scatter Plot / Mark: Point
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Land Area | value, quantitative | horizontal spatial region (x-axis) |
| Total Water Area |  value, quantitative  | vertical spatial region (y-axis) |

**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

Q1 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data1.csv')

Q1 = Q1[['POST OFFICE ABBR', 'Land area SQ MILE', 'Total Water SQ MILE']]

Q1.columns = ['Post Office ABBR', 'Land Area (sq mi)', 'Total Water Area (sq mi)']

Q1['Land Area (sq mi)'] = pd.to_numeric(Q1['Land Area (sq mi)'], errors='coerce').abs()
Q1['Total Water Area (sq mi)'] = pd.to_numeric(Q1['Total Water Area (sq mi)'], errors='coerce').abs()


# Drop rows with NaN values
Q1 = Q1.dropna()

# Ignore District of Columbia
Q1 = Q1[Q1['Post Office ABBR'] != 'DC']

plt.figure(figsize=(12, 8))


plt.scatter(Q1['Land Area (sq mi)'], Q1['Total Water Area (sq mi)'], 
         color='blue', alpha=0.5)

max_point = Q1.loc[Q1['Total Water Area (sq mi)'].idxmax()]


plt.scatter(max_point['Land Area (sq mi)'], max_point['Total Water Area (sq mi)'], 
         color='red', s=100, label=f'Highest: {max_point["Post Office ABBR"]}', edgecolor='black')

for i in range(len(Q1)):
 plt.text(Q1['Land Area (sq mi)'].iloc[i], Q1['Total Water Area (sq mi)'].iloc[i], 
          Q1['Post Office ABBR'].iloc[i], fontsize=8, ha='right')
 
 plt.title('Land Area vs. Total Water Area by POST OFFICE ABBR (Excluding District of Columbia)')
plt.xlabel('Land Area (square miles)')
plt.ylabel('Total Water Area (square miles)')
plt.xscale('log')  # Optional: Logarithmic scale for better visualization
plt.yscale('log')  # Optional: Logarithmic scale for better visualization
plt.legend(title='Significant Points', bbox_to_anchor=(1.05, 1), loc='upper left')
plt.grid(True)

plt.show()
   ```
I used a scatterplot as this is a  comparision of two quantitative attributes. In my chart I found that Alaska was a popout in the plot having the highest water and land area. A logrithmic scale was used to design this chart as the scale was big due to the amount of land and water. Labels were added to each state to allow the viwer to understand which state was where. 



# Q2: Pick 10 states and compare the proportion of their total area that is land and the proportion that is water. You may pick the 10 states however you wish (e.g., 10 largest, 10 smallest, 10 largest based on land area, 10 largest based on water area, 10 favorite states), but you must discuss how you chose the states.

![D1.2](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/90520a22ad07ed947ad3c248539c6b7eeccc3cca/HW4/D1.2.png)

Idiom: STACKED BAR CHART / Mark: Bar
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Area | value, quantitative| Position: The height or length of each segment in the bar (y-axis) |
| States |  key, categorical | Label: Text labels can be used to indicate the states (x-axis) |


**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

Q1 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data1.csv')

Q1 = Q1[['POST OFFICE ABBR', 'Total area SQ MILE', 'Land area SQ MILE', 'Total Water SQ MILE']]

Q1.columns = ['Post Office ABBR', 'Total Area (sq mi)', 'Land Area (sq mi)', 'Total Water Area (sq mi)']

Q1['Total Area (sq mi)'] = pd.to_numeric(Q1['Total Area (sq mi)'], errors='coerce')
Q1['Land Area (sq mi)'] = pd.to_numeric(Q1['Land Area (sq mi)'], errors='coerce')
Q1['Total Water Area (sq mi)'] = pd.to_numeric(Q1['Total Water Area (sq mi)'], errors='coerce')

Q1 = Q1.dropna()

largest_states = Q1.nlargest(10, 'Total Area (sq mi)')

plt.figure(figsize=(14, 7))

plt.bar(largest_states['Post Office ABBR'], largest_states['Land Area (sq mi)'], 
        color='lightgreen', label='Land Area (sq mi)')
plt.bar(largest_states['Post Office ABBR'], largest_states['Total Water Area (sq mi)'], 
        bottom=largest_states['Land Area (sq mi)'], color='royalblue', label='Total Water Area (sq mi)')

plt.title('Total Area (sq mi) = Land Area (sq mi) + Total Water Area (sq mi) for the 10 Largest States')
plt.xlabel('States')
plt.ylabel('Area (square miles)')

plt.ylim(0, largest_states['Total Area (sq mi)'].max() * 1.1)

plt.grid(True, which="both", ls="--", linewidth=0.5)

plt.legend()

for index, row in largest_states.iterrows():
    plt.text(row['Post Office ABBR'], row['Land Area (sq mi)'] / 2, 
             f"{row['Land Area (sq mi)']:.1f}", 
             ha='center', va='center', color='black')
    plt.text(row['Post Office ABBR'], row['Land Area (sq mi)'] + row['Total Water Area (sq mi)'] / 2, 
             f"{row['Total Water Area (sq mi)']:.1f}", 
             ha='center', va='center', color='black')
    
plt.tight_layout()
plt.show()
   ```

A stacked bar chart was used to show the fraction of water and land in the total area. After making the chart I found that Alaska was the largest bar, with its land mass being double that of Texas and its waterr area being almost as large as Wymoing. The group of states I chose were the top ten largest states in the US by Land area. The bars are labeled to allow for a more accurate numerical comparison as it can be difficult to accurately compare stacked bar charts. 


## Dataset 2
Table 358. U.S. Water Withdrawals Per Day by End Use


# Q1: Show how the amount of water withdrawals attributed to the public supply has changed over time.

![D2.1](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/90520a22ad07ed947ad3c248539c6b7eeccc3cca/HW4/D2.1.png)


Idiom: LINE CHART / Mark: Points
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Water Withdrawals | value, quantitative| Position: Showing measure value of water (y-axis) |
| Year |  key, categorical | Position: Showing Years (x-axis) |


**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

Q2 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data2.csv')

Q2 = Q2[['Year', 'Public Supply']]

Q2['Year'] = Q2['Year'].str.replace(r'\D', '', regex=True)

Q2['Year'] = Q2['Year'].str[:4]

Q2['Year'] = pd.to_numeric(Q2['Year'], errors='coerce')

Q2['Public Supply'] = pd.to_numeric(Q2['Public Supply'], errors='coerce')

Q2 = Q2.dropna()

plt.figure(figsize=(12, 6))
plt.plot(Q2['Year'], Q2['Public Supply'], marker='o', linestyle='-', color='royalblue')

plt.title('Changes in Water Withdrawals Attributed to Public Supply Over Time')
plt.xlabel('Year')
plt.ylabel('Water Withdrawals (billion gallons)')
plt.grid()

plt.tight_layout()
plt.show()
   ```

A line chart wass used as they are a good way to show off trends. After Making the chart I can see that there has been a continous increase in water withdrawals each year. I used a linear scale as the number of yearly withdrawls was not very large. This chart did not require any special customizations. 


# Q2: Which of the end uses has contributed the most to the growth over time?
![D2.2](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/90520a22ad07ed947ad3c248539c6b7eeccc3cca/HW4/D2.2.png)


Idiom: Multi-Line Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Water Widthdrawals | value, quantitative| Continuous and color (y-axis) |
| Year |  key, categorical | Continuous and color (x-axis) |



**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure

Q2 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data2.csv')

columns_of_interest = [
    'Year', 'Public Supply', 'Self Supply Domestic', 'Livestock', 
    'Irrigation', 'Thermo-electric power', 'Self-supplied industrial', 
    'Mining', 'Commercial', 'Aquaculture'
]
Q2 = Q2[columns_of_interest]

Q2['Year'] = Q2['Year'].str.replace(r'\D', '', regex=True).str[:4]
Q2['Year'] = pd.to_numeric(Q2['Year'], errors='coerce')


for col in columns_of_interest[1:]:  
    Q2[col] = pd.to_numeric(Q2[col], errors='coerce').fillna(0)


Q2 = Q2.dropna(subset=['Year'])

annual_withdrawals = Q2.groupby('Year').sum()

annual_withdrawals.plot(kind='line', marker='o', alpha=0.8)

plt.title('Water Withdrawals by End Use Over Time')
plt.xlabel('Year')
plt.ylabel('Water Withdrawals (Billion gallons')
plt.grid()

plt.legend(title='End Uses', bbox_to_anchor=(1.05, 1), loc='upper left')

plt.figure(figsize=(20, 12))
plt.tight_layout()
plt.show()
   ```

A multi-line chart was used as it is the best way to show a trend across the various uses over time. After making the chart I found that mining,  aquaculture and Commercial did not significantly increase over time, but irrigation use is begining to decline. I used distinct colors to represent each end use, but no special customizations.


## Dataset 3
Table 379. Highest Temperature of Record - Selected Cities


# Q1: Choose 5 cities and compare their record highs in each month. You may pick the 5 cities however you wish, but you must discuss how you chose the cities.
![D3.1](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/90520a22ad07ed947ad3c248539c6b7eeccc3cca/HW4/D3.1.png)

Idiom: Multi-Line Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Temperature | value, quantitative| Continuous and color (y-axis) |
| Month |  key, categorical | Continuous and color (x-axis) |


**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure

Q3 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data3.csv')

Q3.columns = Q3.columns.str.strip()

columns_to_convert = [
    'Length of record (years)', 'January', 'February', 'March', 'April', 
    'May', 'June', 'July', 'August', 'September', 'October', 'November', 
    'December', 'Annual \\1'  ]

for col in columns_to_convert:
    Q3[col] = pd.to_numeric(Q3[col], errors='coerce').fillna(0)

cities_of_interest = ['Norfolk', 'Mobile', 'New Orleans', 'Jackson', 'Providence']
Q3_filtered = Q3[Q3['Cities'].isin(cities_of_interest)]

Q3_filtered.set_index('Cities', inplace=True)

monthly_temps = Q3_filtered[['January', 'February', 'March', 'April', 'May', 'June',
                              'July', 'August', 'September', 'October', 'November', 'December']]
plt.figure(figsize=(14, 7))

for city in cities_of_interest:
    plt.plot(monthly_temps.columns, monthly_temps.loc[city], marker='o', label=city)

plt.title('Monthly Record High Temperatures for Selected Cities')
plt.xlabel('Month')
plt.ylabel('Temperature (°F)')
plt.xticks(rotation=45)
plt.legend(title='Cities', loc='upper left', bbox_to_anchor=(1, 1))


plt.grid()
plt.tight_layout()
plt.show()
   ```

A multi-line chart was used as it is the best way to show a trend across the various cities over time. After making the chart I chose the cities Norfolk, Mobile, New Orlean, Jackson and Providence, as I have lived in or visit these cities frequently.  I used distinct colors to represent each end use, but no special customizations.



# Q2: Using the data from all of the cities, which month most often has the highest high? (Hint: For each month, show the number of times it had the highest high for a city.)
![D3.2](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/90520a22ad07ed947ad3c248539c6b7eeccc3cca/HW4/D3.2.png)

Idiom: BAR Chart / Mark: BAR
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Frequency | value, quantitative| Height of Bar (y-axis) |
| Month |  key, categorical |  color (x-axis) |



**Python Code**
   ```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from matplotlib.pyplot import figure


Q3 = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW4/Data3.csv')

Q3.columns = Q3.columns.str.strip()

monthly_columns = ['January', 'February', 'March', 'April', 
                   'May', 'June', 'July', 'August', 
                   'September', 'October', 'November', 'December']

Q3[col] = pd.to_numeric(Q3[col], errors='coerce').fillna(0)


highest_months = []

for index, row in Q3.iterrows():
    city_highest_month = row[monthly_columns].idxmax()
    highest_months.append(city_highest_month)

month_counts = pd.Series(highest_months).value_counts()

print("Number of times each month had the highest high temperature:")
print(month_counts)

colors = plt.cm.Set3(np.linspace(0, 1, len(month_counts)))

plt.figure(figsize=(10, 6))
bars = plt.bar(month_counts.index, month_counts.values, color=colors)
plt.title('Frequency of Highest High Temperatures by Month')
plt.xlabel('Month')
plt.ylabel('Number of Cities with Highest Record High')
plt.xticks(rotation=45)
plt.grid(axis='y')


for bar in bars:
    yval = bar.get_height()
    plt.text(bar.get_x() + bar.get_width()/2, yval, int(yval), ha='center', va='bottom')

plt.show()
   ```
A  Bar chart was used because it best shows frequency with the height of the bars. After making the chart I found the months of July and August had the the same frequecy of highest temperatures. Each of the bars were given a unique color to allow for better readability, and frequency as a label to the bars. 



## References
* Reference 1, https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
* Reference 2, https://www.census.gov/library/publications/2009/compendia/statab/129ed/geography-environment.html
* Reference 3, https://matplotlib.org/stable/users/explain/colors/colormaps.html
* Reference 4, https://colab.research.google.com/drive/1BePXcKO656kX-goloV0jptmNjPJyDzW0?usp=sharing




