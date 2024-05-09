# HR-Dashboards-using-Power-BI 

## Problem Statement

Human Resources departments frequently face challenges in effectively managing and visualizing complex employee data. This includes difficulties in tracking and analyzing workforce distribution, turnover rates, and performance metrics across different demographics and operational units. 
Traditional HR management tools often lack the capability to provide real-time, actionable insights, leading to inefficient workforce planning and decision-making. 
There is a critical need for an integrated solution that enables HR professionals to swiftly access, analyze, and interpret data to support strategic human capital decisions and enhance employee engagement and retention strategies.

### For Dashboard 1:

![image](https://github.com/nehapereira/HR-Dashboards-using-Power-BI/assets/136058806/165f7270-74b4-4ef5-814f-7679fe876737)
![image](https://github.com/nehapereira/HR-Dashboards-using-Power-BI/assets/136058806/6eddf04d-9582-42d8-8d07-14fc3bd31289)
![image](https://github.com/nehapereira/HR-Dashboards-using-Power-BI/assets/136058806/86188930-c48c-44d3-b705-21c34958b5ed)

###   DAX Measures

Headcount = VAR _Max = MAX('Date'[Date])
VAR Result= CALCULATE(DISTINCTCOUNT('HR Data'[Employee Number]),('HR Data'[Hire Date])<=_Max && ('HR Data'[Termination Date ]>=_Max ||INT(ISBLANK('HR Data'[Termination Date ]))=1),ALL('HR Data'[Hire Date])) 
return Result

Number of Males = CALCULATE([Headcount], 'HR Data'[Gender]="Male")
Number of Females = CALCULATE([Headcount], 'HR Data'[Gender]="Female")

% Males = DIVIDE([Number of Males], [Headcount],0)
% Females = DIVIDE([Number of Females], [Headcount],0)

Employee Count = CALCULATE(COUNTROWS('HR Data'),USERELATIONSHIP('Date'[Date],'HR Data'[Hire Date]))

Average Working Years = VAR _Max=MAX('Date'[Date])
VAR Result= CALCULATE(AVERAGE('HR Data'[Years Of Service]),('HR Data'[Hire Date])<=_Max && ('HR Data'[Termination Date ]>=_Max ||INT(ISBLANK('HR Data'[Termination Date ]))=1),ALL('HR Data'[Hire Date])) 
RETURN Result

Average Gross Salary = VAR _Max=MAX('Date'[Date])
VAR Result= CALCULATE(AVERAGE('HR Data'[Gross]), ('HR Data'[Hire Date])<=_Max && ('HR Data'[Termination Date ]>=_Max ||INT(ISBLANK('HR Data'[Termination Date ]))=1),ALL('HR Data'[Hire Date])) 
RETURN Result

Average Gross Salary min per Grade = 
MINX(
	KEEPFILTERS(VALUES('HR Data'[Grade])),
	CALCULATE([Average Gross Salary])
)

Average Gross Salary max per Grade = 
MAXX(
	KEEPFILTERS(VALUES('HR Data'[Grade])),
	CALCULATE([Average Gross Salary])
)

### For Dashboard 2:

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

