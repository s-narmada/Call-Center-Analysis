# Call Center Analysis | Pwc Switzerland Power BI Virtual Case Experience
![PWC_Logo](https://github.com/s-narmada/Call-Center-Analysis/assets/58018941/1db8e82f-7a32-40ad-a16d-fb52d51d7fc5)

## Dashboard Link :

## Problem Statement
- Problem: The manager at PhoneNow (a big telecom company) is seeking transparency and insight into the Call Center dataset to gain an accurate overview of long-term customer and agent behavior trends.
- Objective: The purpose of this analysis is to create a dashboard in Power BI for Call Center Manager that reflects all relevant Key Performance Indicators (KPIs) and metrics to:
  * Self-exploratory call trends
  * Overview of the agent’s performance and behaviors
  * Overview the customer satisfaction
  * Contain many metrics and plots related to a single area of business for discussing with higher managers and generating further analysis.
  * Allows for minimal interaction.
- Possible KPIs include (but are not limited to):
  * Overall customer satisfaction
  * Overall calls answered/abandoned
  * Calls by time
  * Average speed of answer
  * Agents performance quadrant -> average handle time(talk duration) vs calls answered

## Data Sourcing
The Dataset used for this analysis was provided by https://www.pwc.ch/en/careers-with-pwc/students/virtual-case-experience.html.

## Data Preparation
The dataset was loaded into Microsoft Power BI Desktop for transformation in Power Query and modeling.

### Data Cleaning
Data Cleaning for the dataset was done in Power Query as follows:
- Unnecessary columns were removed
- Each of the columns in the table was validated to have the correct data type
- Unnecessary rows were removed

### Data Transformation
To ensure the comprehensive satisfaction of customers, an additional column named Satisfaction Likert was created for referencing using the M-formula:

          Table.AddColumn(#"Replaced Value", "Satisfaction Likert", each if [Satisfaction rating] = 1 then "Very Poor" else if [Satisfaction rating] = 2 then "Poor" else if [Satisfaction rating] = 3 then "Average" else if [Satisfaction rating] = 4 then "Good" else "Very Good")

#### Here is a breakdown of what the formula does:
For the dataset, we want to transform the satisfaction rating from number to text based on the Likert scale with the condition if Satisfaction rating = 1, it will display the rating as “Very poor”, respectively for each value of Satisfaction rating .

### Data Modeling
After the dataset was cleaned and transformed, it was ready to be modeled, but the dataset just included one table, so the Data Modeling is nothing much to modify.
