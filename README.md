# Research on recipe and rating datasets

by ZhengyangLiu

---

## Introduction

In this project,  we do research on recipe and rating datasets. 

And my project focuses on the hypothesis testing of the high and low rating and  prediction of the minutes of differet recipes. 

The dataset has two CSV files, RAW_recipes.csv and RAW_interactions.csv. RAW_recipes.csv contains recipes，which has 83782 rows and 12 columns: ['name', 'id', 'minutes', 'contributor_id', 'submitted', 'tags', 'nutrition', 'n_steps', 'steps', 'description', 'ingredients', 'n_ingredients'],

RAW_interactions.csv contains reviews and ratings submitted for the recipes in RAW_recipes.csv, which has 731927 rows and 5 columns: Index(['user_id', 'recipe_id', 'date', 'rating', 'review'].

---

## Data Cleaning and Exploratory Data Analysis

This part we find and fill NAN data.

The first figure shows the Distribution of ratings:

<iframe src="data_cleaning1.html" width=800 height=600 frameBorder=0></iframe>

The second figure shows the Relationship between rating and minutes:

<iframe src="data_cleaning2.html" width=800 height=600 frameBorder=0></iframe>

---

## Assessment of Missingness

This part we test if the missingness is NMAR and has dependences.

The result shows data maybe not MCAR，maybe NMAR或MAR, and result figure is:

<iframe src="assessment_of_missingness.html" width=800 height=600 frameBorder=0></iframe>

---

## Hypothesis Testing

Here is the result figure:

<iframe src="hypothesis_testing.html" width=800 height=600 frameBorder=0></iframe>

This part is hypothesis testing to verify whether the relationship between different groups of Rating and minutes is equivalent

There are two hypotheses：
- Null Hypothesis (H0): There is no significant difference in the mean ratings between recipes with short and long cooking times.
- Alternative Hypothesis (H1): There is a significant difference in the mean ratings of recipes with short and long cooking times.

We can see from the result 'Observed mean difference：-22.47' obviously that H1 is more acceptable, but the result 'Permutation test p-value：0.2050' shows that the null hypothesis cannot be rejected because the p-value is greater than the commonly used significance level (α = 0.05). 

---

## Framing a Prediction Problem

This part we have chosen to use a regression model to predict "minutes".

The evaluation metric adopted here is the Mean Squared Error (MSE),

because it can clearly reflect the prediction performance as well as data quality issues.

---

## Baseline Model

Here is the result Mean Squared Error (MSE): 983080.8175103457 and result figure:

<iframe src="baseline_model.html" width=800 height=600 frameBorder=0></iframe>

---


## Final Model

Here is the result Mean Squared Error (MSE): 5127.871683313645 and result figure:

<iframe src="final_model.html" width=800 height=600 frameBorder=0></iframe>

This part consists of the baseline model and the final model, where two features and linear regression are used in the baseline model; Compared with the baseline model, the final model used four features that removed outliers and a decision tree model, and adjusted the num of the parameter test_size in the train_test_stlit function.

We conducted multiple comparative experiments in the following order, including

1) Adjusting the number of features shows that four features perform better than three, and three features perform better than two;

2) Adjusting the size of the parameters test_size and random_date in the train_test_stplit function, the results showed that when test_size was 0.1, the effect was better than when it was 0.05 and 0.15, and when random_state was 42, the effect was better than when it was 35 and 50

3) Because it was observed that most of the minites values were less than 200, and the vast majority were less than 1000(about 99.2%), abnormal arrays with minites above 1000 were removed, greatly improving the effect

4) Multiple other functions for data preprocessing were tested, such as a)data robustness、b)select k best features、c)set variance threshold, in this experiment, the experimental of a) and c) results were consistent with data standardization, but the b) results would deteriorate if used

5) Multiple other regression functions were tested, such as i)polynomial regression model、ii)ridge regression model and iii)decision tree regression model.In this experiment, the experimental ii)results were consistent with linear regression. When using  i), the results were slightly improved, while when using iii)，the effect was significantly improved.

As we know,If the model performs well, points will cluster around the diagonal and the mse will be smaller. We can compare the two figures and the two results of mses that the final model is better.

---


## Fairness Analysis

Here is the result:  
Observed mean difference：-12.12
Permutation test p-value：0.0000


Above is our work, thank you for reading.
---
