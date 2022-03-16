<a name="BackToTop"></a>


# Predicting_Income

**Contributors: Cameron Stewart, Michael Mazel, Rick Fontenot, and Tricia Herrera**

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

In the [full report](../main/Final%20Report/Final%20Report.pdf), you can see the team's deep dive into the relationships within and between variables to understand the data.

[Back to Top](#BackToTop)

---

<a name="P2"></a>

## Create Simple Classification Model

Our team set out to create a simplified interpretable model to understand the features that explain whether someone makes over $50K in 1994 in the US. To do this, our team created an 80/20 training and test split of the original data. Next, we used the EDA to guide the initial model creation and refined the model using significance testing and AIC. After selecting a model, we verified the assumptions were met and interpreted the selected predictors.

Our final simplified interpretable logistic regression model includes age, education_num, race, sex, captial_gain, capital_loss, hours_per_week, marriage_status, and collar. The model has an AUC of 0.896. Summary of estimates and significance for features of simplified logistic regression model:

<img width="900" alt="image" src="https://user-images.githubusercontent.com/37990637/158546526-65a50d11-f1c4-4d05-a1ee-f5c0e0bba9cb.png">

We then verified the assumptions of Logistic Regression were reasonable for this model:
- Observations are independent (Assumed based on data source)
- For interpretation, explanatory variables should have little to no correlation (Verified with variance inflation factor (VIF) analysis)
- Model is sensitive to outliers (Verified by visualizing Cook's D and Leverage)

The team provided the interpretations and confidence intervals in the full report.

Sample Interpretations:
- Collar - the odds of earning over $50K for the White-Collar population is expected to be 125.35% higher than the Blue-Collar population
- Education_num - for every 1-year increase in education, we expect the odds of earning over $50K to increase by 33.71%


[Back to Top](#BackToTop)

---

<a name="P3"></a>

## Create Complex Classification Models

A total of three complex models were built to compete against the simplified logistic regression model. Since the focus has shifted to prediction rather than interpretation, a complex logistic regression model, a quadratic discriminant analysis (QDA) model, and a random forest model were developed.

The complex logistic regression model added interaction terms and considered non-linearity of continuous features. The model is detailed in the full report and has an AUC of 0.902.

When deciding between linear discriminant analysis (LDA) vs. quadratic discriminant analysis (QDA), the team stepped through the assumptions:
- The predictors of each response category must follow a multivariate normal distribution (Verified with Shaprio-Wilk Test)
- Constant variance
- Independence
- Identical covariance matrices for LDA
- Each having its own covariance matrix for QDA

To verify our assumption of homogeneity of the covariance matrices, we performed a Box’s M test. The results had a p-value of 2.2e-16, thus we reject the null hypothesis. There is evidence the covariance matrices are not equal across all groups. With this violation, QDA is more appropriate than LDA modeling. The final QDA model had an AUC of 0.825.

Random forest was chosen as an alternative, nonparametric method in predicting income. Unlike regression models, random forest naturally captures polynomial and interaction terms, and thus they need not be included. When inputting variables into a random forest, the only preliminary steps involve transforming categorical types. The model that performed best on our test set was the traditional random forest with quantitative variables and categorical variables handled with caret’s default method. With a mtry of 2, this random forest model produced an AUC of 0.918.

Random forest has the highest AUC, with the complex and simple logistic regression closely behind. The QDA model, having the lowest AUC, then followed. With random forest’s ability to minimize overfitting via ensembling, the model was able to produce the highest AUC and accuracy scores. Random forest also likely benefited from the nonparametric requirement. ROC comparison of all models shown below:

<img width="644" alt="image" src="https://user-images.githubusercontent.com/37990637/158550737-9ce961ea-b205-4000-b1db-928ba9b455a8.png">


[Back to Top](#BackToTop)

---

<a name="P4"></a>

## Conclusion

Due to the data collection methods being performed observationally, rather than experimentally, it should be stressed that all potential relationships identified are correlations not causations. It should also be noted that although the data came from the census, we do not know if the rows provided in the data set are a random sample. As a result, we cannot confidently apply our findings to the entire United States 1994 population. In summary, various models ranging in complexity and interpretability were produced to generate predictions whether this sample of citizens earned more or less than $50k a year.

[Back to Top](#BackToTop)

---

<a name="References"></a>

## References

[UCI Machine Learning Repository](http://archive.ics.uci.edu/ml)

[Full Report](../main/Final%20Report/Final%20Report.pdf)

[EDA and Modeling Analysis](../main/Final_EDA_and_Modeling/EDA_and_modeling.pdf)

[Model Performance Summary](../main/Model%20Performance%20Summary)

##### Technologies:

R Studio

R version 4.1.2

[Back to Top](#BackToTop)
![image](https://user-images.githubusercontent.com/37990637/158562633-5018b17b-6bcb-4c14-91a8-bf4332b964e3.png)
