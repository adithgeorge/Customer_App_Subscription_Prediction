# Customer_App_Subscription_Prediction

**Still working on this by improving the result, insights and further deployment. Do read this file and check the conclusion to get an  accurate idea on my project and what are its limitations.**

## Introduction

In today's market, many companies have a mobile presence. Often, these companies provide free products/services in their mobile apps in an attempt to transition their customers to a paid membership. For this, you need a Budget. Since marketing efforts are never free, these companies need to know exactly who to target with offers and promotions.

* Market: The target audience is customers who use a company's free product. In this case study, this refers to users who installed (and used) the company's free mobile app.

* Product: The paid memberships often provide enhanced versions of the free products already given for free, alongside new features.

* Goal: The objective of this model is to predict which users will and will not subscribe to the premium membership so that we can focus our marketing efforts to convert these users to paid users. The marketing strategy can be bothways, We can either focus our limited resources on those who are more willing to take a subscription thereby increasing our profit with less effort or we could focus on converting those who are less willing to take a subscription.

## Model Building

The Model Building Process is composed of the following sections:

* Plotting with Matplotlib and Seaborn - Exploratory Data Analysis (EDA)
* Data Preprocessing - We will use Pandas and Numpy for all of our data preprocessing.
* Classification Models from Sklearn Library (Logistic Regression, Tree, SVM, ...)
* K-Fold Cross Validation, Grid Search (Parameter Tuning), and Feature Selection algorithms.

## The Problem Statement

In this Case Study, we will be working for a fin-tech company that wants to provide its customers with a paid mobile app subscription that will allow them to track all of their finances in one place. To attract customers, the company releases a free version of its app with some of the main features unlocked.

The company has tasked you to identify which users will most likely NOT enroll in the paid product so that additional offers can be given to them. Because of the costs of these offers, the company does not want to offer them to everybody, especially customers who were going to enroll anyways.

This app is used for financial purposes like bank loans, savings, etc. in one place. It has two versions free and premium. The free version app contains basic features and customer wants to use the premium feature then they have to pay some amount to unlock it.

The main goal of the company is to sell the premium version app with low advertisement cost but they don’t know how to do it. That’s a reason they are provided the premium feature in the free version app for 24 hours to collect the customer’s behavior.

The job of the scientist is to find or predict new customer who is interested to buy the product or not. If the customers will buy a product anyway so no need to give an offer to that customer and loss the business. Only give offers to those customers who are interested to use premium version app but they can’t afford its cost. So the company will give offers to those customers and earn more money.

## Data Description

* user - The client ID number
* first_open - The date and time, the user first open the app
* dayofweek - The day in numerical form (0: Sunday,..., 6: Saturday)
* hour - The hour of first open in 24h format
* age - The age of the user
* screen_lists - Describes every single screen name the user has set in this 24-hours
* numscreens - The number of screens apairs in screen_lists
* minigame - The app has a mini-game, if the user played in the 24h it is set to 1, otherwise, it is set to 0
* liked - If the user liked any feature of the app it is set to 1, otherwise, it is set to 0
* used_premium_features - The user usage of the free trial of premium features is set to 1, otherwise, it is set to 0
* enrolled - This is the target column. If the user has enrolled in the premium offer it is set to 1, otherwise, it is set to 0
* enrolled_date - The date of enrollement if they did

## EDA

* As you can see the dataset size we have is good. More the data, more insights we can leverage.

* **Missing Values:** Features don't have missing values except 'enrolled_date' because not all user have enrolled for the premium version. So we have 18926 users who have not enrolled.

* **Conversion of Data Types:** As 'first_open', 'hour', and 'enrolled_date' are datetime objects but in our dataset they are of object type there is a need to convert them.

### Some Insights

* The app is being used daily irrespective of the day, we will need to look into the type of users for each day.
* The app is used more either in the early morning or at night where the number of free user usage is greatest at night time. Further research is needed in this area.
* It is seen more users are in the 20 - 30 bracket and the number of free users are also in this bracket. Greater age is associated with premium users. Maybe the young users need only the basic features.
* Very few people are playing the minigame, but those who are playing it have also subscribed to the premium version, we may need to check on the type of mini game players also a check is needed on the quality of the game.
* It is seen that those who have already used the premium version have a lower chance of subscribing to it. This shows the need for a check on the necessity and quality of the premium version in the app.
* liked and used_premium_feature are showing a similar trend.

