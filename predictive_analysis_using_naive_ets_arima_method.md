---
Title: "Data Predictive Analysis Using Naive, ETS And Arima Methods"
Author: "Muhammad Pajrul Palah"
Date: "2023-10-23"
Output: html_document
---

# Sales Revenue Prediction Using Naive, ETS and Arima Method in Rstudio

In this session we want to predict the total profit sales in current period 2023 from january until December using **data dummy** with dataset name sales_company_riseUp.


Before it you can generate this data below to CSV file and upload it in Rstudio. 
```{r}
date,revenue,cost,profit
2023-01-01,56789,45678,11111
2023-01-02,78965,65432,13533
2023-01-03,98654,78542,20112
2023-01-04,10236,8456,1780
2023-01-05,43124,32678,10446
2023-01-06,76893,62341,14552
2023-01-07,23456,19874,3578
2023-01-08,98765,83245,15520
2023-01-09,45678,36987,8689
2023-01-10,54321,43216,11105
2023-01-11,23456,18974,4482
2023-01-12,87654,73456,14298
2023-01-13,12345,10876,1470
2023-01-14,67890,56543,11347
2023-01-15,56789,45678,11111
2023-01-16,78965,65432,13533
2023-01-17,98654,78542,20112
2023-01-18,10236,8456,1780
2023-01-19,43124,32678,10446
2023-01-20,76893,62341,14552
2023-01-21,23456,19874,3578
2023-01-22,98765,83245,15520
2023-01-23,45678,36987,8689
2023-01-24,54321,43216,11105
2023-01-25,23456,18974,4482
2023-01-26,87654,73456,14298
2023-01-27,12345,10876,1470
2023-01-28,67890,56543,11347
2023-01-29,56789,45678,11111
2023-01-30,78965,65432,13533
2023-01-31,98654,78542,20112
2023-02-01,10236,8456,1780
2023-02-02,43124,32678,10446
2023-02-03,76893,62341,14552
2023-02-04,23456,19874,3578
2023-02-05,98765,83245,15520
2023-02-06,45678,36987,8689
2023-02-07,54321,43216,11105
2023-02-08,23456,18974,4482
2023-02-09,87654,73456,14298
2023-02-10,12345,10876,1470
2023-02-11,67890,56543,11347
2023-02-12,56789,45678,11111
2023-02-13,78965,65432,13533
2023-02-14,98654,78542,20112
2023-02-15,10236,8456,1780
2023-02-16,43124,32678,10446
2023-02-17,76893,62341,14552
2023-02-18,23456,19874,3578
2023-02-19,98765,83245,15520
2023-02-20,45678,36987,8689
2023-02-21,54321,43216,11105
2023-02-22,23456,18974,4482
2023-02-23,87654,73456,14298
2023-02-24,12345,10876,1470
2023-02-25,67890,56543,11347
2023-02-26,56789,45678,11111
2023-02-27,78965,65432,13533
2023-02-28,98654,78542,20112
2023-03-01,10236,8456,1780
2023-03-02,43124,32678,10446
2023-03-03,76893,62341,14552
2023-03-04,23456,19874,3578
2023-03-05,98765,83245,15520
2023-03-06,45678,36987,8689
2023-03-07,54321,43216,11105
2023-03-08,23456,18974,4482
2023-03-09,87654,73456,14298
2023-03-10,12345,10876,1470
2023-03-11,67890,56543,11347
2023-03-12,56789,45678,11111
2023-03-13,78965,65432,13533
2023-03-14,98654,78542,20112
2023-03-15,10236,8456,1780
2023-03-16,43124,32678,10446
2023-03-17,76893,62341,14552
2023-03-18,23456,19874,3578
2023-03-19,98765,83245,15520
2023-03-20,45678,36987,8689
2023-03-21,54321,43216,11105
2023-03-22,23456,18974,4482
2023-03-23,87654,73456,14298
2023-03-24,12345,10876,1470
2023-03-25,67890,56543,11347
2023-03-26,56789,45678,11111
2023-03-27,78965,65432,13533
2023-03-28,98654,78542,20112
2023-03-29,10236,8456,1780
2023-03-30,43124,32678,10446
2023-03-31,76893,62341,14552
2023-04-01,23456,19874,3578
2023-04-02,98765,83245,15520
2023-04-03,45678,36987,8689
2023-04-04,54321,43216,11105
2023-04-05,23456,18974,4482
2023-04-06,87654,73456,14298
2023-04-07,12345,10876,1470
2023-04-08,67890,56543,11347
2023-04-09,56789,45678,11111
2023-04-10,78965,65432,13533
2023-04-11,98654,78542,20112
2023-04-12,10236,8456,1780
2023-04-13,43124,32678,10446
2023-04-14,76893,62341,14552
2023-04-15,23456,19874,3578
2023-04-16,98765,83245,15520
2023-04-17,45678,36987,8689
2023-04-18,54321,43216,11105
2023-04-19,23456,18974,4482
2023-04-20,87654,73456,14298
2023-04-21,12345,10876,1470
2023-04-22,67890,56543,11347
2023-04-23,56789,45678,11111
2023-04-24,78965,65432,13533
2023-04-25,98654,78542,20112
2023-04-26,10236,8456,1780
2023-04-27,43124,32678,10446
2023-04-28,76893,62341,14552
2023-04-29,23456,19874,3578
2023-04-30,98765,83245,15520
2023-05-01,45678,36987,8689
2023-05-02,54321,43216,11105
2023-05-03,23456,18974,4482
2023-05-04,87654,73456,14298
2023-05-05,12345,10876,1470
2023-05-06,67890,56543,11347
2023-05-07,56789,45678,11111
2023-05-08,78965,65432,13533
2023-05-09,98654,78542,20112
2023-05-10,10236,8456,1780
2023-05-11,43124,32678,10446
2023-05-12,76893,62341,14552
2023-05-13,23456,19874,3578
2023-05-14,98765,83245,15520
2023-05-15,45678,36987,8689
2023-05-16,54321,43216,11105
2023-05-17,23456,18974,4482
2023-05-18,87654,73456,14298
2023-05-19,12345,10876,1470
2023-05-20,67890,56543,11347
2023-05-21,56789,45678,11111
2023-05-22,78965,65432,13533
2023-05-23,98654,78542,20112
2023-05-24,10236,8456,1780
2023-05-25,43124,32678,10446
2023-05-26,76893,62341,14552
2023-05-27,23456,19874,3578
2023-05-28,98765,83245,15520
2023-05-29,45678,36987,8689
2023-05-30,54321,43216,11105
2023-05-31,23456,18974,4482
2023-06-01,87654,73456,14298
2023-06-02,12345,10876,1470
2023-06-03,67890,56543,11347
2023-06-04,56789,45678,11111
2023-06-05,78965,65432,13533
2023-06-06,98654,78542,20112
2023-06-07,10236,8456,1780
2023-06-08,43124,32678,10446
2023-06-09,76893,62341,14552
2023-06-10,23456,19874,3578
2023-06-11,98765,83245,15520
2023-06-12,45678,36987,8689
2023-06-13,54321,43216,11105
2023-06-14,23456,18974,4482
2023-06-15,87654,73456,14298
2023-06-16,12345,10876,1470
2023-06-17,67890,56543,11347
2023-06-18,56789,45678,11111
2023-06-19,78965,65432,13533
2023-06-20,98654,78542,20112
2023-06-21,10236,8456,1780
2023-06-22,43124,32678,10446
2023-06-23,76893,62341,14552
2023-06-24,23456,19874,3578
2023-06-25,98765,83245,15520
2023-06-26,45678,36987,8689
2023-06-27,54321,43216,11105
2023-06-28,23456,18974,4482
2023-06-29,87654,73456,14298
2023-06-30,12345,10876,1470
2023-07-01,67890,56543,11347
2023-07-02,56789,45678,11111
2023-07-03,78965,65432,13533
2023-07-04,98654,78542,20112
2023-07-05,10236,8456,1780
2023-07-06,43124,32678,10446
2023-07-07,76893,62341,14552
2023-07-08,23456,19874,3578
2023-07-09,98765,83245,15520
2023-07-10,45678,36987,8689
2023-07-11,54321,43216,11105
2023-07-12,23456,18974,4482
2023-07-13,87654,73456,14298
2023-07-14,12345,10876,1470
2023-07-15,67890,56543,11347
2023-07-16,56789,45678,11111
2023-07-17,78965,65432,13533
2023-07-18,98654,78542,20112
2023-07-19,10236,8456,1780
2023-07-20,43124,32678,10446
2023-07-21,76893,62341,14552
2023-07-22,23456,19874,3578
2023-07-23,98765,83245,15520
2023-07-24,45678,36987,8689
2023-07-25,54321,43216,11105
2023-07-26,23456,18974,4482
2023-07-27,87654,73456,14298
2023-07-28,12345,10876,1470
2023-07-29,67890,56543,11347
2023-07-30,56789,45678,11111
2023-07-31,78965,65432,13533
2023-08-01,98654,78542,20112
2023-08-02,10236,8456,1780
2023-08-03,43124,32678,10446
2023-08-04,76893,62341,14552
2023-08-05,23456,19874,3578
2023-08-06,98765,83245,15520
2023-08-07,45678,36987,8689
2023-08-08,54321,43216,11105
2023-08-09,23456,18974,4482
2023-08-10,87654,73456,14298
2023-08-11,12345,10876,1470
2023-08-12,67890,56543,11347
2023-08-13,56789,45678,11111
2023-08-14,78965,65432,13533
2023-08-15,98654,78542,20112
2023-08-16,10236,8456,1780
2023-08-17,43124,32678,10446
2023-08-18,76893,62341,14552
2023-08-19,23456,19874,3578
2023-08-20,98765,83245,15520
2023-08-21,45678,36987,8689
2023-08-22,54321,43216,11105
2023-08-23,23456,18974,4482
2023-08-24,87654,73456,14298
2023-08-25,12345,10876,1470
2023-08-26,67890,56543,11347
2023-08-27,56789,45678,11111
2023-08-28,78965,65432,13533
2023-08-29,98654,78542,20112
2023-08-30,10236,8456,1780
2023-08-31,43124,32678,10446
2023-09-01,76893,62341,14552
2023-09-02,23456,19874,3578
2023-09-03,98765,83245,15520
2023-09-04,45678,36987,8689
2023-09-05,54321,43216,11105
2023-09-06,23456,18974,4482
2023-09-07,87654,73456,14298
2023-09-08,12345,10876,1470
2023-09-09,67890,56543,11347
2023-09-10,56789,45678,11111
2023-09-11,78965,65432,13533
2023-09-12,98654,78542,20112
2023-09-13,10236,8456,1780
2023-09-14,43124,32678,10446
2023-09-15,76893,62341,14552
2023-09-16,23456,19874,3578
2023-09-17,98765,83245,15520
2023-09-18,45678,36987,8689
2023-09-19,54321,43216,11105
2023-09-20,23456,18974,4482
2023-09-21,87654,73456,14298
2023-09-22,12345,10876,1470
2023-09-23,67890,56543,11347
2023-09-24,56789,45678,11111
2023-09-25,78965,65432,13533
2023-09-26,98654,78542,20112
2023-09-27,10236,8456,1780
2023-09-28,43124,32678,10446
2023-09-29,76893,62341,14552
2023-09-30,23456,19874,3578
2023-10-01,98765,83245,15520
2023-10-02,45678,36987,8689
2023-10-03,54321,43216,11105
2023-10-04,23456,18974,4482
2023-10-05,87654,73456,14298
2023-10-06,12345,10876,1470
2023-10-07,67890,56543,11347
2023-10-08,56789,45678,11111
2023-10-09,78965,65432,13533
2023-10-10,98654,78542,20112
2023-10-11,10236,8456,1780
2023-10-12,43124,32678,10446
2023-10-13,76893,62341,14552
2023-10-14,23456,19874,3578
2023-10-15,98765,83245,15520
2023-10-16,45678,36987,8689
2023-10-17,54321,43216,11105
2023-10-18,23456,18974,4482
2023-10-19,87654,73456,14298
2023-10-20,12345,10876,1470
2023-10-21,67890,56543,11347
2023-10-22,56789,45678,11111
2023-10-23,78965,65432,13533
2023-10-24,98654,78542,20112
2023-10-25,10236,8456,1780
2023-10-26,43124,32678,10446
2023-10-27,76893,62341,14552
2023-10-28,23456,19874,3578
2023-10-29,98765,83245,15520
2023-10-30,45678,36987,8689
2023-10-31,54321,43216,11105
2023-11-01,23456,18974,4482
2023-11-02,87654,73456,14298
2023-11-03,12345,10876,1470
2023-11-04,67890,56543,11347
2023-11-05,56789,45678,11111
2023-11-06,78965,65432,13533
2023-11-07,98654,78542,20112
2023-11-08,10236,8456,1780
2023-11-09,43124,32678,10446
2023-11-10,76893,62341,14552
2023-11-11,23456,19874,3578
2023-11-12,98765,83245,15520
2023-11-13,45678,36987,8689
2023-11-14,54321,43216,11105
2023-11-15,23456,18974,4482
2023-11-16,87654,73456,14298
2023-11-17,12345,10876,1470
2023-11-18,67890,56543,11347
2023-11-19,56789,45678,11111
2023-11-20,78965,65432,13533
2023-11-21,98654,78542,20112
2023-11-22,10236,8456,1780
2023-11-23,43124,32678,10446
2023-11-24,76893,62341,14552
2023-11-25,23456,19874,3578
2023-11-26,98765,83245,15520
2023-11-27,45678,36987,8689
2023-11-28,54321,43216,11105
2023-11-29,23456,18974,4482
2023-11-30,87654,73456,14298
2023-12-01,12345,10876,1470
2023-12-02,67890,56543,11347
2023-12-03,56789,45678,11111
2023-12-04,78965,65432,13533
2023-12-05,98654,78542,20112
2023-12-06,10236,8456,1780
2023-12-07,43124,32678,10446
2023-12-08,76893,62341,14552
2023-12-09,23456,19874,3578
2023-12-10,98765,83245,15520
2023-12-11,45678,36987,8689
2023-12-12,54321,43216,11105
2023-12-13,23456,18974,4482
2023-12-14,87654,73456,14298
2023-12-15,12345,10876,1470
2023-12-16,67890,56543,11347
2023-12-17,56789,45678,11111
2023-12-18,78965,65432,13533
2023-12-19,98654,78542,20112
2023-12-20,10236,8456,1780
2023-12-21,43124,32678,10446
2023-12-22,76893,62341,14552
2023-12-23,23456,19874,3578
2023-12-24,98765,83245,15520
2023-12-25,45678,36987,8689
2023-12-26,54321,43216,11105
2023-12-27,23456,18974,4482
2023-12-28,87654,73456,14298
2023-12-29,12345,10876,1470
2023-12-30,67890,56543,11347
2023-12-31,56789,45678,11111

```

