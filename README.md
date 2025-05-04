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

### Assess stationarity using the Augmented Dickey-Fuller test from statsmodels
![image](https://github.com/user-attachments/assets/94eb3647-e839-4f75-8450-966cc038dd1d)
Stationarity is confirmed and therefore no differencing is required.

### Resample data into monthly increments
Previous attempts at running the model on daily data had proved to make my computer crash! I higher spec computer is needed, but we settle at this stage for adjusting to monthly data, using teh average value.
![image](https://github.com/user-attachments/assets/a18c20f9-620d-40c9-af57-5b0f87e03a6d)

### Perform seasonal decomposition on the monthly data

![image](https://github.com/user-attachments/assets/07540150-b2fa-4eb5-b83b-e94fbe0b6a93)
The monthly data illustrates a major peak every 12 months, indicating that seasonlity is 12.

### Produce ACF and PACF charts to assess pdq,PDQ
![image](https://github.com/user-attachments/assets/9c7ebf67-9ba6-4868-90f5-fd3ee07b4681)

ACF demonstrates a sinusoidal wave indicating seasonality and potentially an AR component. 
The PACF has significant peaks at lags 1, 2, 5, 9, 14, indicating strong seasonality.

### Check stationarity of the monthly data
![image](https://github.com/user-attachments/assets/4ab70b99-fc0a-438c-a477-2269ddb3258e)
The monthly data is confirmed as non-stationary. Therefore we could proceed with differencing manually, however as we are using the auto-arima function, we will make a note to set d as 1.

### Split data into training and testing data sets
![image](https://github.com/user-attachments/assets/d462af23-c9fc-4952-a3b8-1c3cbd0c3898)
![image](https://github.com/user-attachments/assets/bfa2d0f3-fc36-48b0-afe6-c2587038e8e0)

# Analysis: Run the ARIMA model
### Import the necessary libraries
![image](https://github.com/user-attachments/assets/c373dc90-ac2e-4182-8a89-0b6185e38922)
The auto_arima function is imported from pmdarima. This will automatically detect values for (p,d,q)(P,D,Q).

### Fit the model
![image](https://github.com/user-attachments/assets/9716c8c3-461e-4c75-8fe5-9944a024c8ec)
Seasonality is stated as 'True' and defined as every 12 months (m). Differencing is explicitly defined as 1 to start with.
Trace is set to 'True' so a detailed record of each model attempt is produced.
Warnings are suppressed to produce a cleaner output.
Stepwise is set to 'False' in order to improve the chances of producing a better fitting model
n_jobs = -1 is incorporated to allow for parallel processing using mutliple CPU code, to speed up the model.

![image](https://github.com/user-attachments/assets/58486873-b292-4216-b513-d98b80003393)
The returned model is ARIMA(0,1,1)(2,1,0)[12]

### Predict values and plot against Test data

![image](https://github.com/user-attachments/assets/19a588df-68fc-4113-9047-8b3cae3f7380)
![image](https://github.com/user-attachments/assets/078c9fc4-7d24-4e22-90c4-aed0f96a0520)
The visual shows that the predicted values appear to follow the testing data fairly well. However accuracy metrics are required to further assess this.

### Test Accuracy
![image](https://github.com/user-attachments/assets/677df5ce-54cb-4195-bd35-1e3b789798fc)
An R-squared of 0.41 indicates that the model fits fairly well. The model explains 41% of the variance in the data.
The mean absolute error (MAE) of 11.02 implies that there is a low magnitude of error.
The mean absolute percentage error (MAPE) of 19.28 indicates that predictions will be off by approximately 20%. 
In summary, the model is fitting ok, however we can look to improve it.

### Iterate the model fitting (1)
We can try to remove the specified differencing to allow the auto_arima to automatically detect this and assess how this performs.

![image](https://github.com/user-attachments/assets/85bc3cd2-bf8e-405a-b562-7a4970516989)
![image](https://github.com/user-attachments/assets/8896e4e6-49a9-4226-8b51-82d2ebb8d66b)
![image](https://github.com/user-attachments/assets/aa2ded90-30cb-406d-8db0-831833087303)
![image](https://github.com/user-attachments/assets/cebd056d-da93-4f40-8559-4b9d18419924)
![image](https://github.com/user-attachments/assets/5b91ebaf-b9ed-49b8-8213-5a0c8b91aa0a)

Allowing auto_arima to automatically detect differencing has produced a less accurate model:
MSE = 15 --> higher magnitude of error
MAPE = 26 --> predictions are off by a higher %

### Iterate the model fitting (2)
As the PACF has significant peaks at lags 1, 2, 5, and 9 this could indicate that values could be strongly affected by values from 2 months ago. We can test changing seasonality to  2 i.e. m=2.

The produced the following chart which clearly identifies it is a very poorly fitting model.
![image](https://github.com/user-attachments/assets/c3b5c290-981d-4086-8898-5ebff674a1b0)

Therefore, we revert to using the model ARIMA(0,1,1)(2,1,0)[12].

### Residual Analysis
Residual analysis in a residual distribution plot demonstrates that the residuals are normally distributed. This indicates that the assumptions made by he model are valid.
![image](https://github.com/user-attachments/assets/2b8b1807-d810-4584-8cb8-19b773adc89d)
![image](https://github.com/user-attachments/assets/e74266f3-893f-400b-92ef-1a7243937267)

# Forecast Future Values

















### Applying Business Logic



### Bringing it all Together



### Validating the Outputs



### Displaying Results to the User


# Conclusion

## Outline



## Considerations



#  Bibliography

