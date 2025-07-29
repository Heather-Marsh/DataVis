# HW 3 - CS 625, Spring 2025


Homework 3: Create Visualization Idioms from Real-World Data

Heather Marsh 



**Due:** February 23, 2025 by 11:59pm

## Part 1: Pre-Processing Data
- I cleaned my datasets using OpenRefine. The first dataset that I clean was the Video games sales dataset where I first got rid or any row that did not have a year listed, then i deleted the rows that had zeros in the sales columns starting with North America first then so on, this reduced my number of rows from 16,598 down to 2,365.
- My other datset was on earthquake data. To clean this data set I got rid of quite a few columns such as: Depth Error, Depth Seismic Stations, Magnitude Error, Magnitude Seismic Stations, Azimuthal Gap, Horizontal Distance, Horizontal Error, and Root Mean Square to name a few. I then seperated the date column into month day and year, then got rid of the / characters. I also got rid of the rows that did not have a magnitude type or were missing the year. I also reduced the number of years from 53 to 7 as that reduced the number of rows from 23,407 to 3,573



## Part 2: Data
- For the bar bar/column chart, I will be making a stacked bar plot using the video game dataset to plot the sales of Nintendo games by the year. I am using this subset as it is the largest subset amongst my dataset. 
- For the scatterplot/dot plot, I will be making a scatter plot with the earthquakaes dataset and I will be plotting the magtidude of earthquakes by the year. 
- For the multiple line/area chart, I will be making a multiple line chart and I will be using the video game dataset to plot the sales of Electronic Arts games (EA Games) by the year. I am using this subset as it is a different subset to the Nintendo subset. 




## Part 3: Visualizations
- Link to Google Colab, https://colab.research.google.com/drive/1YiCT849OzoAe1kA6tMM0T3XtE21_OF8Z?usp=sharing

### Stacked Bar Plot


  Idiom: Bar Chart / Mark: Bar
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Total Sales | value, quantitative | length of bars (y-axis) |
| Year |  key, categorical  | horizontal spatial region (x-axis) |

![BarChart](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW3/StackedBar.png)


- Link to Google Colab, https://colab.research.google.com/drive/1YiCT849OzoAe1kA6tMM0T3XtE21_OF8Z?usp=sharing

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

VideoG = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW3/CleanedVGsales.csv')

# Group by Year and sum the sales
sales_by_year = VideoG.groupby('Year')[['NA_Sales', 'JP_Sales', 'EU_Sales', 'Other_Sales']].sum().reset_index()

# Create a stacked bar plot
plt.figure(figsize=(10, 6))

#color pallette
plt.rcdefaults()

plt.bar(sales_by_year['Year'].astype(str), sales_by_year['NA_Sales'], label='NA Sales', color='turquoise')
plt.bar(sales_by_year['Year'].astype(str), sales_by_year['JP_Sales'], bottom=sales_by_year['NA_Sales'], label='JP Sales', color='plum')
plt.bar(sales_by_year['Year'].astype(str), sales_by_year['EU_Sales'], bottom=sales_by_year['NA_Sales'] + sales_by_year['JP_Sales'], label='EU Sales', color='lightgreen')
plt.bar(sales_by_year['Year'].astype(str), sales_by_year['Other_Sales'], bottom=sales_by_year['NA_Sales'] + sales_by_year['JP_Sales'] + sales_by_year['EU_Sales'], label='Other Sales', color='orange')

# Add labels and title
plt.title('Stacked Bar Plot of Nintendo Sales by Year (1983-2010)')
plt.xlabel('Year')
plt.ylabel('Total Sales (in millions)')
plt.xticks(rotation=45)
plt.legend()
plt.tight_layout()

plt.show()

```
### Scatter Plot


Idiom: Scatter Plot / Mark: Dots
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Magnitude | value, quantitative| color (y-axis) |
| Depth | value, quantitative| color (x-axis) |

![ScatterChart](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW3/Scatter.png)


- Link to Google Colab, https://colab.research.google.com/drive/1YiCT849OzoAe1kA6tMM0T3XtE21_OF8Z?usp=sharing

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

Earth = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW3/CleanedEarthquakes.csv')

# Group by Year and sum the Depth and Magnitude
scale_by_year = Earth.groupby('Year')[['Depth', 'Magnitude']].sum().reset_index()

# Create a scatter plot for Depth vs Magnitude
plt.figure(figsize=(10, 6))

# Plot all points
plt.scatter(scale_by_year['Depth'], scale_by_year['Magnitude'], color='turquoise', alpha=0.6, edgecolors='w', s=100)

# Find the index of the highest Magnitude
max_index = scale_by_year['Magnitude'].idxmax()
max_row = scale_by_year.iloc[max_index]

# Highlight the maximum point
plt.scatter(max_row['Depth'], max_row['Magnitude'], color='plum', s=100, label='Max Magnitude')

# Label the maximum point
plt.text(max_row['Depth'], max_row['Magnitude'], '', fontsize=10, ha='right', color='plum')
plt.text(max_row['Depth'], max_row['Magnitude'], str(int(max_row['Year'])), fontsize=10, ha='left')

# Add labels and title
plt.title('Scatter Plot of Depth vs Magnitude (1965-2016)')
plt.xlabel('Depth')
plt.ylabel('Magnitude')
plt.legend()
plt.grid()

# Show the plot
plt.tight_layout()
plt.show()

```

