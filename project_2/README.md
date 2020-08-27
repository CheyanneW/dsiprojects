# Project 2 - Ames Housing Data and Kaggle Challenge

## 1. Problem Statement

Our real estate consulting firm in Ames, Iowa specialises in helping clients to conduct house inspections before closing a sale transaction and provide valuable insights and feedback to our clients on the true value of the properties that they are interested in. We aim to develop a good linear regression model based on various external and internal features of a property to estimate its true value. The model will be built using past sales transaction data and we will evaluate our model using RMSE and R2 evaluation metrics. This valuable information will provide useful insights to our clients in helping them to make a decision on which property to purchase.

## 2. Executive Summary

In this project, we will be looking at the Ames housing data set (train.csv) and analyse the various features and their relationship to the sale prices of each property. We are going to first clean up the data and do an analysis on the distribution of each features, and based on these statistics, we will shortlist 49 features for our model.

We started off with building a model that only includes the key features from Size to get a gauge of the model performance. This starts off as the base of our model. We then built a second test model with all the 49 selected features, and as expected, we obtained a very poor R2 score and clearly, the model is overfitting. We then applied Ridge regression and Lasso regression on the second test models to see how the features actually affect the sale prices. Lasso was very useful in this case since we have an overwhelming number of features, it helped to eliminate some of the features that are not as significant. From there, we modified and reselected some of the other features based on prior experience and eventually arrived at Test Model 7 that we used to predict sale prices for our test data. We have decided to use Ridge regression for our final selected model as we do not want to elminate any more features but intead to decrease the variance of our model so as to minimise any overfitting. Test Model 7 gave a relatively good RMSE value as well as higher consistency in its R2 scores before train and test data.

Contents:
3. Data Import & Cleaning
4. Exploratory Data Analysis
5. Linear Regression Model & Evaluation
6. Prediction using test data set
7. Key Observations and Conclusions

## 3. Data Import & Cleaning

The train data list contains information for 2051 properties, each with 81 descriptive features including the sale price of each property. The descriptive features come in both numerical values as well as classes as object data type. The data set seems to contain many null values across various categories/festures that we need to deal with later.

Since there are 113 properties with garage area which is zero, 113 out of 114 null values from Garage Yr Blt, Garage Finish, Garage Qual and Garage Cond comes about because there is no garage, 'NA' is missing data from these features. We can fill the null values of Garage Finish, Garage Qual and Garage Cond to be 'NA', and tentatively set null values of Garage Yr Blt to be 0. However, we have to locate the property that has a garage but missing values for various fields.

The year in which the garage was built must be in the same year the property was built or later. Many of the garage built was in the same year that property was built. With limited information, we will assume that year garage was built for 1712 to be the same year that property was built.

There are 54 properties with no basement. 'NA' is a missing class for Bsmt Qual, Bsmt Cond, Bsmt Exposure, BsmtFin Type 1 and BsmtFin Type 2. We can fill in NA as missing value for the above features for the 54 properties with no basement.

In total, 28 rows and 2 columns were dropped. We have removed about 1.4% of the original data from the train data set.

For the test data set, there are 879 data rows and 80 features related to the properties. The column 'SalePrice' is missing as this is what we need to estimate using our linear regression model. We will clean the test data in a way similar to the train data by first dropping 2 unwanted columns with too many incomplete data and then fill in the missing null values for the other columns.

## 4. Exploratory Data Analysis

For data exploratory, we will break down the columns into different group and look at them one by one as there are too many features. Traditionally, size and land features have significant impact on sale prices. We will look at features from these two groups separately. As there are many features that are categorial in nature, we will look at the ordinal and nominal features next, followed by the rest of numerical data.

The frequency distribution of the sale prices is slightly skewed right with mean of 180,762.60. It has a standard deviation of 79,109 and median of 161,000. From the frequency distribution, we can see that majority of the sale price of properties are within the IQR. There are also a small percentage of properties with very high values, thus pulling the mean prices to be higher than the median.

Gr Liv Area, Mas Vnr Area, Total Bsmt SF, 1st Flr SF and Garage Area have a positive correlation greater than 0.5. However, Total Bsmt SF and 1st Flr SF are also highly correlated with a value of 0.79, we will exclude 1st Flr SF in our model.
We will build our linear regression model using these features: Gr Liv Area, Mas Vnr Area, Total Bsmt SF and Garage Area.

Land: MS SubClass, MS Zoning, Street, Land Contour, Lot Config, Neighborhood, Condition 1, Condition 2, Bldg Type, House Style
The 10 features above are all nominal data and we will use one-hot encoding to transform them to numerical data.
Looking at the breakdown of various land features, we will do an initial selection of features that might affect sale price significantly based on their median sale pricing as well as number of outliers. If a certain feature class has a median that is not close to the mean sale price, and it does not have too many outliers, we make an initial assumption that this particular feature class will impact the estimated sale price.

There are a total of 23 features that are ordinal in nature. We will investigate the impact of each class of the features and select those that appears to be more significant. We will then apply ordinal encoding or one-hot encoding to these features for our linear regression model.

Features selected based on its distribution of prices in a particular class against the mean:

|Feature|Remarks|
|---|---|
|Overall Qual|keep as ordinal values|
|Exter Qual|Use ordinal encoding|
|Exter Cond (Fa, Po)|One-hot encoding|
|Bsmt Qual (Ex)|One-hot encoding|
|Bsmt Exposure (Gd, NO)| One-hot encoding|
|Heating QC (Fa, Po)|One-hot encoding|
|Electrical (FuseF, FuseP) | One-hot encoding|
|Kitchen Qual |Use ordinal encoding|
|Functional (Sev, Sal, Maj2)| one-hot encoding|
|Fireplace Qu(Ex) | One-hot encoding|
|Pool QC (Fa, Gd) | One-hot encoding|

