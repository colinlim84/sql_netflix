# Case Study #2: Netflix : Most Critically Acclaimed Genre

## 📚 Table of Contents
- [Business Task](#business-task)
- [Entity Relationship Diagram](#entity-relationship-diagram)
- [Question and Solution](#question-and-solution)

All information regarding this case has been sourced from [here](https://platform.stratascratch.com/coding/10171-find-the-genre-of-the-person-with-the-most-number-of-oscar-winnings?code_type=1). 


***

## Business Task
Find the genre of with the most number of oscar winnings.
If there are more than one genre with the same number of oscar wins, return the first one in alphabetic order. Use the names as keys when joining the tables.
***

## Entity Relationship Diagram
![image](https://github.com/colinlim84/sql_netflix/blob/main/Netflix_ERD.png)

***

## Table Preview

**oscar_nominees**

| year | category                     | nominee           | movie            | winner | id   |
| ---- | ---------------------------- | ----------------- | ---------------- | ------ | ---- |
| 2010 | actor in a leading role      | James Franco      | 127 Hours        | FALSE  | 648  |
| 2003 | actor in a supporting role   | Benicio Del Toro  | 21 Grams         | FALSE  | 139  |
| 2003 | actress in a leading role    | Naomi Watts       | 21 Grams         | FALSE  | 1119 |
| 2001 | actress in a supporting role | Jennifer Connelly | A Beautiful Mind | TRUE   | 710  |
| 2001 | actor in a leading role      | Russell Crowe     | A Beautiful Mind | FALSE  | 1315 |

**nominee_information**

| name            | amg_person_id | top_genre | birthday | id  |
| --------------- | ------------- | --------- | -------- | --- |
| Ruby Dee        | P 18243       | Drama     | 27/10/24 | 234 |
| Hal Holbrook    | P 32790       | Drama     | 17/2/25  | 241 |
| Cloris Leachman | P 41211       | Comedy    | 30/4/26  | 257 |
| Rosemary Harris | P 30676       | Drama     | 19/9/30  | 301 |
| Martin Landau   | P 40247       | Spy Film  | 20/6/31  | 312 |

***
## Question and Solution

### Breakdown the task

#### Request
1. Find number of Oscar won for each genre
2. Get the max number of Oscar count

#### What's needed?
1. Genre

#### Any specific order?
1. If there was a tie, return all result in alphabetical order

### Solution
````sql
-- 1. Find number of Oscar won for each genre
WITH winning_cnt AS (
SELECT 
    i.top_genre,
    COUNT(*) as winning_cnt
FROM oscar_nominees n
LEFT JOIN nominee_information i
ON n.nominee=i.name
WHERE winner=TRUE
    AND top_genre IS NOT NULL
GROUP BY 1)

SELECT top_genre
FROM winning_cnt
WHERE winning_cnt=(SELECT MAX(winning_cnt) FROM winning_cnt) --2. Get the max number of Oscar count
ORDER BY 1

````



### Output:
| title | 
| ----------- | 
| Drama | 
