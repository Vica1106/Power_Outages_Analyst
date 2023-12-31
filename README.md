# Exploring the Relationship: Power Outages and Severe Weather Events
This is a project for DSC 80 at UCSD

**Name(s)**: Haoyang Yu, Jessie Zhang

 
### Introduction
Our dataset encompasses records of significant power outages observed across various states in the continental U.S. during January 2000–July 2016, comprising 1534 entries and 55 variables. To enhance the analytical focus on power outage research, a decision has been made to streamline the dataset by retaining only 10 pertinent columns. 

Our main goal is to explore the correlation between severe weather events and power outages. The research is focused on determining whether severe weather conditions play a significant role in the increased occurrence of power outages compared to other contributing factors throughout the years. Our specific research question addresses whether the occurrence of severe weather contribute to a higher frequency of power outages compared to other causative factors in the year with the highest number of outages.

Columns include the following:
- **'POSTAL.CODE'**: Represents the postal code of the U.S. states
- **'OUTAGE.START.DATE'**: This variable indicates the day of the year when the outage event started (as reported by the corresponding Utility in the region)
- **'OUTAGE.START.TIME'**: This variable indicates the time of the day when the outage event started (as reported by the corresponding Utility in the region)
- **'OUTAGE.RESTORATION.DATE'**: This variable indicates the day of the year when power was restored to all the customers (as reported by the corresponding Utility in the region)
- **'OUTAGE.RESTORATION.TIME'**: This variable indicates the time of the day when power was restored to all the customers (as reported by the corresponding Utility in the region)
- **'CAUSE.CATEGORY'**: Categories of all the events causing the major power outages
- **'CAUSE.CATEGORY.DETAIL'**: Detailed description of the event categories causing the major power outages
- **'OUTAGE.DURATION'**: Duration of outage events (in minutes)
- **'CUSTOMERS.AFFECTED'**: Number of customers affected by the power outage event
- **'TOTAL.PRICE'**: Average monthly electricity price in the U.S. state (cents/kilowatt-hour)

This choropleth map below visualizes the total number of power outages for each state in the United States from 2000 to 2016. The darker the color, the higher the number of outages that occurred in that state during this 16-year period. 
- For Alaska, where no outage duration information is available, it appears in grey instead of the color map.
<iframe src="assets/map.html" width=800 height=600 frameBorder=0></iframe>


### Cleaning and EDA
#### Step 1: Data Cleaning
**Step 1.1**: 
   1. Combine power outage start date and time
   2. Combine power restoration date and time

After step 1.1, we have 1534 rows and 10 columns. 
Part of our data frame: (Only top 5 rows)

|    | STATES   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   OUTAGE.DURATION |   CUSTOMERS.AFFECTED |   TOTAL.PRICE | OUTAGE.START        | OUTAGE.RESTORATION   |   YEAR |
|---:|:---------|:-------------------|:------------------------|------------------:|---------------------:|--------------:|:--------------------|:---------------------|-------:|
|  1 | MN       | severe weather     | nan                     |              3060 |                70000 |          9.28 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |   2011 |
|  2 | MN       | intentional attack | vandalism               |                 1 |                  nan |          9.28 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |   2014 |
|  3 | MN       | severe weather     | heavy wind              |              3000 |                70000 |          8.15 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |   2010 |
|  4 | MN       | severe weather     | thunderstorm            |              2550 |                68200 |          9.19 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |   2012 |
|  5 | MN       | severe weather     | nan                     |              1740 |               250000 |         10.43 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |   2015 |


**Step 1.2**:
   1. Change column "POSTAL.CODE" to "STATE" to be more readble.
   2. Clean the data of column ‘OUTAGE.DURATION’ and ignore the np.NANs in column ‘OUTAGE.DURATION’ 
   3. Create new column ‘YEAR’ as integer for convinience of  further analysis.

After step 1.2, we have 1398 rows and 9 columns. 
Part of our data frame: (Only top 5 rows)

