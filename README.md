# Cyclistic bike-share analysis - Case study

## Introduction

### Company Background

Cyclistic is a bike-share company in Chicago that features more than 5,800 bicycles and 600 docking stations
Cyclistic offers three different pricing options: day passes, annual memberships, and single-ride passes. Casual riders are customers who purchase single-ride or full-day passes. Member riders are customers who buy annual memberships.
The bikes can be unlocked from one station and returned to any other station in the system anytime.

### Business task
I’m a junior data analyst working in the marketing analyst team at Cyclistic. The director of marketing believes the company’s future success depends on maximising the number of annual memberships. Therefore, our team wants to understand how casual riders and annual members use Cyclistic bikes differently. 
These insights will then be used to develop marketing strategies to convert casual riders into member riders. 
Three questions will guide the future marketing program:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclists use digital media to influence casual riders to become members? 

The director of marketing has assigned our team the first question to answer: How do annual members and casual riders use Cyclistic bikes differently?

 ### Data

The data has been provided and used under the (Divvy Data License Agreement) Divvy generously open sources their internal historical trip data to the public.(Note: The datasets have a different name because Cyclistic is a fictional company)
The data has been made available by Motivate International Inc. under this licence.) It is released on a monthly schedule and can be downloaded from the Divvy bikes webpage in csv format.

We will analyse the previous 12 months from march 2023 to february 2024. 
This dataset contains monthly trip information for over 5.7 million trips.
The data provides details on each trip that took place in the given time period. This includes the:
- ride_id
- member_casual
- Start date and time
- End date and time
- Type of bike
- Start station
- End station

## Prepare and clean the data 

In order to upload and use the data in BigQuery, we downloaded the 12 CSV files from the period 3-2023 to 2-2024 and merged them into one CSV file. We saved the file in Google Drive and uploaded it to BigQuery. (the file contain 13 columns and 5,707,168 rows)

### Check for duplicates

![image](https://github.com/Nizar2804/Cyclistic-/blob/20061e7788d529a927799f31181f77d8e12890d7/images/duplicate%20check.png)

The query return “ There is no data to display ” mean there is no duplicate cells in the ride_id column

### Create new columns

- 1- start_hour ( Extract the start hour of a trip from started_at)
- 2- end_hour ( Extract the end hour of a trip from ended_at)
- 3- month ( Extract the month from started_at)
- 4- day_of_week ( Extract the day of week from started_at)
- 5- trip _duration_minutes ( calculate the trip length by subtracting ended_at and started_at)

![image](https://github.com/Nizar2804/Cyclistic-/blob/d7b13f15193ca4f03119da47e595984588921f9f/images/clean%20data.png)


We created a new table that includes 5 new columns as mentioned above. 
We used the started_at data to extract the ( Month, Day of week and hour)  of every trip. 
The calculation of trip length had returned some negative values ( the ended_at date is prior to the started_at date ).
         The rows have been removed. 


 ## ANALYZE

To answer the question: How do annual members and casual riders use Cyclistic bikes differently? 
- We started by analysing the proportion of member and casual riders: 
![image](https://github.com/Nizar2804/Cyclistic-/blob/946e16e59190c56b981ff1a57d25cee9d85c06ba/images/Total%20trips%20by%20customer%20type.png)

Over 64% of the trips are made by members and nearly 36% by casual riders During the period 3-2023 to 2-2024.


# Bike type preferences 
![image](https://github.com/Nizar2804/Cyclistic-/blob/main/images/Trips%20by%20Customer%20and%20Bike%20type.png)

- Annual members slightly prefer Classic bikes 51% to 49% Electric bikes usage. 
- Casual riders prefer Electric bikes: 
Electric bike 53% , Classic bike 44% , Docked bike 3%. 


# Trip count by time periods and Bike type

![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20bu%20months%20and%20bike%20type.png)			
- Both causal riders and annual members had more trips during the warmer months compared to	autumn and winter.
- Annual members had slightly increase during february using the classic bike.


   
![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20by%20dow%20and%20bike%20type.png)		

- Casual riders made more trips during the weekends, possibly part of them as a visitors.
- Annual members made more trips during the weekdays, possibly due to commuting.
  
![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20by%20hour%20and%20biketype.png)									
- Casual rides start a steady increase in the morning hours until they reach the peak at 5 PM.
- Annual members increase their bike usage significantly during 7-9 AM and 3-6 PM (commuting).

# Average trip duration

![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/avg%20by%20months.png)	


![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/avg%20by%20day%20of%20week.png)						


# Most popular start and end stations

![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/top%2010%20start%20stations.png)																									

![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/top%2010%20end%20stations.png)																									