Or you can directly download with this link [Download Datset sales_company_riseUp](https://drive.google.com/uc?export=download&id=1FYEgOJdg4wHRnnaaCFQXh4xadxMfhXOc)

After download the data we can continue to upload it in RStudio. if you don't have the Rstudio you can use the Rstudio Online in PositCloud in this link [Posit Cloud Link](https://posit.cloud/)

If already started to sign in using your google account you can directly choose the programming language what you want to choose and please Choose RStudio Project.

## Let's Get Started

Firstly, Install the packages of these codes below
```{r}
install.packages("readr")
install.packages("rlang")
install.packages("lazyeval")
install.packages("ggplot2")
install.packages("fpp2")
install.packages("readxl")
```

After install and call it in the library to use its

```{r}
library("readr")
library("rlang")
library("lazyeval")
library("ggplot2")
library("fpp2")
library("readxl")
# for library you can use "" or not its same.
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/92c5ab2e-793b-42cf-980f-1d59607e0859)
Please makesure all the libraries already used and installed.

The Next Step is Define the data and read the csv file in directory you uploaded in Rstudio Files.
```{r}
sales_company_riseUp <- read.csv("sales_company_riseUp.csv")
```

**We will check data using view, head, tail, summary and str for data structures.**
1. view
```{r}
View(sales_company_riseUp)
# view(sales_company_riseUp) ini salah pada "view" harus capital "V"
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/7eadca4a-ebe4-48cf-97c7-e117d7e6cd0f)

