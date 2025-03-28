# Power BI project Customer Trend Analysis

### Dashboard Link: [(https://acemeduin-my.sharepoint.com/:u:/g/personal/ritik_gupta_acem_edu_in/EYEFwnBoZmpGsbFoaMge4NABJ8t04tD_Sbt1B4KXP1xgHg?e=sPWVjG)]

# Telecom-Call-Center-Dashboard
## Problem Statement

This dashboard helps PhoneNow, a telecom company, understand their call center performance and customer interactions better. It provides insights into customer satisfaction, call handling efficiency, and agent performance. By analyzing key metrics such as the number of calls answered/abandoned, average speed of answer, and agent handle times, the company can identify areas for improvement in their call center operations. The dashboard also highlights trends in call volumes over time, enabling PhoneNow to optimize staffing and improve service quality.

The analysis reveals that a significant portion of calls are abandoned, and the average speed of answer needs improvement. Additionally, agent performance varies, indicating a need for targeted training to reduce handle times and increase the number of calls answered.

## Steps Followed

- **Step 1**: Load data into Power BI Desktop; the dataset is a CSV file containing call center records.
- **Step 2**: Open the Power Query Editor and, under the View tab in the Data Preview section, enable "Column Distribution," "Column Quality," and "Column Profile" options.
- **Step 3**: Select "Column Profiling Based on Entire Dataset" to ensure profiling is not limited to the default 1000 rows.
- **Step 4**: Observe that some columns, such as "Call Duration" and "Wait Time," contain null values, but these are less than 2% of the total data and are ignored for average calculations.
- **Step 5**: In the Report View, under the View tab, select a theme to enhance the visual appeal of the dashboard.
- **Step 6**: Add visual filters (slicers) for fields like "Call Type," "Time of Day," "Agent Name," and "Customer Segment" to allow dynamic filtering.
- **Step 7**: Add two card visuals to the canvas:
  - One to display the **Average Speed of Answer** (in seconds).
  - Another to display the **Overall Customer Satisfaction** (average rating out of 5).
  Null values in "Wait Time" and "Satisfaction Rating" are excluded from calculations using visual-level filters.
- **Step 8**: Create a bar chart to represent the number of calls answered vs. abandoned, segmented by "Time of Day" (e.g., morning, afternoon, evening) using the Legends bucket.
- **Step 9**: Add a line chart to show **Calls by Time** (e.g., hourly or daily call volume trends) to identify peak call periods.
- **Step 10**: Create a scatter plot to visualize **Agent Performance**:
  - X-axis: Average Handle Time (talk duration in minutes).
  - Y-axis: Number of Calls Answered.
  - This helps identify agents who handle calls efficiently vs. those who need training.
- **Step 11**: Add a KPI visual to represent overall customer satisfaction trends over time, using the "Satisfaction Rating" field.
- **Step 12**: In the Report View, under the Insert tab, add two text boxes:
  - One for the company name (PhoneNow).
  - Another for the company tagline ("Connecting You, Always").
- **Step 13**: Under the Insert tab, use the Shapes option to insert a rectangle and the Image option to add the company logo to the report design area.
- **Step 14**: Create a calculated column to group calls by duration:
  ```DAX
  Call Duration Group = 
  IF(Call_Center_Data[Call Duration] <= 5, "0-5 mins (5 included)",
  IF(Call_Center_Data[Call Duration] <= 10, "5-10 mins (10 included)",
  IF(Call_Center_Data[Call Duration] <= 15, "10-15 mins (15 included)",
  "15+ mins")))


Step 15: Create a new measure to calculate the total number of calls:
```
Total Calls = COUNT(Call_Center_Data[Call ID])
```
Step 16: Create a new measure to calculate the percentage of calls answered:
```
% Calls Answered = (DIVIDE(COUNTROWS(FILTER(Call_Center_Data, Call_Center_Data[Status] = "Answered")), [Total Calls]) * 100)
```
Step 17: Create a new measure to calculate the total wait time:
```
Total Wait Time = SUM(Call_Center_Data[Wait Time])
```

