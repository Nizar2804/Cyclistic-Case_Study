Cyclistic bike-share analysis - Case study

Introduction

Company Background

Cyclistic is a bike-share company in Chicago that features more than 5,800 bicycles and 600 docking stations
Cyclistic offers three different pricing options: day passes, annual memberships, and single-ride passes. Casual riders are customers who purchase single-ride or full-day passes. Member riders are customers who buy annual memberships.
The bikes can be unlocked from one station and returned to any other station in the system anytime.

Business task
I’m a junior data analyst working in the marketing analyst team at Cyclistic. The director of marketing believes the company’s future success depends on maximising the number of annual memberships. Therefore, our team wants to understand how casual riders and annual members use Cyclistic bikes differently. 
These insights will then be used to develop marketing strategies to convert casual riders into member riders. 
Three questions will guide the future marketing program:

       1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclists use digital media to influence casual riders to become members? 

The director of marketing has assigned our team the first question to answer: How do annual members and casual riders use Cyclistic bikes differently?



Data

The data has been provided and used under the (Divvy Data License Agreement) Divvy generously open sources their internal historical trip data to the public.(Note: The datasets have a different name because Cyclistic is a fictional company)
The data has been made available by Motivate International Inc. under this licence.) It is released on a monthly schedule and can be downloaded from the Divvy bikes webpage in csv format.

We will analyse the previous 12 months from march 2023 to february 2024. 
This dataset contains monthly trip information for over 5.7 million trips.
The data provides details on each trip that took place in the given time period. This includes the:
ride_id
member_casual
Start date and time
End date and time
Type of bike
Start station
End station

Prepare and clean the data 

In order to upload and use the data in BigQuery, we downloaded the 12 CSV files from the period 3-2023 to 2-2024 and merged them into one CSV file. We saved the file in Google Drive and uploaded it to BigQuery. (the file contain 13 columns and 5,707,168 rows)






Check for duplicates

The query return “ There is no data to display ” mean there is no duplicate cells in the ride_id column

Create new columns

 1- start_hour ( Extract the start hour of a trip from started_at)
 2- end_hour ( Extract the end hour of a trip from ended_at)
 3- month ( Extract the month from started_at)
 4- day_of_week ( Extract the day of week from started_at)
 5- trip _duration_minutes ( calculate the trip length by subtracting ended_at and started_at)

CREATE TABLE
`airy-charmer-416112.Cyclistic.new_table` AS
SELECT
ride_id,
rideable_type,
member_casual,
started_at,
ended_at,
EXTRACT(HOUR FROM started_at) AS start_hour,
EXTRACT(HOUR FROM ended_at) AS end_hour,
CASE EXTRACT(MONTH FROM started_at)
   WHEN 1 THEN 'JAN'
   WHEN 2 THEN 'FEB'
   WHEN 3 THEN 'MAR'
   WHEN 4 THEN 'APR'
   WHEN 5 THEN 'MAY'
   WHEN 6 THEN 'JUN'
   WHEN 7 THEN 'JUL'
   WHEN 8 THEN 'AUG'
   WHEN 9 THEN 'SEP'
   WHEN 10 THEN 'OCT'
   WHEN 11 THEN 'NOV'
   WHEN 12 THEN 'DEC'
   END AS month,
CASE EXTRACT(DAYOFWEEK FROM started_at)
   WHEN 1 THEN 'SUNDAY'
   WHEN 2 THEN 'MONDAY'
   WHEN 3 THEN 'TUESDAY'
   WHEN 4 THEN 'WEDNESDAY'
   WHEN 5 THEN 'THURSDAY'
   WHEN 6 THEN 'FRIDAY'
   WHEN 7 THEN 'SATURDAY'   
   END AS day_of_week,
DATETIME_DIFF(ended_at,started_at, MINUTE)
       AS trip_duration_minutes
FROM `airy-charmer-416112.Cyclistic.3-2023_to_2-2024`
WHERE DATETIME_DIFF(ended_at,started_at, MINUTE) > 0


We created a new table that includes 5 new columns as mentioned above. 
We used the started_at data to extract the ( Month, Day of week and hour)  of every trip. 
The calculation of trip length had returned some negative values ( the ended_at date is prior to the started_at date ).
         The rows have been removed. 














ANALYZE
To answer the question: How do annual members and casual riders use Cyclistic bikes differently? We started by analysing the proportion of member and casual riders: 


Over 64% of the trips are made by members and nearly 36% by casual riders During the period 3-2023 to 2-2024.












Bike type preferences 




Annual members slightly prefer Classic bikes 51% to
          49% Electric bikes usage. 
While casual riders prefer Electric bikes: 
          Electric bike 53% , Classic bike 44% , Docked bike 3%. 

![image](https://github.com/Nizar2804/Cyclistic-/blob/main/images/a%20whole%20new%20world.tif)
