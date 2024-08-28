# HR-Dashboards-using-Power-BI 

## Problem Statement

Human Resources departments frequently face challenges in effectively managing and visualizing complex employee data. This includes difficulties in tracking and analyzing workforce distribution, turnover rates, and performance metrics across different demographics and operational units. 
Traditional HR management tools often lack the capability to provide real-time, actionable insights, leading to inefficient workforce planning and decision-making. 
There is a critical need for an integrated solution that enables HR professionals to swiftly access, analyze, and interpret data to support strategic human capital decisions and enhance employee engagement and retention strategies.

(For the time-being I'll upload only the second dashboard I'll upload the first one later)

![image](https://github.com/nehapereira/HR-Dashboards-using-Power-BI/assets/136058806/c3f2db2c-965f-4c76-bccc-cb3defd5e298)
![image](https://github.com/nehapereira/HR-Dashboards-using-Power-BI/assets/136058806/662ac304-8c70-45b5-95ee-69a7f3164715)


###   DAX Measures

Employee Count = DISTINCTCOUNT('HR Analytics'[EmpID])

Avg Years At Company = AVERAGE('HR Analytics'[YearsAtCompany])

Years With Text = ROUND([Avg Years At Company],0)&" Years"

Employee Attrition = CALCULATE([Employee Count],'HR Analytics'[Attrition]="Yes")

Attrition% = [Employee Attrition]/[Employee Count]

Avg Age = AVERAGE('HR Analytics'[Age])

Avg Salary = AVERAGE('HR Analytics'[MonthlyIncome])

