# HW 2 - CS 625, Spring 2025


Homework 2: Data Cleaning

Heather Marsh 



**Due:** Februrary  09, 2025 by 11:59pm  

## Part 1. Data Cleaning
1.	Remove rows/columns:

    i.	Remove blank rows/row contain misleading values/columns that has no values (more than one column of the same row for example). Remove the column "Gross".
- I removed the column "Gross" by clicking on the "Gross" column → Edit Column → Remove Column.
- To remove the blank rows/row contain misleading values/columns I first created a new column that I called "Missing Values". This new column counts the number of missing values in each row using a GREL expression:
  
    ```grel
    if(isNull(cells['MOVIES'].value), 1, 0) +
    if(isNull(cells['GENRE'].value), 1, 0) + 
    if(isNull(cells['RATING'].value), 1, 0) + 
    if(isNull(cells['ONE-LINE'].value), 1, 0) +
    if(isNull(cells['STARS'].value), 1, 0) + 
    if(isNull(cells['VOTES'].value), 1, 0) + 
    if(isNull(cells['RunTime'].value), 1, 0)
    ```
  - I then preformed a numeric facet on the "Missing Values" column and sorted it to show me the rows that had 1 or greater blank values. I then deleted the rows with blank values and the "Missing Values" column.

    ii.	Remove rows that contain misleading info. You must explain in your report the criteria you defined to remove those selected row(s)/column(s). [It should be noted movie/series may have several sequels with same name]
    - I merged all the clusters of the "Stars" column then the "Movies" column using the Key collision and fingerprint method. My resoning is that if the cells clustered, they were likely the same movie. I found 26 clusters in the "Stars" column and 3 clusters in the "Movies" column.


2.	Refilling the values in the column(s):

Refill the blank cells for the columns "Rating", "Votes", and "Run Time" to 0 and change their data type to numeric. Similarly check values of all other columns and update the values accordingly (free to decide). 
- I refilled the blank cells for the columns "Rating", "Votes", and "Run Time" with 0 and changed their data types to numeric. I checked the values of all other columns and update the values accordingly as well. To change the columns to numeric I clicked on the desired Column → Edit Cells → Common Transforms → To Number.To refill the blank cells and check the values of the other columns I used these GREL expressions:
  
      - `if(isNull(value), 0, value)`, For Rating
  
      - `if(isNull(value), 0, value)`, For Votes
  
      - `if(isNull(value), 0, value)`, For RunTime
  
      - `value.replace(",", "")`, for votes
  
      - `if(isNull(value), "N/A", value)`, Replaces the empty Movies with "N/A".
  
      - `if(isNull(value), "N/A", value)`, Replaces the empty Year with "N/A".
  
      - `if(isNull(value), "N/A", value)` , Replaces the  empty One-Line with "N/A".
  


3. The column "Year
   
   i. Remove the rows if the cell value is Roman numerals/string only.
   
   ii. Replace the value of the year that enclosed by (xxxx) single year only.

   
-- `value.trim()`  (Remove all spaces)
- `if(length(value) < 9, value.replace("(", "").replace(")", ""), value)`, Removes the parentheses for single year values.
- `if(length(value) < 7, value.replace(/–/,""), value)`, Removes the symbol "–" for single year values.
- `value.replace(/[a-zA-Z ]+/, '')`, Removes all the letters and spaces.
- `value.replace("()", "")`, Removes the empty parentheses.
- `if(length(value) < 9, value.replace("(", "").replace(")", ""), value)`, Removes the  perenthesis for columns with single year value. This can catch the new values after letters have been removed.
- `if(length(value) < 7, value.replace(/–/,""),value)`, Removes the symbol (–) for single year values, This can catch the new values after letters have been removed.

   iii. After successful execution of (i) to (iii) the "Year" column may have values in the format (xxxx-xxxx) or ( xxxx-xxxx). Create new columns namely "startYear" and "endYear". Then fill the their cell by extracting value(s) from "Year" column.
  
- `if(length(value) < 7, value.replace(value,"(" + value + /–/ + value + ")"),value)`
  This to transform all the single year values to this format, (xxxx-xxxx)
