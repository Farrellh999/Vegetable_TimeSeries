# Data Science Project: Forecasting soup ingredients to assist decision-making for the most cost-effective production of soup.

# Overview

This project uses a publicly available dataset which provides data on the cost of various ingredients, including potatoes ('tatties') and tomatoes ('tommies'), between the years 2013 and 2021.

The goal of this project is to explore the use of a time series forecast model as a tool to decide which main ingredient to use (tatties or tommies) for the soup of the week, based on the predicted cost of the two ingredients i.e., whichever ingredient is forecast to be the least expensive for that month will be used and advertised as the 'soup of the day'.

### Positive Impact
The business will be able to hopefully make data-driven business decisions in order to optimise profit.

### Negative Impact
The forecast may influence the use of a certain ingredient at a time when that ingredient is of poor quality, leading to problems further down the line such as customer disatisfaction, the requirement to use additional ingredients to improve the quality of the soup.

## Conclusion

##  Bibliography

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

## Remove commas from numerical data and convert to int.64

kc_columns_to_convert = ['2013','2014','2015','2016','2017','2018','2019','2020','2021','2022']  
kc_data[kc_columns_to_convert] = kc_data[kc_columns_to_convert].replace({',':''},regex=True).astype(int)  
kc_data.info()  
![image](https://github.com/user-attachments/assets/b0de7f02-3064-49a1-8cc2-7ac9c6be0676)

## Check for null values and types of data
char_data.info()  
![image](https://github.com/user-attachments/assets/34ebaa08-5ac8-44d3-aa5c-4c07d2d584ce)  




### Applying Business Logic



### Bringing it all Together



### Validating the Outputs



### Displaying Results to the User


# Conclusion

## Outline



## Considerations



#  Bibliography

