# Practical-machine-learning

Note - This is part of the Practical machine learning courrse offered by Coursera as part of the Data Science Specliazation by Johns Hopkins University

## Executive Summary
The data is from accelerometers on the belt, forearm, arm, and dumbell of 6 participants. They were asked to perform barbell lifts correctly and incorrectly in 5 different ways. The goal was to predict the manner in which they did the exercise. This is the "classe" variable in the training set. 

## Methods

### Data cleaning steps
* Remove irrelevant features
* remove columns that have NA or blank values
* Check if any feaatures for zero variance. Zero variance means the value is the same across all features and would not add new information to the ML model. Hence can be removed. 
* Split cleaned data into 70%-30% (training and test set)

### Perform exploratory analysis on cleaned training set
* Correlation plot
* The corrlelation plot showed a number of highly correlated variables. So we need to do some feature selection and choose only those features that are the most informative

### Model building
In this report, we used cross validation and evaluated three different predition methods on the training set and chose the model that gave the highest accuracy as the "best model". This model was then applied one time on the test dataset to get the final class prediction. 

Note - The kappa statistic is a measure of how closely the instances classified by the machine learning classifier matched the data labeled as ground truth, controlling for the accuracy of a random classifier as measured by the expected accuracy. This statistic can shed light into how the classifier itself performed, the kappa statistic for one model is directly comparable to the kappa statistic for any other model used for the same classification task. According to Fleiss,  kappas > 0.75 are excellent, 0.40-0.75 as fair to good, and < 0.40 as poor. 


#### Model 1 -  Principal Component Analyis (PCA) and Support Vector machine(SVM)
  * Find the number of features that can explain 90% of variability
  * 5 fold cross validation
  * Build model. Model short listed 18 PC features
  * Apply model on test data
  * Results - Accuracy of 0.8766 (87%) and a Kappa of 0.8423 (excellent)

#### Model 2 - Random forest 
* Random Forst will automatically also deso feature selection. 
* Results - From this model, we got Acuracy of 0.9912 (99%), and OOB estimate of error rate 0.76%

#### Model 3 - Generalized linear model (GLM)
In order to choose from the various models with different lambda values provided by glmnet, we performed cross validation using the cv.glmnet function with misclassification error as the criterion for 5-fold procedure. The lambda value that yields the minimum cross validation error gives the best model. The figure below shows a plot of lambda with mis-classification error. The very small error rate at the optimal lambda is a sign of the model’s effectiveness.

* When the penalty Alpha = 0 is ridge regression, alpha = 1 means it is lasso. Alpha = 0.5 is elastic net. 
* Lambda is the shrinkage parameter: when Lambda=0, no shrinkage is performed, and as Lambda increases, the coefficients are shrunk ever more strongly. 
* We can see that the final GLM model has an accuracy of 0.7321 (73%), with Kappa value of 0.6603 (good). 
* Results - From this model, we got Accuracy = 0.732

### Best model 
So we can see that Random Forest gave the highest accuracy, so that is the model that we selected. Accuracy is 0.9911 and Out of sample error is 0.0088 (0.8%).  Ideally it would have been better to use 10 or more fold cross validation to get a more robust model, but was not possible due to RAM restrictions.
If we had a 2 class problem, we would have been able to plot ROC curves. But since this is a multi-class problem, I have not plotted ROC curves

## Results
After comparing three methods - PCA with SVM, Random Forest, and GLM Net, I found that the Random Forest model gave the highest accuracy and chose that as the best model to apply on the validation set

Applied Random Forest model on the validation set to obtain the predicted values. Ground truth was not provided. 

## RMarkdown report
Click here: https://github.com/Krithika-Bhuvan/Practical-machine-learning/blob/master/Project.pdf