- I then split the "Year" column in two by a field length of 5 each, the result was two columns, Year 1 with format (xxxx and Year 2 with format, –xxxx.
- I then renamed the column YEAR 1 to startYear and the column YEAR 2 to endYear.
- I then used: `value.replace("(", "")` to replace the open parenthesis symbol in startYear.
- Then I used: `value.replace(/–/, "")` to replace the "–" symbol in endYear.
- Now I had to two columns that I could convert to numeric values.
  
   iv. Remove the column "Year" after successful execution of steps 3.(i) - 3(iii).
- I then removed the "Year" column.


4.	Create a new column called "Verdict" and fill its values based on the criteria given below:

|   Rating       |  Verdict     |
|----------------|--------------|
| 0              |  Not known   |
|>0 and <=4.5    |    Flop      |
|>4.5 and <=6.5  |   Average    |
|>6.5 and <=8.0  |     Hit      |
| Above>8.0      |   Super Hit  |
|----------------|--------------|

- To create a new column I clicked on the desired Column → Edit column → Add column based on this column
- The first GREL expression I used was `if(value == 0, "Not known", value)`, no values were changed.
- Then `if(isNumeric(value), if ((value > 0).and(value <= 4.5), "Flop", value), value)` Replace values >0 and <=4.5 with Flop and ignore none numeric values in verdict, 330 values were changed.
- `if(isNumeric(value), if ((value > 4.5).and(value <= 6.5), "Average", value), value)` Replace values >4.5 and <=6.5 with  Average and ignore none numeric values in verdict, 2081 values were changed.
- `if(isNumeric(value), if ((value > 6.5).and(value <= 8.0), "Hit", value), value)` Replace values >6.5 and <=8.0 with  Hit and ignore none numeric values in verdict, 3256 values were changed.
-  `if(value > 8.0, "Super Hit", value)` if value is greater than 8 in Verdict replace with "Super Hit", 1103 values were changed.


Export
 - I then exported the file as HW2-Movies.csv, https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW2/HW2-Movies.csv
 - Then I extracted the JSON scripts containing all operations and saved as HW2-Movies.json, https://github.com/odu-cs625-datavis/Spring25-asv-Heather-Marsh/blob/main/HW2/HW2-Movies.json

## Part 2. Analyze Cleaned Data

1.	How many movies were listed as “Super Hit” in the year 2021?
- 58 movies were listed as “Super Hit” in the year 2021, I found this numberr by created two text facets, one on the "startYear" column and one on the "Verdict" column. I then selected "Super Hit" and "2021" from the facets to see that there were 58 matches. 


2.	Which movie got highest rating in the years 2018 to 2020 by genre, one movie for each genre?
- In this time frame there are 312 genres so I decided to only pick the movies that had one genre listed as there were a lot of movies that had three genres listed and I was unsure if they counted as their own genre or if they counted as allof the generes listed. If the Three genre movies counted as all of their genres then I would have tio pick whuch genere I listed them as and this could of led to inconsistencies, therefore I am only looking at movies that list one genre.
  
Listed below are the movies I found by preforming a text facet on "startYear" and "Genre" then sorting the "Rating" by largest numbers first:
- Action: Wira
- Adventure: Dolphin Kick
- Animation: LEGO Friends: Girls on a Mission
- Biography: Rocco Chinnici
- Comedy: Middleditch & Schwartz
- Crime: Historia de un crimen: Colmenares and Jamtara: Sabka Number Ayega tied
- Documentary: Our Planet
- Drama: The Queen's Gambit
- Family: Go! La Fiesta Inolvidable
- Fantasy: Meomchoogo Sipeun Soongan: Eobawoottaim
- Gameshow: Interior Design Masters
- Horror: Dachra
- Music: Ben Platt Live from Radio City Music Hall
- Musical: Westside
- Mystery: Khan: No. 1 Crime Hunter
- Reality-TV: Car Masters: Rust to Riches
- Romance: TharnType
- Sci-Fi: Futmalls
- Sport: Selection Day
- Talk-Show: My Next Guest Needs No Introduction with David Letterman
- Thriller: Black Earth Rising
- War: 21 Sarfarosh Saragarhi 1897


 
3.	List the top 3 genres (no duplicates) that got lowest number of votes (excluding 0)
- The first genre is Animation, the second genre is Comedy, and the third genre is Documentary. I found these genres by preforming a text facet on  the "Votes" column and then selecting the lowest counts. Animation and was in the count with 10 votes and Comedy and Documentary had 100 votes. 


 
4.	Name the director who directed the 10 minutes run time movie in the year 2020 that received highest number of votes. The output must list name of the movie, number of votes, and genre.
 - The director who directed the 10 minutes run time movie in the year 2020 that received highest number of votes is Hong Won-ki. Hong Won-ki directed Goedam, a Short, Horror, Mystery with 694 votes. I found this by cretaing a text facet on the "RunTime" column and selecting "10". I then created a text facet on the "startYear" column and selected 2020. I  was left with two options so I selected the movie with the most ratings. 

 
5.	List the top 5 movies that received highest number of votes, but verdict is “Flop” 
 -    The top five movies are: Death Note, The Human Centipede (First Sequence), Scary Movie 5, 365 Days, and Sharknado. I found these movies by text facting the "Verdict" column and then I selected "Flop" from the "Verdict" column. Then I sorted the votes column to see the largest number of votes on top. 


## References
* Reference 1, https://www.kaggle.com/datasets/bharatnatrayn/movies-dataset-for-feature-extracion-prediction?select=movies.csv
* Reference 2, https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet
* Reference 3, https://openrefine.org/docs/manual/grel
