#  ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 2 - Singapore Housing Data and Kaggle Challenge


## Introduction

Singapore's HDB resale market has been one of the largest source of property transactions in the last 3 decades. In an increasingly competitive market, access to information and the accuracy of information received is vital to sellers, buyers, and the brokers of such sales. First hand information on transactions are now publically available on the market and the moment you get your hands on it, chances are, all your competitors, be it sellers, buyers, or other real estate agents probably also have the same data that you have.

## Problem Statement

A team of realtors has engaged me to run this project for them in order to aid in their own presentations to prospective clients when projecting listings of their properties on online portals. They also want to use the model to help them better advise their clients who are buying on the prices that they should be expecting to pay. The model should be both complex enough for accuracy, yet simple enough to explain to people with varying degrees of knowledge on the subject matter.

## Import and cleaning of data

1. General steps were taken to ensure data was clear of null values.
2. Nll values were dropped altogether for "mall_nearest_distance". Small enough number of values compared to the entire train set.
3. Other null values were replaced with 0 values as they accurately reflected the values in the data.


## EDA and Visualization

First, intuitively droppable features were dropped from the dataset. The remaining data was then separated into categorical and continuous featues.

Data that was dropped
1. price_per_sqft - it is essentially a derivitive of our target predictions and may cause data leakage if included
2. all latitudes, longitudes and postal code - using these actual values to calculate exact distances may be too complex, other location features like town, planning area and address can be used.
3. street_name - already contained in address.
4. tranc_yearmonth - we already have tranc_year, tranc_month.
5. lease_commence_date and year_completed - we already have the age of the flat which is a derivitive of this feature.
6. mid - same as mid_storey
7. town - overlaps with planning area
8. flat_type - over laps with full_flat_type

Continuous features were evaluated using their correlation coefficients, and scatter plots were then used to confirm the initial impressions 
that we had on the data. The top 10 was then picked from this list to be used in the model.

1. floor_area_sqm
2. max_floor_lvl
3. 5room_sold
4. upper
5. exec_sold
6. hawker_within_2km
7. 3room_sold
8. hdb_age
9. 2room_sold
10. total_dwelling_units

Categorical data was looked at via box plots in relation to resale price and the top 3 were selected.

1. floor_area_sqm
2. hdb_age
3. max_floor_lvl


## Preprocessing and Modelling

A baseline model was first created using 3 continuous features with which to compare against.

1. floor_area_sqm
2. hdb_age
3. max_floor_lvl

An RMSE score of 86695 was obtained using cross validation.

Categorical and continuous features that were selected were then drawn out and put into a dataframe with which to work with.
Onehot Encoding was performed on the categorical features to binarize them and then the model was scaled.

Linear regression model, ridgeCV and lassoCV models were also created and evaluated.

The linear regression model was selected for use as the r2 scores indicated very little sign of overfitting, and there was little differences in the result of using the regularized models.

Model was put to use on Kaggle test data and a Kaggle score of RMSE 60862 was obtained.


### Conclusion

1. The model that was created was based off main features that included, size of the property, location of the property, age of the property and some demand and supply factors. 

2. Model will be able to give a rough gauge of the required budgets for buyers, and also estimate to a certain degree the amount that a seller would be able to list the property for.

3. The model is simple enough to explain to clients based on features that are commonly thought factors in affecting property prices.


### Limitations

1. The model is based off past information and has to be continually retrained in order to be useful.

2. The model also does not take into account special circumstances like HDB cooling measures and interest rate hikes.

3. The model is not able to factor in wider demand and supply issues, like covid lockdown and the effect it had on the supply of new BTO flats which also caused an accross the board raise in HDB resale prices.


### Recommendations

1. Property agents should use this model to help estimate both buying and selling budgets for clients based off the main features highlighted above in the conclusions.

2. Agents will be able to help selling clients highlight which features should be marketed in order to get better resale prices.

3. It is recommended that in later models, information on demand and supply factors, interest rates and govt policy be added in.


### Data Dictionary
|Feature|Type|Dataset|Description|
|---|---|---|---|
|storey_range|object|train.csv|floor level (range) of the resale flat unit, e.g. 07 TO 09.|
|full_flat_type|object|train.csv|type of the resale flat unit, e.g. 3 ROOM and HDB model of the resale flat, e.g. Multi Generation.|
|planning_area|object|train.csv|Government planning area that the flat is located.|
|resale_price|float|train.csv|the property's sale price in Singapore dollars.|
|floor_area_sqm|float|train.csv|floor area of the resale flat unit in square metres.|
|max_floor_lvl|int|train.csv|highest floor of the resale flat.|
|5room_sold|int|train.csv|number of 5-room residential units in the resale flat.|
|upper|int|train.csv|upper value of storey_range.|
|exec_sold|int|train.csv|number of executive type residential units in the resale flat block.|
|hawker_within_2km|int|train.csv|number of hawker centres within 2 kilometres.|
|3room_sold|int|train.csv|number of 3-room residential units in the resale flat.|
|hdb_age|int|train.csv|number of years from lease_commence_date to present year.|
|2room_sold|int|train.csv|number of 2-room residential units in the resale flat.|
|total_dwelling_units|int|train.csv|total number of residential dwelling units in the resale flat.|
