---
title: Data Preparation
layout: default
---
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

[🔝 Back to Top](#top)

➡️ [Next: Analysis]({{site.baseurl}}/Analysis)

⬅️ [Back]({{site.baseurl}}/Project-Summary)

🏠 [Return to Homepage]({{site.baseurl}}/index)
