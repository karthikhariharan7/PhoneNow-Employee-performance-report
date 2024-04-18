
# PhoneNow Perfomance report 2021
This dashboard helps Manager at PhoneNow to analyse overview of long-term trends in customer and agent behaviour.
# PhoneNow Perfomance report-Dashboard

### Dashboard Link : https://app.powerbi.com/view?r=eyJrIjoiNTgzM2JmMTktNWU4Yi00ODcxLWI1ODEtODIyMTRkMjRkMzljIiwidCI6ImRmODY3OWNkLWE4MGUtNDVkOC05OWFjLWM4M2VkN2ZmOTVhMCJ9

## Problem Statement

Create a dashboard in Power BI for Claire that reflects all relevant Key Performance Indicators (KPIs) and metrics in the dataset. Get creative! 

Possible KPIs include (to get you started, but not limited to):

- Overall customer satisfaction
- Overall calls answered/abandoned
- Calls by time
- Average speed of answer
- Agent’s performance quadrant -> average handle time (talk duration) vs calls answered


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : Date & Time columns was entered in a single column so split by column is used to seperate into two columns and their types are changed and renamed.
- Step 5 : After this change the Data is pretty good to start calculations so a measure table is created.
- Step 6 : A calculated column was created to convert average talktime into seconds.

            Call_Seconds = HOUR(Call_center_data[AvgTalkDuration]) * 3600 + MINUTE(Call_center_data[AvgTalkDuration]) * 60 + SECOND(Call_center_data[AvgTalkDuration])
    create a measure for Average Talktime in seconds to and use it to convert into time format.
            
            Average Talk Time (Seconds) = AVERAGE('Call_center_data'[Call_Seconds])
            Average Talk Time = TIME(INT([Average Talk Time (Seconds)] / 3600), INT(MOD([Average Talk Time (Seconds)], 3600) / 60), MOD([Average Talk Time (Seconds)], 60))
- Step 7 : Measures created for Calls answered, Calls abandoned, Average answer speed, Issues resolved, Issues notresolved and Average rating.

            Calls_answered = CALCULATE(count(Call_center_data[Answered (Y/N)]),FILTER(Call_center_data,Call_center_data[Answered (Y/N)]="Y"))
            Calls_abandoned = CALCULATE(count(Call_center_data[Answered (Y/N)]),FILTER(Call_center_data,Call_center_data[Answered (Y/N)]="N"))
            Avg_speed_of_answer_in_secs = AVERAGE(Call_center_data[Speed of answer in seconds])
            Resolved Count = CALCULATE(count(Call_center_data[Resolved]),filter(Call_center_data,Call_center_data[Resolved]="Y"))
            Resolved_% = DIVIDE([Resolved Count],[Calls_answered])*100
            NotResolved Count = [Calls_answered]-[Resolved Count]
            NotResolved_% = DIVIDE([NotResolved Count],[Calls_answered])*100
            Average Rating = AVERAGE(Call_center_data[Satisfaction rating])
- Step 8 : Create a quick measure for average star rating and use average rating as  Base value and specify No of stars, value for lowest star and value for highest star.
- Step 9 : Slicer is used to filter the report based on Agent’s.
- Step 10 : Card, Stacked bar charts, Line Charts are used to represent these data.
- Step 11 : A Double page report was created on Power BI Desktop & it was then published to Power BI Service.

# Insights

## Key Findings:
- Calls Answered: 4,054
- Issues Resolved: 89.94%
- Overall Star Ratings: ⭐⭐⭐ Stars

## Strategic Recommendations:
- Trend Analysis: The average rating is on a declining trend month-over-month, which indicates a need for immediate attention to customer satisfaction strategies.
- Unanswered Calls: A significant number of calls (946) are not being answered, suggesting a need for increased staffing or improved call distribution.
- Response Time: The average answer speed exceeds 1 minute, highlighting an opportunity for improvement in response efficiency.
