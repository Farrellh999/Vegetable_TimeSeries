# Data Science Project: Tommies or Tatties?

# Overview

This project uses a publicly available dataset which provides data on the cost of various ingredients, including potatoes ('tatties') and tomatoes ('tommies'), between the years 2013 and 2021.

The goal of this project is to explore the use of a time series forecast model as a tool to decide which main ingredient to use (tatties or tommies) for the soup of the month, based on the predicted cost of the two ingredients.

A SARIMA forecasting model was used to forecast cost of ingredients 12 months ahead. The results were then uploaded to PowerBI to create an interactive dashboard whereby the end-user can select the purchase month and be advised on which ingredient to buy according to how the forecasted price compared to the average price for that ingredient, and the price of the alternative ingredient.

### Positive Impact
The business will be able to make data-driven business decisions in order to optimise profit.

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
A chef must decide what the 'soup of the day' will be for the following month, ready to advertise to customers, based on the price of the main ingredient. This project focuses on assessing the forecasted price of the the two main ingredients potatoes ('tatties') and tomatoes ('tommies').

Whilst the raw data is daily, it was decided to transform this into monthly data as the original dataset made the python kernel run too slowly.

A time series SARIMA forecasting model is run following data cleansing in python. The auto-arima function uses AIC to detect the best fitting parameters of p,d,q, and P,D,Q using the test dataset. The model is then run on the training dataset and the model accuracy is assessed using r-squared, mean absolute error (MAE), and mean absolute percentage error (MAPE), in addition to a visual inspection.

Once satisfied with the model, the next 12 months are forecast and then merged into the original dataframe, before being exported to a csv file.

The chosen model is imported into Power BI where custom measures are produced and incorporated into visuals to enable the end-user to interpret the model guidance easily.

# Project Summary

## Question
Can a SARIMA time-series forecasting model help a chef to make the most cost effective decision when deciding on which soup to make and what main ingredient to buy?

## Solution

## Outcome

# Data Preparation
The dataset is a publicly available dataset from Kaggle.com that provides daily average/min/max prices/unit data on a variety of vegetables between a large, relatively recent date range (June 2013 and May 2021) in Nepal. The data is well structured and labelled, making interpretation easy. However, it does fail to specify the currency; for this project we choose to use GBP, but this should be explored further before implementing into a real-world scenario. The table headers do not make it abundantly clear that the minimum, maximum, and average are the prices per unit, and this would be important for context.

## Extract Data in Power Query
Prior to uploading to the Jupyter Notebook, PowerQuery was used to extract the target data (tommies and tatties) into separate datasets. Minor transformation were undertaken, such as changing dtype, and the data was grouped by ingredient, date, and summed the total price.
![image](https://github.com/user-attachments/assets/af151e56-87b3-48c6-a078-0c8b5b189624)
![image](https://github.com/user-attachments/assets/a2964ccb-2f01-490c-a006-c7e659b9412a)


## Load chosen libraries
The datasets are imported into Jupyter notebooks with the pandas, numpy, and matplotlib libraries imported.
![image](https://github.com/user-attachments/assets/0ce50dea-0a0f-4670-9434-250a6df08f2f)

## Import the datasets and explore
![image](https://github.com/user-attachments/assets/f4908683-2637-4a9d-9390-c7adbadcdb05)

## Check for null values and types of data
![image](https://github.com/user-attachments/assets/bd7cb94c-5060-472f-a472-75c98a16019b)
There are no null values present and the data types appear accurate.

## Plot the time series data
![image](https://github.com/user-attachments/assets/749ef627-51eb-4bb6-8fb5-5895ec031c3d)

## Perform Seasonal Decomposition using statsmodels
![image](https://github.com/user-attachments/assets/c114aa65-ef20-454e-a919-4826011e7ed7)
The trend demonstrated peaks and troughs over the course of each year, with a very slight upwards trend, and a significant spike between 2020 and 2021 (most likely due to the Covid-19 pandemic impacting the economy).

Residuals appear to be scattered at random, close to zero, indicating that trend and seasonality are responsible for the majority of variation of the data.

Seasonality is initially hugely difficult to visualise due to the number of data points. Therefore seasonality between a specific timeframe was performed to 'zoom' into the data.
![image](https://github.com/user-attachments/assets/582ca49b-201a-4948-aaa9-76d1d3bbd1ba)

The seasonality appears to have four major peaks each year, indicating quarterly seasonality. Consequently, we can be confident in proceeding with an ARIMA model.


### Check for outliers by producing a Z score and identifying records with an average price 3 SDs away from the mean
![image](https://github.com/user-attachments/assets/7f2533b1-bc6c-492c-be58-dd52c42216b3)

There appears to be a large number of outliers (62), comprising 2.25% of the dataset. Consequently, these are observed in a summary table.
![image](https://github.com/user-attachments/assets/38459d33-a5c2-4f18-b616-d3ff81577319)

Upon further inspection, it is clear that these outliers appear to fall during the Covid-19 panemic; as this was a significant and very real life event, it is important that we do not remove these outliers, but instead acknowledge them.

### Drop unnecessary columns
![image](https://github.com/user-attachments/assets/b8556ce7-868d-4d12-a0bf-b38e26768db1)

### Assess stationarity using the Augmented Dickey-Fuller test

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

### Compare Model Results with Actual
<img width="652" alt="image" src="https://github.com/user-attachments/assets/300a2b1a-9dfa-4e9e-a981-6daa451eb255" />

<img width="785" alt="image" src="https://github.com/user-attachments/assets/b5f30f24-7be6-490d-a0a4-0fe3371a24a6" />

From a visual inspection, the model does reflect the pattern fo the actual data, but it doensn't look particularly accurate.

### Check the forecast accuracy

<img width="521" alt="image" src="https://github.com/user-attachments/assets/5bcff958-9da6-4fc4-b61a-28bb3e915116" />

The mean average percentage error (MAPE) is 29%, indicating a relatively poor fitting model.









### Applying Business Logic



### Bringing it all Together



### Validating the Outputs



### Displaying Results to the User


# Conclusion

## Outline



## Considerations



#  Bibliography