### Correlation

* 'hour', 'age', 'used_premium_feature', and 'liked' are negatively correlated with enrolled, that's means that the more those parameter increase, the less likely that the user register for premium offer.

* 'numscreens' and 'minigame' are positively correlated with enrolled, that's means that the more those parameter increase, the more likely that the user register for premium offer.

* The most interesting remark from the graph is that 'used_premium_feature' is negatively correlated with enrolled. Users who used the premium feature are convinced that the product isn't worth the price.

### Feature Engineering

* **Understanding the time taken by user to subscribe:** We need to measure the difference between 'first_open' and 'enrolled_date', and save it in a new column. We notice that most of the users enroll within the first 20 to 30 hours. We can infer that 50 hours is a good cut-off time to test the response of the users. So every user that enrolled after 50 hours can be considered as Non-enrolled for checking the accurate response of the users.

* **Analysing the screen list features and getting insights from the number and type of windows/ screens used.**
* The saving columns are highly correlated, so we need to delete them. But before so we need to create a SavingsCount feature. The same for Credit, CreditCards, and Loan.

### Data Preprocessing

* We will be converting the 'age' data into age groups to get more accuracy and also convert the categorical variables into dummy variables. The model will be 
* **Due to computational limitations, further model building was done on a part of the data only.** 
* We can see that the target columns is not imbalanced and therefore we can proceed with this small dataset for model building.
* Feature scaling may not be necessary as almost all the values are either 1 or 0.
* Note: There was no big difference in the accuracy after feature scaling.

## Model Building

We have gained some insights from the EDA part. But with that, we cannot accurately predict or tell whether a user will opt for the premium version or not. So now we will predict that using some great Classification Algorithms. Following are the algorithms I will use to make the model:

* Logistic Regression

* Support Vector Machines(Linear)

* Random Forest

* K-Nearest Neighbours

* Naive Bayes

* Decision Tree

The accuracy of a model is not the only factor that determines the robustness of the classifier. As the training and testing data changes, the accuracy will also change. It may increase or decrease. This is known as model variance.

To overcome this and get a generalized model,we use Cross Validation.

Many a times, the data is imbalanced, i.e there may be a high number of one specific class instances but less number of other class instances. Thus we should train and test our algorithm on each and every instance of the dataset. Then we can take an average of all the noted accuracies over the dataset.

An algorithm may underfit over a dataset for some training data and sometimes also overfit the data for other training set. Thus with cross-validation, we can achieve a generalised model and we can predict the average accuracy for the model when data is provided.

**As we can see the best performing algorithms are SVM (linear), Random Forest Classifer, Logistic Regression.**

### Cross Validation

Here, we can see that the Linear SVM, Logistic Regression and Random Forest are all performing well enough after cross validation and their variance is also low. So, we can be confident that we can get a generalised model and a consistent accuracy for different data.

### Hyperparameter Tuning

Hyper Parameter Tuning can be done to change the learning rate of the algorithm and get a better model.

After this process we can conclude that almost all the algorithms are giving a good enough accuracy and also has a similar clasification report, therefore we can fix on one model and take the Random Forest Classifer model as the best possible one.

### Confusion Matrix

Here we can infer the following from the confusion matrix:

* 0 - Not enrolled, 1 - Enrolled
* We have the actual classes on the y-axis and the predicted classes on the x-axis.
* The model is able to dstinguish between the both classes,but still there is some error.
* 485 samples were actually positive but were predicted as negative - False Negative
* 311 samples were actually negative but were predicted as positive - False Positive.
* There is margin for improvement of the model.

* The feature importances were also calculated

# Conclusion

* Our efforts have given us a model that will label every new user as "highly likely" (or "unlikely") to subscribe. We can further validate our results by running our predictions on daily new installs, and see whether our accuracy is consistent. From there, we can narrow our marketing efforts only to those users "unlikely" to subscribe, and thus increase our subscription rate.

* The increase in overall subscriptions can measure the benefits of this model to the company. Recall that those already likely to subscribe will do so, and although we can still give them offers, we don't have to go all out. On the other hand, users who are likely to leave may convert to paid subscribers if we give them an offer they cannot refuse. For example, these offers can come in the form of "1st month free", or "50% off yearly subscriptions". The latter shows that great offers can still be structured in a way that brings overall benefits to the company because we are locking the user in for an extended period. This is a model of SaaS services provided through the app.


