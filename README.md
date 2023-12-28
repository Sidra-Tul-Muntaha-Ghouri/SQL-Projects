# Yelp Data Analysis

## Table of Contents

1. [Overview](#overview)
2. [About the Dataset](#about-the-dataset)
3. [ER-Diagram of the Data](#er-diagram-of-the-data)
4. [Part 1: Dataset Profiling and Understanding](#part-1-dataset-profiling-and-understanding)
   1. [Profile the data by finding the total number of records for each of the tables](#profile-the-data-by-finding-the-total-number-of-records-for-each-of-the-tables)
   2. [Find the total distinct records by either the foreign key or primary key for each table](#question-2-find-the-total-distinct-records-by-either-the-foreign-key-or-primary-key-for-each-table)
   3. [Are there any columns with null values in the Users table? Indicate "yes," or "no."](#question-3-are-there-any-columns-with-null-values-in-the-users-table-indicate-yes-or-no)
   4. [For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields](#question-4-for-each-table-and-column-listed-below-display-the-smallest-minimum-largest-maximum-and-average-mean-value-for-the-following-fields)
   5. [List the cities with the most reviews in descending order](#question-5-list-the-cities-with-the-most-reviews-in-descending-order)
   6. [Find the distribution of star ratings to the business in the following cities](#question-6-find-the-distribution-of-star-ratings-to-the-business-in-the-following-cities)
   7. [Find the top 3 users based on their total number of reviews](#question-7-find-the-top-3-users-based-on-their-total-number-of-reviews)
   8. [Does posing more reviews correlate with more fans?](#question-8-does-posing-more-reviews-correlate-with-more-fans)
   9. [Are there more reviews with the word "love" or with the word "hate" in them?](#question-9-are-there-more-reviews-with-the-word-love-or-with-the-word-hate-in-them)
   10. [Find the distribution of star ratings to the business in the following cities](#question-10-find-the-distribution-of-star-ratings-to-the-business-in-the-following-cities)
5. [Part 2: Inferences and Analysis](#part-2-inferences-and-analysis)
   1. [Pick one city and category of your choice and group the businesses in that city or category by their overall star rating](#question-1-pick-one-city-and-category-of-your-choice-and-group-the-businesses-in-that-city-or-category-by-their-overall-star-rating)
   2. [Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed?](#question-2-group-business-based-on-the-ones-that-are-open-and-the-ones-that-are-closed-what-differences-can-you-find-between-the-ones-that-are-still-open-and-the-ones-that-are-closed)
   3. [For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis](#question-3-for-this-last-part-of-your-analysis-you-are-going-to-choose-the-type-of-analysis-you-want-to-conduct-on-the-yelp-dataset-and-are-going-to-prepare-the-data-for-analysis)

## Overview
This Project is an assignment from [SQL For Data Science](https://coursera.org/share/af562401cc2e1311f74e6ef3acec7fb2) This project utilized the knowledge of a wide range of concepts and SQL design techniques discussed throughout the course. 

In this project, I played the role of a real-world **Data Scientist** using SQL to both answer specific questions for an organization and make inferences based on my discoveries. 

## About the Dataset
The dataset used in this project is from a US-based organization called Yelp, which provides a platform for users to provide reviews and rate their interactions with a variety of organizations – businesses, restaurants, health clubs, hospitals, local governmental offices, charitable organizations, etc. Yelp has made a portion of this data available for personal, educational, and academic purposes.

## ER-Diagram of the Data
![ER Diagram](https://github.com/Sidra-Tul-Muntaha-Ghouri/Yelp_Data_Analysis/blob/main/Yelp%20Dataset%20ER%20diagram.PNG?raw=true)

## Part 1: Dataset Profiling and Understanding

In this section, a series of questions were posed with the primary goal of unraveling the composition and scale of the data, shedding light on its fundamental characteristics.
### Questions:
Following questions are addressed in this section:

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
Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

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
	
		min:1		max:5		avg:3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min:1		max:5		avg:3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min:0		max:2		avg:0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min:1		max:53		avg:1.9414
		
	
	v. Table: User, Column: Review_count
	
		min:0		max:2000		avg:24.2995

**CODE**:
```SQL
SELECT Min(COLUMN)  AS min,
       Max (COLUMN) AS max,
       Avg(COLUMN)  AS avg
FROM   _relevant_table 
```

5. List the cities with the most reviews in descending order.
   
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

**CODE**:
```SQL
SELECT   city,
         Sum(review_count) AS total reviews
FROM     business
GROUP BY city
ORDER BY review_count DESC
```
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
	
**ANSWER**: There is no correlation between reviews and fans.

_Order by reviews count in descending_

| name      | fans | review_count |
|-----------|------|--------------|
| Gerald    |  253 |         2000 |
| Sara      |   50 |         1629 |
| Yuri      |   76 |         1339 |
| .Hon      |  101 |         1246 |
| William   |  126 |         1215 |
| Harald    |  311 |         1153 |
| eric      |   16 |         1116 |
| Roanna    |  104 |         1039 |
| Mimi      |  497 |          968 |
| Christine |  173 |          930 |
| Ed        |   38 |          904 |
| Nicole    |   43 |          864 |
| Fran      |  124 |          862 |
| Mark      |  115 |          861 |
| Christina |   85 |          842 |
| Dominic   |   37 |          836 |
| Lissa     |  120 |          834 |
| Lisa      |  159 |          813 |
| Alison    |   61 |          775 |
| Sui       |   78 |          754 |
| Tim       |   35 |          702 |
| L         |   10 |          696 |
| Angela    |  101 |          694 |
| Crissy    |   25 |          676 |
| Lyn       |   45 |          675 |


_Order by fans in descending_ 

| name      | fans | review_count |
|-----------|------|--------------|
| Amy       |  503 |          609 |
| Mimi      |  497 |          968 |
| Harald    |  311 |         1153 |
| Gerald    |  253 |         2000 |
| Christine |  173 |          930 |
| Lisa      |  159 |          813 |
| Cat       |  133 |          377 |
| William   |  126 |         1215 |
| Fran      |  124 |          862 |
| Lissa     |  120 |          834 |
| Mark      |  115 |          861 |
| Tiffany   |  111 |          408 |
| bernice   |  105 |          255 |
| Roanna    |  104 |         1039 |
| Angela    |  101 |          694 |
| .Hon      |  101 |         1246 |
| Ben       |   96 |          307 |
| Linda     |   89 |          584 |
| Christina |   85 |          842 |
| Jessica   |   84 |          220 |
| Greg      |   81 |          408 |
| Nieves    |   80 |          178 |
| Sui       |   78 |          754 |
| Yuri      |   76 |         1339 |
| Nicole    |   73 |          161 |

Based on the results above, we can conclude that fans and the number of reviews are not correlated.

9. Are there more reviews with the word "love" or with the word "hate" in them?

**CODE** used to arrive at answer:
```SQLSELECT reviews,
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

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
   
> i. Do the two groups you chose to analyze have a different distribution of hours?

  _I analyzed the data of Toronto Restaurants & Phoenix Restaurants. The distribution of hours was just a little bit different. The restaurants having 4-5 stars rating seems to have less hours where as the restaurants with 2-3 stars rating have more hours._

> ii. Do the two groups you chose to analyze have a different number of reviews?

  _Yes, the restaurants with 4-5 stars rating have more reviews than the restaurants with 2-3 stars rating._

> iii. Are you able to infer anything from the location data provided between these two groups? Explain.

  _No, every business is related to a different zip-code._

**CODE**:
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
**OUTPUT**
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

		
2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		


i. Average review count of the closed businesses is less than the opened ones.\
ii.  No other difference in this particular category.

**CODE** used to arrive at answer:
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

	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
         I'm gonna analyze which business category is most popular.
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:

I'll need star ratings, review counts, and the names of the businesses. I chose this because I want to know which categories of businesses are more popular globally.
Within the categories, I compute the mean star rating, total reviews and total number of businesses for each category. To ensure statistical validity, I only focus on 25 categories with most businesses. 

The results reveal that;
	1.Restaurants have an average star rating of 3.45, with a substantial total of 3,772 reviews spread across 53 businesses.
	2.Shopping businesses exhibit a higher average star rating of 4.0, based on 945 reviews from 25 businesses.
	3.The Food category receives an average star rating of 3.73, derived from 1,588 reviews spanning 20 businesses.
	4.Health & Medical services showcase positive feedback, with an average star rating of 4.22 from 198 reviews across 16 businesses.
	5.Home Services have an average star rating of 3.93, derived from 91 reviews across 15 businesses.
	6.Beauty & Spas receive an average star rating of 3.79 based on 116 reviews from 12 businesses.
	7.Nightlife establishments receive an average star rating of 3.63, with a total of 952 reviews distributed among 12 businesses.
	8.Bars, with a slightly higher average star rating of 3.64, are represented by 945 reviews across 11 businesses.
	9.Active Life businesses demonstrate an average star rating of 4.15, based on 131 reviews from 10 businesses.
	10.Local Services have an exceptionally high average star rating of 4.35, with 94 reviews spread across 10 businesses.
                  
iii. Output of your finished dataset:
         
| category               | avg_star_rating | total_review_count | business_count |
|------------------------|-----------------|--------------------|----------------|
| Restaurants            | 3.45            | 3772               | 53             |
| Shopping               | 4.0             | 945                | 25             |
| Food                   | 3.73            | 1588               | 20             |
| Health & Medical       | 4.22            | 198                | 16             |
| Home Services          | 3.93            | 91                 | 15             |
| Beauty & Spas          | 3.79            | 116                | 12             |
| Nightlife              | 3.63            | 952                | 12             |
| Bars                   | 3.64            | 945                | 11             |
| Active Life            | 4.15            | 131                | 10             |
| Local Services         | 4.35            | 94                 | 10             |
| Automotive             | 4.5             | 198                | 9              |
| American (Traditional) | 3.81            | 1114               | 8              |
| Hotels & Travel        | 3.44            | 372                | 8              |
| Arts & Entertainment   | 4.0             | 388                | 7              |
| Burgers                | 2.86            | 293                | 7              |
| Fast Food              | 3.21            | 185                | 7              |
| Hair Salons            | 4.08            | 65                 | 6              |
| Sandwiches             | 3.92            | 715                | 6              |
| Doctors                | 4.2             | 55                 | 5              |
| Mexican                | 3.7             | 315                | 5              |
| Apartments             | 3.5             | 20                 | 4              |
| Auto Repair            | 4.63            | 122                | 4              |
| Bakeries               | 4.13            | 209                | 4              |
| Indian                 | 3.63            | 60                 | 4              |
| Parks                  | 3.88            | 80                 | 4              |

