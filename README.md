# HR_ATTRTION
SQL + Excel project analyzing employee attrition patterns through data queries and interactive dashboards.

Employee Attrition Analysis
This project analyzes employee attrition using HR data to uncover patterns, key risk factors, and business insights. The goal is to help the company understand why employees leave, who is most at risk, and how to improve retention.

Key Insights
Overall Attrition Rate: 16.11%

Younger Employees (20s) experience the highest attrition.

Males are leaving the organization at a higher rate than females.

Overtime workers show significantly higher attrition than non-overtime workers.

Laboratory Technicians have the highest attrition among job roles.

Employees with lower Job Satisfaction scores (1 or 2) are more likely to leave.

Employees with no Stock Options are more likely to leave than those with higher stock option levels.

💡 Business Recommendations
Support Early-Career Employees
Provide mentorship, clear career paths, and onboarding programs for employees in their 20s.

Improve Job Satisfaction
Conduct regular engagement surveys and build a culture that values employee feedback and recognition.

Address Overtime Culture
Monitor workloads and promote better work-life balance through policy and staffing support.

Introduce or Expand Stock Option Plans
Employees with stock incentives show stronger retention. Offer stock options to more roles.

Focus on At-Risk Job Roles
Investigate reasons for high attrition among Laboratory Technicians and other vulnerable roles.

Targeted Retention Strategies for Males
Since men are leaving more, explore career growth, flexibility, and financial recognition tailored to this group.

🛠️ Tools Used
SQL: Data cleaning, querying, and exploration

Excel / Google Sheets: Pivot tables, visual dashboards, filters

link to google sheet
https://docs.google.com/spreadsheets/d/1wg1hY-G_vbNTr0VSeHXS_5k1ursKW3hXaVwTD-zL2CM/edit?usp=sharing

my sql queries

CREATE DATABASE HRDATA;

USE HRDATA;


#CHECK FOR NULL
SELECT *
FROM HRDATA
WHERE 
    Age IS NULL OR
    Attrition IS NULL OR
    BusinessTravel IS NULL OR
    DailyRate IS NULL OR
    Department IS NULL OR
    DistanceFromHome IS NULL OR
    Education IS NULL OR
    EducationField IS NULL OR
    EmployeeCount IS NULL OR
    EmployeeNumber IS NULL OR
    EnvironmentSatisfaction IS NULL OR
    Gender IS NULL OR
    HourlyRate IS NULL OR
    JobInvolvement IS NULL OR
    JobLevel IS NULL OR
    JobRole IS NULL OR
    JobSatisfaction IS NULL OR
    MaritalStatus IS NULL OR
    MonthlyIncome IS NULL OR
    MonthlyRate IS NULL OR
    NumCompaniesWorked IS NULL OR
    Over18 IS NULL OR
    OverTime IS NULL OR
    PercentSalaryHike IS NULL OR
    PerformanceRating IS NULL OR
    RelationshipSatisfaction IS NULL OR
    StandardHours IS NULL OR
    StockOptionLevel IS NULL OR
    TotalWorkingYears IS NULL OR
    TrainingTimesLastYear IS NULL OR
    WorkLifeBalance IS NULL OR
    YearsAtCompany IS NULL OR
    YearsInCurrentRole IS NULL OR
    YearsSinceLastPromotion IS NULL OR
    YearsWithCurrManager IS NULL;



SELECT 
    SUM(CASE WHEN Age IS NULL THEN 1 ELSE 0 END) AS null_age,
    SUM(CASE WHEN Attrition IS NULL THEN 1 ELSE 0 END) AS null_attrition,
    SUM(CASE WHEN BusinessTravel IS NULL THEN 1 ELSE 0 END) AS null_businesstravel,
    SUM(CASE WHEN DailyRate IS NULL THEN 1 ELSE 0 END) AS null_dailyrate,
    SUM(CASE WHEN Department IS NULL THEN 1 ELSE 0 END) AS null_department,
    SUM(CASE WHEN DistanceFromHome IS NULL THEN 1 ELSE 0 END) AS null_distancefromhome,
    SUM(CASE WHEN Education IS NULL THEN 1 ELSE 0 END) AS null_education,
    SUM(CASE WHEN Educationfield IS NULL THEN 1 ELSE 0 END) AS null_educationfield,
    SUM(CASE WHEN Employeenumber IS NULL THEN 1 ELSE 0 END) AS null_employeenumber,
    SUM(CASE WHEN Employeecount IS NULL THEN 1 ELSE 0 END) AS null_employeecount,
    SUM(CASE WHEN EnvironmentSatisfaction IS NULL THEN 1 ELSE 0 END) AS null_EnvironmentSatisfaction,
    SUM(CASE WHEN Gender IS NULL THEN 1 ELSE 0 END) AS null_gender,
    SUM(CASE WHEN Hourlyrate IS NULL THEN 1 else 0 END) AS null_hourlyrate,
    SUM(CASE WHEN Jobinvolvement IS NULL THEN 1 ELSE 0 END) AS null_jobinvolvement,
    SUM(CASE WHEN Joblevel IS NULL THEN 1 ELSE 0 END) AS null_joblevel,
    SUM(CASE WHEN Gender IS NULL THEN 1 ELSE 0 END) AS null_gender,
       SUM(CASE WHEN JobRole IS NULL THEN 1 ELSE 0 END) AS null_jobrole,
    SUM(CASE WHEN JobSatisfaction IS NULL THEN 1 ELSE 0 END) AS null_jobsatisfaction,
    SUM(CASE WHEN MaritalStatus IS NULL THEN 1 ELSE 0 END) AS null_maritalstatus,
    SUM(CASE WHEN MonthlyIncome IS NULL THEN 1 ELSE 0 END) AS null_monthlyincome,
    SUM(CASE WHEN MonthlyRate IS NULL THEN 1 ELSE 0 END) AS null_monthlyrate,
    SUM(CASE WHEN NumCompaniesWorked IS NULL THEN 1 ELSE 0 END) AS null_numcompaniesworked,
    SUM(CASE WHEN Over18 IS NULL THEN 1 ELSE 0 END) AS null_over18,
    SUM(CASE WHEN OverTime IS NULL THEN 1 ELSE 0 END) AS null_overtime,
    SUM(CASE WHEN PercentSalaryHike IS NULL THEN 1 ELSE 0 END) AS null_percentsalaryhike,
    SUM(CASE WHEN PerformanceRating IS NULL THEN 1 ELSE 0 END) AS null_performancerating,
    SUM(CASE WHEN RelationshipSatisfaction IS NULL THEN 1 ELSE 0 END) AS null_relationshipsatisfaction,
    SUM(CASE WHEN StandardHours IS NULL THEN 1 ELSE 0 END) AS null_standardhours,
    SUM(CASE WHEN StockOptionLevel IS NULL THEN 1 ELSE 0 END) AS null_stockoptionlevel,
    SUM(CASE WHEN TotalWorkingYears IS NULL THEN 1 ELSE 0 END) AS null_totalworkingyears,
    SUM(CASE WHEN TrainingTimesLastYear IS NULL THEN 1 ELSE 0 END) AS null_trainingtimeslastyear,
    SUM(CASE WHEN YearsWithCurrManager IS NULL THEN 1 ELSE 0 END) AS null_yearswithcurrmanager