2. head
```{r}
head(sales_company_riseUp,10)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/042ab7cd-328f-4451-9b7b-5ef1c0f48d2e)

3. tail
```{r}
tail(sales_company_riseUp,10)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/3c7ba016-3cb7-49b1-a0f2-2179a8563c60)

4. summary
```{r}
summary(sales_company_riseUp)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/c872785b-719b-410d-81fe-d3dbd687bf93)

5. str
```{r}
str(sales_company_riseUp)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/cfe8e6cb-ae77-4a87-9162-9c8d80ac3c81)
We see the data full 1 year from January until December and having 4 coulmns variables: date, revenue, cost and profit.

after that we define 
```{r}
Y <- ts(sales_company_riseUp[, 2])
autoplot(Y) + ggtitle("Times Series Plot: riseUp Sales Per Day") + ylab("Rupiah")
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/cc296957-bbe6-416e-bc97-2c27079ce0b7)
Y <- ts(sales_company_riseUp[, 2]): This line creates a time series object Y using data from the second column ([, 2]) of the sales_company_riseUp dataset. This column likely contains the daily sales data.

autoplot(Y) + ggtitle("Times Series Plot: riseUp Sales Per Day") + ylab("Rupiah"): This line generates a time series plot of the original data Y using the autoplot function from the ggplot2 package. It also sets the title of the plot to "Times Series Plot: riseUp Sales Per Day" and labels the y-axis as "Rupiah." This plot visualizes the daily sales data over time.

The result from data above actually was statisionary and fococed in the center of mean. but we will make more statisionary using diff(Y) and state the variable DY
```{r}
DY <- diff(Y)
autoplot(DY) + ggtitle("Time Series Plot: riseUp Sales per Day") + ylab("Rupiah")
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/3de7aac5-a3d0-46c7-a593-6494bf403c7a)
DY <- diff(Y): This line calculates the first difference of the Y time series, resulting in a new time series object DY. The differencing operation computes the change between consecutive observations in the original time series. This is often done to make the data stationary or remove trends and seasonality.

