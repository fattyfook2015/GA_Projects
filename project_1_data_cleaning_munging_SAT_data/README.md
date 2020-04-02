

### Overview



# Project 1: Standardized Testing, Statistical Summaries and Inference - US State SAT/ACT 2017/2018 Data

### Context and Problem Statement

SAT and ACT are the two major nation-wide college admission tests used by US colleges for high school graduates. SAT wishes to increase its SAT participation rates in states across the USA.

As such, by using past data for 2017 and 2018, together with external research, we aim to find correlations to better target increase of SAT participation rates.

Data was provided via csv files. However, data cleaning was necessary. 4 clear errors were found in the files provided. After cleaning, data analysis began.

---

## Executive Summary

### Contents:

- [2017 Data Import & Cleaning](#2017-Data)
- [2018 Data Import and Cleaning](#2018-Data)
- [Exploratory Data Analysis](#EDA)
- [Data Visualization](#Data-Visualization)
- [Descriptive and Inferential Statistics](#Descriptive-and-Inferential-Statistics)
- [Outside Research, Conclusions and Recommendations](#Outside-Research-Conclusions-Recommendations)

---

### 2017-Data

After checking through the data and doing research on range of legal values, the following errors were found:

These errors were:

A) Integrity Constraint Violations or Illegal Values
B) Misspellings
C) Wrong Datatype
D) Outlier Data, later revealed to be Misspelling

After cleaning, renaming of column headers was done, to differentiate clearly data columns before doing any merges.

2017 SAT and ACT data were then merged into one dataframe. This 2017 dataframe would later be merged with the 2018 dataframe to form a consolidated, final dataframe.

Extra 'National' row entries were removed to ensure like-to-like comparison.

---

### 2018-Data

ACT 2018 data had two files. One was the updated version which was used instead of the incomplete one. This highlighted the importance of always checking the data before further processing, to prevent wasted time and effort, or even worse, wrong conclusions due to wrong or insufficient data.

Likewise, SAT 2018 and ACT 2018 data were merged into a 2018 dataframe. Checks were made to ensure that column headers were renamed appropriately and data was in order.

2017 and 2018 dataframes were then merged into a final_df dataframe.


---

### EDA

Many states seem to have 100% ACT Participation as opposed to no. of states having 100% SAT Participation.


Colorado has a sharp increase in SAT participation from 2017 (11%) to 2018 (100%). It has a corresponding large drop in ACT participation rate from 2017 (100%) to 2018 (30%).

Illinois has an increase in SAT participation from 2017 (9%) to 2018 (100%). It has a large corresponding drop in ACT participation rate from 2017 (93%) to 2018 (43%).

Florida has a significant drop in SAT participation from 2017 (83%) to 2018 (56%). It also has a drop in ACT participation rate from 2017 (73%) to 2018 (66%).


---

### Data-Visualization

Histograms, scatter plots and boxplots were used to visualise the data extracted, and to glean further insights.

Medians for both SAT 2017 and SAT 2018 participation rates were similar, with 2018 showing an increase of about 10%.

Upper and Lower Tails for SAT 2017 and SAT 2018 participation rates were similar, stretching to 100% participation, or almost 0% participation.

SAT 2018 participation showed a wider/longer interquartile range, states in 2018 seemed to differ more in terms of participating in SAT.

Medians for both ACT 2017 and ACT 2018 participation rates were similar.

Upper and Lower Tails for ACT 2017 and ACT 2018 participation rates were similar, stretching to 100% participation, or almost 0% participation.

Interquartile ranges for ACT 2017 and 2018 participation rates were similar, not much change is observed over these two years.

Comparing SAT to ACT medians, there was a significantly higher % of average participation of about 15-20% for ACT as opposed to SAT for both 2017 and 2018.

After checking all variables, it was observed that there was not much change in results or participation rates on a whole, across all states from 2017 to 2018.

Outliers were discovered, however, and upon further investigation, revealed as a typing error from data source provided. This highlighted the importance of not assuming data is fully cleaned, and investigating outliers further.

If any changes were implemented to the tests themselves or teaching methodology, it might be too soon for the effects to be realised.

---

### Descriptive-and-Inferential-Statistics

**Central Dependency, Spread and Skew**

Numerical variables (participation rates of SAT and ACT, as well as their component and overall test scores) were then plotted against states, and the frequency distribution of the average scores themselves plotted to investigate any normal distribution behaviour, for modeling.

Their central dependency, spread and skew values were also extracted for inspection.

Normal Distributions have a Skew of 0.0. Note that this does not mean that every distribution with a Skew of 0.0 is Normal, it just means that distributions with skew far away from 0 are definitely not Normal Distributions.

In general, let us consider distributions with skew between -0.5 and 0.5 as having the possibility of being Normal Distributions, and warrant further investigation if proving they can be considered Normal Distributions.

Any distributions with skew of less than 0.5 or more than 0.5 are definitely not Normal Distributions.

Note that in our project, 'state' is the key variable that the other variables are being measured against. As 'state' is a discrete, catergorical variable, it does not make sense for any normal relationship nor distribution for other variables to exist against it.

Instead, let us consider looking at distribution of values within each column to determine if they have frequencies of their values exhibiting normal distribution.

**Barplot and Distplot**

For SAT 2017 participation rate, visually, we can see that many states have either high or low participation rates, with approximately only half the states having participation rates around the median.

Median and mean are similar with standard deviation having similar value. Indicates that high frequencies at both ends of the possible values, visually confirmed by the distribution plot.

This goes well with our research indicating certain states have compulsory SAT testing. Some states that have only compulsory ACT have a low SAT participation rate. Note that from earlier data pulled, we know some states have high participation rates for ACT and SAT, and some states have low participation rates for both ACT and SAT.

No normal distribution observed here, as expected due to the definition of the variable being SAT 2017 participation rate of each state. This gives it a narrow fixed maximum population of 51 data points (if allowing Washington DC to be counted as 51st state), with all 51 data points being merely part of a categorical variable, 'state'.

Instead we can look at 'score' variables after the 'participation rate' variables, as an indication of scores across an expanded population. Sample size unknown and likely indeterminate, with different populations across different states, but with 51 being the number of samples taken, 1 for each state.

Distribution plots often exhibited two peaks. The two peaks might be indicative of two different education systems within the states, generating, in fact, 2 normal distributions based on different education systems. Note that the whatever is causing the secondary peak, it is less impactful on ACT scores as opposed to SAT scores.

**Central Limit Theorem**

The Central Limit Theorem states that the sampling distribution of the sample means approaches a normal distribution as the sample size gets larger — no matter what the shape of the population distribution. This fact holds especially true for sample sizes over 30.

Our sample sizes are 51, which are over 30.

However, only Average Science Score for ACT 2018 seems to have a normal distribution.

Most of the other numerical variables seem to have a two-peak distribution, which might indicate 2 normal distributions laid over each other.

This could be indicative of two different educational policies or systems across the 50 states plus District of Columbia.

It is possible that increased sample size will result in a distribution approachng normal distribution, however as there are only 50 states plus District of Columbia, we are unable to have larger sample sizes, unless we base our sampling off the entire USA population instead of each sample being one mean value per state.

---

### Outside-Research-Conclusions-Recommendations


**Outside-Research**

(Source: Article from Chalkbeat.org; Goodbye ACT, hello SAT: a significant change for Colorado high schoolers By Eric Gorski December 23, 2015)
(https://chalkbeat.org/posts/co/2015/12/23/goodbye-act-hello-sat-a-significant-change-for-colorado-high-schoolers/

For Colorado, there was "... a competitive bidding process required by hard-fought testing reform legislation ...a selection committee chose The College Board, makers of the SAT, over the ACT testing company, which has been testing juniors in Colorado since 2001...SAT has a reputation for being more reason-based and focused on critical thinking, while the ACT has a reputation for being more of a fact-recall test..."

This took effect around the year 2016-2017, hence explaining the sharp increase in SAT, and drop in ACT participation in 2017.


(Source: CHICAGO TRIBUNE; Illinois moves ahead with new testing plan, replacing ACT with SAT By DIANE RADO FEB 11, 2016) https://www.chicagotribune.com/news/ct-illinois-chooses-sat-met-20160211-story.html

For Illinois, "...It's official, according to the state: Testing giant ACT is out and the College Board's SAT is in, bringing a new college entrance exam into Illinois public high schools..."

This was a decision made by the State Board to award the contract to SAT instead of ACT.

This took effect also around the year 2016-2017, in a similar manner to that of Colorado, hence explaining the sharp increase in SAT, and drop in ACT participation in 2017 for Illinois.


(Source: Stateimpact.npr.org; Meet Florida’s New Statewide Test BY JOHN O'CONNOR NOVEMBER 24, 2014) https://stateimpact.npr.org/florida/2014/11/24/meet-floridas-new-statewide-test/)

For Florida, Florida Standards Assessment was a new state exit exams independent of SAT or ACT, which could be taken in lieu of either ACT or SAT. This led to no requirement on Florida's students to take either SAT or ACT, which explains the decrease of participation over the years.

Site showing overall high school graduation requirements for all US States: https://www.edweek.org/ew/section/multimedia/states-require-students-take-sat-or-act.html

**Additional Plots**

Investigation was done for relationship of SAT and ACT Scores against their Participation Rates. Unfortunately, no meaningful relationship could be established. Additional data would be needed:

Do note that it has been indicated that the higher the participation rate, the more accurate the mean, and with a low participation rate, it is logical that only the more confident students will be taking the tests.

In order to explore if states which are likely to score better are more likely to adopt the SAT system, we will need more details such as actual amount of students taking the tests.


**Null Hypothesis**

A null hypothesis based on the score distributions consistently showing 2 peaks, is that:

There aren't two education system models distinct enough, such that each state's student population tends to perform differently at SAT or ACT based on their training.

This would require additional data not available in the timeframe, and would require further investigation, and separating the states along their perceived education system differences.


**Conclusions and Recommendations**

Oregon could be the state with lower participation rate to be chosen.

Oregon has participation rates for SAT and ACT in years 2017 and 2018 at about 40-45% each. The statewide particiation is quite balanced between SAT and ACT. Oregon also does not have state-level exit exams for high school.

This makes it a good opportunity to push for SAT as a pathway for Oregon students to better secure their college position.

The College Board could focus on its strengths by convincing the State Education that SAT has more critical thinking required, against the impression of the ACT being a fact-recall test. This strategy has already been proven successful in Colorado, and could apply to Oregon as well.

Cost of exams was raised by some, so initial SAT fees could be reduced to gain market share.

Additional information could be:

1) Economic GDP of each state against the partipation rate, if we think that social-economic factors will affect participation rate.

States with specific SAT prep classes should logically attract more students to take SATs too. This could be investigated further if the data can be obtained.

SAT could also provide SAT prep classes on its own as well, it could even be subsidised, combining addressing of both economic and preparatory concerns via this recommendation.

2) Would like to have more data on similarity of state education systems, to test null hypothesis that there aren't two education system models distinct enough, such that each state's student population tends to perform differently at SAT or ACT based on their training.

If this relationship could be identified, would like to target states where the education system is more suited for students taking SAT. Allocate the marketing budget to those states.



---
