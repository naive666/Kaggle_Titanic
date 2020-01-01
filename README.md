# Kaggle_Titanic
<div align=center><img width='1000', height='400' src='/Titanic.png' /></div>

## Content
   - [Introduction](#introduction)
   - [Data Understanding](#data-understanding)
   - [Feature Engineering](#feature-engineering)

## Introduction 
Titanic is a classic and famous kaggle competition which has been widely learnt by many novoices. This respository introduces some fundamental knowledge and processes to work with a data science project.  

## [Data Understanding](/Data_Summary.ipynb)
   - [data](/titanic_data/)
   - Usually when we get a dataset, the first thing is to check the data: how many instances? how many features? What type of data of each feature? Is there any null value? What is the distribution of each feature? We have many questions needed to solve by 'Data Understanding' process. One powerful tool is Matplotlib, a plotting tool, which could directly visualize the data so that I can read information through the pictures. 
   - From the previous step, I have a skeptical understanding of the data, and the next step is to do feature engineering which I believe is the most important thing in kaggle competitions. 

## [Feature Engineering]()
  - Concat the train data and the test data in order to keep the same distribution of data
  - Fill the null features by different methods: for numeric feature, it is reasonable to use mean or mode to represent the null values, while for categorical features, use the most frequent category is a widely used method. If a feature has too many null values, in general we skip this feature, but in some special cases, if this feature is closely corelated to the predictions, it might apply some Machine Learning models to fill in such feature. 
    - Fill in Null values 
      - There are only two null values of feature 'Embarked', and it is convenient to find out the information of these two persons from the Internet to fill in the blanks.    
      - For feature 'Cabin', I directly drop this feature because there are excessive null values. The cost of gain the complete feature will outweight its benefits.
      - It is easy to ask if there is a correlation between 'Age' and 'Survived', and in most situations in data science we follow our intuition to find out the important features without any data processing, and then collect evidence to prove our disprove the proposition. The evidence may come from literature reviews, data preprocessing, kaggle discussion board and so on. Here I guess 'Age' is a vital factor of prediction, and I calculate the correlation score of 'Age' and 'Survived', the result verify my suppostion. Therefore, it is important to predict the empty values of 'Age'. Hence, I tried disparate models such as Random Forest Regressor, Linear Model with regularization(Ridge Regressor), even XGBoost to predict age, and select the best one based on CV score. [Here]() is what I have done. 
