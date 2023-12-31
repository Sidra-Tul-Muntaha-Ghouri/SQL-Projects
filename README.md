# Yelp Data Analysis 
  
 ## Table of Contents 

1. [Overview](#overview)
2. [About the Dataset](#about-the-dataset)
3. [ER-Diagram of the Data](#er-diagram-of-the-data)
4. [Workflow](#workflow)
5. [Part 1: Dataset Profiling and Understanding](#part-1-dataset-profiling-and-understanding)
6. [Part 2: Inferences and Analysis](#part-2-inferences-and-analysis)
  
 ## Overview 
 This Project is an assignment from [SQL For Data Science](https://coursera.org/share/af562401cc2e1311f74e6ef3acec7fb2). This project utilized the knowledge of a wide range of concepts and SQL design techniques discussed throughout the course.  
  
 In this project, I played the role of a real-world **Data Scientist**, using SQL to both answer specific questions for an organization and make inferences based on my discoveries.  
  
 ## About the Dataset 
 The dataset used in this project is from a US-based organization called Yelp, which provides a platform for users to provide reviews and rate their interactions with a variety of organizations – businesses, restaurants, health clubs, hospitals, local governmental offices, charitable organizations, etc. Yelp has made a portion of this data available for personal, educational, and academic purposes. 
  
 ## ER-Diagram of the Data
 Below is the Entity Diagram (ER Diagram) of the Yelp dataset.
 ![ER Diagram](https://github.com/Sidra-Tul-Muntaha-Ghouri/Yelp_Data_Analysis/blob/main/Yelp%20Dataset%20ER%20diagram.PNG?raw=true) 
 
 An ER diagram is a visual tool that can represent various elements like entities, entity attributes, relationship sets, and attributes of relationship sets. In the context of this diagram:

- The **Yellow key** icons found in tables, such as the 'id' in the business table, signify the primary key of that table.
- The **Red diamond** icons, on the other hand, represent foreign keys linking to another table. For instance, 'business_id' in the review table is a foreign key associated with the business table.
- **Dashed lines** connecting tables illustrate the relationships between them. For example, if the business table has a one-to-many relationship with other tables, this connection is depicted by dashed lines in the diagram. 
## Workflow

The analysis is structured into two main parts, each serving a distinct purpose in understanding and extracting valuable insights from the Yelp dataset.
###  1. Data profiling & Understanding
     
In this initial phase, the focus is on unraveling the composition and scale of the Yelp dataset. A series of questions guide the exploration, ranging from profiling the data by finding the total number of records for each table to uncovering the distribution of star ratings across various cities. The intent is to lay the groundwork for a comprehensive understanding of the dataset's fundamental characteristics.

###  2. Inferences and Analysis.
  
Building upon the insights gained from dataset profiling, the second part delves into more nuanced analyses. Specific questions guide the examination of factors such as the differences between businesses with 2-3 stars and those with 4-5 stars, the distinctions between open and closed businesses, and the identification of the most popular business categories. Each analysis is designed to extract actionable insights, fostering a deeper understanding of Yelp's rich dataset.

This structured workflow ensures a systematic approach, allowing for a holistic exploration of the dataset and the generation of meaningful inferences that can inform decision-making processes.

 ## Part 1: Dataset Profiling and Understanding 
  
 In this section, a series of questions are posed with the primary goal of unraveling the composition and scale of the data, shedding light on its fundamental characteristics. 
 ### Questions: 
  
 1. Profile the data by finding the total number of records for each of the tables. 
  
  i. Attribute table = 10000\
  ii. Business table = 10000\
  iii. Category table = 10000\
  iv. Checkin table = 10000\
  v. elite_years table = 10000\
  vi. friend table = 10000\
  vii. hours table =10000\
  viii. photo table =10000\
  ix. review table = 10000\
  x. tip table = 10000\
  xi. user table = 10000\
  
 **CODE:**  
 ```SQL 
 SELECT Count(*) 
 FROM   _relevant_table  
 ``` 

  
 2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key. 
  
     i. Business = 10000 (id)\
     ii. Hours = 1562 (business_id)\
     iii. Category = 2643 (business_id)\
     iv. Attribute = 1115 (business_id)\
     v. Review = 8090 (business_id)\
     vi. Checkin = 493 (business_id)\
     vii. Photo = 6493 (business_id)\
     viii. Tip = 3979 (business_id)\
     ix. User = 10000 (id)\
     x. Friend = 11 (user_id)\
     xi. Elite_years = 2780 (user_id) 
  
 **CODE:** 
 ```SQL 
 SELECT Count(DISTINCT( KEY )) 
 FROM   _relevant_table  
 ``` 
 Note: Primary Keys are denoted in the ER Diagram with a yellow key icon. 
  
 3. Are there any columns with null values in the Users table? Indicate "yes," or "no." 
  
 Answer: NO
  
 **CODE**: 
 ```SQL 
 SELECT * 
 FROM user 
 WHERE column_name IS NULL 
 ``` 
 **Another Approach** 
 ```SQL 
 SELECT Count(*) 
 FROM   USER 
 WHERE  id IS NULL 
         OR NAME IS NULL 
         OR review_count IS NULL 
         OR yelping_since IS NULL 
         OR useful IS NULL 
         OR funny IS NULL 
         OR cool IS NULL 
         OR fans IS NULL 
         OR average_stars IS NULL 
         OR compliment_hot IS NULL 
         OR compliment_more IS NULL 
         OR compliment_profile IS NULL 
         OR compliment_cute IS NULL 
         OR compliment_list IS NULL 
         OR compliment_note IS NULL 
         OR compliment_plain IS NULL 
         OR compliment_cool IS NULL 
         OR compliment_funny IS NULL 
         OR compliment_writer IS NULL 
         OR compliment_photos IS NULL  
 ``` 
 3. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields: 
  
           i. Table: Review, Column: Stars 
  
                 min:1                max:5                avg:3.7082 
  
  
         ii. Table: Business, Column: Stars 
  
                 min:1                max:5                avg:3.6549 
  
  
         iii. Table: Tip, Column: Likes 
  
                 min:0                max:2                avg:0.0144 
  
  
         iv. Table: Checkin, Column: Count 
  
                 min:1                max:53                avg:1.9414 
  
  
         v. Table: User, Column: Review_count 
  
                 min:0                max:2000                avg:24.2995 
  
 **CODE**: 
 ```SQL 
 SELECT Min(COLUMN)  AS min, 
        Max (COLUMN) AS max, 
        Avg(COLUMN)  AS avg 
 FROM   _relevant_table  
 ``` 
  
 5. List the cities with the most reviews in descending order.

     **CODE**: 
 ```SQL 
 SELECT   city, 
          Sum(review_count) AS total reviews 
 FROM     business 
 GROUP BY city 
 ORDER BY review_count DESC 
 ``` 
  
 | city            | total_reviews | 
 |-----------------|---------------| 
 | Las Vegas       | 82854         | 
 | Phoenix         | 34503         | 
 | Toronto         | 24113         | 
 | Scottsdale      | 20614         | 
 | Charlotte       | 12523         | 
 | Henderson       | 10871         | 
 | Tempe           | 10504         | 
 | Pittsburgh      | 9798          | 
 | Montréal        | 9448          | 
 | Chandler        | 8112          | 
 | Mesa            | 6875          | 
 | Gilbert         | 6380          | 
 | Cleveland       | 5593          | 
 | Madison         | 5265          | 
 | Glendale        | 4406          | 
 | Mississauga     | 3814          | 
 | Edinburgh       | 2792          | 
 | Peoria          | 2624          | 
 | North Las Vegas | 2438          | 
 | Markham         | 2352          | 
 | Champaign       | 2029          | 
 | Stuttgart       | 1849          | 
 | Surprise        | 1520          | 
 | Lakewood        | 1465          | 
 | Goodyear        | 1155          | 
  
 (Output limit exceeded, 25 of 362 total rows shown)"  
  

 6. Find the distribution of star ratings to the business in the following cities: 
  
         i. Avon 
  
 **CODE**: 
 ```SQL 
 SELECT stars, 
        Count (*) AS stars_count 
 FROM   business 
 WHERE  city = 'Avon' 
 GROUP  BY stars 
 ORDER  BY stars DESC  
 ``` 
 **OUTPUT** 
  
 | stars | stars_count | 
 |-------|-------------| 
 | 5.0   | 1           | 
 | 4.5   | 1           | 
 | 4.0   | 2           | 
 | 3.5   | 3           | 
 | 2.5   | 2           | 
 | 1.5   | 1           | 
  
         ii. Beachwood 
  
 **CODE**: 
  
 ```SQL 
 SELECT stars, 
        Count (*) AS stars_count 
 FROM   business 
 WHERE  city = 'Beachwood' 
 GROUP  BY stars 
 ORDER  BY stars DESC  
 ``` 
 **OUTPUT** 
  
 | stars | stars_count | 
 |-------|-------------| 
 |   5.0 |           5 | 
 |   4.5 |           2 | 
 |   4.0 |           1 | 
 |   3.5 |           2 | 
 |   3.0 |           2 | 
 |   2.5 |           1 | 
 |   2.0 |           1 | 
  
  
 7. Find the top 3 users based on their total number of reviews: 
  
 **CODE**: 
 ```SQL 
 SELECT name, 
        review_count 
 FROM   user 
 ORDER  BY review_count DESC 
 LIMIT  3  
 ```                 
 **OUTPUT** 
  
 | name      | review_count | 
 |-----------|--------------| 
 | Gerald    |         2000 | 
 | Sara      |         1629 | 
 | Yuri      |         1339 | 
  
  
 8. Does posing more reviews correlate with more fans? 
  
 _Order by reviews count in descending_    | |    _Order by fans in descending_ 

 | name      | fans | review_count |   | name      | fans | review_count |
|-----------|------|--------------|---|-----------|------|--------------|
| Gerald    | 253  | 2000         |   | Amy       | 503  | 609          |
| Sara      | 50   | 1629         |   | Mimi      | 497  | 968          |
| Yuri      | 76   | 1339         |   | Harald    | 311  | 1153         |
| .Hon      | 101  | 1246         |   | Gerald    | 253  | 2000         |
| William   | 126  | 1215         |   | Christine | 173  | 930          |
| Harald    | 311  | 1153         |   | Lisa      | 159  | 813          |
| eric      | 16   | 1116         |   | Cat       | 133  | 377          |
| Roanna    | 104  | 1039         |   | William   | 126  | 1215         |
| Mimi      | 497  | 968          |   | Fran      | 124  | 862          |
| Christine | 173  | 930          |   | Lissa     | 120  | 834          |
| Ed        | 38   | 904          |   | Mark      | 115  | 861          |
| Nicole    | 43   | 864          |   | Tiffany   | 111  | 408          |
| Fran      | 124  | 862          |   | bernice   | 105  | 255          |
| Mark      | 115  | 861          |   | Roanna    | 104  | 1039         |
| Christina | 85   | 842          |   | Angela    | 101  | 694          |
| Dominic   | 37   | 836          |   | .Hon      | 101  | 1246         |
| Lissa     | 120  | 834          |   | Ben       | 96   | 307          |
| Lisa      | 159  | 813          |   | Linda     | 89   | 584          |
| Alison    | 61   | 775          |   | Christina | 85   | 842          |
| Sui       | 78   | 754          |   | Jessica   | 84   | 220          |
| Tim       | 35   | 702          |   | Greg      | 81   | 408          |
| L         | 10   | 696          |   | Nieves    | 80   | 178          |
| Angela    | 101  | 694          |   | Sui       | 78   | 754          |
| Crissy    | 25   | 676          |   | Yuri      | 76   | 1339         |
| Lyn       | 45   | 675          |   | Nicole    | 73   | 161          |

 
 Based on the results above, i can say that fans and the number of reviews are not correlated.\Gerald, who has the most fans, only has 253 reviews. Yuri has only 76 fans, but has the 1339 reviews. 
  
 9. Are there more reviews with the word "love" or with the word "hate" in them? 
  
 **CODE**: 
 ```SQL
SELECT reviews, 
        Count(reviews)                               AS review_count, 
        ( Count(reviews) * 100.0 / (SELECT Count(*) 
                                    FROM   review) ) AS percentage 
 FROM   (SELECT CASE 
                  WHEN text LIKE '%love%' THEN 'love' 
                  WHEN text LIKE '%hate%' THEN 'hate' 
                  ELSE 'others' 
                END reviews 
         FROM   review) 
 GROUP  BY reviews  
 ``` 
 **OUTPUT** 
  
 | reviews | review_count | percentage | 
 |---------|--------------|------------| 
 | hate    | 178          | 1.78       | 
 | love    | 1780         | 17.8       | 
 | others  | 8042         | 80.42      | 
  
  
 10. Find the distribution of star ratings to the business in the following cities. 
  
 ```SQL 
 SELECT name, 
        fans 
 FROM   user 
 ORDER  BY fans DESC 
 LIMIT  10  
 ``` 
 **OUTPUT** 
 | name      | total_fans | 
 |-----------|------------| 
 | Amy       | 503        | 
 | Mimi      | 497        | 
 | Harald    | 311        | 
 | Gerald    | 253        | 
 | Christine | 173        | 
 | Lisa      | 159        | 
 | Cat       | 133        | 
 | William   | 126        | 
 | Fran      | 124        | 
 | Lissa     | 120        | 
  
  
 ## Part 2: Inferences and Analysis 
  
###** 1. Pick one city and category and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions.**
### Analysis Details:
City: Phoenix
Category: Restaurants

### CODE:

 ```SQL 
 SELECT b.NAME, 
        b.city, 
        c.category, 
        h.hours, 
        Avg(b.review_count), 
        postal_code, 
        CASE 
          WHEN b.stars BETWEEN 2 AND 3 THEN '2-3 stars' 
          WHEN B.stars BETWEEN 4 AND 5 THEN '4-5 stars' 
          ELSE '1 or less stars' 
        END AS star_rating 
 FROM   business b 
        INNER JOIN hours h 
                ON b.id = h.business_id 
        INNER JOIN category c 
                ON c.business_id = b.id 
 WHERE  city IN ( 'Toronto', 'Phoenix' ) 
        AND category = 'Restaurants' 
 GROUP  BY NAME 
 ORDER  BY star_rating DESC  
 ``` 
 **OUTPUT DATASET** 
 | name                                   | city    | category    | hours                | Avg(b.review_count) | postal_code | star_rating     | 
 |----------------------------------------|---------|-------------|----------------------|---------------------|-------------|-----------------| 
 | Bootleggers Modern American Smokehouse | Phoenix | Restaurants | Saturday|11:00-22:00 | 431.0               | 85028       | 4-5 stars       | 
 | Cabin Fever                            | Toronto | Restaurants | Saturday|16:00-2:00  | 26.0                | M6P 1A6     | 4-5 stars       | 
 | Charlie D's Catfish & Chicken          | Phoenix | Restaurants | Saturday|11:00-18:00 | 7.0                 | 85034       | 4-5 stars       | 
 | Edulis                                 | Toronto | Restaurants | Saturday|18:00-23:00 | 89.0                | M5V         | 4-5 stars       | 
 | Sushi Osaka                            | Toronto | Restaurants | Saturday|11:00-23:00 | 8.0                 | M9A 1C2     | 4-5 stars       | 
 | 99 Cent Sushi                          | Toronto | Restaurants | Saturday|11:00-23:00 | 5.0                 | M5B 2E5     | 2-3 stars       | 
 | Big Smoke Burger                       | Toronto | Restaurants | Saturday|10:30-21:00 | 47.0                | M4B 2L9     | 2-3 stars       | 
 | Gallagher's                            | Phoenix | Restaurants | Saturday|9:00-2:00   | 60.0                | 85024       | 2-3 stars       | 
 | McDonald's                             | Phoenix | Restaurants | Saturday|5:00-0:00   | 8.0                 | 85004       | 2-3 stars       | 
 | Pizzaiolo                              | Toronto | Restaurants | Saturday|10:00-4:00  | 34.0                | M5H 1X6     | 2-3 stars       | 
 | Five Guys                              | Phoenix | Restaurants | Saturday|10:00-22:00 | 63.0                | 85008       | 1 or less stars | 
  
  
 > i. Do the two groups you chose to analyze have a different distribution of hours? 
  
   I analyzed the data of Toronto Restaurants & Phoenix Restaurants. The distribution of hours was just a little bit different. The restaurants having 4-5 star ratings seem to have fewer hours where whereas the restaurants with 2-3 star ratings have more hours._
  
 > ii. Do the two groups you chose to analyze have a different number of reviews? 
  
   The two groups i chose for analysis are restaurants in Phoenix and Toronto.
- Phoenix Restaurants:
  - Bootleggers Modern American Smokehouse: 431.0 reviews
  - Cabin Fever: 26.0 reviews
  - Charlie D's Catfish & Chicken: 7.0 reviews
  - Gallagher's: 60.0 reviews
  - McDonald's: 8.0 reviews
  - Total reviews for Phoenix Restaurants: 431.0+26.0+7.0+60.0+8.0=532.0

- Toronto Restaurants:
  - Cabin Fever: 26.0 reviews
  - Edulis: 89.0 reviews
  - Sushi Osaka: 8.0 reviews
  - 99 Cent Sushi: 5.0 reviews
  - Big Smoke Burger: 47.0 reviews
  - Pizzaiolo: 34.0 reviews
  - Total reviews for Toronto Restaurants: 26.0+89.0+8.0+5.0+47.0+34.0=209.0

### Conclusion:
Phoenix Restaurants have a total review count of 532.0, while Toronto Restaurants have a total review count of 209.0.

 > iii. Are you able to infer anything from the location data provided between these two groups? Explain.
### Inference from Location Data:
- The location data includes postal codes and city information.
- Phoenix Restaurants have postal codes like 85028, 85034, 85024, and 85004.
- Toronto Restaurants have postal codes like M6P 1A6, M5V, M9A 1C2, M5B 2E5, M4B 2L9, and M5H 1X6.
- There is a clear distinction in postal codes between the two groups, indicating they are in different geographical locations.
                 
### 2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed?

 **CODE**: 
 ```SQL 
  
 SELECT b.NAME, 
        b.city, 
        c.category, 
        h.hours, 
        Avg(b.review_count), 
        postal_code, 
        b.is_open, 
        CASE 
          WHEN b.stars BETWEEN 2 AND 3 THEN '2-3 stars' 
          WHEN B.stars BETWEEN 4 AND 5 THEN '4-5 stars' 
          ELSE '1 or less stars' 
        END AS star_rating 
 FROM   business b 
        INNER JOIN hours h 
                ON b.id = h.business_id 
        INNER JOIN category c 
                ON c.business_id = b.id 
 WHERE  city IN ( 'Toronto', 'Phoenix' ) 
        AND category = 'Restaurants' 
 GROUP  BY NAME 
 ORDER  BY is_open DESC  
 ``` 

 **OUTPUT** 
 | name                                   | city    | category    | hours                | AVG(b.review_count) | postal_code | is_open | star_rating | 
 |----------------------------------------|---------|-------------|----------------------|---------------------|-------------|---------|-------------| 
 | Big Smoke Burger                       | Toronto | Restaurants | Saturday|10:30-21:00 | 47.0                | M4B 2L9     | 1       | 2-3 stars   | 
 | Bootleggers Modern American Smokehouse | Phoenix | Restaurants | Saturday|11:00-22:00 | 431.0               | 85028       | 1       | 4-5 stars   | 
 | Cabin Fever                            | Toronto | Restaurants | Saturday|16:00-2:00  | 26.0                | M6P 1A6     | 1       | 4-5 stars   | 
 | Edulis                                 | Toronto | Restaurants | Saturday|18:00-23:00 | 89.0                | M5V         | 1       | 4-5 stars   | 
 | Five Guys                              | Phoenix | Restaurants | Saturday|10:00-22:00 | 63.0                | 85008       | 1       | 2-3 stars   | 
 | Gallagher's                            | Phoenix | Restaurants | Saturday|9:00-2:00   | 60.0                | 85024       | 1       | 2-3 stars   | 
 | McDonald's                             | Phoenix | Restaurants | Saturday|5:00-0:00   | 8.0                 | 85004       | 1       | 2-3 stars   | 
 | Pizzaiolo                              | Toronto | Restaurants | Saturday|10:00-4:00  | 34.0                | M5H 1X6     | 1       | 2-3 stars   | 
 | Sushi Osaka                            | Toronto | Restaurants | Saturday|11:00-23:00 | 8.0                 | M9A 1C2     | 1       | 4-5 stars   | 
 | 99 Cent Sushi                          | Toronto | Restaurants | Saturday|11:00-23:00 | 5.0                 | M5B 2E5     | 0       | 2-3 stars   | 
 | Charlie D's Catfish & Chicken          | Phoenix | Restaurants | Saturday|11:00-18:00 | 7.0                 | 85034       | 0       | 4-5 stars   | 

  ### Differences
1. Restaurants that are closed usually have fewer reviews on average.
2. Both open and closed restaurants have a combination of different star ratings.
3. The operating hours differ between open and closed establishments.
4. Additionally, there's a variety of postal codes for both open and closed restaurants.
  
### 3. For this part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis. 

In this section, I analyzed the data to ascertain the most popular business category.
  
I used star ratings, review counts, and the names of the businesses. This decision was made to discern the global popularity of various business categories. Within each category, I calculated the mean star rating, total reviews, and the overall number of businesses.
To ensure statistical validity, I only focused on 25 categories with most businesses.  

Here's the SQL code I wrote for the analysis:

## CODE
```SQL
SELECT c.category,
       Round(Avg(b.stars), 2) AS avg_star_rating,
       Sum(b.review_count)    AS total_reviews,
       Count(b.id)            AS business_count
FROM   category c
       INNER JOIN business b
               ON b.id = c.business_id
GROUP  BY c.category
ORDER  BY business_count DESC
```
### OUTPUT DATASET:
  
| category               | avg_star_rating | total_reviews | business_count | open_business |
|------------------------|-----------------|---------------|----------------|---------------|
| Restaurants            | 3.46            | 4504          | 71             | 71            |
| Shopping               | 3.98            | 977           | 30             | 30            |
| Food                   | 3.78            | 1781          | 23             | 23            |
| Nightlife              | 3.48            | 1351          | 20             | 20            |
| Bars                   | 3.5             | 1322          | 17             | 17            |
| Health & Medical       | 4.09            | 203           | 17             | 17            |
| Home Services          | 4.0             | 94            | 16             | 16            |
| Beauty & Spas          | 3.88            | 119           | 13             | 13            |
| Local Services         | 4.21            | 100           | 12             | 12            |
| American (Traditional) | 3.82            | 1128          | 11             | 11            |

 ### Key Findings  
1. **Restaurants**: Unsurprisingly, "Restaurants" emerge as the most common type of business, boasting 71 establishments. The sheer volume of businesses, coupled with a substantial 4504 reviews, signifies the prevalent choice of entrepreneurs and the high engagement level of Yelp users in the restaurant category.
2. **Health & Medical** and **Home Services**: Although relatively fewer in number, "Health & Medical" and "Home Services" stand out with high average star ratings of 4.09 and 4.0, respectively. This suggests positive perceptions and satisfied customers within these categories.
3. **Bars and American (Traditional)**: Categories like "Bars" and "American (Traditional)" present a competitive landscape with a moderate average star rating. Despite this, their considerable number of businesses indicates a vibrant market.
4. **Local Services**: Topping the list with an impressive 4.21 average star rating, "Local Services" showcases businesses that consistently garner positive reviews, indicating a high level of customer satisfaction.

### Wrap-Up
Looking at the popular business types gives us a picture of what people enjoy and what's competitive. If you're thinking of starting a business, you might want to consider how restaurants dominate, the potential in Health and medical and Home Services, and the competitive nature of Bars and American (Traditional). The success of Local Services tells us that making customers happy is a big deal. Overall, this info helps businesses make smart choices and do well.

