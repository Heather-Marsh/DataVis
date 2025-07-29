# Final Project, Spring 2025


World Happiness Report 2005 - 2024

Heather Marsh 



Due: Sunday, April 20, 2025 by 11:59pm


# Introduction
I will be looking at the World Happiness Report from 2005-2024. The full scale report combines data from over 140 countries with high-quality analysis by world-leading researchers from a wide range of academic disciplines. This particular dataset that I have is a smaller scale report that only includes 10 of the 140 countries. The report focuses on factors that impact the happiness score of a country such as the GDP per capita, education index, life satisfaction score, mental health index, climate index and crime rate to name a few. Analyzing this data can show what problems countries are facing, how their populations are being impacted and how they compare to other countries.

## Data Source

- Name: World Happiness Report
- URL: https://www.kaggle.com/datasets/khushikyad001/world-happiness-report/data
- GitHub Link: https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/world_happiness_report.csv
- Description: This dataset contains 4,000 entries with 24 columns related to happiness, economic, social, and political indicators for different countries across multiple years.


## Project Code
- Colab: https://colab.research.google.com/drive/1Ji2xTqAubKQ9mTPqNJv1h_lhbp_H2Zim?usp=sharing
- GitHub: https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Project.ipynb

# Question 1, What are the key factors contributing to and from happiness across different countries?

Final Chart:


![Fg1](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg1.png)

Idiom: Bar Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Factors | key, categorical | vertical spatial region (y-axis) |
| Normalized Happiness Value | value, quantitative | horizontal position on a common scale (x-axis) |


This chart answers the question as it takes the normalized values for each selected factor and plots it on the graph to visualize the impact the factors have on the happinness score of the country. The chart is interactive as it filters per country to allow the viwer to see how the each country was impacted by the different factors. The graphs also have a feature where if you hover your cursor over the differnt bars it will display the name of the factor and the normalized value, allowing for clarity when viewing as the viewer does not need to guess the values of the bars. 

For a supporting chart I made a heatmap:



![Fg2](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg2.png)

This heatmap is a correlation analysis of all of the factors. With this we can see how the different factors impact eacch other. This heatmap is also interactive and you can select the country and it has teh same hover feature that tells you th evariables being used and the correlation score, allowing for an easier viewing experience as the heatmap is so large. A strong negative correlation indicates a strong inverse relationship between two variables, meaning as one variable increases, the other variable decreases significantly. A strong positive correlation means that two variables tend to move in the same direction, and this relationship is very strong

# Question 2, How does happiness change around the world from year to year?
Final Chart:


![Fg3](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg3.png)

Idiom: Bar Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| Country | key, Geographic geometry data |Space: use given geometry for area mark boundaries. |
| Happiness Score | value, quantitative per region|Color: sequential segmented colormap |


This chart solves the question as it is animated and shows through a color scale how happiness rates change for each country from 2005-2024. The map is interactive and you can move it around, it also has the hover feature that will tell you the name of the country and the happiness score, you can also interact with the bar on the bottom and manually slide or click to a year or you can press play and watch the animation. 

Supporting Charts:


![Fg4](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg4.png)

This scatter plot will show an animation that displays countries happiness scores vs their GDPs throughout the years (2005-2024). As the World Happiness Report contains multiple instances from the same year this chart can be a little confusing so the next graph is for better clarity. 

![Fg5](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg5.png)
This is another scatter plot that displays the maximum, minimum, and medium GDP per Captia scores for each country from 2005-2024, to get a better understanding of how a country's GDP can impact its happiness score. Unlike the previous graph which used color as a scale based on GDP per Capita, this graph filters the countries and gives each country its own unique color. By doing this it is easier to track the country throughout the time serie. So size was used a way to measure the GDP per Capita, to allow for enhanced visualizations.  

![Fg6](https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Fg6.png)
This last chart is a line chart the shows the average happiness score over time (2005-2024) for a selected country. This chart is interactive as it has the hover feature that allows a view to place their cursor over a point on the graph to see the year and the average happiness score. The happiness scores were averaged due to the fact that there are multiple instance of each country per year. I also started the y-axis at 4, as the countries never scored below a 3 and never rose above an 8. Having the y-axis start at 4 and stop at 7 allows for a better view of the data as the points are close together and with this new scale the visualizations can be compared more fairly.  

# Final Thoughts

Overall this project was very interesting and I was able to use a lot of libraries that I have not used before. Using plotly was interesting but I did have some challenges as some of my libraries seemingly did not want to work together in my Colab environment. For some of my visualizations I used widgets which did not always render correctly and when that happened I would have to uninstall and reinstall plotly. I had better sucess with using plotly express as it is a version of plotly that is more streamlined but it does not contain all of the interactive features that I wanted to use, and if my charts needed to use a widget I caould not use plotly express I needed to use plotly. I also experienced some challenges with using the colorscales in plotly but after looking at the tutorials, I had a better understanding of how they worked. There were also some challenges with the animated graphs as I had to sort the years before processing so that way the plots would play in the correct order. The development process was challenging but very rewarding. My two final main visualizations did take the most time, followed by the heatmap as sometimes the title for the heatmap would not appear. I enjoyed this project and I found my dataset very interesting and I believe that there is further investigation into the dataset that could be done. 




# References
-   Reference 1, https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/world_happiness_report.csv
-   Reference 2, https://colab.research.google.com/drive/1Ji2xTqAubKQ9mTPqNJv1h_lhbp_H2Zim?usp=sharing
-   Reference 3, https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/Project/Project.ipynb
-   Reference 4, https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
-   Reference 5, https://www.kaggle.com/datasets/khushikyad001/world-happiness-report/data
-   Reference 6, https://plotly.com/python/
-   Reference 7, https://ipywidgets.readthedocs.io/en/stable/examples/Widget%20List.html
-   Reference 8, https://ipython.readthedocs.io/en/stable/index.html
-   Reference 9, https://plotly.com/python/builtin-colorscales/
-   Reference 10, https://plotly.com/python/discrete-color
-   Reference 11, https://ipywidgets.readthedocs.io/en/latest/examples/Widget%20Basics.html
