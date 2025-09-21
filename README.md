# Hospital Patient Records Dataset

### Project Overview

A dataset containing patients of Massachussets General Hospital from 2011-2022, including information of over 75,000 records and 55 fields showing the records of patient demographics, insurance coverage, and medical encounters and procedures.

### Data Source

Hospital+Patient+Records.zip: The primary datasets used for this analysis was the "encounters.xlsx" Excel Workbook containing detailed information about patient encounters and the "procedures.xlsx" Excel Workbook containing detailed information about patient procedure data including surgeries.

### Tools

- Excel - Data Cleaning & Transformation
- Excel - Data Analysis
- Power Bi - Visualization

### Data Cleaning/Preparation

In the initial data preparation phase, I performed the following tasks:
1. Data loading & Inspection
2. Handling missing values (no missing values)
3. Removing duplicates (no duplicate values)
4. Data cleaning and formatting
5. Analysis
6. Visualization

### Exploratory Data Analysis (EDA)

EDA involved exploring the data to answer key questions such as:
- How many total encounters occurred each year?
- For each year, what percentage of all encounters belonged to each encounter class (ambulatory, outpatient, wellness, urgent care, emergency, and inpatient)?
- What percentage of encounters were over 24 hours versus under 24 hours?
- How many encounters had zero payer coverage, and what percentage of total encounters does this represent?
- What are the top 10 most frequent procedures performed and the average base cost for each?
- What are the top 10 procedures with the highest average base cost and the number of times they were performed?
- What is the average total claim cost for encounters, broken down by payer?

### Data Analysis

After inspection, it was seen that there are no duplicates nor missing values in the cells. No to answer the analytical questions a Pivot Table is needed. To find the total encounters each year, the encounter class in selected for both the rows and values. With the values having a field setting of "Count". The same can be done to find the percentage of encounters for each class but this time the values are divided by the grand total number of encounters and multiplied by 100. Instead of multiplying by 100, you can change the cell format to percentage.

To find the encounters over 24 hours, a time difference between the START and the STOP needs to be foound. The time in START and STOP can be found by extracting them to a new column using the MID() formula. When gotten, the formula below is used to find the time difference.

```excel
=IF([@StartHour]>[@StopHour],[@StopHour]+1,[@StopHour])-[@StartHour]
```

Once found, in a new column insert the formula ```=(TEXT([@TimeDifference], "hh"))*1```. This is used to extract the hour. Then finally, an IF statement is used to find is the encounter period (the time difference between the START and the STOP) is above 24 hours.

```excel
=IF([@Above24Hrs]>24, "yes", "no")
```

Now that we know which encouter is over or under 24 hours we can put this into a Pivot Table with the encounter class in both the rows and the value field. With the value field having a setting of "Count". A slicer is then inserted with the column which indicates which encounter is over or below 24 hours ticked.

The rest of the questions can be answered following the same pattern of inserting the needed values into the row and value fields of the Pivot Table. When one or more conditions are needed, a slicer can be inserted to filter out the needed value.

### Results/Findings

The analysis results are summarized as follows:
1. From 2011-2022 there were different total intervals for each year as follow; 1336, 2106, 2495, 3885, 2469, 2451, 2360, 2292, 2228, 2519, 3530, 220 respectively. A total of 12 years.
2. The encounters ambulatory, emergency, inpatient, outpatient, urgentcare, wellness have percentages of 44.95%, 8.33%, 4.07%, 22.59%, 13.14%, 6.92% respectively.
3. No encounters where above 24 hours
4. 13,586 encounters had zero payer coverage. A percentage of 48.71%
5. The total Avg Claim Cost is 3,639.68

### Limitations

A column showing the date and time when patients were admitted over time is missing from the dataset. Meaning insights cannot be generated to answer curious questions like;
1. How many unique patients were admitted each quarter over time?
2. How many patients were readmitted within 30 days of a previous encounter?
3. Which patients had the most readmissions?

### References

None
