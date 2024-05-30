# Call Center Analysis | Pwc Switzerland Power BI Virtual Case Experience
![pwc logo1](https://github.com/s-narmada/Call-Center-Analysis/assets/58018941/83ef8ce5-6f0b-4be5-9854-2cf212f5b343)

## Dashboard Link :
https://app.powerbi.com/groups/me/reports/741f1191-abfb-4a43-beaf-5fb0bbc3a977/cb20746e83dc170ca517?experience=power-bi&bookmarkGuid=47783e82e8d3d69e247e

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
- To ensure the comprehensive satisfaction of customers, an additional column named Satisfaction Likert was created for referencing using the M-formula:

          Table.AddColumn(#"Replaced Value", "Satisfaction Likert", each if [Satisfaction rating] = 1 then "Very Poor" else if [Satisfaction rating] = 2 then "Poor" else if [Satisfaction rating] = 3 then "Average" else if [Satisfaction rating] = 4 then "Good" else "Very Good")

- To ensure comprehensive analysis I replaced the null values with '0'.

          Table.ReplaceValue(#"Changed Type1",null,0,Replacer.ReplaceValue,{"Speed of answer in seconds"})

- I had to add custom column to find the call duration by substracting the start time from end time.

          Table.AddColumn(#"Changed Type2", "Call_Duration", each [AvgTalkDuration]-[Time])

- I have added the custom column to translate the call duration into minutes.

          Table.AddColumn(#"Added Custom1", "Custom", each let splitCallDuration = Splitter.SplitTextByDelimiter("-", QuoteStyle.None)(Text.From([Call_Duration], "en-US")) in Text.Combine({Text.Combine(List.Transform(splitCallDuration, each Text.Start(_, 2)), "("), "*60)+", Text.Middle(Text.From([Call_Duration], "en-US"), 4, 2)}), type text)

- I have added the custom column to translate the text expression and evaluate it.

          Table.AddColumn(#"Renamed Columns3", "Custom", each Expression.Evaluate([Call_Duration_Text]))

#### Here is a breakdown of what the formula does:
For the dataset, we want to transform the satisfaction rating from number to text based on the Likert scale with the condition if Satisfaction rating = 1, it will display the rating as “Very poor”, respectively for each value of Satisfaction rating .

## Data Modeling
After the dataset was cleaned and transformed, it was ready to be modeled, but the dataset just included one table, so the Data Modeling just includes original dataset and the DATE table.
![CallCanter-DataModeling](https://github.com/s-narmada/Call-Center-Analysis/assets/58018941/e377d9c3-dffd-4555-83f0-53c3b10f4ed7)

## Data Visualization
![CallCenter-Dashboard](https://github.com/s-narmada/Call-Center-Analysis/assets/58018941/72943069-d1ba-469b-8a96-ac066fa8a386)
Data visualization for the datasets was done in Microsoft Power BI Desktop and designed in PowerPoint, the dashboard includes:
- One main dashboard
- 3 tooltip pages

### Dashboard type
Dashboard by the level of detail: **Tactical dashboard**

Dashboard by use-case: **Exploratory**

arget audience: **Team lead & Manager** (non-technical users)

### Key Performance Indicators and Metrics:
#### About Calls and Agents:
- Overall calls answered/abandoned
- Calls received by time, day
- Average speed of answer, handle duration
- Resolved rate by Agents, Topics
- Agent’s performance quadrant -> average handle time (talk duration) vs calls answered

#### About Customer satisfaction:
- Overall customer satisfaction
- Customer satisfaction distribution by Agents, Topics

### Measures
The measure used in visualization are:
- Calculated measures:
    -     Total Number of calls = COUNT(Sheet1[Call Id])
    -     Total Number of answered calls = CALCULATE(COUNT(Sheet1[Answered (Y/N)]),Sheet1[Answered (Y/N)]="Y")
    -     Total Number of missed calls = CALCULATE(COUNT(Sheet1[Call Id]),Sheet1[Answered (Y/N)]="N")
    -     MissedCall_Rate = ([MissedCalls]/[TotalCalls])*100
    -     Average Speed of answer = AVERAGE(Sheet1[Speed of answer in seconds])
    -     Average Call Duration = AVERAGE(Sheet1[Call_Duration(Minutes)])
    -     Average Customer Satisfaction = AVERAGE(Sheet1[Satisfaction rating])
    -     Total no of resolved issues = CALCULATE(COUNT(Sheet1[Call Id]),Sheet1[Resolved]="Y")
    -     Resolved Issues Rate = [ResolvedIssues]/[TotalCalls]
    -     Total no of unresolved issues = CALCULATE(COUNT(Sheet1[Call Id]),Sheet1[Resolved]="N")
    -     unresolved Issues rate = [UnresolvedIssues]/[TotalCalls]

- Format Measures:
    -     Color_KPI = SWITCH(TRUE(),[Target]>[AvgCustomer_Satisfaction],"#ff0000",[Target]>[AvgCustomer_Satisfaction],"#009900")

## Analysis and Insights
The purpose of this dashboard is to serve as self-exploratory for managers, but I still note some highlighted points that I recognize below:
#### About Call trends:
- Customers tend to call more between 5:00 pm - 5:30 pm at 250 calls received with an abandoned rate is 18.92% (approximately to the average abandoned rate).
- Customers have more problems with Streaming service.
- The resolved rate is at a high rate (72.92%).
#### About performance of agents:
- The agent who satisfies customers most is Dan with a 3.02% highest average customer satisfaction.
- The agent who has the highest resolved rate is Dan and he is effective with solving problems with 74.4% resolved rate.
#### About customer satisfaction:
- The correlation between call answered and call resolved is strongly positive which resulted in a increase in the customer satisfaction rate.
- The agent who satisfies customers most is Dan with a 3.02% highest average customer satisfaction.

## Shareable Link
You can interact and have fun with the dashboard here:
https://app.powerbi.com/groups/me/reports/741f1191-abfb-4a43-beaf-5fb0bbc3a977/cb20746e83dc170ca517?experience=power-bi&bookmarkGuid=47783e82e8d3d69e247e


