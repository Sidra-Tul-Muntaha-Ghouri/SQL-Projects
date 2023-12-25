# Yelp Data Analysis

## Table of Content
- [Overview](#overview)
- [About the Dataset](#about_the_dataset)
- [ER-Diagram of the Data](#ER-Diagram-of-the-Data)
- [Part 1: Dataset Profiling and Understanding](#Part-1:-Dataset-Profiling-and-Understanding)
  - [Questions](#questions)
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
Following questions were addressed in this section:
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

**CODE** used to arrive at answer:
```SQL
SELECT COUNT(*) FROM _Relevant_Table
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
    xi. Elite_years = 2780 (user_id)\
   
**CODE** used to arrive at answer:
```SQL
SELECT COUNT(DISTINCT(KEY)) FROM _Relevant_Table
```
Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.

3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

Answer: NO

**CODE** used to arrive at answer:
```SQL
SELECT *
FROM user
WHERE column_name IS NULL_Relevant_Table
```
**Another Approach**
```SQL
SELECT COUNT(*) 
	FROM user
	WHERE id IS NULL OR
	name IS NULL OR
	review_count IS NULL OR
	yelping_since IS NULL OR
	useful IS NULL OR
	funny IS NULL OR
	cool IS NULL OR
	fans IS NULL OR	
	average_stars IS NULL OR
	compliment_hot IS NULL OR
	compliment_more IS NULL OR
	compliment_profile IS NULL OR
	compliment_cute IS NULL OR
	compliment_list IS NULL OR
	compliment_note IS NULL OR
	compliment_plain IS NULL OR	
	compliment_cool IS NULL OR	
	compliment_funny IS NULL OR
	compliment_writer IS NULL OR
	compliment_photos IS NULL
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

**CODE** used to arrive at answer:
```SQL
SELECT
MIN(column) AS min,
MAX (column) AS max,
AVG(column) AS avg
FROM _Relevant_Table
```

5. List the cities with the most reviews in descending order.
+-----------------+---------------+
		| city            | total_reviews |
		+-----------------+---------------+
		| Las Vegas       |         82854 |
		| Phoenix         |         34503 |
		| Toronto         |         24113 |
		| Scottsdale      |         20614 |
		| Charlotte       |         12523 |
		| Henderson       |         10871 |
		| Tempe           |         10504 |
		| Pittsburgh      |          9798 |
		| MontrÃƒÂ©al       |          9448 |
		| Chandler        |          8112 |
		| Mesa            |          6875 |
		| Gilbert         |          6380 |
		| Cleveland       |          5593 |
		| Madison         |          5265 |
		| Glendale        |          4406 |
		| Mississauga     |          3814 |
		| Edinburgh       |          2792 |
		| Peoria          |          2624 |
		| North Las Vegas |          2438 |
		| Markham         |          2352 |
		| Champaign       |          2029 |
		| Stuttgart       |          1849 |
		| Surprise        |          1520 |
		| Lakewood        |          1465 |
		| Goodyear        |          1155 |
		+-----------------+---------------+
		(Output limit exceeded, 25 of 362 total rows shown)
   
```SQL
SELECT city, SUM(review_count) AS total reviews
FROM business
GROUP BY city
ORDER BY review_count DESC
```

   
10. Find the distribution of star ratings to the business in the following cities.
```SQL
SELECT city, SUM(review_count) AS total reviews
FROM business
GROUP BY city
ORDER BY review_count DESC
```

## Part 2: Inferences and Analysis
