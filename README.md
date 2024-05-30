# Cyclistic bike-share analysis - Case study

## Introduction

### Company Background

Cyclistic, a bike-share company in Chicago that features more than 5,800 bicycles and 600 docking stations
Cyclistic offers three pricing options: day passes, annual memberships, and single-ride passes. Casual riders are customers who purchase single-ride or full-day passes. Member riders are customers who buy annual memberships.

### Business task
I’m a junior data analyst working in the marketing analyst team at Cyclistic. The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, our team wants to understand how casual riders and annual members use Cyclistic bikes differently. 
These insights will then be used to develop marketing strategies to convert casual riders into member riders. 
Three questions will guide the future marketing program:

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships? 
3. How can Cyclists use digital media to influence casual riders to become members? 

The director of marketing has assigned our team the first question to answer: How do annual members and casual riders use Cyclistic bikes differently?

 ### Data

The data has been provided and used under the (Divvy Data License Agreement) Divvy generously open sources their internal historical trip data to the public. (Note: The datasets have a different name because Cyclistic is a fictional company).

We will analyze the previous 12 months from March 2023 to February 2024. 
This dataset contains monthly trip information for over 5.7 million trips.
The data provides details on each trip that took place in the given period. This includes the following:
- ride_id
- member_casual
- Start date and time
- End date and time
- Type of bike
- Start station
- End station

## Prepare and clean the data 

To upload and use the data in BigQuery, we downloaded the 12 CSV files from the period 3-2023 to 2-2024 and merged them into one CSV file. We saved the file in Google Drive and uploaded it to BigQuery. (the file contains 13 columns and 5,707,168 rows).

### Check for duplicates

![image](https://github.com/Nizar2804/Cyclistic-/blob/c758b3ab33fbfba038fb19666b36a4100ef33e63/images/duplicate%20check.png)

Ensured no duplicate entries based on "ride_id".

### Create new columns

- 1- start_hour ( Extract the start hour of a trip from started_at)
- 2- end_hour ( Extract the end hour of a trip from ended_at)
- 3- month ( Extract the month from started_at)
- 4- day_of_week ( Extract the day of the week from started_at)
- 5- trip _duration_minutes ( calculate the trip length by subtracting ended_at and started_at)

![image](https://github.com/Nizar2804/Cyclistic-/blob/c758b3ab33fbfba038fb19666b36a4100ef33e63/images/clean%20data.png)


We created a new table that includes 5 new columns as mentioned above. 
We used the started_at data to extract the ( Month, Day of week, and hour)  of every trip. 
The calculation of trip length returned some negative values ( the ended_at date is before the started_at date ), The rows have been removed. 


 ## ANALYZE

To answer the question: How do annual members and casual riders use Cyclistic bikes differently? 
- We started by analyzing the proportion of member and casual riders: 
![image](https://github.com/Nizar2804/Cyclistic-/blob/c758b3ab33fbfba038fb19666b36a4100ef33e63/images/Total%20trips%20by%20customer%20type%20.png)

Over 64% of the trips are made by members and nearly 36% by casual riders During the period 3-2023 to 2-2024.


# Bike type preferences 
![image](https://github.com/Nizar2804/Cyclistic-/blob/c758b3ab33fbfba038fb19666b36a4100ef33e63/images/Trips%20by%20Customer%20and%20Bike%20type%20.png)

- Casual Riders Prefer Electric bikes (53%), followed by Classic bikes (44%), and 
  Docked bikes (3%). 
- Annual members, slightly preference for Classic bikes (51%) over Electric bikes 
  (49%).



# Trip count by periods and Bike type

![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20bu%20months%20and%20bike%20type.png)			
- Both causal riders and annual members had more trips during the warmer months compared to winter.
- Annual members show a slight increase in February, especially with classic bikes.


   
![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20by%20dow%20and%20bike%20type.png)		

- Casual riders made more trips during the weekends, likely due to tourists. 
- Annual members made more trips during the weekdays, likely for commuting.
  
![image](https://github.com/Nizar2804/Cyclistic-/blob/6323088c422bdf98c7f68b48ed9ea77bc9a57171/images/trips%20by%20hour%20and%20biketype.png)									
- Casual rides steadily increase in the morning hours, peaking at 5 PM.
- Annual members increase their bike usage significantly during 7-9 AM and 3-6 PM , aligning with typical commuting hours.

# Average trip duration

![image](https://github.com/Nizar2804/Cyclistic-/blob/cdf649bdad4e733f7800e5d72b8a2e4d88b53819/images/avg%20by%20months.png)

- The average trip duration of casual riders ranges between 21-25 minutes throughout the year (Peaking at 25 minutes in September), abnormally 18 minutes in March. 
- The average trip duration of annual members ranges between 10.5 minutes (March) and 13.5 minutes (July). 

![image](https://github.com/Nizar2804/Cyclistic-/blob/0c54dcde991772a7c3fb9b014a8d0e61200d4b4e/images/avg%20trip%20duration%20by%20dow.png)
- The average trip duration of casual riders is approximately double the annual members, (21-27 casual) to (12-14 annual members). 
- Both casual and annual members made longer trips during the weekends.

# Most popular start and end stations

![image](https://github.com/Nizar2804/Cyclistic-/blob/22c7e7b35a9464bbe26db76a8b984bc990188435/images/top%2010%20start%20stations%20-%20casual.png)
![image](https://github.com/Nizar2804/Cyclistic-/blob/22c7e7b35a9464bbe26db76a8b984bc990188435/images/top%2010%20end%20station%20-casual.png)
- Casual Riders: The most popular start and end station is Streeter Dr & Grand Ave.

![image](https://github.com/Nizar2804/Cyclistic-/blob/22c7e7b35a9464bbe26db76a8b984bc990188435/images/top%2010%20start%20station%20-%20member.png)																
![image](https://github.com/Nizar2804/Cyclistic-/blob/22c7e7b35a9464bbe26db76a8b984bc990188435/images/top%2010%20end%20station%20-%20members.png)
- Annual Members: Top stations include Clinton St & Washington Blvd, Kingsbury St & Kinzie St, and Clark St & Elm St.




# Recommendations and Marketing Strategies

- Target casual riders who are commuting, by offering them a discount if they sign up for an annual membership.
- Because of the popularity of Electric bikes among casual riders, offer special promotions or highlight the benefits of Electric bikes in 
  the annual membership package.
- Because of high usage by Casual riders on weekends, promote annual memberships to casual riders during their weekend rides, emphasizing 
  the benefits of frequent usage.
- Because of high usage by Casual riders in warmer months, target casual local riders through the summer highlight the cost-saving Annual 
  membership.
- Focusing marketing efforts on the most popular stations for both casual riders and annual members.









                      