'Year Built','Full Bath','TotRms AbvGrd','Fireplaces' and 'Garage Cars' are chosen as they have the highest correlation with sale prices compared to other numerical features.

## 5. Linear Regression Model & Evaluation

In total, we have initially shortlist 9 continuous features as well as 40 categorial features for building our linear regression model. We have test using 7 different models.

|Model|R2 mean|	RMSE	|train R2|	test R2|
|---|---|---|---|---|
|Model 1|	0.78246|	36064.40536|	0.79228	|0.81354|
|Model 2|	-2.38E+24|	26466.31301	|0.88945|	0.86693|
|Model 3|	0.87657	|27336.86493|	0.88859|	0.87321|
|Model 4|	0.87912|	27065.39498|	0.88711|	0.87342|
|Model 5|	0.89618|25243.09539	|0.90105|	0.88276|
|Model 6|	0.89282|	25981.87113|	0.90241|	0.89081|
|Model 7|	0.87879|	27124.30376|	0.88570|	0.88014|

Model 5 and Model 6 has very high R2 value and a low RMSE, which made them seems like better models. However, when we do a scoring on the train and unseen test data, there seems to be overfitting in both cases. With Model 7, the train and test scores are more consistent and would be a better model choice. We will use Test Model 6 and 7 to predict values of our test set property sale prices to see if our observation is right.

From the plot of coefficients above, the top five features are Gr Liv Area, Total Bsmt SF, Overall Qual, Bsmt Qual_Ex as well as Kitchen Qual Sq. Other features that are performing relatively well to predict sale prices will be Exter Qual Sq, Fireplaces, Year Built and Garage Area.

As we can see from the scatter plot of actual sale price VS predicted sale prices, the model can generally predicted the sale price with a RMSE of $27124. However, properties with high sale prices have very large residuals, meaning that the predicted sale price of these properties tend to be below the actual value and the model is not good in predicting high value houses.


## 6. Prediction using test data set

As expected, sale prices that is predicted using Test model 7 gave better scoring as compared to Test Model 6. For Test Model 6, we have a public score of 141554 which is much higher than sol_3 Kaggle score which is 32765. We will select Test Model 7 as our prediction base.


## 7. Key Observations and Conclusions

#### Key Observations:

We have seen many features having a positive correlation relationship, indicating that many features multicollinear in nature. When doing features selection, we need to keep this in mind so that we will not overfit our model.

For this project, in the initial stage, I have separated out Size and Land features separately. It is found that some of the size features have the highest significance in affecting the prediction of sale prices. For the other features, we look at three different groups of data - ordinal, nominal and numerical features.

We started off with building a model that only includes the key features from Size to get a gauge of the model performance. This starts off as the base of our model. We then built a second test model with all the 49 selected features, and as expected, we obtained a very poor R2 score and clearly, the model is overfitting. We then applied Ridge regression and Lasso regression on the second test models to see how the features actually affect the sale prices. Lasso was very useful in this case since we have an overwhelming number of features, it helped to eliminate some of the features that are not as significant. From there, we modified and reselected some of the other features based on prior experience and eventually arrived at Test Model 7 that we used to predict sale prices for our test data. We have decided to use Ridge regression for our final selected model as we do not want to elminate any more features but intead to decrease the variance of our model so as to minimise any overfitting. Test Model 7 gave a relatively good RMSE value as well as higher consistency in its R2 scores before train and test data.

#### Conclusion:

Our clients often come to our consultation team with a list of properties that they are interested in. Our team will then collect data on these properties and provide a thorough analysis on important features and also give an estimate of their sale prices. Using Test Model 7's coefficent table, we have quickly identified five main features: Gr Liv Area, Total Bsmt SF, Overall Qual, Bsmt Qual_Ex as well as Kitchen Qual Sq. A glance at these features will provide us with an initial estimate on the range of expected sale prices to manage clients expectations.

We will then perform an estimate of the sale prices using our regression model, and compare our estimated pricing with the actual asking prices from the property owners. With these information, we can then advise our clients on the perceived property values and which of the selected properties are worth the asking sale prices, and which ones are overpriced or underpriced.

#### To improve on the model...

There are steps that we can take to create a better model. We will continue to explore and improve our linear regression model from here.

1. By taking the log of Sale Price, it is found that the frequency distribution follows the shape of a normal curve, which mean 95% of our data will fall within 2-sigma from the mean of log of sale prices. We can model our linear regression using the log of sale prices instead as our current model does not fit the properties with high value very well. Alternatively, we can also remove these properties with high values before building our linear regression model. By removing these outliers, we can get a better regression fit between our features and sale prices for the rest of the properties.

2. For our current model, we have used ordinal values for selected features and for some features, we have chosen to use one-hot encoding. We can use ordinal values for more features such as Neighbourhood, by grouping neighborhoods with higher mean prices together and giving them a higher ranking, than the properties with lower mean prices across the group. This is because for each dummies feature created from Neighborhood, each dummy feature has a very small sample size and using ordinal values for features which combines a few classes together might be a better idea. Similar for other features like Functional and Exter Cond, and some of others with very small sample classes can change to ordinal assignment.

3. As there were quite a large number of missing data, we need to form our data collection team and collect better data so as to reduce bias and variance of our linear regression model. They will also be doing inspections with our clients and verifying new property data so ensure that the information is accurate.

4. For each test model, we can run all 4 regularization techniques to compare their performance, namely, Ridge regression, Lasso regression, eNet regression as well as RFE. We can continuous refine our data and create more test models and obtain better performaning model as time changes.

5. There are other external factors that we have not explored, like economical factors (financial crisis), natural disasters prone areas, population density and community demographics etc.