autoplot(DY) + ggtitle("Time Series Plot: riseUp Sales Per Day") + ylab("Rupiah"): This line generates a time series plot of the differenced time series DY. It has the same title and y-axis label as the original data plot. The differenced plot helps visualize any remaining patterns in the data after removing trends and seasonality by differencing.

it creates a time series plot of the differenced data to better understand the remaining patterns or variations in the sales data over time. The differencing operation is often used in time series analysis to make the data suitable for modeling and forecasting.

Checking the data, is the data is seasonal data ?
```{r}
ggseasonplot(DY) + ggtitle("Time Series Plot: riseUp Sales per Day") + ylab("Rupiah")
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/142547b2-d5d1-4484-b74c-b2bb8607ae39)
The error message "Data are not seasonal" is returned by the ggseasonplot function because it expects the time series data to exhibit a seasonal pattern, but the differenced time series DY does not display a clear seasonal component.


## **Let's Make The Forecast Use Naive Method**
```{r}

fit <- naive(DY)
print(summary(fit))

```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/09d998c0-cf46-4791-b966-4d11833f5b60)

![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/2bd43d3b-3856-4b49-a0a7-d542c00d8efa)

fit <- naive(DY): In this line, a forecasting model is created using the naive forecasting method. The DY time series, which represents the first differences of the daily sales data, is used as the input to the forecasting model.

The naive forecasting method is one of the simplest time series forecasting methods. It involves simply using the most recent observation as the forecast for the next period. In other words, it assumes that future values will be the same as the most recent observed value. This method is often used as a baseline or benchmark for more complex forecasting models.

print(summary(fit)): This line prints a summary of the forecasting model created using the naive method. The summary function provides information about the model forecasts.

The summary typically includes metrics such as Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), Root Mean Squared Error (RMSE), and others. These metrics help evaluate the accuracy of the forecasts generated by the model.

From data results :

Residual sd = 94080.3183 

Error measures:
                ME  RMSE   MAE MPE MAPE MASE   ACF1
Training set -91.7 94080 81827 230  232    1 -0.786

```{r}
checkresiduals(fit)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/f3f969d8-3e73-4a5d-af5f-0443d8ec2781)
checkresiduals(fit): The checkresiduals function is used to assess the residuals of the forecasting model. Residuals are the differences between the observed values and the forecasts. This function helps identify any patterns or anomalies in the residuals, which can be indicative of model inadequacies

