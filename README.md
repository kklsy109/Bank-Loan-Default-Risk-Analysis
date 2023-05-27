# Bank Loan Default Risk Analysis
 
## Table Of Content
[Project Dataset](https://www.kaggle.com/datasets/gauravduttakiit/loan-defaulter)<br>
1. Introduction<br>
    1.1 Purpose of this Analysis<br>
    1.2 Understanding Datasets<br>
    1.3 Model building and evaluation metrics<br>
2. [Data Cleansing](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Bank_Loan_Data_Processing.ipynb)<br>
    2.1 load and view data<br>
    2.2 Filter Data<br>
    2.3 Classify and standardize data<br>
    2.4 Convert data type<br>
    2.5 Default value padding<br>
3. [Data Analysis](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Bank_Loan_Data_analysis.ipynb)<br>
    3.1 View the distribution of target data
    3.2 Feature analysis
    3.3 Numerical variable analysis
4. [Building Prediction Model](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Bank_Loan_Building_Prediction_Model.ipynb)<br>
   

### 1. Introduction
#### 1.1 Purpose of this Analysis
In this project, I employed Exploratory Data Analysis (EDA) to analyze the risk of loan default in banks. EDA analysis can assist banks in gaining in-depth understanding of loan data, identifying key customer characteristics, and identifying anomalies, thereby minimizing the risk of financial loss when lending to customers.

#### 1.2 Understanding Datasets

#### Application_data.csv

This dataset contains customers' financial and other personal information. The "target" column represents the labels of the customers. (1 - customers with payment difficulties, 0 - all other cases)

#### Previous_application.csv

This dataset contains information about customers with a history of loan applications. This dataset is supplementary data for identifying loan defaulters.

#### 1.3 Model building and evaluation metrics

This project utilizes the random forest method to predict the risk of customer loan default and assesses the model's performance using AUC (roc_auc_score).



### 2. Data Cleansing

#### 2.1 load and view data

I first load and view the data, the application dataset has 122 columns, and the previous dataset has 37 columns.

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/1.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/2.png)


#### 2.2 Filter Data

#### 2.2.1 Check for null values


Next, I will examine the missing value situation in two datasets separately and filter out columns with missing values exceeding 40% for each attribute.


Application data

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/3.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/4.png)

Previous data

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/5.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/6.png)

By examining the percentage of missing values in the application data and previous data, it can be observed that there are a significant number of attributes with missing values exceeding 40%. I will perform a drop operation on these attributes during the subsequent data cleansing process.

#### 2.2.2 Analyze and remove unnecessary columns

In addition, I continue to check whether there are columns in the application data that need to be deleted.I selected four attributes: Flag class attributes, personal contact information class attributes, and EXT_SOURCE_X class attributes. I performed visualizations on them and examined whether they need to be removed.


![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/7.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/8.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/9.png)

Do the same analysis for Previous

#### 2.2.3 Drop the columns that are not needed.


Based on the analysis results, I will drop columns with missing values exceeding 40% and unnecessary columns.


![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/10.png)

Do the same for Previous Data

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/11.png)


#### 2.3 Classify and standardize data

#### 2.3.1 Convert all negative numbers in days to positive numbers

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/12.png)

#### 2.3.2 Pick out some numeric attributes, merge and create categorical columns

I selected the following numerical attributes: AMT_INCOME_TOTAL, AMT_CREDIT, AGE, YEARS_EMPLOYED, and converted them one by one into categorical attributes for analysis.

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/13.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/14.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/15.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/16.png)



#### 2.4 Convert data type

I first examined the number of unique values in each column and the data types of each attribute. I converted some object and numeric attributes into categorical types.


![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/17.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/18.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/19.png)


#### 2.5 Default value padding

I'm going to do default padding in three ways:

1)  For columns with relatively few missing values, I will fill them with the most frequently occurring value.

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/20.png)

For columns with a large number of missing values:

2)  I will fill the missing values of categorical attributes with "None";

3)  I will fill the missing values of numerical attributes with "median."

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/21.png)

### 3. Data Analysis

#### 3.1 View the distribution of target data

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/22.png)

#### 3.2 Feature analysis

I have selected 18 attributes that may impact the customer default rate, including NAME_CONTRACT_TYPE, CODE_GENDER, FLAG_OWN_CAR, FLAG_OWN_REALTY, NAME_HOUSING_TYPE, NAME_FAMILY_STATUS, NAME_EDUCATION_TYPE, NAME_INCOME_TYPE, REGION_RATING_CLIENT, OCCUPATION_TYPE, ORGANIZATION_TYPE, FLAG_DOCUMENT_3, AGE_GROUP, EMPLOYMENT_YEAR, AMT_CREDIT_RANGE, AMT_INCOME_RANGE, CNT_CHILDREN, CNT_FAM_MEMBERS. I will present and explain each attribute in a visual format.

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/23.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/24.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/25.png)

......

More detailed visualization and analysis are shown in the code file

#### 3.3 Numerical variable analysis


Analyze correlations between numeric attributes


![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/26.png)
![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/27.png)


According to the analysis of the heat map, the number columns related to the amount have highly correlated attributes, and I will draw a line chart to analyze the relationship between them and the customer default rate


![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/28.png)




### 4. Building Prediction Model

I use the results of the previous data analysis and convert the numerical data into categorical data, then use the random forest model to predict

Because defaulters make up only a small percentage of all applicants. The goal of our analysis is to identify loan defaulters and minimize the risk of losing funds, so we cannot simply take accuracy (predicted correct samples/total samples) as an evaluation metric.

I need a metric to select the model with the lowest false positive rate when all models have the same true positive rate. Under this premise, "ROC_AUC_SCORE" would be a good choice.

I split the dataset into train and test and use GridSearchCV to pick out the best parameters of the model

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/29.png)

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/30.png)

It can be seen from the figure that when the training samples increase, the scores of training and cross-validation converge towards the same limit, and the scores perform well. This means that the predictive model is neither overfit nor underfit.


In the end I got a roc_auc_score of 0.6435393455152716

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/31.png)


Finally, based on the results of predicting feature importance, it can be determined which features are more likely to influence customer default rates and repayment rates.

![](https://github.com/kklsy109/Bank-Loan-Default-Risk-Analysis/blob/main/Pictures/32.png)