FROM hrdata;






# create a view to keep data 

CREATE VIEW clean_hr_data AS
SELECT 
    EmployeeNumber,
    Age,
    Gender,
    JobRole,
    JobSatisfaction,
    MaritalStatus,
    MonthlyIncome,
    MonthlyRate,
    NumCompaniesWorked,
    OverTime,
    PercentSalaryHike,
    PerformanceRating,
    RelationshipSatisfaction,
    StockOptionLevel,
    TotalWorkingYears,
    TrainingTimesLastYear,
    WorkLifeBalance,
    YearsAtCompany,
    Attrition
FROM hrdata
WHERE 
    JobRole IS NOT NULL AND
    MonthlyIncome IS NOT NULL AND
    TotalWorkingYears IS NOT NULL AND
    PerformanceRating IS NOT NULL;






# OVERALL ATTRITION RATE

SELECT COUNT(*) AS TOTAL_EMPLOYEE,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS ATTRITIONS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2)
FROM hrdata;
# TOTAL EMPLOYEE 147 ATTRITIONS 237 AND ATTRICATION RATE IS 16.12




# ATTRITION BY GENDER

SELECT GENDER, COUNT(*) AS TOTAL,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS LEAVERS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2) AS ATTRITION_RATE
FROM HRDATA
GROUP BY GENDER;






# ATTRITION BY JOBROLE

SELECT JOBROLE,
COUNT(*) AS TOTAL,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS LEAVERS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2) AS ATTRITION_RATE
FROM HRDATA
GROUP BY JOBROLE
ORDER BY ATTRITION_RATE;




#OVERTIME VS ATTRITION

SELECT OVERTIME,
COUNT(*) AS TOTAL,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS LEAVERS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2) AS ATTRITION_RATE
FROM HRDATA
GROUP BY OVERTIME;




# AVERAGE INCOME AND SATISFACTION BY ATTRITION
SELECT 
  Attrition,
  ROUND(AVG(MonthlyIncome), 2) AS Avg_Income,
  ROUND(AVG(JobSatisfaction), 2) AS Avg_JobSatisfaction,
  ROUND(AVG(YearsAtCompany), 2) AS Avg_Tenure
FROM HRDATA
GROUP BY Attrition;





# MARTIAL STATUS BY ATTRITION

SELECT 
    MaritalStatus,
    COUNT(*) AS TOTAL,
    SUM(CASE
        WHEN ATTRITION = 'YES' THEN 1
        ELSE 0
    END) AS LEAVERS,
    ROUND(SUM(CASE
                WHEN ATTRITION = 'YES' THEN 1
                ELSE 0
            END) * 100.00 / COUNT(*),
            2) AS ATTRITION_RATE
FROM
    HRDATA
GROUP BY MaritalStatus;






#AGEBAND VS ATTRITION

SELECT 
CASE
WHEN AGE < 25 THEN '<25'
WHEN AGE  BETWEEN 25 AND 34 THEN '25-34'
WHEN AGE BETWEEN 35 AND 44 THEN '35-44'
WHEN AGE BETWEEN 45 AND 54 THEN '45-54'
ELSE '55+' END
AS AGEBAND,
COUNT(*) AS TOTAL,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS LEAVERS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2) AS ATTRITION_RATE
FROM HRDATA
GROUP BY AGEBAND
ORDER BY AGEBAND;


#Top 5 Job Roles with Highest Attrition Rate
SELECT JOBROLE,
COUNT(*) AS TOTAL,
SUM(CASE WHEN ATTRITION = 'YES' THEN 1 ELSE 0 END) AS LEAVERS,
ROUND(SUM(CASE WHEN ATTRITION ='YES' THEN 1 ELSE 0 END)* 100.0/COUNT(*), 2) AS ATTRITION_RATE
FROM HRDATA
GROUP BY JOBROLE
ORDER BY ATTRITION_RATE DESC
LIMIT 5