if the result of **Naive Method** is still relative high we can use the second method. in data above the result of RMSE In this case, it's 94080, which is relatively high.

## **Forecasting Method Using ETS Method**
```{r}
fit_ets <- ets(Y)
print(summary(fit_ets))
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/c91dda21-3065-4b47-a374-b1854c725223)
Exponential Smoothing State Space Model (ETS) method, evaluate the model's performance, and check the residuals.
Let's break down each part of the code:

fit_ets <- ets(Y): In this line, the ets function is used to fit an ETS model to the time series data Y. ETS is a method for time series forecasting that models data with exponential smoothing, trend, and seasonality components. The result of this line is a fitted ETS model stored in the fit_ets variable.

print(summary(fit_ets)): This line prints a summary of the ETS model fitted in the previous step. The summary function provides information about the model, including details about the estimated parameters, error measures, and other relevant statistics. The summary is used to assess the quality of the model and its ability to capture the patterns in the data.

The summary typically includes information about the estimated smoothing parameters, the type of error (e.g., additive or multiplicative), and performance metrics such as Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), and Root Mean Squared Error (RMSE).

```{r}
checkresiduals(fit_ets)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/dfd1976c-49b9-4831-90c7-13f1402b142e)
From data result use the ETS Forecast Method:
ME (Mean Error): ME is -11.5, which suggests that, on average, the model's forecasts are underestimating the actual values by 11.5 units.

