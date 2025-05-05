---
title: Analysis
layout: default
---
[➡️ Next: Dashboard]({{site.baseurl}}/Dashboard) • [⬅️ Back]({{site.baseurl}}/Data-Preparation) • [🏠 Return to Homepage]({{site.baseurl}}/index)

# Analysis - Run the ARIMA model
### 1) Import the necessary libraries
![image](https://github.com/user-attachments/assets/c373dc90-ac2e-4182-8a89-0b6185e38922)
The auto_arima function is imported from pmdarima. This will automatically detect values for (p,d,q)(P,D,Q).

### 2) Fit the model
![image](https://github.com/user-attachments/assets/9716c8c3-461e-4c75-8fe5-9944a024c8ec)
Seasonality is stated as 'True' and defined as every 12 months (m). Differencing is explicitly defined as 1 to start with.
Trace is set to 'True' so a detailed record of each model attempt is produced.
Warnings are suppressed to produce a cleaner output.
Stepwise is set to 'False' in order to improve the chances of producing a better fitting model
n_jobs = -1 is incorporated to allow for parallel processing using mutliple CPU code, to speed up the model.

![image](https://github.com/user-attachments/assets/58486873-b292-4216-b513-d98b80003393)
The returned model is ARIMA(0,1,1)(2,1,0)[12]

### 3) Predict values and plot against Test data

![image](https://github.com/user-attachments/assets/19a588df-68fc-4113-9047-8b3cae3f7380)
![image](https://github.com/user-attachments/assets/078c9fc4-7d24-4e22-90c4-aed0f96a0520)
The visual shows that the predicted values appear to follow the testing data fairly well. However accuracy metrics are required to further assess this.

### 4) Test Accuracy
![image](https://github.com/user-attachments/assets/677df5ce-54cb-4195-bd35-1e3b789798fc)
An R-squared of 0.41 indicates that the model fits fairly well. The model explains 41% of the variance in the data.
The mean absolute error (MAE) of 11.02 implies that there is a low magnitude of error.
The mean absolute percentage error (MAPE) of 19.28 indicates that predictions will be off by approximately 20%. 
In summary, the model is fitting ok, however we can look to improve it.

### 5) Iterate the model fitting (1)
We can try to remove the specified differencing to allow the auto_arima to automatically detect this and assess how this performs.

![image](https://github.com/user-attachments/assets/85bc3cd2-bf8e-405a-b562-7a4970516989)
![image](https://github.com/user-attachments/assets/8896e4e6-49a9-4226-8b51-82d2ebb8d66b)
![image](https://github.com/user-attachments/assets/aa2ded90-30cb-406d-8db0-831833087303)
![image](https://github.com/user-attachments/assets/cebd056d-da93-4f40-8559-4b9d18419924)
![image](https://github.com/user-attachments/assets/5b91ebaf-b9ed-49b8-8213-5a0c8b91aa0a)

Allowing auto_arima to automatically detect differencing has produced a less accurate model:
MSE = 15 --> higher magnitude of error
MAPE = 26 --> predictions are off by a higher %

### 6) Iterate the model fitting (2)
As the PACF has significant peaks at lags 1, 2, 5, and 9 this could indicate that values could be strongly affected by values from 2 months ago. We can test changing seasonality to  2 i.e. m=2.

The produced the following chart which clearly identifies it is a very poorly fitting model.
![image](https://github.com/user-attachments/assets/c3b5c290-981d-4086-8898-5ebff674a1b0)

Therefore, we revert to using the model ARIMA(0,1,1)(2,1,0)[12].

### 7) Residual Analysis
Residual analysis in a residual distribution plot demonstrates that the residuals are normally distributed. This indicates that the assumptions made by he model are valid.
![image](https://github.com/user-attachments/assets/2b8b1807-d810-4584-8cb8-19b773adc89d)
![image](https://github.com/user-attachments/assets/e74266f3-893f-400b-92ef-1a7243937267)

## Forecast Future Values
### 1) Forecast vales for future dates
The index is set to the monthly frequency.
A period of 12 future dates are generated using the test dataset index.
The forecasted data is then combined with the future dates.
![image](https://github.com/user-attachments/assets/6263e366-fa7b-46a8-a462-2f09c2942e05)
![image](https://github.com/user-attachments/assets/2e6bc544-3297-4d79-b715-47d9571a1e1c)

### 2) Visualise forecast values and actual values
![image](https://github.com/user-attachments/assets/155d4337-fe2f-4278-8a29-b4455d5bf4f2)
The forecast values are shown in orange

## Export Data
### 1) Combine the dataframes
The dataframe containing forecasted values is merged on the indices with the monthly dataset. This ensures that all values from each dataframe are kept.
![image](https://github.com/user-attachments/assets/4de20324-8a2e-4eff-b160-d5bb4d9d68fa)

### 2) Export to CSV
![image](https://github.com/user-attachments/assets/d60b6199-cd6b-4144-9f55-faa0df005a8a)

## Repeat the Process for Tommies Data
The process was repeated for the tommies dataset. The key differences were as follows:

### Outliers
* Outliers were identified to be a minimal number of values and were therefore removed

### PACF
* PACF ony had significant peaks at lags 1, 4, and 8
* ![image](https://github.com/user-attachments/assets/47c4ba2d-aa50-49f3-b936-ce0979ba05fd)

### Stationarity
* ADF confirmed the monthly data to be stationary so differencing was not required
* ![image](https://github.com/user-attachments/assets/54bb1c1a-2c86-4cb6-b14b-baee456cbfba)
* However, upon running the model, it produced a better fit if D=1

### Seasonality
* seasonality - quarterly - peaks every 12-13 weeks.
* m = 3
* ![image](https://github.com/user-attachments/assets/f9efbf32-933e-4c36-a8b9-f2b7afb5c470)
* Whilst seasonality had been detected as quarterly initially, when this was incorporated into the model, poor results were given
* ![image](https://github.com/user-attachments/assets/4d3223c1-3d4e-404a-bbe4-8fc361fbc6d8)

* Therefore, bi-annual seasonality and annual seasonality were attempted to assess if these were stronger trends.

### Bi-Annual
* m = 6
* Accuracy metrics were poor still
![image](https://github.com/user-attachments/assets/826f7f86-bd7b-4494-9cf1-e31daae2ea62)

### Annual
* m = 12
* * Whilst still not fantastic, the accuracy metrics were far better and the data visual demonstrates a much better fit
![image](https://github.com/user-attachments/assets/811bc77a-b96a-4224-bd0d-f6510529422a)
![image](https://github.com/user-attachments/assets/29c25474-d7df-4a29-babf-3e1ed54416e4)

[🔝 Back to Top](#top)

[➡️ Next: Dashboard]({{site.baseurl}}/Dashboard)

[⬅️ Back]({{site.baseurl}}/Data-Preparation)

[🏠 Return to Homepage]({{site.baseurl}}/index)