|    | STATES   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   OUTAGE.DURATION |   CUSTOMERS.AFFECTED |   TOTAL.PRICE | OUTAGE.START        | OUTAGE.RESTORATION   |   YEAR |
|---:|:---------|:-------------------|:------------------------|------------------:|---------------------:|--------------:|:--------------------|:---------------------|-------:|
|  1 | MN       | severe weather     | nan                     |              3060 |                70000 |          9.28 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |   2011 |
|  2 | MN       | intentional attack | vandalism               |                 1 |                  nan |          9.28 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |   2014 |
|  3 | MN       | severe weather     | heavy wind              |              3000 |                70000 |          8.15 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |   2010 |
|  4 | MN       | severe weather     | thunderstorm            |              2550 |                68200 |          9.19 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |   2012 |
|  5 | MN       | severe weather     | nan                     |              1740 |               250000 |         10.43 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |   2015 |

#### Step 2: Univariate Analysis
**Step 2.1**:
The initial graph is a bar chart depicting the frequency of major outages each year. This visualization provides insights into the occurrence of major outages throughout different years. Before 2011, there was a consistent annual increase in the number of outages, peaking significantly in 2011. Subsequently, post-2011, there has been a gradual decline in outage occurrences. 
<iframe src="assets/bar_chart_1.html" width=800 height=600 frameBorder=0></iframe>

**Step 2.2**: 
This histogram illustrates the distribution of outage duration times. The majority of outages occurred within the range of 0 to 500 minutes. 
To enhance readability and understanding, outliers with extremely large duration times have been filtered from the dataset.
<iframe src="assets/2_2.html" width=800 height=600 frameBorder=0></iframe>


#### Step 3: Bivariate Analysis
During the process of identify possible associations:

**Step 3.1**: 
 The initial graph we generate is a line graph comprising three distinct lines. The first line represents the count of major outages caused by severe weather over the years. The second line reflects the count of major outages attributed to causes other than severe weather. Lastly, the third line illustrates the total count of major outages encompassing all causes. 
 This graph effectively demonstrates the distribution and relationship between different outage causes over time. All three lines exhibit a parallel pattern over time, with an upward trend leading to a peak around 2011, followed by a decline in subsequent years. This consistent trend of increase before 2011, a substantial peak in 2011, and a subsequent decrease is evident across all three lines.
<iframe src="assets/3_1.html" width=800 height=600 frameBorder=0></iframe>

**Step 3.2**: The second graph we create is a histogram featuring two accompanying box plots. The histogram visually represents the distribution of outage durations caused by severe weather and other factors. Additionally, the box plots provide comprehensive statistical information, including measures of central tendency and the range of both distribution datasets, offering a comparative view of outage durations across different causes. 
The data indicates that factors other than severe weather predominantly resulted in shorter outage durations, as observed from their lower median values. However, these cases exhibit numerous smaller outliers. Conversely, outages attributed to severe weather tended to have longer durations, with a wider range of variability in outage times.
<iframe src="assets/3_2.html" width=800 height=600 frameBorder=0></iframe>


#### Step 4: Interesting Aggregates

We choose to group CAUSE.CATEGORY column and index of each year to create the pivot table. This presentation directly illustrates the distribution of various causes of power outages across different years, facilitating an understanding of the variations in the number of power outages attributed to each specific cause.

|   YEAR |   equipment failure |   fuel supply emergency |   intentional attack |   islanding |   public appeal |   severe weather |   system operability disruption |
|-------:|--------------------:|------------------------:|---------------------:|------------:|----------------:|-----------------:|--------------------------------:|
|   2000 |                   0 |                       0 |                    0 |           0 |               0 |                9 |                               3 |
|   2001 |                   1 |                       0 |                    0 |           0 |               3 |                1 |                               9 |
|   2002 |                   0 |                       0 |                    0 |           0 |               0 |               11 |                               3 |
|   2003 |                   6 |                       0 |                    2 |           0 |               1 |               30 |                               7 |
|   2004 |                   5 |                       0 |                    0 |           0 |               7 |               56 |                               3 |
|   2005 |                   3 |                       0 |                    0 |           0 |               0 |               47 |                               4 |
|   2006 |                   1 |                       0 |                    0 |           0 |               2 |               54 |                               9 |
|   2007 |                   6 |                       1 |                    0 |           1 |               2 |               40 |                               4 |
|   2008 |                   9 |                       3 |                    0 |           6 |               2 |               76 |                              14 |
|   2009 |                  10 |                       2 |                    0 |           4 |              10 |               45 |                               6 |
|   2010 |                   5 |                       3 |                    0 |           9 |              14 |               62 |                              12 |
|   2011 |                   3 |                       6 |                   77 |           3 |              16 |              104 |                              12 |
|   2012 |                   1 |                       4 |                   70 |           4 |               3 |               65 |                               6 |
|   2013 |                   4 |                       6 |                   75 |           7 |               0 |               49 |                               6 |
|   2014 |                   0 |                      10 |                   42 |           1 |               5 |               43 |                               1 |
|   2015 |                   0 |                       1 |                   41 |           8 |               4 |               39 |                              13 |
|   2016 |                   0 |                       2 |                   25 |           1 |               0 |               10 |                               8 |