RMSE (Root Mean Squared Error): RMSE is 29,417. It's a measure of the accuracy of the model's forecasts. A lower RMSE indicates better model performance.

MAE (Mean Absolute Error): MAE is 25,150. It's the mean of the absolute values of the model's errors, providing the average magnitude of errors.

MPE (Mean Percentage Error): MPE is -65.5. This indicates that, on average, the model's forecasts are off by 65.5% of the actual values. A negative MPE suggests the model tends to under-forecast.

MAPE (Mean Absolute Percentage Error): MAPE is 94.2. It represents the mean of the absolute percentage errors, indicating the average absolute percentage error of the model's forecasts.

MASE (Mean Absolute Scaled Error): MASE is 0.564. It's a measure of forecast accuracy relative to a naive forecast (e.g., simple lag model). A value close to 1 suggests that the model's forecasts are similar in accuracy to a naive forecast.

ACF1 (Autocorrelation Function 1): ACF1 is -0.494, which is the lag-1 autocorrelation of the residuals. It measures the correlation between the residuals at time t and t-1.

## Recommendation NAIVE vs ETS

1. Based on the provided results, it appears that the ETS method performs better than the Naive method in terms of several error measures.The ETS method has a lower residual standard deviation (sigma), a lower RMSE, a lower MAE, and a lower MASE compared to the Naive method.
2. However, it's important to note that the ETS method still has certain weaknesses, such as a bias toward under-forecasting and relatively high MAPE.

Therefore, the recommendation is to use the ETS method, as it shows some improvements in forecast accuracy compared to the Naive method. However, further model refinement and possibly the consideration of alternative forecasting methods should be explored to address the remaining biases and errors in the forecasts.

## **Arima Method**

ARIMA, which stands for AutoRegressive Integrated Moving Average, is a widely used time series forecasting method in statistics and econometrics. ARIMA models are designed to capture and model the underlying patterns and structures in time series data.
```{r}
fit_arima <- auto.arima(DY,d=0,D=0, stepwise = FALSE, approximation = FALSE, trace = TRUE)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/994dc128-64ee-4c35-9d1a-808a27f90aae)

```{r}
print(summary(fit_arima))
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/85916208-d153-4496-bae7-e09c24514635)

```{r}
checkresiduals(fit_arima)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/de04d9fb-1d11-48f6-ac74-fd9010337a82)

```{r}
# sigma^2 = 3.69e+08
sqrt(3.69e+08)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/faceb1f4-9750-4059-8938-9605ee59164d)


Best Model Selection:

The best-fitting ARIMA model selected by the auto.arima function is ARIMA(0,0,5) with a non-zero mean. This means that the model includes 5 moving average (MA) terms without any autoregressive (AR) terms and has a non-zero mean.
Model Coefficients:

The coefficients for the MA terms are listed, with their standard errors (s.e.). This information shows the values of the moving average terms in the model. The mean coefficient represents the non-zero mean.
Model Summary:

The variance (sigma^2) of the model's errors is approximately 3.69e+08.
The log likelihood of the model is -4113.
The model selection criteria are provided:
AIC (Akaike Information Criterion) is 8241.
AICc (Corrected Akaike Information Criterion) is 8241.
BIC (Bayesian Information Criterion) is 8268.
Training Set Error Measures:

