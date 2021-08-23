### Timeseries: Linear Models

We tackled the average ridership data for CTA buses and trains. We were able to determine seasonality by looking at the auto correlation and partial auto correlation plots, as well as by interpreting stationarity through the Dicky-Fuller Test p-values with and without differencing our target of monthly total ridership.

This was by far the best model for predictive ability, which is not surprising since the data itself is sequentially linear. We got an r2 score of 0.89, and a mean squared error of 3605.66 for the bus data. We got an r2 score of 0.93, and a mean squared error of 2514.46 for the train data. Since auto correlation was taken into account, we were able to predict the slightly downward trend in both models.

### Timeseries: SARIMA

A grid search was performed to find the ideal, p, d, q, and m (periodicity) for the bus and train data. After fitting our model, we found the ideal seasonal order for bus data to be (1, 1, 7, 6) which is semiannual seasonality, and for train data we found (3, 1, 5, 12) which is annual seasonality. The RMSE scores were 12537.14 and 16851.8 respectively. We were surprised that this is not the best model since it did not accurately follow the downward trend. With some tweaking and a larger grid search, this can become the best model.