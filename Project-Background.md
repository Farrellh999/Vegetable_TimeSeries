---
title: Project Background
layout: default
---

[➡️ Next: Project Summary]({{site.baseurl}}/Project-Summary) * [⬅️ Back]({{site.baseurl}}/Introduction) * [🏠 Return to Homepage]({{site.baseurl}}/index)

# Project Background
A chef must decide what the 'soup of the day' will be for the following month, ready to advertise to customers, based on the price of the main ingredient. This project focuses on assessing the forecasted price of the the two main ingredients potatoes ('tatties') and tomatoes ('tommies').

Whilst the raw data is daily, it was decided to transform this into monthly data as the original dataset made the python kernel run too slowly.

A time series SARIMA forecasting model is run following data cleansing in python. The auto-arima function uses AIC to detect the best fitting parameters of p,d,q, and P,D,Q using the test dataset. The model is then run on the training dataset and the model accuracy is assessed using r-squared, mean absolute error (MAE), and mean absolute percentage error (MAPE), in addition to a visual inspection.

Once satisfied with the model, the next 12 months are forecast and then merged into the original dataframe, before being exported to a csv file.

The chosen model is imported into Power BI where custom measures are produced and incorporated into visuals to enable the end-user to interpret the model guidance easily.

[➡️ Next: Project Summary]({{site.baseurl}}/Project-Summary) * [⬅️ Back]({{site.baseurl}}/Introduction) * [🏠 Return to Homepage]({{site.baseurl}}/index)
