# Emerald-SQL-Project
These are SQL queries written to provide actionable insights and recommendations to enhance organizational performance and foster a positive work environment.


### Descriptive and Diagnostic Analysis Using SQL on Employee Performance & Attrition Analysis 

### Project Overview
 This project aims to conduct a descriptive and diagnostic analysis to understand the causes and patterns related to employee performance and attrition of this organization . The findings will guide evidence-based decision-making to address attrition, improve performance management, and optimize training programs.

### Data Sources
The primary dataset used are employee performance and employee test which contains information about employees in the organisation

### Tools
- Excel - Data cleaning 
- SQL Server - Data Analysis
  
  ### Data Cleaning
  In preparation of the data for analysis,the following steps were performed;

  1. Download of data,creation of duplicate,and inspection
  2. Handling of missing values
  3. Data cleaning and formatting
     
  ### Descriptive Analysis
  DA is deployed to summarize and understand the key characteristics of the dataset. This will serve as a foundation for deeper analysis and modeling. The main goals is to prepare data for further analysis,detect anomalises and understand the data structure

-How many employees do we have in the organization and what is the maximum length of service
```sql
select count ("employee_id"),max(length_of_service)
from employee_test;
```
-Which department has the most employees, and which department has the fewest employees
```sql
select "department",count ("employee_id")
from employee_test
group by "department"
order by count ("employee_id") desc;
```
- What is the proportion of male to female
employees?
```sql
select "gender", COUNT(*) AS "CountGender",
     round(count(*)*1.0/
	  (select count(*) from employee_test)*100,2)
from employee_test
group by "gender";
```

- Group Employee age into 5 categories (20 29, 30,39, 40 49, 50 59 , 60
- What age group has the highest and lowest employee
```sql
select
    case
	    when "age" between 20 and 29 then '20-29'
		when "age" between 30 and 39 then '30-39'
		when "age" between 40 and 49 then '40-49'
		when "age" between 50 and 59 then '50-59'
		else '60+'
	end as "age_group",
count("employee_id")
from employee_test
group by "age_group"
order by count("employee_id");	
```
### Diagnostic analysis in data science focuses on identifying the causes behind observed patterns, trends, or anomalies within a dataset. It delves deeper than descriptive analysis answering the question: "Why did this happen?"

- Who has the highest average training score among all employees?
```sql
select "employee_id","avg_training_score"
from employee_test
order by "avg_training_score" desc
limit 2;
```

- What is the average training score of employees in each department
```sql
select "department",round(avg("avg_training_score"),2)
from employee_test
group by "department"
order by avg("avg_training_score") desc;
```

- What is the average previous year rating by department
```sql
select "department",round(avg("avg_training_score"),2)
from employee_test
group by "department"
order by avg("avg_training_score") desc;
```

- What is the average training score of employees by education type?
```sql
select "department",round(avg("avg_training_score"),2)
from employee_test
group by "department"
order by avg("avg_training_score") desc;
```
- What is the average previous year rating by recruitment channel?
```sql
Select "recruitment_channel",round(avg(previous_year_rating),1)
from employee_test
group by "recruitment_channel";
```

-What is the Average Attrition Rate
```sql
select
    round(avg(case when "attrition"='Yes' then 1 else 0
	 end),2) as "attritionrate"
from employee_perf;
 ```
-Which regions have the highest rate of departures(employees who have left), and what are the corresponding departments
```sql
select* 
from employee_test;

select "region","department",
      round(sum(case when "attrition"='Yes' then 1 else 0
	 end)) as "Noofattritionrate"
from employee_perf
left join employee_test on
employee_test.employee_id=employee_perf.employee_id
group by "department" ,"region"
order by "Noofattritionrate" desc ;
```
- Which regions have the highest average job satisfaction
```sql
select "region",round( avg("jobsatisfaction"),2) as "AvgJobSatisfaction"
from employee_test
right join employee_perf on
employee_test.employee_id=employee_perf.employee_id
group by "region"
order by "AvgJobSatisfaction" desc;
```

- Which departments have the highest rate of
departures
```sql
select "region",round( avg("jobsatisfaction"),2) as "AvgJobSatisfaction"
from employee_test
right join employee_perf on
employee_test.employee_id=employee_perf.employee_id
group by "region"
order by "AvgJobSatisfaction" desc;
```


Based on the age group created what is the average
previous year rating and average training score



### Results/Findings
- Total numbers of employees are 1470
- The maximum lenght of service is 31
### Recommendation
### Limitations
### References
   
