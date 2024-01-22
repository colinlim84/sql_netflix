# Case Study #1: Netflix : Most Critically Acclaimed Genre

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
