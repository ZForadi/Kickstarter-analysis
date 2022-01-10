# KickStarter Challenge Analysis

## Overview of Project
An up and coming playwright, Louise, has reached out for help regarding her Kickstarter campaign project. She wanted to start a crowdfunding campaign to help fund her play, Fever. By utilizing data in Kickstarter tab of the [data-1-1-3-StarterBook](docs/data-1-1-3-StarterBook.xlsx.zip), an initial analysis was created to to provide her with some valuable insight to guide a successful campaign. For background on the initial analysis, please see the [data-1-1-3-StarterBook](docs/data-1-1-3-StarterBook.xlsx.zip) workbook. 

With the insights from the initial analysis in mind, Louise launched her campaign and she came close to her fundraising goal in a short amount of time. Now, she would like to know how similar campaigns had fared in relation to their launch dates and funding goals. 

### Purpose
The purpose of this project is to utilize data in the Kickstarter tab of the [Kickstarter_Challenge](Kickstarter_Challenge.xlsx.zip) to visualize and analyze the outcomes of similar Kickstarter Campaigns in relation to their launch dates and funding goals (specifically campaigns in the Parent Category, Theater, and campaigns in the Sub Category, Plays). 

#### Purpose of Theater Outcomes by Launch Date
The first analysis, Theater Outcomes By Launch Date, will utilize a pivot table to observe the outcomes for global campaigns in the Parent Category, Theatre, based on the month the campaign was launched. Specifically, it will look at how many theatre campaigns were "Successful," "Failed," and "Canceled" based on the month it was launched. The purpose of this analysis is to see which launch month(s) had the:
* most amount of successful campaigns
* least amount of successful campaigns
* most amount of failed campaigns 
* least amount of canceled campaigns 

#### Purpose of Outcomes Based on Goals
The second analysis, Outcomes Based on Goals, will utilize the `COUNTIFS()` function in excel, to observe the outcomes for global campaigns in the Sub Category, Plays, based on the campaigns' goal. Specifically, it will show the count and percentage of play campaigns that were "Successful," "Failed," and "Canceled" by categorizing the play campaigns into 12 different goal-amount ranges. The goal-amount ranges are defined in the Analysis of Outcomes Based on Goals section below. The purpose of this analysis is to see which goal dollar-amount range(s) had the:
* highest percentage of successful campaigns 
* Lowest percentage of susscessful campaigns
* highest percentage of failed campaigns 


## Analysis and Challenges
This section describes how I performed the analysis of Outcomes Based on Launch Date and Outcomes Based on Goals. This section also describes if any challenges were faced in performing the analysis' and how they were overcome. 

### Definition of Data Used
In both analysis', data in the Kickstarter tab of the [Kickstarter_Challenge](path/to/Kickstarter_Challenge.xlsx.zip) workbook were utilized. Below is a brief description of the data used: 
* Parent Category - the category of campaign (Theater). Columnn Q in the Kickstarter tab. 
* Subcategory - the subcategory of the campaign (Play). Column R in the Kickstart tab. 
* Date Created Conversion- the date the campaign launched. Column T in the Kickstarter tab. 
* Goal - the amount of funding the campaign wanted to achieve. Column D in the Kickstarter tab. 
* Year - the year the campaign launched. Column U in the Kickstart tab. 
* Outcomes - defined whether the campaign was Successful, Failed, Canceled, or Live. Column F in the Kickstarter tab. 
            * Sucsseful - The campaign was able to meet it's fundraising goal (amount pledged met or exceeded the goal amount)
            * Failed - The campaign was unable to meet it's fundraising goal (the amount pledged was less than the goal amount)
            *Canceled - The campaign was canceled 
            * Live - The campaign was still active 

### Analysis of Outcomes Based on Launch Date
To perform the analysis, I created a "Years" column in Column U of the Kickstarter tab and utilized the `Year()` function to extract the year the camapigns launched from the “Date Created Conversion” column. I then created a pivot table with all data in the Kickstarter tab. I put "Outcomes" in Columns, "Date Created Conversion" in Rows and count of "Outcomes" in Values. I also added the option to filter by Parent Category and Years. I then filtered the Parent Category to show only theater campaigns, which is the same Parent Category that Louise's campaign falls under. This ensures we are looking at the outcomes of campaigns that are most relevan to Louise's campaign. I also filtered the column, "Outcomes" to only show the campaigns that were "Successful," "Failed," and "Canceled." We did not want to include "Live" campaigns as the outcomes of these campaigns are not finalzied. I then sorted the "Outcomes" column to show the count of outcomes per month in descending order, such that "Successful" outcomes appeared first, "Failed" showed second and "Cancelled" showed last. The resulting pivot table, seen below, shows how many theater campaigns were "Successful," "Failed," and "Canacelled" based on the month they were launched. 

