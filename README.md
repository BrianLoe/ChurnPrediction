# ChurnPrediction
## Overview
This project aims to identify customers who are at risk of churning based on specific demographic and bank account information. To achieve this, various machine learning models are being employed, along with hyperparameter tuning, to enhance the accuracy of the results. The data utilized for this project has been sourced from Kaggle [here](https://www.kaggle.com/datasets/shubhammeshram579/bank-customer-churn-prediction).

## Methodology
1. Business Understanding  
   The banking institution encountered an issue that requires an investigation into a particular customer segment that is more prone to churning. The data that is provided are customer data, including demographic information, bank account details, and historical data on churned customers. This issue was classified as a classification problem, with the objective of categorizing customers based on their likelihood of churning, utilizing past churn data for predictive analytics.

2. EDA Stage  
   The initial step in our data analysis process involves comprehending the data provided, which is formatted in a csv file. Our first task is to conduct a thorough cleaning phase to identify and validate the data. Upon review, we determined that the data was accurate, contained no missing values, and was correctly formatted. As a result, we can proceed to the next phase, which is the data exploration stage.
   
   Exploratory Data Analysis (EDA) is an effective method for gaining insight into the underlying data. Our first step in this stage is to define the features and target variable. The features can be derived from the data columns, while the target variable is the `exited` indicator. We employ statistical tools and techniques to derive and visualize the data, examining variables such as age, estimated salary, credit score, balance, and others. During EDA, we aim to identify any variables or features that are strongly correlated with our target variable, as well as uncover relationships between the features.

3. Modelling Stage  
   In the modelling stage, I have implemented an approach that utilizes actual data/samples obtained and resamples the data to achieve equal classes. It is common for churning customers to have minimum samples in real-world data. However, when building a machine learning model, it is possible that the model may not generalize well to all classes. In other words, the model may be more likely to predict customers who are not churning rather than those who are, creating a bias in our model while still having high accuracy. To address this issue, I used resampling techniques and ensemble models in addition to tuning hyperparameters. Ensemble models are particularly effective in handling imbalanced data and can benefit from learning from errors. Through hyperparameter tuning, class weights can be adjusted to further optimize the model's performance.

   I have implemented four distinct models for the purpose of comparison and evaluation. These models include logistic regression (as the base model), decision trees, random forest, and gradient boosting. Each of these models utilizes different algorithms, and my objective was to determine which algorithm is most effective in predicting churning customers based on this data. To achieve this, I employed grid search and cross-validation techniques to identify the best parameters for each model. Additionally, I utilized recursive feature elimination and cross-validation to determine the optimal number of features to be used in our best model. Finally, I analyzed feature importances to identify the variables that contribute most significantly to churn, whether positively or negatively. Furthermore, in the resampling method, I used 2 techniques, resampling using Pandas and SMOTE library. The model is built upon the best model evaluated and it is evaluated similarly when using actual data.

4. Evaluation Stage  
   In order to assess the performance of the model, the receiver operating characteristic (ROC) and area under the curve (AUC) score metric are used. The ROC AUC score is particularly useful when dealing with imbalanced classes, as it measures the model's ability to distinguish between binary classes. A higher score closer to one indicates that the model is able to make accurate distinctions, while a score of 0.5 suggests that the model's predictions are no better than random guessing. Additionally, accuracy and confusion matrix were employed to provide a visual representation of the overall and individual class performance, respectively. Accuracy was used to compare the model's performance on both the training and test sets, with the aim of determining whether or not the model was overfitting.

## Key Insights
- Approximately 20% of the dataset comprises customers who have churned.
- Despite representing the minority in terms of customer count, nearly 50% of the customer base from Germany has churned in the past.
- Gender-wise, there is a slight inclination towards female customers that demonstrate a higher probability of churn.
- Customers having a single product with the bank displayed an elevated probability to churn.
- Inactive membership status is significantly associated with an increased probability of churn.
- Remarkably, customers who have registered complaints showcase an overwhelmingly high churn rate, nearing 100%.
- Notably, customers with higher account balances demonstrate an increased probability of churn.

## Best Model Performance
The best model evaluated is Gradient Boosting model. This model were able to highly distinguish classes. Here are the score metrics:

<div align="center"><img src="https://github.com/BrianLoe/ChurnPrediction/assets/58500773/b60be637-1be6-4835-886c-d9bc9f39c7f4" width=700></div>

Interpretations:
- Model obtained the best ROC score of 86.8% which means the model is great at distinguishing churning customers.
- Slight ovefit accuracy score. Although the test score is slightly lower (difference of ~1%), it was supported by ROC score.
- Ensemble methods are prone to overfitting. It is important to tune ensemble models correctly.

Model performance comparison:

<div align="center"><img src="https://github.com/BrianLoe/ChurnPrediction/assets/58500773/ce4bd24d-1177-4da6-b79f-2791c733855f" width=600></div>
<br>
<div align="center"><img src="https://github.com/BrianLoe/ChurnPrediction/assets/58500773/a6e05898-f396-41d2-bcfd-d5e64a50d827" width=600></div>

Interpretations:
- Accuracy and ROC score were higher when trained on ensemble models.
- Scores improvement were seen from our logistic regression base model.
- Decision Trees have the lowest scores.

## RFECV Evaluation

<div align="center"><img src="https://github.com/BrianLoe/ChurnPrediction/assets/58500773/3af38853-8623-46e7-96c4-c2449ae50e7c" width=600></div>

<i>The red point indicates the optimal number of features while the blue filled color point indicates the highest ROC score obtained when using n features</i>  

From the graph, we can see that after 5 features, the ROC score is not increasing. The optimal number of features to be used is 5 features while highest ROC score that was obtained was when using 18 features. The total number of features are 22 features. The five most important features discovered by the best model are:
- Age - Customers in the 40s age group is most prone to churning.
- Number of products - Lower number of products is most prone to churning.
- Member status - Inactive member is most prone to churning.
- Customers' residency - German residents are more likely to churn.
- Balance = Higher balance are more likely to churn.

The two most important features are Age and Number of products.

## Conclusion

In conclusion, churning customers are mainly segmented around complains lodged. Customers that have lodged a complain are highly likely to churn. Other drivers include customers' age and number of products with the bank. It was found that customer in the age group of 40s are more likely to churn. Meanwhile, customers that has only one product are also more likely to churn.
