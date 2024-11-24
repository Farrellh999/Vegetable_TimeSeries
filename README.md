# KC_analysis
# Data Science Project: Dog Breed Popularity vs Genetic Ailments


## Overview

This project uses a publicly available dataset which provides data on the number of litters of dogs registered with the UK Kennel Club, broken down by breed, between the years 2013 and 2022. This dataset is merged with a further publicly available dataset which provides variables such as health issues risk, grooming needs, life span etc.

Using a logistic regression model, following data engineering, this project aims to uncover the relationship between the % change in litters being registered and whether the breed's health risk is high or not.

### Positive Impact


### Negative Impact
Public perception and opinion, breeds becoming extinct.

## Conclusion

##  Bibliography


# Data Sources
The dataset can be found at [https://www.kaggle.com/datasets/beckiku/uk-kennel-club-dog-breed-registrations]. This a public dataset, readily available to download to anyone who has a free Kaggle account.

# Contents

[Introduction](#introduction)

[Project Background](#project-background)

# Project Background
Dogs are notoriously know as man's best friend, with the vast displays on social media of 'doggos' further illustrating this point. However, with the emergence of social media, in addition to the displays of love and affection these animals bring, it is becoming more common to bare witness to the public debates surrounding the ethics of dog breeding and the health of certain dog breeds. This project aims to observe if there is any relationship between the number of litters being registered with the UK Kennel Club and the health risk category the breed falls into. 

If there is a positive relationship between the number of genetic ailments and popularity, this could raise an issue surrounding more dogs being born with a higher risk of illness, and therefore it could open up discussion surrounding the drivers for owning such dogs and exploring owner knowledge of the breeds and potential health ailments.

If there is a negative relationship between the number of genetic ailments and popularing, this could indicate that knowledge surrounding dog health is widely understood in the public and people are actively considering avoiding owning dogs with certain genetic ailments.

If no relationship is discovered, then it indicates that either:
* The public have little awareness of genetic ailments in dog breeds; or
* The public do not hold the possibility of genetic ailments as a strong enough deterrent to buying certain dog breeds.

# Project Summary

## Question
Are dogs with more genetic ailments becoming more popular?

## Solution

## Outcome


## Preparing the data
The datasets are imported into Jupyter notebooks with the pandas, numpy, and matplotlib libraries imported.

import pandas as pd  
import numpy as np  
import matplotlib.pyplot as plt  
import seaborn as sns  

## import the datasets and identify
kc_file = r'C:\Users\HannahFarrell\OneDrive - Greater Manchester GP Federations Toolkit\Desktop\Python\Apprenticeship\Assessments\DPS\kc_breed_registrations (1).csv'  
kc_data = pd.read_csv(kc_file, encoding ='ISO-8859-1')  

CHAR_file = r'C:\Users\HannahFarrell\OneDrive - Greater Manchester GP Federations Toolkit\Desktop\Python\Apprenticeship\Assessments\DPS\dog_characteristics.csv'  
char_data = pd.read_csv(CHAR_file)  

## Check for null values and types of data
kc_data.info()  
![image](https://github.com/user-attachments/assets/a7750b1a-db13-4133-be2c-32ac43c3fc3d)

The data appears to have imported correctly.  

## Remove commas from numerical data and convert to int.64

kc_columns_to_convert = ['2013','2014','2015','2016','2017','2018','2019','2020','2021','2022']  
kc_data[kc_columns_to_convert] = kc_data[kc_columns_to_convert].replace({',':''},regex=True).astype(int)  
kc_data.info()  
![image](https://github.com/user-attachments/assets/b0de7f02-3064-49a1-8cc2-7ac9c6be0676)

## Check for null values and types of data
char_data.info()  
![image](https://github.com/user-attachments/assets/34ebaa08-5ac8-44d3-aa5c-4c07d2d584ce)  

## Remove commas from numerical data and convert to int.64

char_data_to_convert = ['Average Weight (kg)']
char_data[char_data_to_convert] = char_data[char_data_to_convert].astype(float)

![image](https://github.com/user-attachments/assets/0f4d10d5-4261-429b-aafb-986b44339961)  
An error is identified.

## we have identified a record with an incontangible value for weight. This must be assumed to be an error and as we are unable to check this value with the original source of the data, on this occasion we will delete the record and highlight as a limitation.

The record with the invalid data is removed
char_data = char_data[char_data['Average Weight (kg)'] != '25-Jul']  
char_data_to_convert = ['Average Weight (kg)']  

Proceed to convert data to numbers  
char_data[char_data_to_convert] = char_data[char_data_to_convert].astype(float)  
char_data.info()  
![image](https://github.com/user-attachments/assets/abd57b6b-b5c1-429d-abb7-ac257d752414)
The average weight column now appears as a numerical data type (float64).

## Merge the datasets
## the plan is to merge the two datasets using the "breed" column as the key. Therefore need to check that there are no trailing spaces/extra spaces in the key column of each dataset.
kc_data['Extra_Spaces'] = kc_data['Breed'] != kc_data['Breed'].str.strip()  
print(kc_data['Extra_Spaces'].any())  
True

char_data['Extra_Spaces'] = char_data['Breed'] != char_data['Breed'].str.strip()  
print(char_data['Extra_Spaces'].any())  
False

The kc_data contains extra whitespace.

### Remove extra whitespace and check
kc_data['Breed']= kc_data['Breed'].str.strip()  
kc_data['Extra_Spaces'] = kc_data['Breed'] != kc_data['Breed'].str.strip()  
print(kc_data['Extra_Spaces'].any())  
False

### perform the merge. There are unequal numbers of breeds in the datasets. Therefore an inner join is used.

merged_data = pd.merge(kc_data, char_data, on='Breed', how='inner')  

## Check the merged metadata
merged_data.info()  
![image](https://github.com/user-attachments/assets/d6a91f15-c1b1-40bd-b5b9-773721963b48)  

## View the merged dataset
from IPython.display import display  
display(merged_data)  
![image](https://github.com/user-attachments/assets/ef910c4f-6c3e-4f53-8255-cf5418c86968)
The data has merged as expected.

## Calculate the dependent variable (% change in number of litters registered 2013 - 2022)

### Calculate the percentage change in numbers of litters registered between 2013 and 2022, handling incidences where the denominator is 0, if no litters were recorded in the first year.

merged_data['% Change'] = np.where(merged_data['2013'] != 0, ((merged_data['2022'] - merged_data['2013'])/merged_data['2013'])*100, None)  
print(merged_data)  
![image](https://github.com/user-attachments/assets/9eda518d-d891-4c99-ad7c-6794fdad5162)

### Check for null values
merged_data.info()  
![image](https://github.com/user-attachments/assets/4b5c06de-27e6-4d95-a98c-f2df0aaea35e)
There appears to be a null value in the new column, and it is also formatted incorrectly.

### Format % Change from object to numerical

merged_data['% Change'] = pd.to_numeric(merged_data['% Change'])  
![image](https://github.com/user-attachments/assets/920dd551-3168-495e-8fe6-1052c4fad837)
The data is now appearing as a numerical data type (float64)

### Replace null values with 0
merged_data['% Change'].fillna(0, inplace = True)  
merged_data.info()  
![image](https://github.com/user-attachments/assets/531535b7-1a7a-4453-be2e-e7d39fd1b852)
All 117 records now contain values (detected as non-null).

## Visualise the data
## Show data in a histogram
data = merged_data['% Change']

plt.hist(data, bins=6, color='skyblue', edgecolor='black')  
plt.show()  

![image](https://github.com/user-attachments/assets/7b1307c3-9c64-4156-af98-762538bdcd3f)
The histogram shows a high frequency of breeds with a negative % change i.e. there are a large number of breeds who have experienced a decline in the number of litters registered with the UK KC between 2013 and 2022.

I want to explore if there is a relationship between a breed having a high risk of health issues and the % change in the number of litters registered. 

## Create a "High Risk" column and format the result as binary.

merged_data['High Risk'] = merged_data['Health Issues Risk'].str.contains('High', case=False, na=False).astype(int)  

print(merged_data.head())  

![image](https://github.com/user-attachments/assets/87bc90e3-f3d4-447d-ac7e-8cf52ae86618)

## Check that the correct value has been assigned by viewing all rows of data, focused on the two columns.
selected_columns= merged_data[['High Risk','Health Issues Risk']]  
pd.set_option('display.max_rows', None)  
display(selected_columns)  

![image](https://github.com/user-attachments/assets/eae277a4-7b21-40a5-a5cd-675c459b8214)
All rows are displayed and checked to ensure every record identified as having a 'High' value in 'Health Issues Risk' has also been assigned value 1 in the 'High Risk' column.


### Applying Business Logic



### Bringing it all Together



### Validating the Outputs



### Displaying Results to the User


# Conclusion

## Outline



## Considerations



#  Bibliography

