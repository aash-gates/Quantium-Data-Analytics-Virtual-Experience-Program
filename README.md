# Quantium-Data-Analytics-Virtual-Experience-Program
# Quantium Virtual Experience Program in Data Analytics

- This is program consists of 3 tasks 
- All these code files were my personal submissions for this program. Except the data files which were assigned by Quantium.

---

## Code and Resources Used

**Python Version:** 3.7

**Packages:** pandas, numpy, seaborn, sklearn, matplotlib, datetime, scipy

---

### Task 1 - Data preparation and Customer Analytics
Conduct analysis on your client's transaction dataset and identify customer purchasing behaviours to generate insights and provide commercial recommendations.

#### Background information for the task
We need to present a strategic recommendation to Julia that is supported by data which she can then use for the upcoming category review however to do so we need to analyse the data to understand the current purchasing trends and behaviours. The client is particularly interested in customer segments and their chip purchasing behaviour. Consider what metrics would help describe the customers’ purchasing behaviour.

#### Main goals of this task are :
1. Examine transaction data - check for missing data, anomalies, outliers and clean them
2. Examine customer data - similar to above transaction data
3. Data analysis and customer segments - create charts and graphs, note trends and insights
4. Deep dive into customer segments - determine which segments should be targetted

#### Data Cleaning:
- Date column was in integer format. So the date column was changed to date time format.
- There are 365 days in a year but in the DATE column there are only 364 unique values so one was missing. As it was a Christmas day and store was closed there was no anomaly. Value was kept as zero transaction for "TOT_SALES".
![December sales](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%201/December_Sales.png)
- Checked if all the products in given data are chips.
-  Some product names are written in more than one way. Example : Dorito and Doritos, Grains and GrnWves, Infusions and Ifzns, Natural and NCC, Red and RRD, Smith and Smiths and Snbts and Sunbites. It was cleaned thereafter.
- Split and frequency of each word in "PROD_NAME" column. Removed all rows containing "salsa" in "PROD_QTY" column.
- Checked for outliers and removed outliers rows in "PROD_QTY" column.
- Each word value was counted in "PROD_NAME" column to extract the brand name. Combined brands written in multiple ways. Created a new column "Cleaned_Brand_Names".
![Cleaned Brand Names](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%201/Brand_Names.png)

#### Data Analysis on Customer Segments
- The 4 main questions answered in data analysis were:
1. Who spends the most on chips (total sales), describing customers by lifestage and how premium their general purchasing behaviour is
2. How many customers are in each segment
3. How many chips are bought per customer by segment
4. What's the average chip price by customer segment
- Groupby sum TOT_SALES column and identified top 3 highest total sales contributing segments.
- Plot the groupby into stacked bar chart with percentage text on each segment stack.
![Total Sales by Segment](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%201/Stage_Plot1.png)
- The high sales amount by segment "Young Singles/Couples - Mainstream" and "Retirees - Mainstream" are due to their large number of unique customers, but not for the "Older - Budget" segment. Next we'll explore if the "Older - Budget" segment has:
High Frequency of Purchase and, Average Sales per Customer compared to the other segment.
- Used p-value calculation and found statistically significant TOT_SALES difference (pval < 5%) between "Mainstream Young Midage" to "Budget and Premium Young Midage" segment.
- Divided groupby sum to groupby nunique to get average amount of chips bought per customer segment. Older and Young Families bought the highest average amount of chips.
- Unstacked the groupby and plotted it by segment:
![Average Chips per Customer](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%201/Average_Purchase.png)

#### Trends and Insights
- Top 3 total sales contributor segment are
1. Older families (Budget) $156,864
2. Young Singles/Couples (Mainstream) $147,582
3. Retirees (Mainstream) $145,169
- Young Singles/Couples (Mainstream) has the highest population, followed by Retirees (Mainstream). Which explains their high total sales.
- Despite Older Families not having the highest population, they have the highest frequency of purchase, which contributes to their high total sales.
- Older Families followed by Young Families has the highest average quantity of chips bought per purchase.
- The Mainstream category of the "Young and Midage Singles/Couples" have the highest spending of chips per purchase. And the difference to the non-Mainstream "Young and Midage Singles/Couples" are statistically significant.
- Chips brand Kettle is dominating every segment as the most purchased brand.
- Observing the 2nd most purchased brand, "Young and Midage Singles/Couples" is the only segment with a different preference (Doritos) as compared to others' (Smiths).
- Most frequent chip size purchased is 175gr followed by the 150gr chip size for all segments.

#### Views and Recommendations
- Older Families: Focus on the Budget segment. Strength: Frequent purchase. We can give promotions that encourages more frequency of purchase. Strength: High quantity of chips purchased per visit. We can give promotions that encourage them to buy more quantity of chips per purchase.
- Young Singles/Couples: Focus on the Mainstream segment. This segment is the only segment that had Doritos as their 2nd most purchased brand (after Kettle). To specifically target this segment it might be a good idea to collaborate with Doritos merchant to do some branding promotion catered to "Young Singles/Couples - Mainstream" segment. Strength: Population quantity. We can spend more effort on making sure our promotions reach them, and it reaches them frequently.
- Retirees: Focus on the Mainstream segment. Strength: Population quantity. Again, since their population quantity is the contributor to the high total sales, we should spend more effort on making sure our promotions reaches as many of them as possible and frequent.
- General: All segments has Kettle as the most frequently purchased brand, and 175gr (regardless of brand) followed by 150gr as the preferred chip size. When promoting chips in general to all segments it is good to take advantage of these two points.

