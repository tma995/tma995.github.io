---
layout: default
title:  Customer Segmentation Report for Arvato Financial Services
---

{{ page.date | date: '%Y-%m-%d' }}: Capstone project for Udacity Data Nanodegree Program, which is also a [Kaggle competition](http://www.kaggle.com/t/21e6d45d4c574c7fa2d868f0e8c83140). 

# {{ page.title }}

## 1. Introduction

In this project, a mail-order sales company in Germany is interested in identifying segments of the general population to target with their marketing in order to grow. The objective is to describe the core customer base of the company, and to identify which individuals are most likely to respond to the campaign.

### Data Sets
* AZDIAS: Demographics data for the general population of Germany; (891,211 x 366).
* CUSTOMERS: Demographics data for customers of a mail-order company; (191,652 x 369).
* MAILOUT_TRAIN: Demographics data for individuals who were targets of a marketing campaign; (42,982 x 367).
* MAILOUT_TEST: Demographics data for individuals who were targets of a marketing campaign; (42,833 x 366).

### Problem Statement
* Analyze demographics data (provided by Arvato Financial Solutions, a Bertelsmann subsidiary) for customers of a mail-order sales company in Germany, comparing it against demographics information for the general population. 
* Use unsupervised learning techniques to perform customer segmentation, identifying the parts of the population that best describe the core customer base of the company.
* Use supervised learning techniques to predict customer responses in a marketing campaign for the mail-order company, which is also a Kaggle competition.

* * *

## 2. Implementation and Analysis

### Data Pre-processing

* * *

### Customer Segmentation
Since there are hundreds of variables in the demographics dataset, it is necessary to reduce the dimension of the feature space before clustering, in order to reduce complexity of the problem, and to draw underlying pattern of the dataset.

![iacs_pca1](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_pca1.png)

From above curve plot, we see that 18 or more components are able to explain Top 30% of the total variance and the explained variance drops significantly after about 20. So I picked 20 as the parameter for further analysis.

For segmentation purpose, K-Means is applyed to group unlabeled data. From below plots, we see a limited score increase after 10 clusters. So 10 is selected as a reasonable cluster number for further analysis.

![iacs_kmeans1](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_kmeans1.png)

After training, we apply 10 cluster K-Means model on both demographics and customers dataset. 

![iacs_kmeans2](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_kmeans2.png)

Based on cluster distribution histogram on both datasets, it is clear to see that Cluster 6 is outstanding for customers, which means people in this group is more likely to be part of the mail-order company's main customer base than other groups.

The coefficients of Cluster 6 is displayed below:

![iacs_kmeans3](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_kmeans3.png)

Since Cluster 6 is most affected by the first 4 PCA features, let’s look inside for detail.

![iacs_kmeans4](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_kmeans4.png)

Following are the observation for each PCA feature:

1st: Low-income, High mobility, areas with more family houses or business buildings; (should be interpreted on reverse meaning due to negative coefficients {-6.17289942})
2nd: Cars: Upper-class, German, Fast, Sports; 
3rd: Not young, relatively wealthy, Interested in advertising and will to shop online; 
4th: Many online transactions, Not single, Has big family; 

In conclusion, for the entire population, the target customer for this mail-order company is most likely to be:
* Life Stage: in the middle age and has big family;
* Financial Ability: with good income level and have upper class cars;
* Behavior Pattern: comfortable with advertising and online shopping;

* * *

### Prediction Model

XGBoost is selected as a solution for this supervised learning problems. The specialty xgboost differs from other gradient boosting algorithm is that xgboost used a more regularized model formalization to control over-fitting, which gives it better performance.

Based on the limited understanding of data features, I engineered the data in a way that is slightly different from clustering purpose:

* Maintain as many features as possible in the training set, in order to preserve more underlying characteristics of original data;
* Left all NaN values along, because XGBoost is able to deal with missing values;
* Did not scale the data, since XGBoost is a non-linear model;
* Add extra features: By checking LNR column, we know people in both train and test set are included in CUSTOMERS dataset. In this case, `CUSTOMER_GROUP`, `ONLINE_PURCHASE`, `PRODUCT_GROUP` can be used in the predictive model.

Then I split `MAILOUT_TRAIN` data into training and validation set, trained it with AUC score as evaluation metric and 50 as early stopping rounds.

After training, model got a validation score of 0.76322 on the 48th iteration. Refer to below graph for most important features:

![iacs_xgb1](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_xgb1.png)

It turns out that some undocumented feature are very important in the model, such as '`D19_SOZIALES`', '`ANZ_KINDER`', '`EXTSEL992`', and so on.

The final prediction (response.csv) has received a score of 0.80762 on Kaggle’s Public Leaderboard, which ranked top 3 at the time of submission and very close to the Top Score 0.80819. 

![iacs_xgb2](https://github.com/tma995/tma995.github.io/raw/master/_posts/img/iacs_xgb2.png)

* * *

## 3. Conclusion

In this project, demographics data of Germany was analyzed. Various Machine Learning techniques, in both Unsupervised Learning and Supervised Learning, were used to answer different questions. 

While undertaking the research work, I did learn a lot not only in manipulating ML techniques, but also in finding insights of real-life business from unfamiliar domains. I would like to thank Udacity and Arvato Financial Services for setting this up.

Even though the score looks ok on Kaggle’s Public Leaderboard, there is still a lot to be improved:

* Feature Engineering: Better understanding of data will definitely help in feature selection, and additional features extracted from outside resources for Germany population may improve clustering and prediction;
* Other algorithms: lightgbm, catboost, and many more algorithms can be put into experiment in this project;
* Fusion Model: for the time reason, I only trained one model in this project. However, Fusion Model is a necessary part in predictive problems. By combining multiple model which trained in different scheme, will probably further push the score to another level.

In the end, I would like to thank Udacity and Arvato Financial Services for setting all this up.
