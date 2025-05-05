---
layout: default
title: Conclusion & Recommendations
---
[🏠]({{site.baseurl}}/index) • [⬅️]({{site.baseurl}}/Business-Impact) • [➡️ Next: References]({{site.baseurl}}/References)

# Conclusion & Recommendations
An ARIMA forecasting model has been used to assist a chef in making data-driven business decisions on buying ingredients. This will have multiple financial benefits to the chef and provide a longer term view of how the chef may need to structure their business model.

### Accuracy
Whilst the model is relatively accurate and provides insights not available when not having the forecast, the model certainly has room for improvement. The MAPE for the tatties model is approximately 20%, and for the tommies model it was approximately 35%. Therefore the model should be used with caution with the understanding that forecasted prices may be 20% and 35% incorrect for tatties and tommies respectively.

If the model were to be run using the daily data initially shown in the raw dataset, it is more likely a model with higher accuracy would be produced due to the higher number of data points and more granular insights into trend. In order to perform this, a much higher performing laptop would be required in order for the Python kernel to handle the huge volume of data.

### Specificity of ingredients
Whilst these models run on the generic ingredient names, the actual raw data breaks each ingredient down into the different varieties e.g. red potatoe, white potatoe. It would be beneficial to perform analysis on the data at a more granular level for each of the different varieties, which would potentially provide a greater insight into trends for the different varieties of ingredients.

### Code structure
The current python script is written in a monolithic fashion which makes debugging and reusing the code difficult. It would be far better to write the code in a modular fashion in accordance with software engineering best practice, including unit tests to check the functions. This would enable the code to be applied to multiple different data sets, reusing the functions, without the need for timely re-writing of code.

### Additional data
It would be interesting to explore data sets covering the same time period looking at other potential contributing factors e.g. rainfall, country GDP. Further exploratory analysis could be performed to assess if there was a correlation between these new variables and incorporate them into the forecast model.

[➡️ Next: References]({{site.baseurl}}/References)

[⬅️ Back]({{site.baseurl}}/Business-Impact)

[🏠 Return to Homepage]({{site.baseurl}}/index)
