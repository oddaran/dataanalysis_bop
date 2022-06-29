# dataanalysis_bop
The main objective is to discover the industry segments trending higher in Loss Ratios. From the data, propose a hypothesis why, and recommend a solution for it. Investigating the data will consider the overall story and propose changes or solutions.

# Background of property/casualty insurance
An insurance company's loss ratio shows the relationship between incurred losses and earned premiums. Insurance companies with very high loss ratios may need to raise premiums to stay solvent and ensure their ability to pay future claims. A very low loss ratio means that consumers are paying too much for the benefit received. A higher loss ratio means lower profits for the insurance company and is, therefore, a problem for underwriters and investors alike. Underwriters and investors use the loss ratio for various purposes. IL/EP *100 = Loss Ratio %.

High LRs risk being unable to meet future liability payments. Underwriters are particularly interested in the loss ratio. When the claims loss ratio is too high, either the premiums must rise or certain insured groups must be denied coverage. In the insurance industry, this is referred to as a hardening of the market. Investors are also interested in the loss ratio. They may use the combined loss ratio (both losses and expenses) as one of many metrics to compare insurance companies for investment decisions.

What services do casualty/property commercial lines cover?

Property ● Casualty ● Errors & Omissions ● Management Liability ● Cyber Liability
Loss Control ● Workers’ Compensation ● Reps & Warranties Insurance 
● Aviation ● Crime ● International Risk Management ● Surety & Bonding
Business Continuity Planning ● Captives ● Environmental Liability

# Objective
Divide project into five parts; they are:
1. Define the problem.
2. Design test, discover associations.
    -explore numeric data
    -explore categorical data
3. Test models from evaluation.
4. Summarize model findings.
5. Make recommendations.

# 1. Define Problem
1. What are the inputs and outputs for a forecast?
Time series (months 2019-2022), both structured (continuous numeric, categorical renewal, policy lines, region/region code), and partially unstructured data (years in business). Forecasting a time series may yield tremendous commercial value. Consider LR for multivariate time series forecasting.
2. Are you working on a regression or classification predictive modeling problem?
Regression & Descriptive Models.
3. Are you working on a univariate or multivariate time series problem?
Multivariate.
4. Do you require a single-step or a multi-step forecast?
Multi-step to compare against numeric variables, then 
5. Do you require a static or a dynamically updated model?
Static for purposes of project.

# 2. Design Test Modalities and find associations.

1. Summarize dataset and describe characteristics.
2. Discover any correlations w/numerical and categorical data.
3. Formulate test model

# 2.1 Summarize dataset for predictors.

Estimator/predictors. There are 3 properties to define a good predictor: unbiased, consistent, and efficient. The estimator is unbiased, when the expected value of the sample parameter is equal to the population parameter. If the variance of the sample parameter decreases with the increasing sample size, the estimator is consistent. Given the same sample, the estimator with lower variance is more efficient.

Numeric variables. Do the numeric explanatory variables affect the response variable? Linear regression is a good model to consider. Note Gauss-Markov assumptions are strict for time series, in regards to OLS you should have 1) linearity where it assumes B (slope) is linear, 2) no perfect collinearity that X produce complete random results, 3) endogenous relationship of X where residuals don't change with X, 4) no autocorrelation from random X and Y variables, 5) homoscedasticity for residual terms where variance doesn't change with X.

The coefficient of determination (R squared) describes the overall relationship between the independent variables X (deductibles, policies in force, earned premium) and the dependent variable Y (loss ratio). The regression coefficient (b) determines the overall positive/negative relationship. We need to find which variables can best explain the dependent variable. Our inference on the data parameters using hypothesis testing is:

H0. There is no significant relationship between the independent predictor (X1, X2, X3...) and dependent variable (Y); b=0 (a=0.05)
HA. There is a significant relationship between the independent predictor (X1, X2, X3...) and dependent variable (Y); b /=0.

We set the significance level as a=0.05. As long as the probability of the observation is higher than 5%, we do not reject the null hypothesis. Anything under this will be statistically significant to reject the null.

We normalize the data. Normalization can be useful, and even required in some machine learning algorithms when your TS data has input values with differing scales. It may be required for algorithms, like k-Nearest neighbors, and Linear Regression. Use normalization when you don’t know the distribution of your data or you know it is not Gaussian. 

# 2.2 Discover any correlations