---

### Task 2 - Experimentation and Uplift Testing
Extend your analysis from Task 1 to help you identify benchmark stores that allow you to test the impact of the trial store layouts on customer sales.

#### Background Information for the task
Julia has asked us to evaluate the performance of a store trial which was performed in stores 77, 86 and 88.

This can be broken down by:

1. total sales revenue
2. total number of customers
3. average number of transactions per customer

Create a measure to compare different control stores to each of the trial stores to do this write a function to reduce having to re-do the analysis for each trial store. Consider using Pearson correlations or a metric such as a magnitude distance e.g. 1- (Observed distance – minimum distance)/(Maximum distance – minimum distance) as a measure.
Once you have selected your control stores, compare each trial and control pair during the trial period. You want to test if total sales are significantly different in the trial period and if so, check if the driver of change is more purchasing customers or more purchases per customers etc.

#### Main areas of Focus are :
1. Select control stores – Explore data, define metrics, visualize graphs
2. Assessment of the trial – insights/trends by comparing trial stores with control stores
3. Collate findings – summarize and provide recommendations.

#### Experimenting and testing
- Compile each store's monthly:
1. Total sales
2. Number of customers,
3. Average transactions per customer
4. Average chips per customer
5. Average price per unit
- Check significance of Trial minus Control stores TOT_SALES Percentage Difference Pre-Trial vs Trial.

Step 1: Check null hypothesis of 0 difference between control store's Pre-Trial and Trial period performance.

Step 2: Proof control and trial stores are similar statistically

Check p-value of control store's Pre-Trial vs Trial store's Pre-Trial.
If <5%, it is significantly different. If >5%, it is not significantly different (similar).

Step 3: After checking Null Hypothesis of first 2 step to be true, we can check Null Hypothesis of Percentage Difference between Trial and Control stores during pre-trial is the same as during trial.

- Check T-Value of Percentage Difference of each Trial month (Feb, March, April 2019).
- Mean is mean of Percentage Difference during pre-trial.
- Standard deviation is stdev of Percentage Difference during pre-trial.
- Formula is Trial month's Percentage Difference minus Mean, divided by Standard deviation.
- Compare each T-Value with 95% percentage significance critical t-value of 6 degrees of freedom (7 months of sample - 1)

- Null hypothesis is true. There isn't any statistically significant difference between control store's scaled Pre-Trial and Trial period sales.
- There are 3 months' increase in performance that are statistically significant (Above the 95% confidence interval t-score):
1. March and April trial months for trial store 77
2. March trial months for trial store 86

- Check significance of Trial minus Control stores nCustomers Percentage Difference Pre-Trial vs Trial.

Step 1: Check null hypothesis of 0 difference between control store's Pre-Trial and Trial period performance.

Step 2: Proof control and trial stores are similar statistically

Step 3: After checking Null Hypothesis of first 2 step to be true, we can check Null Hypothesis of Percentage Difference between Trial and Control stores during pre-trial is the same as during trial.

- There are 5 months' increase in performance that are statistically significant (Above the 95% confidence interval t-score):

March and April trial months for trial store 77

Feb, March and April trial months for trial store 86

![Total Sales Trial vs Control1](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Compare%20performance%201.png) 
![Total Sales Trial vs Control2](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Compare%20performance%202.png) 
![Total Sales Trial vs Control3](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Compare%20performance%203.png)
![nCustomers Trial vs Control1](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Full_Year_Observations%204.png) 
![nCustomers Trial vs Control2](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Full_Year_Observations%205.png) 
![nCustomers Trial vs Control3](https://github.com/aash-gates/Quantium-Data-Analytics-Virtual-Experience-Program/blob/main/Data%20Visualizations/Task%202/Full_Year_Observations%206.png)

#### Insights and Trends
- We can see that Trial store 77 sales for Feb, March, and April exceeds 95% threshold of control store. Same goes to store 86 sales for all 3 trial months.

1. Trial store 77: Control store 233
2. Trial store 86: Control store 155
3. Trial store 88: Control store 40
4. Both trial store 77 and 86 showed significant increase in Total Sales and Number of Customers during trial period. But not for trial store 88. Perhaps the client knows if there's anything about trial 88 that differs it from the other two trial.
5. Overall the trial showed positive significant result.

----

### Task 3 - Analytics and Commercial Application
- Use your analytics and insights from Task 1 and 2 to prepare a report for your client, the Category Manager.

#### Background Information for the task
- With our project coming to an end its time for us to send a report to Julia, based on our analytics from the previous tasks. We want to provide her with insights and recommendations that she can use when developing the strategic plan for the next half year.
- As best practice at Quantium, we like to use the “Pyramid Principles” framework when putting together a report for our clients. If you are not already familiar with this framework you can find quick introductions on by searching form them on the internet.
- For this report, we need to include data visualisations, key callouts, insights as well as recommendations and/or next steps.
- We recommend you use a tool like PowerPoint (or similar) to create your report.

#### Main goals of the task are:
1. Data literacy level of your audience
2. Table of contents / agenda
3. Problem statement / purpose
4. Overview and context
5. Content balance
6. Layout and content display
7. Summary / next steps

#### Final Report 
- Use analytics and insights from Task 1 and 2 to prepare a report for the client, the Category Manager.
- Delivered the insights and recommendaions to the client in PowerPoint presentation along with easy to understand data visualizations.

