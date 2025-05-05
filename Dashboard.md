---
layout: default
title: Dashboard
---
# Dashboard
<iframe title="Vegetables dashboard" width="600" height="373.5" src="https://app.powerbi.com/view?r=eyJrIjoiOWE5OTFjMDgtYWNiYS00M2FmLTgxOTgtMzljMTg5YzcyMTNiIiwidCI6IjNkZDc2Mzc0LThhNTEtNGZhZS05ZjMyLWQ2OGI5OWI3ZGVjNCJ9" frameborder="0" allowFullScreen="true"></iframe>

The above interactive dashboard has been produced in PowerBI. 

The dashboard allows the chef to select the month they wish to make the purchase, and the dashboard uses the forecast values to provide guidance on which ingredient to buy.

The guidance is provided using the following:
* A custom measure for each dataset is used to find the average prices for tommies and tatties.
* A custom column is added which uses the average prices to indicate for each month whether the forecasted price is above or below average.
* A custom column is added in each dataset which compares the forecasted tommie price with the forecasted tattie price, and deciphers the cheaper of the two.
* A final custom column is produced in each table which follows the below conditions:
    1. Forecast price < average AND < other ingredient = Buy - good price
    2. Forecast price < average AND > other ingredient = Do not buy
    3. Forecast price > average AND < other ingredient = Buy with caution
    4. Forecast prie > average AND > other ingredient = Do not buy


[➡️ Next: Business Impact]({{site.baseurl}}/Business-Impact)

[⬅️ Back]({{site.baseurl}}/Analysis)

[🏠 Return to Homepage]({{site.baseurl}}/index)
