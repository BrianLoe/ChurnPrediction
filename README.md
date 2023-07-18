# ChurnPrediction
## Overview
This is a project to determine which customers with certain features are likely to churn. The features are determined by demographics and customers' bank account information. I am using several machine learning models to improve the accuracy performance as well as hyperparameter tuning. The data from this project are obtained from Kaggle [here](https://www.kaggle.com/datasets/shubhammeshram579/bank-customer-churn-prediction).

## Methodology
1. Business Understanding  
   The bank institution were facing a problem where they wanted us to investigate a specific segment of which customers are more likely to churn. We were given the data about customers information including demographics, bank account information, and historical data where customers have churned. We classified this problem as a classification problem. The goal is to classify customers based on churn since we have data about churning customers in the past. We want to utilise this to do a predictive analytics.

2. EDA Stage  
   First stage is always to understand the data that was given. We were given a data that is formatted in csv file. First is to conduct a cleaning phase to identify and validate the data. The data that was given did not include any missing values, incorrect formatting, and the data was accurate. So we can proceed to the next phase which is the data exploration stage.  
   EDA is a great way to understand the underlying data. We first define what is the features and target variable. The features can include anything from the data columns and the target will be the exited indicator. We used statistical tools and techniques to derive and visualise the data. We look at the distribution of variables such as age, estimated salary, credit score, balance, etc. In EDA, we usually want to find out whether there are any variables or features that is strongly correlated to our target variable. We also want to discover relationships between the features.

3. Modelling Stage
   The approach that I have implemented in the modelling stage is to use the actual data/samples that we have obtained and resampling the data to have equal classes. Equal classes in this data means that its normal to have minimum samples on churning customers. However, in terms of when building a machine learning model, it is possible that the model will not generalise well to all classes. In a simple way, it means that the model will more likely to predict customers not churning rather than churning. This also create a bias in our model. This can possibly be avoided by using resampling techniques or using ensemble model. Ensemble model is a great model to handle imbalanced data. Through hyperparameter tuning, we can tune the class weights. Moreover, ensemble modelling can benefit from learning from errors.

   I implemented 4 models to be compared and evaluated. The 4 models are logistic regression (base model), decision trees, random forest, and gradient boosting. Each of this model perform and utilise different algorithms. I wanted to experiment on which algorithm is the best to predict churning customers. Combined with grid search and cross valdiation, it will find the best parameters for each model. Furthermore, recursive feature elimination and cross validation is used to find out the optimal number of features to be used in our best model. Finally, feature importance is also a great indicator of which variables contribute the most to churn whether positively or negatively.

   In the resampling method, I used 2 techniques, resampling using Pandas and SMOTE library. The model is built upon the best model evaluated and it is evaluated similarly when using actual data.

4. Evaluation Stage
   To evaluate the model performance, I used receiver operating characteristic (ROC) and area under the curve (AUC) score metric. ROC AUC score is a great evaluation metric when dealing with imbalanced dataset. It measures the model ability to distinguish binary classes. Higher score closer to one means that the model is able to distinguish it well. While a score of 0.5 means that the model prediction behave the same way as random guessing. In addition, accuracy and confusion matrix is used to visualise the overall performance and individual class performance respectively. Accuracy is used to compare model on training and test set. The objective is to see if the model is overfitting or not.

## Key Insights
- The total customers that have churned is ~20% of the data.
- Customers from Germany are more likely to churn despite having the lowest number of customers almost 50% have churned in the past.
- Female customers are slighty likely to churn.
- Customers who have 1 product with the bank are more likely to churn.
- Inactive members are more likely to churn.
- Customers who had lodged a complain are strongly more likely to churn with almost 100% rate.
- Customers that have higher balance are more likely to churn.

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
