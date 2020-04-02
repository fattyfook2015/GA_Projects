

### Overview



# Project 2: Project 2 - Ames Housing Data and Kaggle Challenge
-Submitted by Joey Chew 28 Feb 2020

### Context and Problem Statement

Task given to create a Regression Model based on Ames Housing Data, to predict price of a house at point of sale as a function of its predictor variables. These predictor variables are housing attributes such as Lot Size, Size of Garage.

We are also to take part in a Kaggle challenge with our submitted Regression Model, based on unseen data, which is found in test.csv. train-test splits, cross validation are methods to be demonstrated as part of the competition and thus, within our model as well. For Kaggle, the lower the score would be better, indicative of less residuals.

Beyond the academic exercise, as the data is based on real-world information, it could be developed to assist in house purchases, or for an owner wanting to sell, to price appropriately.

---

## Executive Summary

### Contents:

- [Rough Data Cleaning and EDA](#Rough Data Cleaning and EDA)
- [Preprocessing and Modeling](#Preprocessing and Modeling)
- [Conclusion and Recommendations](#Conclusion and Recommendations)
- [Outside-Research](#Outside-Research)


---

### Rough Data Cleaning and EDA

Due to the sheer volume of data at hand, prioritisation was necessary. My first steps were to do rough data cleaning, display correlation, and distribution of data, before zooming in on meaningful variables to explore further.

Quick visuals were plotted, together with value_counts, null counts and frequency of bins were considered for predictor variable shortlisting.

Joint distribution and correlation graphs were plotted for each predictor.

For nominal predictor variables, heatmaps were also examined for their Pearson's coefficient to gauge their significance.

A check_corr function, together with other support functions, was written to faciliate this.

It was noted that the check_corr for non numericals didn't seem that meaningful, due to no scaling, and even for 
dummy variables treatment, the resultant values of 1 and 0 are too steep a divide for a range as diverse as price.

Dummy variables and one-hot encoding was still done, to explore any correlations.

Logically, expensive items such as a basement may add a fixed constant min price to the house.
More meaningful to explore only true ordinal categories with scaling factored in.

Due to repetitive rationale for not picking variables as predictors and the sheer number of columns, descriptions given for about 40-50 of the variables.

Variables chosen as predictors will be described again in a separate file called finalised_predictor_variables.

Some outliers found such as 'Garage Built' in 2207 were crossed-checked against the website link provided as part of the project, and corrected.

A mix of methods were also used to clean missing values. Some missing values were actually 0 or related well to being 0 in their scale, so straightforward substitution was done.

Others were ordinal values which nesitated taking a median value. eg. almost all houses had a garage, and we needed a quality of garage value. by dropping those rows, we might lose too much data. but by comparing the effect of keeping the rows not having much change on correlation, it was deemed as fine to impute it a mean, as the risk of introducing bias would be limited.

Another example would be swimming pools, only 9 out of 2051 houses had them, weighing them equally would skew the results habving the minority affect the vast majority. It would weaken the model's ability to generalise.

Nominal categories that had missing data were considered for dropping, after dummying them. the act of dummying allows the dummy categories with high correlation to stand out, and be focused on instead.

Simple mean was also used in calculating a simple ratio between SalePrice and Lot Frontage to fill in missing figures.


---

### Preprocessing and Modeling

Linear Regression, Ridge Regression, Lasso Regression and ElasticNet Regression were tested for the model. The sum of mean squares, or the R^2 value was the criteria used for judging how well the model fit with the data. The higher the R^2 the better.

By keeping the train.csv and test.csv separate from the start, the test.csv served as a holdout dataset.

The train.csv data was then KFolded, and cross valued at k=10.

Pipeline was used to combine both StandardScaling and KFold smoothly in one step, for scaling to synchronise with the KFold testing.

After determining their optimal hyperparameters, it was found that Lasso Regression had the best results (ElasticNet provided coefficients of alpha and l1 that transformed it into a Lasso as well).

With more computing power and time, a Grid Search could be performed too, to widen the range of parameters, and improve the fit of the model.

Feature Engineeering was done to combine certain attributes that made sense, such as adding 1st Flr SF to 2nd FLr SF, to form a Total Flr SF. It was not surprising that this was one of the stronger predictors which the model flagged out.

Note that while Lasso's coefficients seemed well ordered, and focused amongst only a few variables, Ridge's coefficients varied wildly from large numbers like 17000 to -6000. It is good that Ridge is able to consider so many variables, but the uninutitive relationship also gives doubt to its abilty to generalise.



### Conclusion and Recommendations

Some interesting insights were that Neighborhood_NoRidge seems a good neighborhood to invest in, as Ridge predicts its to be overwhemingly tied to SalePrice with a coefficient of 17000!

Poor Basment Condition stood out as a strong negative correlation to price, with a Ridge coefficient of -6000.

Both models didnt seem to have any common strong predictor variables, and this is yet another reminder, that mathematical models are just that, often domain knowledge has to be paired in order to intuit meaningful information from built models.

The models were able to achieve a R^2 or sum of mean squares value of 0.80. This is a good score, and suggests that it will generalise well. Unfortunately, as holdout data actual values are not available, the actual R^2 cannot be determined.

The Lasso model's coefficients showed strong emphasis on continuous predictors. It was consistent with expectation that age of house would impact greatly; its coefficient was 475, amost 5 times, that of the second predictor, garage area.

The feature engineered variable, total sq ft was third on the list, suggesting that it was a good choice.

Some other selected nominal or ordinal variables with relatively high direct individual correlation with SalePrice, such as Neighborhood_NoRidge with a 0.45 correlation, had eventual impact of almost 0 coefficient as part of the target variable function.

This is also inline with the expectation that discrete scale is generally too steep a jump in range to compare well against a continuous range of the target SalePrice. Even if there is general correlation, multiple high and low values sharing the same predictor value, would skew the modelling.

As for relative performance of the model, Kaggle graded the submission with a score of 38k for my lasso model, and 31k for my ridge model which compares favourably with the average, as 38k would place me 75th or so on the ladder, and 31k within the top 50.

This suggests an above average fit.

However, as mentioned previously, Ridge's high variance in coefficient values across a wide number of variables, suggests an overfit, where alhough the residuals for this particular set of holdout data is good, it may not generalise as well as Lasso.

This fulfills the suggestion that the better Kaggle scoring model may not be the more useful model after all!

For improving future accuracy:

Again, more data would assist in the modeling, not just in terms of reproducibility of the score, but variables with more significant impact, such as price of nearest neighbours's homes, ala KNN would be a good alternative to linear regression models, as we all know that property is often more about location than its own attributes.





### Outside-Research



(Source: A Localized Model for Residential Property Valuation: Nearest Neighbor with Attribute Differences
by Simon K.C. Cheung
Department of Statistics, Room 119, Lady Shaw Building, The Chinese University of Hong Kong, Shatin, N.T., Hong Kong SAR, China. Phone: 852- 27686811. Email: simoncheungkc@gmail.com)
(https://www.um.edu.mo/fba/irer/papers/forthcoming/IR150115RR%20Localized%20Model%20for%20Residential%20Property%20Valuation.pdf)

The paper talks about a hybrid model between nearest neighbours and house attributes. That would be the natural upgrade to the linear regression models used for this project.




---
