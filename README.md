### UK MOT Test Analysis: Finding the Right Used Car

## Project Overview
Once you pass your driving test, the common and usual next step is to get a car and enjoy your new found freedom. Since passing my driving test, I've spent years browsing on Autotrader or facebook market without feeling confident enough to commit. 
I decided to look into the data to answer my simple question: *Which car is actually worth buying?*

Using the UK's Goverment Anonymised MOT results, I set out to uncover which car make, fuel type and age brackets consistently performed best. This project represents an end-to-end data analytics workflow entirely in Excel, from raw data cleaning to insight generation. 

## The Data

Source: [MOT testing data results (2024)](https://www.data.gov.uk/dataset/c63fca52-ae4c-4b75-bab5-8b4735e1a4c9/anonymised-mot-tests-and-results)
I also downloaded MOT testing data lookup tables to help me make sense of the data.

Format: 12 CSV files (January - December 2024), each containing over 1 million rows of test results. 

Key Challenge: Processing over 12 million rows on a mac laptop with hardware limitations required thoughtful data reduction and efficient cleaning strategies.

### Project Details
## Data Cleaning Process- Below is the summary of the data cleaning process for every CSV files: 
1. Removing duplicate `test_id` - Identified and removed duplicates to ensure no test was counted multiple times, which would skew pass/fail calculations
2. Filtering for Cars Only - The dataset includes multiple vehicle types. My focus was passenger cars therefore I filtered the `test_class` to code 4 to represent cars / passenger vehicles
3. Identifyinig duplicate `vehicle_id` - I sorted the `vehicle_id` to descending order and then applied conditional formatting to the column to highlight the duplicate vehicle_ids. This helped me track vehicles with multiple test histories, which became useful for analysing pass / fail rates over time.
4. cleaning the `completed_date` field - The raw `completed_date` field used the format: 
``` 
15/03/2024T14:30:00.00Z
```
I split this into date and time column by
- removing the `T` delimiter
- Extracted the timestamp to its own column and named it `completed_timestamp`
- Cleaned the timestamp by removing the `.000Z` suffix

5. Sorting to identify Test histories- Sorted `test_date`, `completed_date` and `completed_timestamp` into ascending order
6. Standardising Date and Time formats - I ensured all date columns were consistently formatted as DD/MM/YYYY to avoid confusion during analysis. I ensured the `completed_timestamp` were in a consistent 24-hour format for chronological accuracy
7. Cleaning Vehicle Make - Using the `UNIQUE` function, I generated a list of all car makes in the dataset. This then exposed numerous spelling variation and typos. I used Find & Replace to standardise over 50 car makes to their proper names, ensuring accurate grouping for analysis
8. Standardising `fuel_type` - The dataset used codes for fuel types (e.g "ED" for Electric Diesel, "PE" for Petrol) but it not all entries were in the code form. I used Find & Replace all to standardise text entries like "Electric" and "Hybrid Electric (clean)" to "EL" and "HY" respectively.

Lastly, due to hardware constraints, I exctracted over 30,000-row sample for analysis. This allowed me to develop and test my analysis approach before considering how to scale. 

## 1. 📊 Overview / Descriptive Analysis 
-What is the overall pass vs fail rate?
-How many tests are conducted per year / month?
-What is the trend in pass rates over time?
-What is the average vehicle age at test?
-What is the average mileage at time of test?


## 2. 🚗 Vehicle Insights 
Which car makes/models fail the most?
Which vehicles have the highest pass rates?
Do newer vehicles pass more often than older ones?
How does mileage impact pass/fail rate?
Which vehicle types are most reliable over time?

## 3. ❌ Failure Analysis
This dataset is great for this.
What are the most common reasons for MOT failure?
Which failure categories are increasing over time?
Do certain car brands fail for specific reasons?
Are there patterns between:
mileage and failure type?
age and failure type?

## 4. 📈 Trend Analysis 
How have failure rates changed over time (pre/post 2018 changes)?
Are vehicles becoming more reliable over time?
Which failure types are decreasing/increasing year-on-year?
Are newer cars failing for different reasons than older cars?
