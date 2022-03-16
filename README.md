<a name="BackToTop"></a>


# Predicting_Income

**Contributors: Cameron Stewart, Michael Mazel, Rick Fontenot and Tricia Herrera**

>Does marital status affect income? What is the likelihood that a 32-year-old white married male will make more than $50K a year compared to a 59-year-old black divorced female? An individual's income may be influenced by certain factors, and this study examines those factors individually and collectively to determine whether they do have an effect. Using U.S. Census Data, we predict whether an individual will make more or less than $50K a year in the U.S. in 1994. By using each model’s AUC against the test set, we can determine if one model methodology outperforms another in predicting income. The models will select a cutoff that balances accuracy, sensitivity, and specificity.

A summary of the project is shown below. Find the full report [here](../main/Final%20Report/Final%20Report.pdf).

---

## Table of Contents
- [Exploratory Data Analysis](#P1)
- [Create Simple Classification Model](#P2)
- [Create Complex Classification Models](#P3)
- [Conclusion](#P4)
- [References](#References)

---

<a name="P1"></a>

## Exploratory Data Analysis

This study used data from Barry Becker's 1994 Census database. In the data set, 32,561 observations are included along with 14 attributes. There are 6 continuous variables and 8 categorical attributes in this data set. A copy of the data is available at the [UCI Machine Learning Repository](http://archive.ics.uci.edu/ml).

The team first looked at the missing data. Upon initial examination of the data available, we found that 5.6% observations are missing values for both occupation & workclass and 1.7% are missing native country information. Due to the missing data all being in categorical features, the team decided to replace the missing data with a new category called 'no_response' to detect underlying patterns.

Some categorical variables such as Occupation had small sample sizes in each category. For features with this issue, the team looked to converge the categories based on underlying similarities. For example, the mosaic plot below shows how we converged the many categories in Occupation into a condensed feature called Collar that describes the typical working class of the role:

<img width="900" alt="image" src="https://user-images.githubusercontent.com/37990637/158544943-fbb9a8d3-9ca3-4563-8bb8-6bfb79176ec4.png">

In the [full report](../main/Final%20Report/Final%20Report.pdf), you can see the team's deep dive into the reationships within and between variables to understand the data.

[Back to Top](#BackToTop)

---

<a name="P2"></a>

## Create Simple Classification Model

Our team set out to create a simplified interpretable model to understand the features that explain whether someone makes over $50K in 1994 in the US. To do this, our team created an 80/20 training and test split of the original data. Next, we used the EDA to guide the initial model creation and refined the model using significance testing and AIC. After selecting a model, we verified the assumptions were met and interpreted the selected predictors.

Our final simplified model includes age, education_num, race, sex, captial_gain, capital_loss, hours_per_week, marriage_status, and collar. Summary of estimates and significance for features of simplified logistic regression model:

<img width="900" alt="image" src="https://user-images.githubusercontent.com/37990637/158546526-65a50d11-f1c4-4d05-a1ee-f5c0e0bba9cb.png">

We then verified the assumptions of Logistic Regression were reasonable for this model:
- Observations are independent (Assumed based on data source)
- For interpretation, explanatory variables should have little to no correlation (Verified with variance inflation factor (VIF) analysis)
- Model is sensitive to outliers (Verified by visualizing Cook's D and Leverage)

The team provided the interpetations and confidence intervals in the full report.

Sample Interpretations:
- Collar - the odds of earning over $50K for the White-Collar population is expected to be 125.35% higher than the Blue-Collar population
- Education_num - for every 1-year increase in education, we expect the odds of earning over $50K to increase by 33.71%


[Back to Top](#BackToTop)

---

<a name="P3"></a>

## Create Complex Classification Models



[Back to Top](#BackToTop)

---

<a name="P4"></a>

## Conclusion



[Back to Top](#BackToTop)

---

<a name="References"></a>

## References



##### Technologies:

R Studio

R version 4.1.2

[Back to Top](#BackToTop)
