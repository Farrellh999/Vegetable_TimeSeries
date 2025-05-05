---
layout: default
title: Dashboard
---
[➡️ Next: Business Impact]({{site.baseurl}}/Business-Impact) • [⬅️ Back]({{site.baseurl}}/Analysis) • [🏠 Return to Homepage]({{site.baseurl}}/index)

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

## Dashboard Structure
### 1) Datasets were loaded into PowerBI
Each dataset was transformed in PowerQuery:
* Data types were checked and adjusted as necessary.
* The date column was given the header 'Date'.
* The Average Price and Forecast Price columns were unpivoted.
* The 'Value' column was renamed 'Price'.
* The 'Price' column was rounded to 2 decimal points

![image](https://github.com/user-attachments/assets/5c2cd0ae-cfcf-41a5-ad4c-644660d87fab)
Before unpivoting Tommies
![image](https://github.com/user-attachments/assets/813be749-dac6-420b-8317-056bca6d80b2)
After unpivoting Tommies
![image](https://github.com/user-attachments/assets/fc5ff783-e0fa-481d-8077-0c5254dbb67c)
Before unpivoting Tatties
![image](https://github.com/user-attachments/assets/530cb485-f0e2-4aa2-b0aa-7849bbafeb9d)
After unpivoting Tatties

### 2) A date table was produced
The date table was produced using the min and max values in one of the datasets (each dataset has the same timeframe).

![image](https://github.com/user-attachments/assets/020fe07a-ee5a-4d4d-8e9f-651ff3c0d4ce)

A Month-Year column was added to the date table.

![image](https://github.com/user-attachments/assets/9b84addb-a9d0-42c3-9cb3-d0ff12932130)

### 3) Create relationships
One-to-one relationships were built between the tommies and tatties datasets and the date table, using the 'Date' columns.

![image](https://github.com/user-attachments/assets/99816398-917f-4fc2-8537-a3a4211e5840)

### 4) Create custom measures
A custom measure was created in each dataset to produce the average price.

![image](https://github.com/user-attachments/assets/d0c2f0d5-0e18-4c83-8689-b3c4f217a8b6)
![image](https://github.com/user-attachments/assets/285c3011-3b85-4663-9130-57866133f0e5)

### 5) Create custom columns
Custom columns were created in each dataset to identify:
* If the price for each month is above/below the average for that ingredient

![image](https://github.com/user-attachments/assets/df8fa378-7d1e-449f-8463-49a9d5f8d94e)
![image](https://github.com/user-attachments/assets/0b730f70-5718-4f87-a1f6-3bc01b025377)

* If the price for each month is higher or lower than the price for the respective month in the alternative ingredient table

![image](https://github.com/user-attachments/assets/ab6f1f58-4b5b-4da2-adf1-50f07c02d208)
![image](https://github.com/user-attachments/assets/35d2c703-b21a-4a72-af5d-953c10428ed6)

* Taking into consideration the above, whether it is advised to buy or not.

![image](https://github.com/user-attachments/assets/9b96acbe-8031-4ba7-8f76-7d5712a15adb)
![image](https://github.com/user-attachments/assets/0c29fdf6-c422-4f2c-b8fb-631a49ecce09)










[➡️ Next: Business Impact]({{site.baseurl}}/Business-Impact)

[⬅️ Back]({{site.baseurl}}/Analysis)

[🏠 Return to Homepage]({{site.baseurl}}/index)
