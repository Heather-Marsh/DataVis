# HW 1 - CS 625, Spring 2025

Heather Marsh  
Due: January 26, 2025

## Git, GitHub

*What is the URL of the GitHub repo that you created in your personal account?*
- https://github.com/Heather-Marsh/CS625HW1repo.git
   
*What is pull vs clone in GitHub?*
- Pull in Github refers to when modified friles are copied to a local machine. Clone refers to when all files regardless of modification are copied to a local machine. 
   
*You have committed a change on your local machine/remote. However, you want to undo the changes committed. How would you do that?*
- To undo the changes committed you should create a new commit with the changes that you want to undo.

## Markdown

*Create a bulleted list with at least 3 items*
- One item
- Two items
- Three items
- Four items

*Write a single paragraph that demonstrates the use of italics, bold, bold italics, code, and includes a link. The paragraph must explain your favorite Olympic sport/game, the country that won the most number of olympic GOLD medals (Summer) in your favorite sport in 2020 (Japan) and 2024 (France). You are free to include more information.*
- My favorite **Summer Olympic Sport** is *Gymnastics*. **_Olympic gymnastics_** has been an event at *every* Summer Olympic Games since the start of the modern olympics at the **1896 Summer Olympics in Athens**. For the **_first 32 years_**, *only men* were allowed to compete but starting at the **_1928 Summer Olympics in Amsterdam_** women were allowed to compete in artistic gymnastics events. **Rhythmic gymnastics** events were introduced at the **_1984 Summer Olympics in Los Angeles_**, and *trampoline events* were added at the **_2000 Summer Olympics in Sydney_**. This informatin was found at this link [Gymnastics at the Summer Olympics](https://en.wikipedia.org/wiki/Gymnastics_at_the_Summer_Olympics). `The country with the most gold medals in 2020 was the People's Republic of China with 4` and `the country with the most gold medals in 2024 was the People's Republic of China with 3`. 
 
```python
s = "Python syntax highlighting"
print s
```

*Create a level 3 heading*
### Level 3 heading

*Insert a image of your favorite Olympics sport/game, sized appropriately*

![alt text](https://www.insidegymnastics.com/wp-content/uploads/2024/07/WomensFinalTeamLeo-1536x1268.jpg "USA Gymnastics")


## Tableau

*Insert the image of your horizontal bar chart here. Reminder, this should show countries that won the least number of medals only (excluding ZERO) in Paris2024 Summer Olynpics by continent (one country from each continent is ok).*

![MedalTable](https://github.com/user-attachments/assets/9d1f83a9-c688-4b08-a5cc-bd1d1a7943e2)


## Google Colab

*What is the URL of your Google Colab notebook?*
- https://colab.research.google.com/drive/1t8e__7lrDA3nValYMUZn42JsDKEZ4ex2?usp=sharing

## Python/Seaborn

*Insert the first penguin chart here*
![Penguin1](https://github.com/user-attachments/assets/f28df837-751e-442a-a6ab-a5d4721dd3e1)

*Describe what the figure is showing.*
- This figure is showing how individual penguins dill depth related to their bill lengths, other wise how long and how wide the beaks of the penguins are. 

*Insert the second penguin chart here*
![Penguin2](https://github.com/user-attachments/assets/71d3c514-059d-4cda-8ac5-ae30fff7de2b)

*Describe what the figure is showing.*
- This figure shows how penguin species compare to eac other based on sex and body weight. 

*What happened when you removed the outer parentheses from the code? Why?*
- What happened when I removed the outher parentheses was that I recieved this error "SyntaxError: invalid syntax". I got this error because in order for this code to run it needs the outer parentheses otherwise it is an invalid piece of code. 

## Observable and Vega-Lite

*What happens when you replace `markCircle()` with `markSquare()`?*
- When you replace `markCircle()` with `markSquare()` the shape of the markers on the grraph change from circles to squares. 

*What happens when you replace `markCircle()` with `markPoint()`?*
- When you replace `markCircle()` with `markPoint()` the shape of the markers on the grraph change from circles to circles with no center. 

*What change do you need to make to swap the x and y axes on the scatterplot?*
- To swap the x and y axes on the scatterplot you need to `change vl.x()` to `vl.y()` and `vl.y()` to `vl.x()`.

*Insert the bar chart image here*
![CarsByCountry](https://github.com/user-attachments/assets/350e19fa-4df8-4157-adf7-e3ac1e1701dd)

*Why do you think this chart is the result of this code change?*
- This chart is the result of the code change as if you delete `vl.y().fieldN("Origin"),` from the code you get rid of the countries of origin otherwise known as the y axis so all of the data gets combined int oone bar. 

## References

*Every report must list the references (including the URL) that you consulted while completing the assignment. Replace the items below with the references you consulted*

* Reference 1, <[https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet]>
* Reference 2, <[https://en.wikipedia.org/wiki/Gymnastics_at_the_2024_Summer_Olympics]>
* Reference 3, <[https://www.insidegymnastics.com/news-features/2024-paris-olympics-gymnastics-gk-elite-and-usa-gymnastics-unveil-leotards-and-apparel-for-summer-olympics/]>
* Reference 4, <[https://en.wikipedia.org/wiki/Gymnastics_at_the_Summer_Olympics]>
* Reference 5, <[https://observablehq.com/@observablehq/vega-lite]>
* Reference 6, <[https://rogerdudler.github.io/git-guide/]>
* Reference 7, <[https://help.tableau.com/current/guides/get-started-tutorial/en-us/get-started-tutorial-home.htm]>
*  Reference 8, <[https://colab.research.google.com/notebooks/basic_features_overview.ipynb]>
*  Reference 9, <[https://github.com/mcnakhaee/palmerpenguins]>
*  Reference 10, <[https://seaborn.pydata.org/tutorial/objects_interface.html]>
*  Reference 11, <[https://observablehq.com/@observablehq/a-taste-of-observable]>
