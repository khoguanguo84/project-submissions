# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Capstone Project - Predicting Loan Default: Part 1

Prepared by: Kho Guan Guo, 27 Apr 2023
<br>
<br>
### Overview
<br>

**Background**

Banks run into losses when a customer doesn't pay their loans on time. Because of this, every year, banks have losses in millions, and this also impacts the country's economic growth to a large extent. Being able to predict if a customer will default on a loan at the application stage would eliminate the problem before the loan is approved. The bank however runs the risk of losing potential business if the prediction is wrong. 
<br><br>
**Problem Statement**

Using the given dataset, this project aims to achieve 3 things as its Primary objectives.
1. To utilize the information given and quantify feature importance to accurately predict loan defaults.
2. To engineer features to help better predict loan defaults.
3. To act as a stepping stone to develop better models that can address this issue that banks have and reduce monetary losses.
<br><br>
**Evaluation**

This is a classification problem and models were evaluated by the following.

1. Accuracy: Banks need to accurately and quickly predict potential defaults. Accuracy in predicting both potential business and potential losses are essential for any business.

2. F1: False negatives and False positives will be crucial to the evaluating of bank loan approvals based on the predictions in order to reduce loss, especially in imbalanced datasets like this.

3. Log Loss: Log-loss is indicative of how close the prediction probability is to the corresponding actual/true value (0 or 1 in case of binary classification). The more the predicted probability diverges from the actual value, the higher is the log-loss value. It was also used to evaluate a MachineHack competition and a good way to benchmark my model to others who have tried this.

---

### Datasets

Datasets are provided on Kaggle.
https://www.kaggle.com/datasets/ankitkalauni/bank-loan-defaulter-prediction-hackathon

Datasets: 
* [`train.csv`](./data/train.csv)

Cleaned Datasets found at my Google Drive
https://drive.google.com/drive/folders/1apfFIzSIq_Hg-zLlrYlukSICO4SSzC-i?usp=share_link

<br>

#### Data dictionary of selected features only

|Features|Type|Description|
|:---|:---|:---|
|id|int|individual loan applicant ids|
|loan_amount|int|loan amount applied for|
|funded_amount|int|amount of loan funded by bank|
|funded_amount_investor|int|amount of loan funded by investors|
|term|int|loan term|
|batch_enrolled|str|batch number|
|interest_rate|float|interest rate on loan|
|grade|str|credit rating|
|sub_grade|str|alternative credit rating|
|home_ownership|str|home is owned, rent or mortgage|
|employment_duration|float|income statistic|
|verification_status|str|income source verified or not|
|loan_title|str|type of loan applied for|
|debitto_income|float|ratio of debt to income|
|delinquency_twoyears|int|number of 30 day failure to pay loan installments in 2 years|
|inquires_sixmonths|int|number of inquiries in the last 6 months|
|open_account|int|number of open accounts|
|public_record|int|number of public records|
|revolving_balance|int|asset statistic|
|revolving_utilities|float|debt access statistic|
|total_accounts|int|debt access statistic|
|initial_list_status|str|w for wait, f for forwarded|
|total_received_interest|float|debt statistic|
|total_received_late_fee|float|debt statistic|
|recoveries|float|debt statistic|
|collection_recovery_fee|float|debt statistic|
|collection12months_medical|int|debt statistic|
|application_type|str|joint or individual application|
|lastweek_pay|int|debt statistic|
|total_collection_amount|int|debt statistic|
|total_current_balance|int|asset statistic|
|total_revolving_credit_limit|int|debt statistic|
|loan_status|boolean|1 if defaulted, 0 if not defaulted|

---

### Submissions

Technical reports submitted: 
(./Capstone Part 1.ipynb): Overview and Data Cleaning
(./Capstone Part 2.ipynb): EDA
(./Capstone Part 3.ipynb): Feature Selection and Modelling
(./Capstone Part 3a.ipynb): Feature Selection and Modelling
(./Capstone Part 3b.ipynb): Feature Selection and Modelling
(./Capstone Presentation Loan Default Predictions.pdf): Presentation slides

---

### Modelling

**Summary of results**

Best Model: XGBoost
Best Params: {'smote__sampling_strategy': 'minority', 'xgb__learning_rate': 0.14, 'xgb__max_depth': 4, 'xgb__n_estimators': 150}
Best Log Loss Score: 0.5161713545211244

Test data scores
Log Loss Score: 0.52156
Accuracy Score: 0.7605
F1 Score: 0.1246

**Possible improvements**

Feature engineering can be further explored based on the most important features in the current models.
I would like to try clustering to obtain certain features next before using the supervised learning models.

---

xxx

---

### Recommendations

The model is not yet the finished product to be deployed, but can be used as a base to continue improving.

Feature engineering based on the feature importance from the best model will play a big role in the next steps in the next phase of the project which I will continue to work on over the next few weeks.

Obtaining the right data from customers to be used as features in the model besides what was provided might prove more useful than tweaking existing data.

In order to get the model good enough to deploy, a few things need to be accomplished.

1. Feature engineering and continued tuning to get better Accuracy and F1 scores
2. Reduction of features such that the deployment feature ranges are easily obtainable by bank clients and the bank.
3. Model needs to run fast in order to be deployed for customer use.

---
