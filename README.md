# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**This dataset contains bank marketing campaign for potential target customer.The target column is the deposit column (Y/N)**

**The solution is to run classification ML model using LogisticRegression with HyperDrive and AutoML and compare the result**

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

HyperDrive pipeline was based on prescribed Scikit-learn Logistic Regression classifier. LogisticRegression generates a function called logit which ranges between 0 and 1. The Arewa Under the curve with max area is the best threhold which maximum accuracy. Hence suitable for binary classifiaction problems.

DataSet has 32,950 rows. Its was split at 80/20 for taining and test set. 2 fold crossvalidation is performed for better accuracy.

hyperparameter tuned are C: Inverse of regularization strength and max_iter: Maximum number of iterations.

We used HyperDrive to run multiple simulation automatically and selecting the best model. This is a trial and error method to find the best fit by running all combination in case of GridSampling or running certain parameters randomly in case of random sampling.. 

In order to define sample space for hyperparameter tuning we used RandomParameterSampling class. In this sampling algorithm, parameter values are chosen from a set of discrete values or a distribution over a continuous range.

**What are the benefits of the parameter sampler you chose?**
Parameter sampler has 3 options , Grid, Random and Bayesian.Bayesian sampling build a probability model of the objective function and use it to select the most promising hyperparameters to evaluate in the true objective function. RandomSampling is faster and usullay always yield similar accuracy compared to GridSampling.

**What are the benefits of the early stopping policy you chose?**
Early stooping in general in machine learning stops the training when a certain accuracy is acieved or the accuracy gain is minimal for eachconsecutive epoch or if it runs for long time which might be an indication of Gradient Decent overshooting insteam of convering This can happen when the learning rate is large.

I used Bandit policy that defines early termination based on slack criteria and frequency and delay interval for evaluation.

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

AutoML pipeline evaluated multiple classifier and was also able to do feature engineering on the raw dataset as well. These range from simple classifiers such as Logistic Regression and Random forest to complex ensemble classifiers such XGBoostClassiers, GradientBoosting etc. It was able to tune across a large no of hyperparameter (10 main for best classifier)

The model selected was VotingEnsemble.

![image](https://user-images.githubusercontent.com/19474037/131574189-13310373-1f0b-4b73-824a-fcc1a4b4889a.png)


## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**
Logistic Regression model with 90.75% Accuracy

Azure AutoML: VotingEnsemble classifier with 91.43 % Accuracy. 

Hence, the best pipeline was Azure AutoML and best model was VotingEnsemble classifier with 91.43 % Accuracy.

AutoMl runs a gamut of classifiers and does incredible number crunching when it comes to HyperParameter tuning. Its possible to manually do that in the code but its would take days if not weeks. Hence we can get a verygood accuracy using AutoML.


## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

DeepLearning technique like FFNN can be used to fit the dataset, with proper tuning , it might surpass the AutoML. 

Using BayesianSampling might improve the HyperDrive pipeline. 

Last but not the least, if provided poweful compute, we can increase the sampling space for HyperParamater and improve the model. 

