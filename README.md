# Problem Satement #

Rossmann is a European drug distributor which operates over 3,000 drug stores across seven European countries. 
Since a lot of drugs come with a short shelf life, that is, they do not have a long expiry date, it becomes imperative for Rossmann to accurately forecast sales at their individual stores. 
Currently, the forecasting is taken care of by the store managers who are tasked with forecasting daily sales for the next six weeks.

As expected, store sales are influenced by many factors, including promotional campaigns, competition, state holidays, seasonality, and locality.

With thousands of individual managers predicting sales based on their unique circumstances and intuitions, the accuracy of the forecasts is quite varied. 
To overcome this problem, we are building a forecasting model to forecast the daily sales for the next six weeks. 

# Data #
Data for historical sales for 1,115 Rossmann stores has been provided.

Since the company is just embarking on this project, the scope has been kept to nine key stores across Europe. 
The stores are key for the company keeping in mind the revenue and historical prestige associated with them. These stores are numbered - 1,3,8,9,13,25,29,31 and 46.
The data for sales of each store is provided in aa file called train.csv and the data related to each store is in a file named store.csv.

# Approach Taken #

## Data preparation : ##
1) First inspected both the train and stores datasets and merged both of them.
2) Checked for null values . There were many null values contributed from the stores dataset. Since competition distance had just 3 missing values imputed those values with the mean. 
   The other columns in which values were missing , were all columns of variables which are not much of importance for our forecast . Hence imputed them with zeros .
3) Filtered the data for the 9 key stores.
4) Removed outliers at 99th percentile .
5) Standardised the sales and the customers column using Zscore standerdisation.

## EDA ##
1) Performed ADF test to check the staionarity of the sales time series.
2) Plotted a bar plot to check the effect of promo and promo2 variables on sales . Promo affected the sales positively and promo2 did not have any effect.
3) Dropped prom2 and a few other unnecessary columns.

## Checking cointegration ##
1) Performed Johansen's test to check the cointegration between the customers and sales time series. The result was a rank 2 .
   This indicates no cointegration between the 2 time series. However, rank 2 indicates both series are stationary we can go ahead an build a VAR or VARMAX model.
2) Splitting the data for testing and training . I set aside 6 weeks of data accross all 9 stores for testing.
3) Plotted the ACF and PACF plots to determine the highest order of lags to be used in the VARMAX model building.

## Model building and evaluation ##
1) First built a VAR Model with sales and customers data ,with no exogeneous variable and no moving average part. Calculated RMSE and MAPE . Both were very high . 
2) Hence built another model VARMAX Model with "Promo" as exogeneous variable and with moving average parameter. The RMSE improve da little bit .

# Conclusion # 
The model performance improves when moving average and exogeneous variables are added.

# Scope for further work #
Need to experiment with the AR and MA parameters and by dealing with the missing values differently to optimize the model.
Forecasting separatly for each store can also be tried to improve model performance.
   
