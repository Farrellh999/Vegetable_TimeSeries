---
title: Project Summary
layout: default
---
[🏠]({{site.baseurl}}/index) • [⬅️]({{site.baseurl}}/Project-Background) • [➡️ Next: Data Preparation]({{site.baseurl}}/Data-Preparation) 

# Project Summary

## Problem
A chef must decide on the most cost-effective main ingredient of the 'soup of the month', in sufficient time to produce marketing materials to boost customer interest.

## Solution
* An automated pipeline was produced in Python to import the datasets for cleansing and analysis.
* Pmdarima's auto_arima function was used to produce time-series forecast models for the two main ingredients: tommies and tatties.
* The models were used to forecast average price for the future 12 months and exported into datasets.
* The data was imported into a PowerBI dashboard, where custom measures and columns were used to produce informative visuals, based on average price and comparison between ingredients, to guide the chef.


## Outcome
* The chef is able to ascertain which main ingredient is most cost effective to purchase in advance of producing marketing material to advertise the 'soup of the month'.
* The chef is able to financially plan for the upcoming months, taking into consideration any price fluctuations.
* Marketing materials are able to be produced far in advance in order to boost customer interest.

[➡️ Next: Data Preparation]({{site.baseurl}}/Data-Preparation)

[⬅️ Back]({{site.baseurl}}/Project-Background)

[🏠 Return to Homepage]({{site.baseurl}}/index)