### Assessment of Missingness
#### NMAR Analysis
We posit that there exists a NMAR relationship between the data in the CUSTOMERS.AFFECTED and TOTAL.PRICE columns. Given that power outages attributable to factors such as severe weather and various other causes, the customer affected population will be various, the TOTAL.PRICE is unlikely to exert a direct influence on the CUSTOMERS.AFFECTED variable.
However, the influence on the CUSTOMERS.AFFECTED variable may be discerned through the temporal aspect captured by the OUTAGE.DURATION column. It is conceivable that an extended outage duration could result in a higher number of affected customers, thereby introducing a missing at random (MAR) pattern in the CUSTOMERS.AFFECTED column.

#### Step 5: Missingness Dependency
**Step 5.1**:
- **Null Hypothesis**: Values in the 'TOTAL.PRICE' column for rows where the 'CUSTOMERS.AFFECTED' was missing were drawn from the same distribution as the values in rows where 'CUSTOMERS.AFFECTED' was not missing.
- **Alternative Hypothesis**: They were drawn from different distributions.
- **Significance level**: 0.05
<iframe src="assets/g5_2_1.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/g5_2_2.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/5_2_3.html" width=800 height=600 frameBorder=0></iframe>
The p-value is approximately 0.85 , which is higher than our significance level. We fail to reject the null hypothesis, the missing data from CUSTOMERS.AFFECTED are not depends on TOTAL.PRICE.

**Step 5.2**:
- **Null Hypothesis**: Values in the 'OUTAGE.DURATION' column for rows where the 'CUSTOMERS.AFFECTED' was missing were drawn from the same distribution as the values in rows where 'CUSTOMERS.AFFECTED' was not missing.
- **Alternative Hypothesis**: They were drawn from different distributions.
- **Significance level**: 0.05
<iframe src="assets/g5_1.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/g5_1_2.html" width=800 height=600 frameBorder=0></iframe>
<iframe src="assets/5_1_3.html" width=800 height=600 frameBorder=0></iframe>
The p-value is approximately 0.011, which is lower than our significance level. We reject the null hypothesis. The missing data from CUSTOMERS.AFFECTED are depends on OUTAGE.DURATION.

### Hypothesis Testing
#### Severe Weather V.S. All Causes
The question we are trying to answer is whether the occurrence of severe weather contribute to a higher frequency of power outages compared to other causative factors in the year with the highest number of outages. These choices below are good to answer the question since they all aligns with our research question. And the significance Level is a common choice. 

In our dataset, the most outage-prone year is 2011. 

- **Null Hypothesis**: The distribution of outages in 2011 due to severe weather is consistent with the overall distribution of outages across all causes and years.
- **Alternative Hypothesis**: The distribution of outages in 2011 due to severe weather is larger than from the overall distribution of outages across all causes and years.
- **Test Statistic**:  The count of severe weather-caused outages.
- **Significance level**: 0.05

#### The plan
To conduct our hypothesis test, we will:
- Calculate the overall probability distribution of outage causes for all years.
- Run a simulation with 100,000 iterations.
<iframe src="assets/hyp.html" width=800 height=600 frameBorder=0></iframe>

### Conclusion
- The p-value is 0.96735, it is more than the significance level of 0.05. 
- We reject the null hypothesis. 
- There is enough evidence to conclude that the distribution of severe weather-caused outages in 2021 is significantly larger than the overall distribution across all causes and years.