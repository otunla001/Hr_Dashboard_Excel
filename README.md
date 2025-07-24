# HR Dashboard – Excel

An interactive Human Resources dashboard built using Microsoft Excel. It provides actionable insights into workforce demographics, recruitment sources, employment status, and employee satisfaction levels.

---

## 📚 Table of Contents

- [🎯 Objective](#-objective)
- [📂 Data Source](#-data-source)
- [🎨 Design](#-design)
- [🛠 Tools](#-tools)
- [🧱 Development](#-development)
  - [🔍 Data Exploration](#-data-exploration)
  - [🧹 Data Cleaning](#-data-cleaning)
  - [🔄 Data Transformation](#-data-transformation)
  - [🧾 SQL Queries](#-sql-queries)
- [📊 Visualization](#-visualization)
- [📈 Analysis](#-analysis)
- [📌 Conclusion](#-conclusion)

---

## 🎯 Objective

**What is the key Main point?**
Provide the HR department with actionable insights into employee performance, demographics, satisfaction
**What is the ideal solution?**
To create a dashboard that provides insights into the Hr Dataset includes their
•	Employee Count by Department & State
•	Total Employee By Gender Breakdown
•	Total Employee By Department
•	Total Employee By Marital Status
•	Total Employee By Recruitment Source 
•	Satisfaction Levels
•	Employment Status (Active vs Terminated)
This will help the marketing team make informed decisions about which Pizza size, category that makes the highest and also lowest sales.
---

## 📂 User Story
As the Head of Human Resources, I want to use the HR dashboard to monitor employee performance and satisfaction across the company.
This dashboard should allow me to identify top-performing departments and low-performing ones based on key metrics such as Employee Satisfaction Score, Marital Status of Total Employee, Active and Terminated Employee, and Employee Recruitment Source.
With this information, I can make more informed decisions about which departments or teams to reward, where to allocate more support or training, and how to improve employee retention and engagement overall.

## 📂 Data Source

- Where is the data coming from? The data is sourced from Kaggle (an Excel extract)

---

## 🎨 Design

User Story:  
> *As the Head of Human Resources, I want to use this dashboard to monitor employee performance and satisfaction across the company, identify top-performing departments, and make better decisions around support, training, and retention.*

---

## 🛠 Tools

| Tool        | Purpose                                              |
|-------------|------------------------------------------------------|
| Excel       | Dashboard creation using Pivot Tables & Charts       |
| Power Query | Data cleaning & transformation                       |
| SQL Server  | Optional: Testing data queries and aggregations      |
| GitHub      | Version control and project documentation            |

---

## 🧱 Development

### 🔍 Data Exploration

Initial observations:
- The dataset has all necessary columns
- Some inconsistencies like gender codes, satisfaction scores, etc.

### 🧹 Data Cleaning

**Expected Clean Format:**
- Retain only relevant columns  
- Correct data types and remove nulls  
- Standardize values (e.g., Gender: M/F → Male/Female)

**Cleaning Steps:**
1. Drop unnecessary columns
2. Standardize gender and status labels
3. Convert satisfaction levels from numbers to categories
4. Rename columns for clarity

**Data Constraints:**
| Property          | Value  |
|-------------------|--------|
| Number of Rows    | 312    |
| Number of Columns | 16     |

---

### 🔄 Data Transformation

Apply Power Query or SQL to aggregate and clean metrics.

### 🧾 SQL Queries (for optional use)

```sql
-- Total Employees
SELECT COUNT(*) AS Headcount FROM hrdata;

-- Total Active
SELECT COUNT(*) FROM hrdata WHERE EmploymentStatus = 'Active';

-- Total Terminated
SELECT SUM(CASE WHEN EmploymentStatus IN ('Voluntarily Terminated', 'Terminated for Cause') THEN 1 ELSE 0 END) AS Terminated_Employee FROM hrdata;

-- Gender Breakdown
SELECT Gender, COUNT(*) FROM hrdata GROUP BY Gender;

-- Recruitment Source
SELECT RecruitmentSource, COUNT(*) FROM hrdata GROUP BY RecruitmentSource;

-- Satisfaction Levels
SELECT
  CASE EmployeeSatisfaction
    WHEN 1 THEN 'Very Low'
    WHEN 2 THEN 'Low'
    WHEN 3 THEN 'Acceptable'
    WHEN 4 THEN 'High'
    WHEN 5 THEN 'Very High'
  END AS Satisfaction_Level,
  COUNT(*) FROM hrdata GROUP BY Satisfaction_Level;
