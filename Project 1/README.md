# Project 1: Standardized Testing, Statistical Summaries and Inference

## Problem Statement

With the release of the new format for SAT in 2016, the test has been improved tremendously making more straight-forward with less tricky vocabulary and wrong answers are no longer penalised. With all these in place, our team has tracked statewide participation and would like to investigate how the College Board can increase the participation rate in North Dakota.

## Executive Summary

North Dakota has reported very low participation rate of only 2% in 2017 and 2018 while its ACT participation showed a 98% in both years. In order to increase its participation rate in SAT, there needs to be a better understanding between the relationships between the SAT and ACT scores as well as the participation rates. The following sections will describe the whole process of investigation and also showcase the findings.

- [2017 Data Import & Cleaning](#2017-Data-Import-and-Cleaning)
- [2018 Data Import and Cleaning](#2018-Data-Import-and-Cleaning)
- [Exploratory Data Analysis](#Exploratory-Data-Analysis)
- [Data Visualization](#Visualize-the-data)
- [Descriptive and Inferential Statistics](#Descriptive-and-Inferential-Statistics)
- [Outside Research](#Outside-Research)
- [Conclusions and Recommendations](#Conclusions-and-Recommendations)

## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**state**|*object*|sat_2017/act_2017/final|The list of states of the country that has participations in the respective test.| 
|**sat_2017_participation**|*integer*|sat_2017/final|The participation rate indicates the percentage of people who take part in SAT 2017 in each state.|
|**sat_2017_reading_and_writing**|*integer*|sat_2017/final|The average score of the evidence-based reading and writing component in SAT by state.|
|**sat_2017_math**|*integer*|sat_2017/final|The average score of the mathematics component in SAT by state.|
|**sat_2017_total**|*integer*|sat_2017/final|The average of total SAT scores in 2017 by state.|
|**act_2017_participation**|*integer*|act_2017/final|The participation rate indicates the percentage of people who take part in ACT 2017 in each state.|
|**act-2017_english**|*float*|act_2017/final|The average score of the english component in ACT by state.|
|**act_2017_math**|*float*|act_2017/final|The average score of the mathematics component in ACT by state.|
|**act_2017_reading**|*float*|act_2017/final|The average score of the reading component in ACT by state.|
|**act_2017_science**|*float*|act_2017/final|The average score of the science component in ACT by state.|
|**act_2017_total**|*float*|act_2017/final|The average composite ACT score in 2017 which shows the average across all components.|
|**sat_2018_participation**|*integer*|sat_2018/final|The participation rate indicates the percentage of people who take part in SAT 2018 in each state.|
|**sat_2018_reading_and_writing**|*integer*|sat_2018/final|The average score of the evidence-based reading and writing component in SAT 2018 by state.|
|**sat_2018_math**|*integer*|sat_2018/final|The average score of the mathematics component in SAT by state.|
|**sat_2018_total**|*integer*|sat_2018/final|The average of total SAT scores in 2018 by state.|
|**act_2018_participation**|*integer*|act_2018/final|The participation rate indicates the percentage of people who take part in ACT 2017 in each state.|
|**act-2018_english**|*float*|act_2018/final|The average score of the english component in ACT by state.|
|**act_2018_math**|*float*|act_2018/final|The average score of the mathematics component in ACT by state.|
|**act_2018_reading**|*float*|act_2018/final|The average score of the reading component in ACT by state.|
|**act_2018_science**|*float*|act_2018/final|The average score of the science component in ACT by state.|
|**act_2018_total**|*float*|act_2018/final|The average composite ACT score in 2018 which shows the average across all components.|


### 2017 Data Import and Cleaning

The sat_2017 data list contains information across 51 locations (states and federal district) on sat participation rate and the  average result in two components, math and evidence-based reading and writing, as well as the average total score for the two components. The act_2017 data list also contains participation rate across the 51 locations. It also shows the state average score for four categories, English, Math, Reading and Science. The composite score is the average of all 4 components.

The data looks complete as there is no empty field in both lists. For SAT, each component of evidence-based reading & writing and mathematics has a minimum and maximum score of 200 and 800 respectively, and the total composite score range from 400 to 1600. The ACT is scored on a scale of 1 to 36 on each of the four components, and the average composite score also has a minimum score of 1 and maximum score of 36.

There were 3 errors found in the data and have been replaced with the correct values. The data type of participation rates have also been converted to interger type so that we can better sort the data later on. SAT and ACT scores were set to either integer or float for data handling. Only the data type for states remains as an object.

Column names have been changed to more expressive and unique names to differentiate between the SAT columns and the ACT columns. The column names are all in lower case and do not contain any space. 

The row information for national has been removed and the data from SAT 2017 and ACT 2017 are then combined together and saved as a new file combined_2017.csv.

### 2018 Data Import and Cleaning

The same steps have been done to SAT 2018 an ACT 2018 data. For the 2018 data, there was no error found and the data is complete as there is no empty field. The columns name have been replaced by unique names to differentiate between the 2017 and 2018 data as well as SAT and ACT data. They are all in lower case with no space. The data types are of the same types as the 2017 data with only the states name saved as an object. The rest of the data are either of integer type or float type.

For ACT 2018, the average composite score column has been shifted to the end so that it is in the same order as ACT 2017 file. 

The two dataframes from SAT 2018 and ACT 2018 were then combined into one file and saved as combined_2018.csv. Finally, the 2017 and 2018 data were also combined and saved as final.csv. This file will be used for the rest of investigation and analysis.

### Exploratory Data Analysis

#### Summary Statistics

We first took a quick overview of the summary statistics with pandas describe() which showed the count, mean, standard deviation, minimum value, maximum value, 25% percentile, 50% percentile (median) and 75% percentile for each of the variables. 

The standard deviation has been manually computed which showed that they were slightly different from pandas describe(). The manually calculated standard deviation values match with those generated from numpy's standard deviation value, but those from pandas describe are not the same. It is because pandas describe uses (n-1) for unbiased sample data instead of n in the calculation for standard deviation and variance.

#### Investigate trends in the data

Highest & Lowest Participation Rates for SAT and ACT in 2017 & 2018:

|Test|Participation Rate|States|
|---|---|---|
|**2017 SAT**|*Highest*|Connecticut, Delaware, District of Columbia and Michigan| 
|**2017 SAT**|*Lowest*|Iowa, Mississippi and North Dakota| 
|**2018 SAT**|*Highest*|Colorado, Connecticut, Delaware, Michigan and Idaho| 
|**2018 SAT**|*Lowest*|North Dakota| 
|**2017 ACT**|*Highest*|Alabama, Arkansas, Colorado, Kentucky, Louisiana, Minnesota, Mississippi, Missouri, Montana, Nevada, North Carolina, Oklahoma, South Carolina, Tennessee, Utah, Wisconsin and Wyoming| 
|**2017 ACT**|*Lowest*|Maine| 
|**2018 ACT**|*Highest*|Alabama, Arkansas, Colorado, Kentucky, Louisiana, Mississippi, Missouri, Montana, Nevada, North Carolina, Oklahoma, South Carolina, Tennessee, Utah, Wisconsin and Wyoming| 
|**2018 ACT**|*Lowest*|Maine| 

It was noted that for SAT, some states are consistently high in participation across the two years. They are Connecticut, Michigan and Delaware. North Dakota has the lowest participation rate for both years.

It was also shown that Colorado showed the highest rate increase in participation of 809% from 11% in 2017 to 100% 2018. District of Columbia showed a 8% decrease in participation rate from 100% to 92%.

For ACT, 15 states has perfect participation rate for both 2017 and 2018. They are Wyoming, Mississippi, Missouri, Tennessee, Montana, Nevada, Kentucky, Alabama, Oklahoma, Wisconsin, North Carolina, Utah, South Carolina, Arkansas and Louisiana. Maine has a consistent low participation rate across both years.

Interesting, Colorado showed the highest rate decrease in participation of 70%, from 100% in 2017 to only 30% in 2018. Nebraska and Ohio both showed an increase in participation rate from 2017 to 2018 with 19% and 33% respectively.

Florida, Georgia and Hawaii showed participation rates greater than 50% for SAT and ACT in both years.
In 2018, 2 other states, North Carolina and South Carolina also had participation rate of more than 50% for both tests.

|Test|Highest score|States|Lowest score|State|
|---|---|---|---|---|
|**2017 SAT**|1295|Minnesota|950|District of Columbia| 
|**2018 SAT**|1298|Minnesota|977|District of Columbia|
|**2017 ACT**|25.5|New Hampshire|17.8|Nevada| 
|**2018 ACT**|25.6|Connecticut|17.7|Nevada| 

For both SAT in 2017 and 2018, the highest mean total score came from Minnesota while the lowest was from District of Columbia.
For ACT, Nevada had the lowest mean composite score for both 2017 and 2018, while New Hampshire and Connecticut had the highest mean composite score in 2017 and 2018 respectively.

### Visualize the data

The following plots have been done to get a better visualization of the relationship between various data:

- Heatmap showing correlation between all the variables (Overview)
- Histograms subplots for Participation rates for SAT & ACT
- Histograms subplots for Math scores for SAT & ACT
- Histograms subplots for Reading/verbal scores for SAT & ACT
- Scatter plot for SAT vs. ACT math scores for 2017
- Scatter plot for SAT vs. ACT verbal/reading scores for 2017
- Scatter plot for SAT vs. ACT total/composite scores for 2017
- Scatter plot for Total scores for SAT 2017 vs. 2018
- Scatter plot for Composite scores for ACT 2017 vs. 2018
- Boxplot for each numeric variable
- Scatter plot for Participation Rate and SAT Mean Total Score in 2017 (Additional)
- Scatter plot for Participation Rate and SAT Mean Total Score in 2018 (Additional)
- Scatter plot for Participation Rate and ACT Mean Composite Score in 2017 (Additional)
- Scatter plot for Participation Rate and ACT Mean Composite Score in 2018 (Additional)
- Scatter plot for Percentage Rate Change in Participation for SAT & ACT (Additional)
- Boxplot for Percentage Rate Change for SAT and ACT (Additional)
- Histograms subplots for English scores for SAT & ACT (Additional)
- Histograms subplots for Science scores for SAT & ACT (Additional)

There is a negative correlation between participation rates and SAT mean total score as well as ACT mean component score. It means that states with a higher participation rate generally showed a poorer performance as compared to states that has a low participation rate.

About half the states showed a decrease in participation rate for ACT from 2017 to 2018, with Colorado having the biggest drop followed by Illinois. Both states also showed tremendous increase in SAT participation rate. As the number of participants has significantly decreased, the mean composite score for ACT has shown a significant increase.

As seen from the choropleth maps, states that have high participation rates in ACT are concentrated in the central and Southern part of the country. However, states at the coastal area which showed lower participation rate had higher mean composite score for ACT in both 2017 and 2018.

The reverse is true for SAT. The choropleth maps show that the central and southern regions has low participation rates but display higher mean total scores. The drastic change in participation rates for Colorado and Illinois is also observed.

### Descriptive and Inferential Statistics

#### SAT Participation Rate

For SAT participation rates in 2017 and 2018, the frequency distribution is slightly skewed left and random with a spike in the lowest rate region. As there is a higher percentage of states with low participation rate for SAT, the mean are low at 39.8% and 45.7% respectively. The median participation rates for 2017 is 38% which is quite close to the mean value, while for 2018, the median is 52%, meaning that in 2018 some states had slightly higher participation rate as compared to 2017, which is also reflected on the distribution graph. In total, 33 states had shown in increase in the participation rate for SAT between 2017 and 2018 while 5 states had reflected a decrease. The standard deviation is high quite with a value of 35.3 and 37.3, indicating a wide spread of participation rates across all the states.

#### ACT Participation Rate

For ACT participation rates in both years, the distributions are bimodal as they showed two spikes, one in the lower rates region and one in the highest rates region. It was found earlier on that about 1/3 of the states had 100% participation rates for both years, pushing the mean higher to be 65.3% and 61.6% for 2017 and 2018 respectively. The median are at 69% and 66% which are quite close to the mean value. In general, more states has a higher participation rate for ACT than SAT. The standard deviation is high quite with a value of 32.1 and 34.1 in both years, indicating a wide spread of participation rates across all the states.

#### SAT Math Component Score

The distribution for SAT Math component are quite uniform in both 2017 and 2018, with both showing a spike in the 510-550 range. The mean math scores for both years are the same at 556, which is just outside the range with the highest frequency. The standard deviation is relatively low with a value of 47.1 and 47.7 in 2017 and 2018 respectively. As we can see that the spread of the math score is not too wide, with an IQR of 75 and 71 in the two years.

#### SAT Evidence-based Reading and Writing Component Score
The distribution for SAT evidenced-based reading and writing component resembles that of a normal distribution with a mean score range of 480 to 615, and then there was a second surge in the frequency in the range of 615 to 645 for both 2017 and 2018. The mean score for both years are 569 and 563, which is higher than that of the math component score. The standard deviation is also relatively low with a value of 45.7 and 47.5 respectively. Similar to the math component score, the data is not too widely spread, with an IQR of 79.5 and 76 for the two years.

#### ACT Math Component Score
The ACT math component mean score for 2017 and 2018 are skewed right, with higher frequencies occuring in the lower score range than in the higher score range. 2017 and 2018 has the same mean of about 21.1, and a median of 20.9 and 20.7 respectively. This is expected as more states are in the lower score range. The standard deviation for both years are low with a value of 1.98 and 2.03, with an IQR of 3.7 and 3.75. The spread of data is similar to that of SAT component score.

#### ACT Reading Component Score
The distribution for ACT reading component resembles that of a normal distribution with mean score range of 18 to 26.1. Since the distribution is normal, the expected mean for both 2017 and 2018 is reflected as 22 which is in the middle score range. The median are 21.8 and 21.6 for 2017 and 2018 respectively, which is also in middle score range.
The reading component score also has a similar spread of data with a standard deviation of about 2.1.

#### ACT English Component Score
The distribtution for ACT english composite score is a bell-shaped curve that is slightly skewed to the right. The mean of the english component is 20.9 for both years, which is the lowest among all the four components of ACT. As compared to the other components, the spread of data is slightly wider with a standard deviation value of 2.4. While the IQR is similar to the other components, the english component has the lowest minimum score of 16.3 and 16.6 for 2017 and 2018.

#### ACT Science Component Score
The ACT science component score has a normal distribution which is more obvious in 2017. For 2018, the distribution also has a spike but the rest of the distribution is more uniform. Similar to the reading component, the mean is expected to be in the middle score range and has a value of 21.4 and 21.3 for 2017 and 2018 respectively. The science component showed slightly lower standard deviation value of 1.74 and 1.87 as compared to other components, with IQR of 3.1 and 3.2 for both years.

#### SAT Total Score
Since the SAT total Score is a combination of the Math component and the Evidenced-based Reading & Writing component, we have expected the distribution to be similar. The distribution for SAT total score resembles that of a normal distribution with a mean score range of 950 to 1230, and then there was a second surge in the frequency in the range from 1230 to 1300 for both 2017 and 2018. The mean total for both years are 1126 and 1120, with a standard deviation of 92.5 and 94.1.

#### ACT Composite Score
The ACT composite score distribution is also similar to its components score distribution, it is bell-shaped curve that is slightly skewed to the right. As it is close to a normal distribution, the mean is expected to be in the middle score range, and they have a value of 21.5 in both years. The median is also in the middle score range with a value of 21.4 and 21.3 in 2017 and 2018 respectively.

#### Distributions in the data
In general, we do see distributions that have a bell-shaped curve or uniform distribution with spikes. They are close to a normal distribution but as we only have 51 samples, the sample size is still relatively small to get a better fit normal distribution. Based on the Central Limit Theorem, we can generally assume that the data means are normally distributed.

MATH:
For both SAT and ACT math component mean score, the assumption is true as mean math scores are taken from 51 different samples (states) and the distributions showed a spike in the frequency. However, as the sample size is relatively small and for each sample, as the number of participants from each states are different, the mean obtained in some states might have biased results.

READING:
Similarly for reading, the obsevation is true, and CLT is somewhat observed but not fully reflected well as the samples taken were different and slightly biased. If we were to increase the sample size across the whole nation, we should be able to get a better fit normal distribution curve.

RATES:
For participation rate, we do not see a normal distribution for the frequency and the assumption does not hold in this case. Participation rate in each sample is affected by a number of different factors, such as location, demographics of the state, market trends, and also state policies. As such, the samples taken are not really random.

#### Estimate Limits of Data
Due to the nature of the frequency distribution with high or low extreme values, and that the CLT does not hold in this case, it is not of interest to conduct statistical inference for these data. In the case of participation rates, we only have the data for percentage without knowing the population size of each sample, we do not have a complete picture of the spread of where the participants come from. Some states might have small population size with high participation rates but that contributed minimally towards the actual population mean. With the low granularity of data given, we are not able to make specific and targeted estimate of the population parameter.

It is not appropriate to compare SAT and ACT math scores. As seen from the scatter plot, there is no correlation between the two variables. States that have performed well in SAT math do not in general also perform better in ACT math. Moreover, we do not have sufficient data to make a good comparison because only five states had participation rate greater than 50% in both tests. Hence, we are looking at the mean scores of different groups of participants for both tests, and no clear conclusion can thus be drawn.

#### Statistical Evaluation of Distributions
HYPOTHESIS TESTING:

Increase in SAT participation rate will lead to a decrease in the mean total score. 
#H(A) : μ_2017 - μ_2018 > 0 
#H(0) : μ_2017 - μ_2018 = 0

Since the p-value > 0.05, there is insufficient evidence to reject the null hypothesis and we cannot conclude that an increase in SAT participation rate across the nation will lead to a decrease in the mean total score.

### Outside Research
For North Dakota, it had the lowest participation rates of 2% for both years for SAT but 98% participation rate for ACT. The University of North Dakota is competitive for SAT scores. The mean total SAT score is also above the 75% percentile, meaning students who took SAT in North Dakota are likely to perform better than national average. For ACT, it is moderately competitive, and hence, majority of participants opted for taking the ACT as there is another advantage of submitting ACT scores over SAT. For ACT, only the highest score for multiples tests taken needs to be sent in for admission to college, but for SAT, the school often required participants to send in all the tests ever taken. With the test submission requirement and also competitive nature of SAT, most candidates from North Dakota has chosen ACT over SAT.

For Colorado and Illinois, both states has shown a drastic switch in participation rates from ACT to SAT. This was due to both states coming into a state-wide contract with the College Board, with College Board making changes to its SAT test to make them more straightforward and approachable with less tricky vocabulary and questions that penalised wrong answers. Other initiatives like SAT School Day whereby participants can take the test during school hours free of charge are also another appeal for the state-wide switch.

### Conclusions and Recommendations
States that have high participation rates in SAT are concentrated in the coastal part of the country. However, states at the central and southern area which showed lower participation rates had higher mean total score for SAT in both 2017 and 2018. This is also true for North Dakota which had the lowest participation rate of 2% but a high average mean total score of 1250 which is above the 75% percentile of the population. 

The College board might want to negotiate more state-wide testing contracts with states in Central and Southern parts of the country especially in NOrth Dakota where the participation rate of ACT is high. With more people taking part in SAT, the college admission with SAT will become slightly less competitive.

The College Board should also provide support and tailor the tests to the needs of different states. There are SAT School Day where tests can be taken on a school day for free. In the example of Illinois, students are able to access themselves first in a Practice SAT in the 10th grade before getting help through online free tutoring and taking the real SAT test in 11th grade. These initiatives are very useful to prepare candidates to take SAT and perform well with without taking the actual tests repeatedly, wasting time and money. 

Useful additional data will be the percentage of incoming freshmen for the colleges submitting SAT for their applications, as well as the actual number of participations from each state.









