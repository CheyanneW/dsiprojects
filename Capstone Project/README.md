# DSI16 - Capstone Project: 

# Recommender System for FMCGWholesale Trading

## Problem Statement

Fain Pte Ltd is an import/export company that deals with wholesale distribution of FMCG (Fast-Moving Consumer Goods) in Singapore. Their customers are local retailers, consisting of both the General Trade and Modern Trade. For this project, I am tasked to do some data analysis on the types of products that their customers are purchasing, and build a recommender system to recommend existing products that their customers might be interested in but have not purchased before. This recommender system will be used by the account managers to increase sales for their target customer, thus increasing overall revenue of the company. 

Increasing revenue comes in two ways: (i) increasing volume of items sold (ii) selling products with higher profit margin. In this project, we are particularly interested in looking at the quantity sold and the profit margin of the items sold. For case study, we will be using 'PINK BEAUTY PTE LTD' as they have average sales volume and we would like to push up the sales revenue from this company.

## Executive Summary

The raw dataset was provided by Fain Pte Ltd. It contains 5585 rows and 35 columns. In total, 93 companies were recorded and there are 549 unique products across 81 brands. It contains sales records across three months (July, August and September) in 2020. Data from September was incomplete as we extracted the data in mid-September. Other important informations include invoice number, quantity purchased, profit margin, unit price, total sales, category and brand. As the raw dataset had many missing information, we will need to clean and prepare the dataset before starting on analysis and building our recommendation system.

For data cleaning, the missing values for the columns 'category', 'brand' and 'invoice_no' were filled using the previous data, and the rest of the missing values were filled with zero. Datatypes for numerical data were converted from object to float or integer. Rows with negative profit margin, no unit cost and no unit proce information were dropped from the dataset. In total, 5.28% of rows were dropped.

We will be building five recommender systems and compare the results generated. The five systems are popularity model, content based filtering, user-based collaborative filtering, collaborative filtering with Singular Values Decomposition and Hybrid Model. After considering the pros and cons of each model, we can look at the combined results from all the five models and recommends the common items found in the top 10 recommendations from each model.

|Item Description|Popularity|CF|CB|SVD|Hybrid|
|:--|:--|:--|:--|:--|:--|
|Kirei-Kirei Handsoap AB+Antiseptic Agent Refill 200ml|Yes|No|Yes|No|Yes|
|Kirei-Kirei Handsoap AB Moist Peach Refill 200ml|Yes|No|Yes|No|Yes|
|Kirei-Kirei Handsoap AB Refreshing Grape Refill 200ml|Yes|Yes|No|No|No|
|Tiger Balm Mosquito Repellent Patch 10s|Yes|No|Yes|No|No|
|Colgate Toal 12 Clean Mint 150g|Yes|No|No|Yes|No|
|Colgate Total 12 Charcoal Deep Clean 150g|Yes|No|No|Yes|No|
|Simple Soap Bar Twinpack 2x125g|No|No|Yes|No|Yes|

Starting from this list, we make different recommendations to PINK BEAUTY over a period of next 3 months, and track which items that they will pick up and evaluate the models. We will also be tracking the total sales for these companies and determine how much the revenue increases with these recommendations.


(No dataset provided due to sensitive information)


### Data Collection

This dataset was collected from FAIN TRADING sales department. It contains sales records across three months (July, August and September) in 2020. Initially, there were 5585 entries (rows) and 39 columns. In total, we have 93 companies and 549 unique items in the record. Other important informations include quantity purchased, profit margin, unit price and category.

### Data Cleaning

We need to prepare the data by filling in all the missing entries, removing unwanted rows/columns, changing the data types of some columns and also extract meaningful data from the existing one. Many columns with numerical data are being stored as object, these need to be converted to float or int. There were rows with missing unit_cost or unit_price information and we will drop these rows. These rows with negative profit margin came from internal purchases or staff purchases as company benefits. We want to exclude these data for our analysis. In total, about 5.28% of rows were dropped. Data is now ready for EDA. After cleaning the data, we have 92 retail companies and 528 unique products.

To prepare our dataset for building our recommendation system, we need to extract item features for content-based filtering. From the dataset, the column 'category' will be used as one of the item features. Other item features that we can create includes size that we need to extract from the item description. We will classify them into 5 different classes: mini, small, medium, large and extra large.

Besides the size of item, we want to create sub-categories like 'shampoo', 'toothpaste' etc. We will extract meaningful words by using the count vectorizer to give us the sub-categories.