![Theater_Outcomes_vs_Launch_PivotTable](path/to/Theater_Outcomes_vs_Launch_PivotTable.png)

Please see the Theater Outcomes by Launch Date tab in the [Kickstarter_Challenge](path/to/Kickstarter_Challenge.xlsx.zip) workbook for access to the pivot table. 

To better visualize the results, I created a line chart from the pivot table to show the relationship between outcomes and launch month.

![Theater_Outcomes_vs_Launch](path/to/Theater_Outcomes_vs_Launch.png)

The months the date launched are on the x-axis, the count of campaigns are on the y-axis. The blue line represents the number of Successful campaigns, the red line represents the number of failed campaigns and the yellow line represents the number of cancelled campaigns. 
 
### Analysis of Outcomes Based on Goals
To perform the analysis, I created a new worksheet called "Outcomes Based on Goals." I then labeled Columns A1:H1 with the following titles, respectively: "Goals," "Number Successful," "Number Failed," "Number Canceled," "Total Projects," "Percentage Successful," "Percentage Failed," and "Percentage Canceled." 

In the Goal column, I created the following dollar-amount ranges so that campaigns can be grouped based on their goal amount (later referenced as goal-amount ranges): 
* Less Than 1000
* 1000 to 4999
* 5000 to 9999
* 10000 to 14999
* 15000 to 19999
* 20000 to 24999
* 25000 to 29999
* 3000 to 34999
* 35000 to 39999
* 40000 to 44999
* 45000 to 49999
* Greater than 50000

I then used the `COUNTIFS()` function in excel to extract the number of successful, failed and canceled campaigns from the Kickstarter tab, based on the goal categories noted above. This involved multiple `COUNTIFS()` functions to account for the different criteria in each row and coluumn. Below is an overview of how I approached the functions: 

1. In the first part of the function, I stated the range to be used from the Kickstarter tab: `Kickstarter!$D:$D`. This is the Goals column in the Kickstarter tab. 
2. Next, I stated the first criteria, which is based on the goal-amount ranges noted above. Within each row of the table, this criteria will change. For example for "Less than 1000" the criteria was written as, "<1000". For the goal category "1000 to 4999," the critera was written as ">=1000",Kickstarter!$D:$D, "<=4999". 
3. The second criteria in the function was based on Outcome and was written as: `Kickstarter!$F:$F, "Outcome_Label"`. The first part of the criteria denotes we want to use the Outcomes column in the Kickstarter Tab. "Outcome_Label" is used here to denote the name of the outcome I wanted to count, based on the column headers in B1:D1. For example, in Column B titled "Number Successful" the criteria would be `Kickstarter!$F:$F, "successful"`. For Column C, the Outcome_Label would be "Failed" and for Column D, the Outcome_Label would be "Canceled."
4. The last criteria was based on the subcategory of the campaign and was written as: `Kickstarter!$R:$R, "plays"`. The first part of the criteria denotes we want to use the subcategory column in the Kickstarter Tab. The second part states we only want to use the "plays" subcategory. This part of the function remained the same for all outcomes and all goal-amount ranges. "Plays"is the same subcategory that Louise's campaign falls under. This ensures we are looking at the outcomes of campaigns that are most relevan to Louise's campaign.

Once B2:D13 was populated with the functions noted above, I then used the `SUM()` function in excel to sum the count of successful campaigns, failed campaigns and canceled campaigns in each goal category. This was populated under the"Total Projects" column. 

Finally, to calculate the percentage of successful, failed and canceled campaigns in each goal category, I divided the count of the respective outcome by the total projects for each goal category. I then formatted the number into a percentage. 

The resulting table is shown below. 

![Outcomes_vs_Goals_Table](path/to/Outcomes_vs_Goals_Table.png)

