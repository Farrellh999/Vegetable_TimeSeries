# Data Science Project: Tommies or Tatties?

# Overview

This project uses a publicly available dataset which provides data on the cost of various ingredients, including potatoes ('tatties') and tomatoes ('tommies'), between the years 2013 and 2021.

The goal of this project is to explore the use of a time series forecast model as a tool to decide which main ingredient to use (tatties or tommies) for the soup of the week, based on the predicted cost of the two ingredients i.e., whichever ingredient is forecast to be the least expensive for that month will be used and advertised as the 'soup of the day'.

### Positive Impact
The business will be able to hopefully make data-driven business decisions in order to optimise profit.

### Negative Impact
The forecast may influence the use of a certain ingredient at a time when that ingredient is of poor quality, leading to problems further down the line such as customer disatisfaction, the requirement to use additional ingredients to improve the quality of the soup.

## Conclusion

## Bibliography

# Data Sources
The dataset can be found at [https://www.kaggle.com/datasets/ramkrijal/agriculture-vegetables-fruits-time-series-prices?resource=download]. This a public dataset, readily available to download to anyone who has a free Kaggle account.

# Contents

[Introduction](#introduction)

[Project Background](#project-background)

[Project Summary](#project-summary)

[Data Preparation](#data-preparation)

# Project Background
A chef must decide what the 'soup of the day' will be for the following month, ready to advertise to customers, based on the price of the main ingredient. This project focuses on the two main ingredients potatoes ('tatties') and tomatoes ('tommies').

Two types of time series models are produced; SARIMA vs Holt-Winters. AIC, BIC, MAE, MSE, and RMSE, in addition to a visual inspection of the models, are all used to assess model accuracy and to decide which model is the most appropriate for implementing.

The chosen model is imported into Power BI and visualisations are produced into a dashboard to imprpve accessibilty to the data and for clear decision making.

# Project Summary

## Question
Can a time series model be used to help forecast the price of soup ingredients, and therefore help make the correct decision on which ingredient to buy.

## Solution

## Outcome

# Data Preparation
The datasets are imported into Jupyter notebooks with the pandas, numpy, and matplotlib libraries imported.

<img width="824" alt="image" src="https://github.com/user-attachments/assets/a6c609b5-b4b5-4606-95e8-f304494d0214" />

## Import the datasets and explore
<img width="570" alt="image" src="https://github.com/user-attachments/assets/fc1c0e88-d8d9-4655-85fe-b572c104ac98" />

<img width="227" alt="image" src="https://github.com/user-attachments/assets/04d6b5ea-2289-473e-be9a-fcd3a4213622" />

## Check for null values and types of data
<img width="422" alt="image" src="https://github.com/user-attachments/assets/a335fcd4-3422-47e8-b711-67cb40c77c2e" />

There are no null values present and the data types appear accurate.

## Plot the time series data
<img width="551" alt="image" src="https://github.com/user-attachments/assets/100e5467-1f6b-420e-8ca9-227e1018c28f" />

## Observe for any trends with rolling mean calculated
<img width="559" alt="image" src="https://github.com/user-attachments/assets/90302e6f-c2c2-44e0-846b-d71842487f54" />

<img width="863" alt="image" src="https://github.com/user-attachments/assets/a2849857-13e6-46ea-a69f-89b9afea9dfa" />

## Decompose the time series
<img width="684" alt="image" src="https://github.com/user-attachments/assets/ee6b378a-1b10-4c67-8e5e-f7feaacb7cf5" />

<img width="644" alt="image" src="https://github.com/user-attachments/assets/48a286d8-3342-4c22-9ac2-c7705c896dd3" />

The decomposition demonstrates a long-term increase in the average prices. There are certain points of price acceleration and price deceleration. The seasonal plot appears very flat, indicating there isn't strong seasonal variation. The residual plot doesn't indicate any specific pattern, with fluctuations being scattered and therefore random.

The primary driver for average price of tatties appers to be a general increase over time, with very little impact from seasonsality, not any systematic error.

Following these observations, it would be best to proceed with an ARIMA model.

### Check for outliers by producing a Z score and identifying records with a price 4 SD away from the mean.
<img width="494" alt="image" src="https://github.com/user-attachments/assets/48a350f3-71bd-499d-bb18-d5d7c502b0d1" />

<img width="374" alt="image" src="https://github.com/user-attachments/assets/c0a59d8d-1ecd-4dd8-b0ba-19ae7639b633" />

### Remove outliers

<img width="634" alt="image" src="https://github.com/user-attachments/assets/b302736b-d4b3-43e4-96f4-8b7018420861" />

### Resample data into monthly increments

<img width="609" alt="image" src="https://github.com/user-attachments/assets/cc50a459-62aa-4799-8f21-e196c7034b16" />

### Plot the monthly data
<img width="511" alt="image" src="https://github.com/user-attachments/assets/229eca65-6110-4e38-964e-42e619f13728" />

<img width="758" alt="image" src="https://github.com/user-attachments/assets/dbf1925f-fc07-4113-a3b4-f1e63d31527c" />

<img width="296" alt="image" src="https://github.com/user-attachments/assets/eef3a904-59b3-41fa-8c7f-1d6e52edb756" />

### Check the quality of the data
<img width="352" alt="image" src="https://github.com/user-attachments/assets/4a0629c5-5eef-4ddd-81b1-a5ad8f59dde8" />

### Use the ADF Test to check for stationarity
<img width="877" alt="image" src="https://github.com/user-attachments/assets/866ea10b-4573-4ee0-a220-16b934d46e0f" />

### Divide the data into a training and a testing set

<img width="587" alt="image" src="https://github.com/user-attachments/assets/0c3f0ad8-9a2e-4bcf-8458-5c9d9326a6ec" />

<img width="728" alt="image" src="https://github.com/user-attachments/assets/2586e229-26cb-4519-b9ec-d9534f5e435a" />

### Perform the SARIMA model
Ensure correct libraries are installed.
<img width="367" alt="image" src="https://github.com/user-attachments/assets/c3f7d7ff-0db3-43fc-b9ca-dbb560e59969" />

Fit the model with the auto-arima function.

<img width="293" alt="image" src="https://github.com/user-attachments/assets/c86f2486-0611-4e4e-8876-656c38692958" />

<img width="433" alt="image" src="https://github.com/user-attachments/assets/52b6fa14-e6e6-41d5-ba92-79dcbba2d029" />

<img width="539" alt="image" src="https://github.com/user-attachments/assets/36cc63eb-1ced-42d5-9059-0cde41785f2a" />

The auto-arima function has detected that there is no seasonality, and the best fitting model has order (p,d,q)(2,0,1) i.e., there autoregressive element and a moving average element.

### Check model fit
Perform residual analysis
<img width="344" alt="image" src="https://github.com/user-attachments/assets/b1bdfed9-376c-4737-88c8-590de30e5ac9" />
<img width="745" alt="image" src="https://github.com/user-attachments/assets/0f726045-93fb-4c76-8e03-8ca8958d9d4e" />

Residual analysis demonstrates that the majority of the residuals are close to zero, indicating a good model fit. The residuals also demonstrate a relatively normal distribution.

Plot ACF residuals
<img width="497" alt="image" src="https://github.com/user-attachments/assets/45a240d9-2130-4d7b-82b6-9d18494457a3" />
ACF plot demonstrates no significant correlation.

View the AIC and BIC values
<img width="247" alt="image" src="https://github.com/user-attachments/assets/9b9d0bfc-de01-403c-92dc-b8ea34c5b1ab" />









### Applying Business Logic



### Bringing it all Together



### Validating the Outputs



### Displaying Results to the User


# Conclusion

## Outline



## Considerations



#  Bibliography

