# DataCoSupplyChain

This code sample demonstrates how to build visualizations using Qlik Cloud | Analytics.  The source data for this project, the DataCo SMART SUPPLY CHAIN FOR BIG DATA ANALYSIS, is found on the Data Mendley website [here.](https://data.mendeley.com/datasets/8gx2fvg2k6/1)  

The dataset contains order transaction data for a single company from 1 January 2015 to 31 January 2018.  The dataset contains 52 columns of data with information about product and product price, customer, order location, and company profit.

An export of the Qlik app can be found [here.](https://github.com/clkessel/DataCoSupplyChain/blob/main/DataCoSupplyChain.qvf)

The load script for this app was straightforward with minimal transformation of the original dataset columns. 

The app itself features a single sheet consisting of a series of visualizations in a layout container.  The layout container provides better flexibility in adjusting the sizing and spacing of visualizations on the sheet, and if the visualization borders are set to the same color as the background of the container, provides a more seamless view of the sheet as a whole.  Below is a snapshot of the app, which we will discuss in more detail below.

![app_view](https://github.com/clkessel/DataCoSupplyChain/blob/main/app_view.png)

Beneath the made up company name of "Global Shipping, Inc.", the app uses an expression to grab the minimum and maximum order dates found within the dataset to provide context to the timeframe of the data.  The expression used is:

<div align="center">min({1}[Order Date]) & ' - ' & max({1}[Order Date])</div><br>

The top right of the app features several Key Performance Indicators (KPIs) of the dataset, such as Total Customers or Average Sales per Customer.  The first row of three visualizations display an overview of the Payment Types, Profit per Quarter, and Delivery Status from a historical perspective.  The bottom right shows a boxplot, faceted along the Customer Segment, of the sum of sales per order.  The bottom left and bottom center visualizations show only 2018 data, the last year in the dataset, or what could be considered "current year data".  

The bottom left pie chart uses the following set analysis to filter to current year only data:

<div align="center">Count({<"=Year([Order Date])"={'2018'}>}[Delivery Status])</div><br>

The bottom center horizontal bar chart uses the following set analysis to filter to current year only data:

<div align="center">Sum({<"=Year([Order Date])"={'2018'}>} [Order Profit Per Order])</div><br>