Per Pearson correlation coefficient, the best linear relationship between 2 variables takes on -1 or 1, where 0 indicates no linear correlation. After performing the correlation plot, incurred loss sits close to 1. All other variables are very close to 0, thus no correlation. After we run the attribute corr to the loss ratio, we find that that incurred loss is very positively correlated to loss ratio (0.89), and may be used as a predictor.

# 2.3 Formulate test model.

In LR we basically find which line best represents variable y from variable (X1,X2,X3...). It is quantified by the ordinary least squares, which chooses the regression line that minimizes the sum of squares of differences b/t independent to predicted variable.

# 3 Test the models from evaluation.
1. Split the dataset into a train and test set.
2. Fit a candidate approach on the training dataset.
3. Make predictions on the test set directly.
4. Calculate a metric that compares the predictions to the expected values.

# 3.1 Split the dataset into a train and test set.

Partition sample and training data, to avoid overfitting. Not training dataset leads to a model that has “overfit”, i.e. it has memorized the data and cannot generalize its “learnings” to unseen data points.

In forecasting time series, we assume that the trend to be analyzed is either linear or exponential over time.  This assumption can induce a model that is overly robust, and even wrong if the time series changes over time (i.e., a harsh winter causing power grid blackout)

# 3.2 Model and run Linear Regression

# 3.3 Compare modeled to actual values

After linear regression, we can infer the quality of the linear regression. Checking the residual terms (error terms of independent variables) can ensure autocorrelation is not violated. We evaluate TS regression forecast with MAE and MAPE (Mean Absolute Percentage Error). MAPE tells you how wrong your forecasts are percentage-wise.

# 3.4 Find associations between categorical and target variable.

We are interested in how categorical independent variables (industry segment) relates to a normally distributed continuous (interval or ratio level) dependent variable. We want to see how the loss ratio changes per industry, and to what extent?

We apply .groupby() method and pass it in a column, to split the data into relevant groups, based on the criteria passed in. The reason for applying this method is to break a big data analysis problem into manageable parts. Then we can perform operations on the individual parts and put them back together. While the apply and combine steps occur separately, Pandas abstracts this and makes it appear as though it was a single step.

Run new dataframes where we involve several manipulations of the industry column, to create pivot table that can find the sums of loss ratios per each industry. This provides enough granular level of detail for drawing conclusions.

# 4. Summarize Model

We explored data from a time series of numerical and categorical variables of commercial insurance data, from mid-2019 to mid-2022. Our target variable loss ratio, a percentage of incurred loss to earned premium. In this data, several numeric variables were found to vary in scales and type. We normalized to this data and then calculated linear regression from trained data, relating independent variables, discovering a high correlation between loss incurred and loss ratio.

We also looked at categorical industry segment, and upon modeling time series and plots, discovered an overall downtrend in loss ratios over time. As the majority of segments are under 70%, this implies healthy profitability. Especially apparent was a very recent uptrend in loss ratio for the warehouse segment.

# 5. Make recommendations.

These recommendations are included in the .html document attached. -Daran Thach

References

(2021 Nov). Normalize a Pandas Column or Dataframe (w/ Pandas or sklearn). https://datagy.io/pandas-normalize-column/

(2021 Dec). Pandas groupby: group, summarize, and aggregate data in python. https://datagy.io/pandas-groupby

Brownlee, J. (2016 Dec 12). How to normalize and standardize time series data in python. https://machinelearningmastery.com/normalize-standardize-time-series-data-python/

Brydon, M. (2019). Multiple linear regression. San Francisco University. https://www.sfu.ca/~mjbrydon/tutorials/BAinPy/10_multiple_regression.html

Financetrain. (nd). Multivariate linear regression in python with scikit learn library. https://financetrain.com/multivariate-linear-regression-in-python-with-scikit-learn-library

U.S. Bureau of Economic Analysis. (2022 Jun 29). Personal Consumption Expenditures: Chain-type Price Index [PCEPI. https://fred.stlouisfed.org/series/PCEPI

Polikoff, C. (2022 May 16). Rates continue to decelerate in many areas Q1 2022 commercial market update. https://woodruffsawyer.com/property-casualty/commercial-insurance-quarterly-market-update/

Wang, J. (2020 Apr 7). How to model time series data with linear regression. https://towardsdatascience.com/how-to-model-time-series-data-with-linear-regression-cd94d1d901c0