Mean Error (ME) is 94.2, indicating a bias in the model's forecasts.
Root Mean Squared Error (RMSE) is 19063, measuring the accuracy of the model's forecasts.
Mean Absolute Error (MAE) is 17467, representing the average magnitude of errors.
Mean Percentage Error (MPE) is 37.8, indicating the percentage bias in the forecasts.
Mean Absolute Percentage Error (MAPE) is 63.5, reflecting the average absolute percentage error.
Mean Absolute Scaled Error (MASE) is 0.213, which indicates how well the model performs relative to a naive forecast.
Autocorrelation Function 1 (ACF1) is 0.0276, which measures the correlation between consecutive residuals.

Additional Calculation:

The square root of sigma^2 is calculated as approximately 19209.
Explanation:
The results show that the selected ARIMA(0,0,5) model includes five moving average terms and has a non-zero mean. The model's error measures, such as RMSE and MAE, indicate the accuracy and bias in the forecasts. The AIC, AICc, and BIC are used for model selection, and they are used to compare the model's fit to the data. The square root of sigma^2 represents the standard deviation of the model's errors.

It's important to consider these results in the context of your specific data and forecasting goals. The error measures help assess the accuracy of the model's forecasts, and lower values of RMSE and MAE generally indicate better model performance. The model's ability to capture the patterns in the data should be evaluated in conjunction with these error measures.

Using the first variable as Series Y with different d=2
```{r}
fit_arima <- auto.arima(Y,d=2,D=0, stepwise = FALSE, approximation = FALSE, trace = TRUE)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/823c5582-e521-4319-bc54-1b7e3cc898b5)

```{r}
print(summary(fit_arima))
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/86a2c9de-4d94-4e9e-8911-8c91c7c679d0)

```{r}
checkresiduals(fit_arima)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/dfa71120-70df-4eef-a6e6-172e2d7bc7c8)

```{r}
sqrt(1.4e+09)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/9156d700-fd23-4778-8d84-6affb75a42cc)

Using the first variable as Series Y with different d=3
```{r}
fit_arima <- auto.arima(Y,d=3,D=0, stepwise = FALSE, approximation = FALSE, trace = TRUE )
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/882aaa5f-5759-4637-b6fa-25db034ce5b8)

```{r}
print(summary(fit_arima))
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/9d169e65-7d0e-4517-929f-c0f2ead6d9f4)

```{r}
checkresiduals(fit_arima)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/6c8d87df-eadb-4ea7-94fa-d2ce0220a4bf)

```{r}
sqrt(7.02e+08)
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/52762e29-6852-4a3d-9238-332ad10b5aa1)

if we use the series Y the residual SD result higher than series DY.
DY = 19209
Y with d equals 2  = 37417
Y with d equals 3 = 26495

if we compare with ETS and Naive
the best recommendation is with ETS method with residuals SD score 0.53

## **Menggunakan fungsi forecast**
```{r}
fcast <- forecast(fit_ets, h=3)
autoplot(fcast)
print(summary(fcast))
```
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/79eb10cd-7ca3-46f4-ac2d-bed143861625)
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/08ec10f3-00ec-4c10-b39d-3eb242af0a1b)
![image](https://github.com/PajrulPalah/RForDataAnalysis/assets/143974279/fa126f8d-81c2-45cf-a3b1-a994871ae50e)

Row: The row numbers represent the time period or observation number for which the forecasts are made. In this case, it starts from row 366, indicating the forecast for time period 366, and continues to row 368.

Point Forecast: The "Point Forecast" column provides the forecasted values for the corresponding time periods. In your data, the point forecast is consistently 55,600 for all three time periods (366, 367, and 368).

Lo 80 and Hi 80: These columns represent the lower and upper limits of the 80% prediction interval (or prediction bands). The 80% prediction interval indicates the range within which you can expect the actual values to fall with an 80% confidence level. In your data, the lower and upper limits are 17,799 and 93,402, respectively, for all three time periods.

Lo 95 and Hi 95: Similarly, these columns represent the lower and upper limits of the 95% prediction interval. The 95% prediction interval is wider than the 80% interval and provides a range with a 95% confidence level. In your data, the lower and upper limits are -2,212 and 113,413, respectively, for all three time periods.

In summary, the data provides forecasts for three time periods (366, 367, and 368) using an ETS model. It includes the point forecasts as well as prediction intervals (both 80% and 95%) to indicate the range of uncertainty around the forecasts. These values are useful for assessing the accuracy and reliability of the forecasts.