Please see the Outcomes Based on Goals tab in the [Kickstarter_Challenge](path/to/Kickstarter_Challenge.xlsx.zip) workbook for access to the table and for further detail on the `COUNTIFS()` functions utilized in each row and column.

To better visualize the results, I created a line chart from the table to show the relationship between the goal-amount ranges 

![Outcomes_vs_Goals](path/to/Outcomes_vs_Goals.png)

The goal-amount ranges is shown on the x-axis and the percentage of successful, failed, or canceled projects is on the y-axis. The blue line represents the percentage of campaigns that were successful. The organe line represents the percentage of campaigns that failed. The grey line represents the percentage of campaigns that were canceled. 

### Challenges and Difficulties Encountered

#### Outcomes Based on Launch Date
When creating the Outcomes Based on Launch Date pivot table, I ran into a couple of challenges. 

The first challenge I encountered was when I created the pivot table, I seleceted the entire Kickstarter worksheet. Once the pivot table was created and filled in with the appropriate fields, I noticed that under the Rows field, which is meant to show the launch date by month, the first row had the labael "(blank)" and did not show any data under any of the outcomes. I realized that the pivot table was including empty rows in the Kickstarter worksheet, as the data source range was `Kickstarter!$A:$U`. To overcome this challenge, I clicked on the Pivot Table Analyze Tab, and clicked on "Change Data Source" in the toolbar. I then changed the data source range to `Kickstarter!$A$1:$U$4115` to only account for rows that contained data in the Kickstarter tab. This removed the "(blank)" row in the pivot table. 

The second challenge was when I put "Date Created Conversion" into the rows field of the pivot table. The date launched was automatically grouped to show the year the campaigns were launched, which could be expanded into another group - the quarter the campaigns were launched. The quarter subgroup could then be expanded to finally show the month the campaigns were launched. This was further observed in the PivotTable Fields, where "Years," "Quarters," and "Date Created Conversions" were all listed as items under the Rows field. This was an issue because I only wanted to show the launch date by month. To overcome this callenge, I removed "Years" and "Quarters" from the Rows field in the PivotTable Fields by dragging the items out of the field box area. I left "Date Created Conversion" as the only item in the Rows field. This allowed the pivot table to only display launch date by month. 

#### Outcomes Based on Goals
While populating the Outcomes Based on Goals table, I ran into one challenge. As I was creating the `COUNTIFS()` functions for the various goal-amount ranges, I was having trouble with the "Min_Range to Max_Range" criteria in the function. Where "Min_Range" is the minimum goal amount of the goal-amount range, and "Max_Range" is the maximum goal amount of the goal-amount range. For example, for the goal-amount range " 1000 to 4999" 1000 would be the Min_Range and 4999 Would be the Max_Range. I initially was typing in `Kickstarter!$D:$D, ">=Min_Range","<=Max_Range"` and was getting an error. To overcome the challenge, I realized that I needed to restate the criteria range again for the Max_Range. The updated criteria looked like this: `Kickstarter!$D:$D, "Min_Range",Kickstarter!$D:$D, "<=Max_Range"`. This allowed the`COUNTIFS()` functions to account for the campaigns that were within the goal-amount range. 

While I did not experience any other issues with this analysis, I would like to note one issue that may arise for other peers who attempt this analysis. When creating the line graph, there may be difficulties in getting the goal-amount ranges on the x-axis and the percentage of the outcomes on the y-axis. It is important to only select the following columns when creating the line graph: "Goal," "Percentage successful," "Percentage failed," and "Percentage Canceled."

## Results

### Outcomes Based on Launch Date Results
- What are two conclusions you can draw about the Outcomes based on Launch Date?

In looking at the the Theater_Outcomes_vs_Launch graph above it can be concluded that across all months, the number of successful theater campaigns is higher than failed and canceled campaigns. In general, theater campaigns are more likely to be succssful when launched in any month. 

Theater campaigns that were launched in May had the highest amount of successful campaigns, while theater campaigns that were launched in December had the lowest amount of successful campaigns. There is a rise in the number of successful campaigns for campaigns that were launched from March to May (spring time). For campaigns that were launched after May all the way to September, the number of successful campaigns fall (summer to winter). The number of successful campaigns rises slightly in October, and then continues to decline for launches in November and December. 