### Multi-Line Chart


Idiom: Multi-Line Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Total Sales | value, quantitative| Continuous and color (y-axis) |
| Year |  key, categorical | Continuous and color (x-axis) |

![MultiChart](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW3/Multi.png)

- Link to Google Colab, https://colab.research.google.com/drive/1YiCT849OzoAe1kA6tMM0T3XtE21_OF8Z?usp=sharing

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

VideoG = pd.read_csv('/content/drive/MyDrive/Colab Notebooks/CS625/HW3/CleanedVGsales.csv')

VideoG = VideoG[(VideoG['Year'].between(2000, 2016)) & (VideoG['Publisher'] == 'Electronic Arts')]
VideoG['Year'] = VideoG['Year'].astype(int)

# Filter for years between 2000 and 2016
fVideoG = VideoG[(VideoG['Year'] >= 2000) & (VideoG['Year'] <= 20016)]

# Group by Year and sum the sales
sales_by_year = VideoG.groupby('Year')[['NA_Sales', 'JP_Sales', 'EU_Sales', 'Other_Sales']].sum().reset_index()

# Create a multi-line plot
plt.figure(figsize=(10, 6))

# Plot each sales category
plt.plot(sales_by_year['Year'].astype(str), sales_by_year['NA_Sales'], label='NA Sales', marker='o', color='turquoise')
plt.plot(sales_by_year['Year'].astype(str), sales_by_year['JP_Sales'], label='JP Sales', marker='o', color='plum')
plt.plot(sales_by_year['Year'].astype(str), sales_by_year['EU_Sales'], label='EU Sales', marker='o', color='lightgreen')
plt.plot(sales_by_year['Year'].astype(str), sales_by_year['Other_Sales'], label='Other Sales', marker='o', color='orange')

# Add labels and title
plt.title('Multi-Line Plot of Sales by Year (2000-2016) For Electronic Arts')
plt.xlabel('Year')
plt.ylabel('Total Sales (in millions)')
plt.xticks(rotation=45)
plt.legend()
plt.tight_layout()
plt.grid()

# Show the plot
plt.show()

```


## Chart from Tableau 

Idiom: Scatter Plot / Mark: Dots
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Magnitude | value, quantitative| color (y-axis) |
| Depth | value, quantitative| color (x-axis) |


![TableauChart](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW3/Tableau.png)



## Reflection
- I thought it was easier to code the chart than to use Tableau to create the chart. Before this class I have never used Tableau and I belive that impacts my ease of use with the tool. It took me awhile to understand how to plot the points on the Tableau chart as I forgot that you have to drag the dimension to one of the options on the marks card before the data is plotted on the chart. It was easier on Tableau to label the points as on the chart I coded if I labeled all the points they would have overlapped but on Tableau there is a setting where you can avoid overlap. It was also relatively easy to change the color of the maximum point from the rest of the points but I could not figure out how to add a legened. I like on Tableau how you can change the chart type with a simple click of a button once you have the data set up. I do believe that once I spend more time with Tableau it will become easier to create charts that are pretty and easy to understand.



## References
* Reference 1, https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
* Reference 2, https://github.com/MainakRepositor/Datasets/blob/master/vgsales.csv
* Reference 3, https://github.com/MainakRepositor/Datasets/blob/master/earthquakes.csv
* Reference 4, https://colab.research.google.com/drive/1YiCT849OzoAe1kA6tMM0T3XtE21_OF8Z?usp=sharing
* Reference 5, https://matplotlib.org/stable/users/explain/colors/colormaps.html
* Reference 6, https://matplotlib.org/stable/users/explain/colors/colors.html#sphx-glr-users-explain-colors-colors-py
*Reference 7, https://help.tableau.com/current/pro/desktop/en-us/buildexamples_scatter.htm

