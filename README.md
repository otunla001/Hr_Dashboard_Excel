# HR_ DASHBOARD

# Data Portfolio: SQL - EXCEL







# Table of contents 

- [Objective](#objective)
- [Data Source](#data-source)
- [Stage](#stage)
 - [Tools](#tools)
- [Development](#development)
   - [Data Exploration](#data-exploration)
  - [Data Cleaning](#data-cleaning)
  - [Transform the Data](#transform-the-data)
  - [Create the SQL View](#create-the-sql-view)
- [Visualization](#visualization)
- [Conclusion](#conclusion)




# Objective 

- What is the key Main point? 

Provide the HR department with actionable insights into employee performance, demographics, satisfaction


- What is the ideal solution? 

To create a dashboard that provides insights into the Hr Data that includes their 
-	Employee Count by Department & State
-	Total Employee By Gender Breakdown
-	Total Employee By Department
-	Total Employee By Marital Status
-	Total Employee By Recruitment Source 
-	Satisfaction Levels
-	Employment Status (Active vs Terminated)




## User story 

As the Head of Human Resources, I want to use the HR dashboard to monitor employee performance and satisfaction across the company.
This dashboard should allow me to identify top-performing departments and low-performing ones based on key metrics such as Employee Satisfaction Score, Marital Status of Total Employee, Active and Terminated Employee, and Employee Recruitment Source.
With this information, I can make more informed decisions about which departments or teams to reward, where to allocate more support or training, and how to improve employee retention and engagement overall.



# Data source 

- Where is the data coming from? 
The data is sourced from Kaggle (an Excel extract)


# Stages

- Design
- Developement
- Testing
- Analysis 

 

## Tools 


| Tool | Purpose |
| --- | --- |
| Excel | Exploring the data, Visualizing the data via interactive dashboards |
| SQL Server | Cleaning, testing, and analyzing the data |
| GitHub | Hosting the project documentation and version control |



# Development

## Pseudocode

- What's the general approach in creating this solution from start to finish?

1. Get the data
2. Explore the data in Excel
3. Load the data into SQL Server
4. Clean the data with Excel
5. Test the data with SQL
6. Visualize the data in Excel
7. Generate the findings based on the insights
8. Write the documentation + commentary
9. Publish the data to GitHub Pages

## Data exploration notes

This is the stage where you have a scan of what's in the data, errors, inconcsistencies, bugs, weird and corrupted characters etc  


- What are your initial observations with this dataset? What's caught your attention so far? 

1. There are at least 12 columns that contain the data we need for this analysis, which signals we have everything we need from the file without needing to contact the client for any more data. 
2. We have more data than we need.




## Data cleaning 
- What do we expect the clean data to look like? (What should it contain? What contraints should we apply to it?)

The aim is to refine our dataset to ensure it is structured and ready for analysis. 

The cleaned data should meet the following criteria and constraints:

- Only relevant columns should be retained.
- All data types should be appropriate for the contents of each column.
- No column should contain null values, indicating complete data for all records.

Below is a table outlining the constraints on our cleaned dataset:

| Property | Description |
| --- | --- |
| Number of Rows | 312 |
| Number of Columns | 16 |


- What steps are needed to clean and shape the data into the desired format?

1. 	Remove unnecessary columns by only selecting the ones you need
2.	Replace Voluntarily Terminated and Terminated for cause to Terminated
3.	Rename columns using aliases
4.	CHANGE M-Male F-Female
5.	CHANGE Employee satisfactory from 1- Very low, 2- low, 3-Acceptable, 4-High, 5- Very high




### Transform the data  

## Analyze key Indicators 
### SQL query 
```sql

-- Total Employees
SELECT COUNT(*) AS Headcount FROM hrdata

-- Active Employees
SELECT COUNT(*) AS Active_Employees FROM hrdata WHERE EmploymentStatus = 'Active'

-- Terminated Employees
SELECT SUM(CASE WHEN EmploymentStatus IN ('Voluntarily Terminated', 'Terminated for Cause') THEN 1 ELSE 0 END) AS Terminated_Employee FROM hrdata

-- 4) Total Male Employee: SELECT COUNT(*) AS Male FROM hrdata WHERE Gender = 'M'

-- 5) Total Female Employee: SELECT COUNT(*) AS Female FROM hrdata WHERE Gender = 'F'


CHARTS RQUIREMENT

We would like to visualize various aspects of our pizza sales data to gain insights and understand key trends. We have identified the following requirements for creating charts:

-- Gender Breakdown
SELECT Gender, COUNT(*) FROM hrdata GROUP BY Gender

-- Recruitment Source
SELECT RecruitmentSource, COUNT(*) AS Total_Employees FROM hrdata GROUP BY RecruitmentSource

-- Department Distribution
SELECT Department, COUNT(*) AS Total_Employees FROM hrdata GROUP BY Department

-- Marital Status
SELECT MaritalStatus, COUNT(*) AS Total_Employees FROM hrdata GROUP BY MaritalStatus

-- Satisfaction Levels
SELECT 
  CASE EmployeeSatisfaction
    WHEN 1 THEN 'Very Low'
    WHEN 2 THEN 'Low'
    WHEN 3 THEN 'Acceptable'
    WHEN 4 THEN 'High'
    WHEN 5 THEN 'Very High'
    ELSE 'Unknown'
  END AS Satisfaction_Level,
  COUNT(*) AS Total_Employees
FROM hrdata
GROUP BY Satisfaction_Level

```
# TOTAL_EMPLOYEE
![Terminated Employees](Document/Headcount.png)
#  ACTIVE_EMPLOYEES
![Active Employees](Document/Active.png)
# TERMINATED_EMPLOYEES
![Terminated](Document/Terminated.png)
# MALE_EMPLOYEES
![Male](Document/Male.png)
#  FEMALE_EMPLOYEES
![Female](Document/Female.png)

# Visualization 


## Results

- What does the dashboard look like?

![Excel Dashboard](Document/Excel%20HR%20DB.png)

# Analysis 

## Findings

- What did we find

-  Gender Breakdown
   - 43% Male / 57% Female  
   - IT/IS mostly male, Production mostly female  

- Department Distribution
  - *Top 3 Departments:*  
    - Production  
    - IT/IS  
    - Sales  
   - These departments drive core company functions  

- Marital Status
   - High number of Singles and Marrieds  

- Recruitment Sources
  - Majority from *Indeed*, followed by *LinkedIn*   

- Satisfaction Levels
  - Most employees fall into *“Acceptable”*  
  - Some departments with high workload scored *“Low”*  

- Employment Status
   - 67% *Active* / 33% *Terminated*



