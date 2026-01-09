#  📊 Data_sciences_salary_dashboard
I’m excited to share my latest project where I analyzed over 32,000 job postings from 2023 to understand the current landscape of the data industry. This project provides a deep dive into what companies are looking for and what they are paying. I used tools functions like: *XLOOKUP , MEDIAN , IF , IFS , COUNTIF, NESTED FUNCTIONS.*  

![Dashboard](/assets/Recording%20dashboard.gif)  

## Project Overview
The layout is designed for intuitive navigation:
* **Left Section (Compensation):** Displays the **Median Salary** benchmarks (currently **$115,000** overall), providing an immediate baseline for financial expectations across different data roles.
* **Middle Section (Geographic Distribution):** Features an interactive **Country Map** that visualizes hiring hotspots and regional salary variations, making it easy to identify which global markets are most active.
* **Right Section (Work Flexibility):** Breaks down **Job Schedule Types**, illustrating the availability of Full-time, Contractor, and Internship positions to help candidates target the right employment structure.

## Key Features
- **Salary Analysis:** Median and average salaries broken down by job title and country.
- **Skill Mapping:** Identification of the top 10 most requested technical skills.
- **Platform Comparison:** Analysis of where jobs are most frequently posted (LinkedIn vs. Indeed vs. others).

## Excel Tools Used
- **Bar charts** 
- **Map chart** 
- **Data validation**   
---
---
## 🖥️ The Dashboard
 ### 📊 Visualizing data jobs median salary (Bar chart)  


![job titles](/assets/job_title.png)

- Utilized bar chart to highlisght the selected job title.

- Horizontal bar chart for display the medial salary of job titles.

- Data validation to add list of data jobs.

---  
### 🌍 Geographic Insights (Map Chart)

![map](/assets/map.png)


* The map visually highlights "hiring hotspots.

* By using color gradients, the chart illustrates the disparity in median salaries across different borders.
---

### 📑 Job Schedule Type (Bar Chart)

![type](/assets/type.png)

* Data jobs can also be filtered by schedule type.

* Job schedule types are:
1. Full-time
2. Part-time
3. Internship
4. Contractor
5. Temporary work

---

### 🧮 Calculating Median Salary

To calculate the median salary a nested formula is used.

```
=MEDIAN(
 IF(
   (jobs[job_country]=A2)*
   (jobs[salary_year_avg]<>0)*
     (ISNUMBER(SEARCH(type,jobs[job_schedule_type]))),
   (jobs[salary_year_avg])
 )
)
```

The formula shown is used to calculate median salary by country. The same formula can be utilized for each variable such as, 'Job_titles' , 'type' , country. Since excel does not provide a built in `=MEDIANIF()` function. To calculate the median with multiple conditions. An `=IF()` function was nested in with a `=MEDIAN()` function.  

Below is the a table of calculated salary:

![job_title_median_salary](/assets/job_title_median_salary.png)


Similarly, to count the job titles following nested `=IF()` function was used in `=COUNT()` function.

```
=COUNT(
IF(
   (jobs[job_title_short]=$K2)*
   (jobs[job_country]=country)*
   (ISNUMBER((SEARCH(type,jobs[job_schedule_type])))),
(jobs[salary_year_avg])
)
)
```
Here instead of using `=COUNTIFS()` function i wanted to keep it simple so I just copy and pasted the `=IF()` conditions and changed `=MEDIAN()` from privous formula to `=COUNT()` function.

Below is the a table of job count:

![job_count](/assets/job_count.png)

Notice a nested `=search()` and `=ISNUMBRER()` function used to filter job schduale type below fourmula.
```
=COUNT(
IF(
   (jobs[job_title_short]=$K2)*
   (jobs[job_country]=country)*
   (ISNUMBER((SEARCH(type,jobs[job_schedule_type])))),
(jobs[salary_year_avg])
)
)
```
👇
```(ISNUMBER((SEARCH(type,jobs[job_schedule_type]))))```  

 This is because the type of data i have in job_schduale_type colomn. The data availabel in mixed as shown below:  

 👇  

![Mixed_data_type](/assets/type%20data.png)

See how the data is mixed with 'commas', '0' plus 'and' . 

To handle this data and get only required values a following nested formula is used to filter values.

`
=FILTER(A2#,NOT(ISNUMBER(SEARCH("and",A2#,1)))*(A2#<>0))
`
Below are the returned values:  

👇

![returned_type_values](/assets/type_values.png)