Campaigns launched in May also had the highest amount of failed campaigns, and had the second highest amount of failed campaigns for those that launched in July and October. November had the least amount of failed campaigns (with December, January and March also having lower occurences of failed campaigns).

The highest amount of canceled campaigns was in January, and there were no canceled campaigns in October. 

When comparing the counts of all outcomes, both successful and failed campaigns had the highest count when launched in May. This may be because May had the largest amount of Theater campaign launches of all months (total of 166) - so the number of overall outcomes increase. May also shows the largest difference between the count of succesful and failed campaigns (there were 59 more successful campaigns than failed campaigns). It should be noted that for May launches, 67% of theater campaigns were successful, 31% failed and 2% were canceled. It can be concluded that May is a good time to launch a theater campaign. Similarly, in October there was a slight rise in both successful and failed campaigns. While there were only 115 campaign launches in the month, there were no canceled campaigns, which could cause the distribution of successful and failed campaigns to increase. Additionally, the number of successful campaigns and failed campaigns are almost the same in December. Based off of this, there is about a 50% chance that the campaign can either succeed or fail. It can be concluded that December is not the best time launch a theater campaign. 


### Outcomes Based on Goals Results
- What can you conclude about the Outcomes based on Goals?
In looking at the the Outcomes_vs_Goals graph above, it can be concluded that plays with goals that are less than $4,999 are most successful. Goals less than $1,000 where most successful with a 76% success rate and goals which ranged $1000 to $4999 had a similar success rate (73% success rate). Most projects where in the $1000 to $4999 goal-amount range, and goals less than $1,000 had the second highest amount of projects. Play campaigns that had goals between $35,000 to $39,999 and $40,000 to $44,999 both had a 67% rate with total projects of 6 and 3 respectively. 

Goals which ranged $45,000 to $49,000 had a 100% fail rate, however, it should be noted that only one play campaign had this goal-amount range. Following closely, goals that were greater than $50,000 had an 88% fail rate (with 16 total projects) and goals that were between $25,000 and $29,000 had an 80% failed rate (with 5 total projects). 

There were no canceled play campaigns. 

In general, it can be concluded that play campaigns that have a lower goal amount (less than $1,000 to $4,999) are most successful, while play campaigns that have goals of $45,000 or higher are least successful. 

### Limitations of the Dataset
- What are some limitations of this dataset?
It should be noted that the dataset only accounts for campaigns that were launched from 2009 - 2017. Assuming Louis launched her campaigin in 2021, this may not be the most up to date information on Kickstarter campaigns.

Additionally, the dataset accounts for campaigns that were launched in 21 different countries. 

It should also be noted the dataset does not include external factors that may have affected the outcome of the campaigns (such as marketing efforts, the city in which the campaign launched and demographics in that area, etc.).

It should also be noted that the goal amount utilized in Outcomes Based on Goals Results utilizes various currencies, which may put non-US campaigns in different goal-amount categories if converted into USD.

### Opportunities for Further Analysis
- What are some other possible tables and/or graphs that we could create?

Another opportunity for further analysis in relation to Louise' campaign is to create a table to calculate the length of time between the date thecampaign launched and the campaign deadline (the length of the campaign) for either Parent Category "Theater" or subcategory "Play". The length of the campaign can be calculated by creating a new column in the Kickstarter worksheet, titled "Length of Campaign" and subtracting the "Date Ended Conversion" by the "Date Created Conversion" to provide the number of days the campaign was live. The length of the campaign can be grouped in a similar manner to what was done in Outcomes Based on Goals (depending on the range of days). Then using, `COUNTIFS()` functions, the outcomes for the different length of campaign ranges can be counted, and similar to Outcomes Based on Goals, the percentage of successful, failed, and canceled campaigns per length of campaign category can be observed. A line graph can be created to visualize the relationship between the length of the campaign and the percentage of successful, failed and canceled campaigns in the given campaign length category. This could show Louise the length of campaign that is most successful for campaigns similar to hers. 

Another opportunity for analysis is to adjust the criteria in Outcomes Based on Goals by adding Country as an additional criteria. Depending on where Louise launched her campaign, we could filter the table for the specific country relevant to her, and observe how the outcomes percentages change. 
