# AIRBNB TOP LISTINGS


---

How to navigate this repo:
- proposal_airbnb.pdf: my initial proposal for a classification project 
- mvp_airbnb.pdf: mvp presented two days before the final project submission
- data folder: data I used for modeling
- images: images I used in my presentation
- final: all files used for the final submission
  1. airbnb_cleaning.ipynb : notebook corresponding to the first phase of data cleaning and EDA
  2. airbnb_modeling.ipynb : notebook corresponding to the second phase of modeling and visualizing results
  3. airbnb_top_listings.pdf : final presentation

---

## ABSTRACT
As a Data Scientist on the Host Team at Airbnb, I have recently been approached by a Product Manager who intends to enhance the set of Host tools with a dashboard visualizing, amongst other things, two categories of listings: top listing and not top listing. To test this new concept, we will first focus on the NYC market.

Our impact hypothesis is that if hosts have more visibility on the expected performance of their listing, they will be able to optimize the listing’s most critical features and work towards achieving the Top Listing status. The more listings and guests’ experiences are optimized, the higher the retention will be on the Airbnb platform. 

I decided to approach this binary classification problem by comparing, in the baselining phase, two simple kNN and Logistic Regression models. I then applied feature engineering and feature selection to these two models before expanding into more complex modeling choices: Random Forest and XGBoost. 
Through cross-validation, I was able to select XGBoost as my model of choice and I proceeded with the final step of tuning the hyperparameters for this model.

## DATA

I have collected data on all the Airbnb listings in NYC from [Inside Airbnb](http://insideairbnb.com/get-the-data.html). 
The data source dates to April 7, 2021, hence presenting listings and related information updated up to that point.  

The original dataset presented around 35,000 rows and 70 features presenting elements characterizing an Airbnb listing.

This model's target, *Top Listing*, has been defined as a listing whose *availability_365* is lower than or equal to the median of *availability_365*. The assumption here is that a listing that is booked for more than 6 months is popular and well performing - hence earning the appellation of Top Listing.

Inactive listings have been filtered out as they should not be included in the model since they cannot be booked onlyne. 
I defined a listing to be inactive when it presents a value of *availability_365* (i.e. availability in the next 365 days) equal to zero and *last_review* occurred before April 7, 2020.

Probably also due to the pandemic, there are a significant portions of listings that are inactive in NYC. Therefore, the size of my final listings dataset was ca. 26,000 rows.

## DESIGN

As reflected in the two jupyter notebooks included in the final folder of this repo, this project is designed around two main components:
1. **Data Cleaning & EDA**: see data cleaning jupyter notebook
2. **Data Modeling**: see data modelingjupyter notebook
3. **Business Insights gathering**: both in the data modeling jupyter notebook and my final presentation

The last step is particularly important because every model must be contextualized and must be evaluated in light of specific domain knowledge. The presentation includes a few ideas for product development and marketing campaigns for the Airbnb team.

## ALGORITHM

As a first step, I have cleaned and explored the data using pandas, numpy, seaborn and matplotlib. <br/>

Next I chose F beta as my metric of choice for this model because it was important to balance recall and precision. However, I have decided to allocate more weight to precision (it's more important to not mislead hosts instead of capturing all the possible Top Listings in NYC), hence choosing a beta of 0.35. 

I then proceeded with baselining the model comparing kNN and Logistic Regression on the selection of features that, from the pairplot, seemed to introduce the largest separability between the classes. In this step, I have also tuned the k hyperparameter of kNN to maximize F beta.

I then conducted a quite extensive phase of feature engineering and tested kNN and Logistic Regression across 22 distinct combinations of features. 

As a next step, I expanded the model and tested the best performing kNN and Logistic Regression models, along with the Random Forest and XGBoost models in a cross-validation scheme. Xgboost turned out to be the winner with a F beta of 0.735. I chose this as my final model.

Finally I used RandomizedSearchCV to tune the XGBoost hyperparameters and I ended up with a F beta of 0.739.

## TOOLS

- Pandas and numpy for data manipulation
- Seaborn and matplotlib for data visualization
- Scikit-learn and XGboost for data modeling

## COMMUNICATION

A slide deck is included in this repo. 

In addition, see below the final confusion matrix and feature importances plots (frequency vs gain).

![confusion](https://user-images.githubusercontent.com/68084582/121629094-82739100-ca48-11eb-9b13-fec7cc07a18f.png)

![feat_imp_plot_freq](https://user-images.githubusercontent.com/68084582/121629132-928b7080-ca48-11eb-8d3b-9a0a83682520.png)

![feat_imp_plot_gain](https://user-images.githubusercontent.com/68084582/121629143-96b78e00-ca48-11eb-9876-da4735ceb28a.png)
