# Kaggle_Titanic
<div align=center><img width='1000', height='400' src='/Titanic.png' /></div>

## Content
   - [Introduction](#introduction)
   - [Data Understanding](#data-understanding)
   - [Feature Engineering](#feature-engineering)
   - [Models](#models)
   - [Summary](#summary)
   - [Contributors](#contributors)
  
## Introduction 
Titanic is a classic and famous kaggle competition which has been widely learnt by many novoices. This respository introduces some fundamental knowledge and processes to work with a data science project.  

## [Data Understanding](/Data_Summary.ipynb)
   - [data](/titanic_data/)
   - Usually when we get a dataset, the first thing is to check the data: how many instances? how many features? What type of data of each feature? Is there any null value? What is the distribution of each feature? We have many questions needed to solve by 'Data Understanding' process. One powerful tool is Matplotlib, a plotting tool, which could directly visualize the data so that I can read information through the pictures. 
   - From the previous step, I have a skeptical understanding of the data, and the next step is to do feature engineering which I believe is the most important thing in kaggle competitions. 

## [Feature Engineering](Feature_Operation.ipynb)
  - Concat the train data and the test data in order to keep the same distribution of data
  - Fill the null features by different methods: for numeric feature, it is reasonable to use mean or mode to represent the null values, while for categorical features, use the most frequent category is a widely used method. If a feature has too many null values, in general we skip this feature, but in some special cases, if this feature is closely corelated to the predictions, it might apply some Machine Learning models to fill in such feature. 
    - Fill in Null values 
      - There are only two null values of feature 'Embarked', and it is convenient to find out the information of these two persons from the Internet to fill in the blanks.    
      - For feature 'Cabin', I directly drop this feature because there are excessive null values. The cost of gain the complete feature will outweight its benefits.
      - Transfer categorical features to numerical for the further steps.
      - It is easy to ask if there is a correlation between 'Age' and 'Survived', and in most situations in data science we follow our intuition to find out the important features without any data processing, and then collect evidence to prove our disprove the proposition. The evidence may come from literature reviews, data preprocessing, kaggle discussion board and so on. Here I guess 'Age' is a vital factor of prediction, and I calculate the correlation score of 'Age' and 'Survived', the result verify my suppostion. Therefore, it is important to predict the empty values of 'Age'. Hence, I tried disparate models such as Random Forest Regressor, Support Vector Machine with RBF Kernel, Gradient Boost Regressor to predict age, and select the best one based on CV score. [Here](/age_prediction.ipynb) is what I have done. After that, I thought is there any obvious difference between age 11 and 12? Seems not! Accordingly, I cut the age into 5 categories: 0-10 10-18 18-35 55-55 55-80. And the prediction object becomes these categories. [This](/Age_prediction.ipynb) is a modified model to predict age, in which I also tested an easy proposed method from Kaggle Kernel.
  - Aside from the original features, I also created some new features for the purpose of better decribing the data: 
    - I extracted the titles from the name of every customer and created a new feature called 'Title'. Since it is much plausible to use the title of a person instead of the name to decribe the social status of a person so as to explain why perple with title 'Ms', 'Miss' had higher survival rate than those with other titles. 
    - Likewise, I created 'Total_Family' to show how many family members one customer had. 'Surname' is another feature created to illustrate the surname of every person. 
    - From the observation, the distribution of 'Fare' is long-tailed, so I applied log to this feature so that the distribution seems more normal.
  - When all valid feature was prepared, it is helpful to visualize the correlation between features and labels using hotmap.
  <div align=center><img width='600', height='600' src='/hotmap.png' /></div>

## Models
Here I present 3 versions of my models. [Model1](/Model.ipynb) is the first version of my model, in which I tried different models with different parameters using GridSearch and evaluated them respectively. Also, I drew a picture reflecting the contribution of each feature to the final prediction. 
<div align=center><img width='1000', height='600' src='/Model_evaluation.png' /></div>
After using different models to predict, I tried stacked models but the results were not good enough due to the complexity of the model. Thus, the second [model](/Model2.ipynb) is a simplified model and the third [model](/Model3.ipynb) is my ultimate model using the best cross-validation scored model.

## Summary
In this project, feature engineering and feature selection are both crucial! When I merely used the original data and made some basic processing such as transfer the categorical to numerical, the result was much worse than my expectation. However, when the new features was appended, the result accuracy showed a perceptible difference. The predict model was not that important as compared to the feature engineering process, the score of the best models were not so huge that affected the rank in Kaggle private board. Also, I found that to small data set, a simple model is usually performing better than those complicated ones.

## Contributors
<a href="https://github.com/naive666"><img src="https://avatars2.githubusercontent.com/u/53068274?s=40&v=4&button=True" /></a>
