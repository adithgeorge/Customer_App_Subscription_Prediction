# Customer_App_Subscription_Prediction

**Still working on this by improving the result, insights and further deployment.**

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

* **Understanding the time taken by user to subscribe:** We need to measure the difference between 'first_open' and 'enrolled_date', and save it in a new column. We notice that most of the users enroll within the first 20 to 30 hours. We can infer that 50 hours is a good cut-off time to test the response of the users. So every user that enrolled after 50 hours can be considered as Non-enrolled for checking the accurate response of the users.

* **Analysing the screen list features and getting insights from the number and type of windows/ screens used.**
* The saving columns are highly correlated, so we need to delete them. But before so we need to create a SavingsCount feature. The same for Credit, CreditCards, and Loan.





