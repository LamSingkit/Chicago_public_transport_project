## Data Collection
Several datasets were obtained from the Chicago Transit Authority. Datasets included monthly total ridership of both train and bus, average weekday, saturday, and sunday/holiday total ridership for all train stations and bus routes from January 2001 to May 2021. 

## Data Transformation and Modeling
In order to add dimensionality to the data to give the models more information, unsupervised learning methods such as KMeans Clustering were. KMeans Clustering was used on location data in order to use lattitude/longitude data more effectively.

The data was clustered by longitude and latitude and a grid search loop was used to optimize for best number of k clusters that was evaluated by silhouette score. Silhouette score is a method of evaluating our results. When looking at silhouette score, we are looking for a high score between 0 and 1 which. The higher the score, the more similar to other points in its cluster it is and dissimilar from points in neighboring clusters it is. 
The best number of clusters was 16 which yielded a silhouette score of 0.42. 

The clusters were then appended onto the data and OneHotEncoder was used to transform the clusters and the data was split into train and test sets to run through a Linear Regression Model. 
The Linear Regression model yielded an R2 score of 0.97 on the training and testing data. This means that the train and test set explains 97% of the variability of the response data around its mean. The model is not overfit, therfore able to account for unseen data. The data is able to both accuarately capture the regularities in the training data but also generalizes well to unseen data with 97% accuracy.

## Time Series: ARIMA Model
Time series models such as ARIMA and VAR models were used to generate forecasts for future values of ridership based off of time data within the dataset. 
Three paramters: p, q, and d were optimized in order to fit the ARIMA model which was evaluated by AIC score, an estimator of prediction error. The lower the AIC score, the better. P represents the number of timesteps to correlate with, q is the number of prior error terms to regress on and d is how much to difference our model. 
Preprocessing: Data collected after March 2020 was removed from the dataset due to COVID-19 pandemic causing nation-wide closures which will misrepresent our data. 
Paramater d: Differencing Paramter
This paramter controls how much we 'difference' our time series by. Differencing is important as stationarity is required for all time series models. Stationarity means there are no systemic changes in our time series over time, our means stay the same, and there is no trend. 
The augmented Dickey-Fukker test was used to test for stationarity and p values were scored against an alpha score of 0.05 to accept or reject stationarity of the data. Average monthly total was first-differenced which revealed a p value of 0.01 and were able to accept stationarity of first differenced average monthly ridership. 
Next, a manual gridsearch was used to evaluate combinations of p and q paramters, along with our known d parameter (1) that would give us the best model with lowest AIC score. 
The gridsearch revealed best combination of p,d,q for the lowest AIC score was 10,1,8 which gave us an AIC score of 3487.56. 

## Time Series: VAR Model
Additionally the VAR times series model was used to predict average monthly ridership, average weekly ridership, average saturday ridership, and average sunday/holiday ridership on train and bus ridership. VAR model allows us to forecast forward many variables simultaneously.
Again, data collected after March 2020 was removed from the dataset due to COVID-19 pandemic causing nation-wide closures which misrepresents the data. The stationarity was accepted at first differenced for average total monthly ridership and average weekday ridership and the stationarity was accepted at second differenced for average saturday ridership and average sunday/holiday ridership. The forecast produced high MSE scores for each variable and the model was not able to forecast well on unseen data. 

# Conclusion and Recommendations
The analysis and modeling was successful in predicting total monthly ridership at a given train station which can serve as an extremely useful tool when evaluating future projects and changes the CTA can make when optimizing its services. I would recommend further research to compare the trends of ridership prior to March 2020 (pre COVID-19 pandemic) with ridership after March 2020 (intra and post COVID-19 pandemic) to assess for any changes to improve services, routes, and train station lines that can be made to account for the unprecedented event that changed many people's lives.  to Forecasting future trends of ridership is more important now more than ever and will allow the CTA to make better,informed decicions during such an uncertain time.