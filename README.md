# Project 5: Recommendations for Increasing Access to Public Transportation in Chicago
##### Aug 22, 2021 - Shengjie Lin, Afsara Ali, Brianna Sazone, Maitiu Sexton

## Problem Statement: Where would be the most effective place(s) to run additional bus/train service?
#### (Recommendations from us, a team of consultants hired by the CTA to decide where new routes or increased service should be instated)
This will be evaluated based on:
- Historical and predicted ridership levels
- Locations of employment
- Current access to public transit
- Population density

## Background
With a budget of \\$1.65 billion for the year of 2021 (up \$350 million from 2011), along with the gradual reopening of the city as our safety procedures regarding COVID-19 have become well-integrated into our operations, it is time to start thinking proactively as to what we can do to get _tomorrow's_ Chicago ready for _today's_ new normal. In order to most effectively utilize our budget, we must identify exactly where it would be most effective to invest in new or increased transit service. This will be determined by the following factors:
1. How do we define current demand?\
    a. High ridership\
    b. Low ridership
2. Where are employment opportunities concentrated?
3. Where do people live?

It is often naïvely assumed that low ridership means low demand. It has been shown by many sources [(1)](https://fas.org/sgp/crs/misc/R45144.pdf) [(2)](https://transweb.sjsu.edu/research/Investigating-Determining-Factors-Transit-Travel-Demand-Bus-Mode-US-Metropolitan-Statistical-Areas) [(3)](https://www.transit.dot.gov/TOD) [(4)](https://www.sciencedirect.com/science/article/pii/S0143622817307166) that quite the opposite is true. Given this assumption, we must look at neighborhoods where a lack of service exists, as measured by the ridership of routes going through those ares. 

In addition to this, Chicago has the vast majority of its rail system arranged in a hub-and-spoke system radiating from the central business district. While it is true that there is a high concentration of employment in the downtown area (which has shown a strong increase over the past 20 years), this is created, at least in part, by the very feedback loop of the public transit system surrounding it. It is relatively easy to get to and from downtown, but if your commute deviates from this pattern, it can take nearly twice as long. For example, the trip from the Irving Park Blue Line station to Clark/Lake (downtown) during morning rush hour takes approximately 23 minutes [(5)](https://www.google.com/maps/dir/Irving+Park+Blue+Line+Station,+Chicago,+IL/Clark%2FLake,+Chicago,+IL+60601/@41.9193017,-87.7505812,12z/data=!3m1!4b1!4m18!4m17!1m5!1m1!1s0x880fcdb74d81cf1f:0xcbaec9c7c47e6e51!2m2!1d-87.7273044!2d41.9520754!1m5!1m1!1s0x880e2cb07dc3de1d:0x478016ed528b9795!2m2!1d-87.6313669!2d41.8857483!2m3!6e0!7e2!8j1629705600!3e3). To start from the same location and go to Loyola University Chicago, which is roughly two-thirds of the distance (as the crow flies), takes nearly an hour [(6)](https://www.google.com/maps/dir/Irving+Park+Blue+Line+Station,+Chicago,+IL/Loyola+University+Chicago,+West+Sheridan+Road,+Chicago,+IL/@41.9425885,-87.749084,12z/data=!3m1!4b1!4m18!4m17!1m5!1m1!1s0x880fcdb74d81cf1f:0xcbaec9c7c47e6e51!2m2!1d-87.7273044!2d41.9520754!1m5!1m1!1s0x880fd10a9033c5ff:0xe613cd876e617e4c!2m2!1d-87.6582585!2d41.9987765!2m3!6e0!7e2!8j1629705600!3e3). Given this, as well as the fact that not all people work downtown, we have to take into consideration the location of people's employment.

Lastly, it behooves us to consider the current population density in each neighborhood, which we will be grouping by ZIP code for consistency's sake. We must find a balance between the fact that more people in a neighborhood means that more people will need access to public transit, along with the understanding that the population density of a particular neighborhood is heavily influenced by the public transportation available within it.

## Data Collection
Several datasets were obtained from the [Chicago Transit Authority](https://data.cityofchicago.org/Transportation/CTA-List-of-CTA-Datasets/pnau-cf66). Datasets included monthly total ridership of both train and bus, average weekday, saturday, and sunday/holiday total ridership for all train stations and bus routes from January 2001 to May 2021. Additionally, data from the annual [Where Workers Work](https://ides.illinois.gov/resources/labor-market-information/where-workers-work.html) report that the Illinois Department of Employment Security publishes was used to determine both the locations and "density" of jobs in Chicago. We also referenced the most recent [population counts](https://data.cityofchicago.org/Health-Human-Services/Chicago-Population-Counts/85cm-7uqa) in Chicago, as published by the city of Chicago.

### Datasets

[CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals](https://data.cityofchicago.org/Transportation/CTA-Ridership-L-Station-Entries-Monthly-Day-Type-A/t2rn-p8d7)

[CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals](https://data.cityofchicago.org/Transportation/CTA-Ridership-Bus-Routes-Monthly-Day-Type-Averages/bynn-gwxy)

[CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012](https://data.cityofchicago.org/Transportation/CTA-Ridership-Avg-Weekday-Bus-Stop-Boardings-in-Oc/mq3i-nnqe)

[Where Workers Work, 2020 Q3 & 2019](https://ides.illinois.gov/resources/labor-market-information/where-workers-work.html)

[Chicago 2019 Population Counts by ZIP Code](https://data.cityofchicago.org/Health-Human-Services/Chicago-Population-Counts/85cm-7uqa)

### Data Dictionary

|Feature|Type|Dataset|Description|
|--:|:--|:--|:--|
|station_id|integer|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|ID # of train station| 
|stationname|object|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|name of train station|
|month_beginning|object|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|date of the beginning of the month in which data was collected for that month|
|avg_weekday_rides|float|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|The average ridership on weekdays of each month|
|avg_saturday_rides|float|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|The average ridership on saturdays of each month|
|avg_sunday-holiday_rides|float|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|The average ridership on sundays/holidays of each month|
|monthtotal|integer|CTA-Ridership-'L' Station Entries-Monthly Day-Type Averages & Totals|The number of total ridership for each month at each train station|
|route|integer|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|ID # of bus route| 
|routrename|object|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|name of bus route|
|month_beginning|object|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|date of the beginning of the month in which data was collected for that month|
|avg_weekday_rides|float|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|The average ridership on weekdays of each month|
|avg_saturday_rides|float|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|The average ridership on saturdays of each month|
|avg_sunday-holiday_rides|float|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|The average ridership on sundays/holidays of each month|
|monthtotal|integer|CTA-Ridership-Bus Routes-Monthly Day-Type Averages & Totals|The number of total ridership for each month for each bus route|
|stop_id|integer|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|ID # of bus stop| 
|onstreet|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|name of the street the bus stop is on|
|cross_street|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|name of the street the bus stop intersects with|
|routes|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The routes available at that bus stop|
|boardings|float|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The average ridership on saturdays of each month|
|allightings|float|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The average ridership on sundays/holidays of each month|
|month_beginning|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The date of the first day of the month in which ridersip was collected for that month (Oct 2012 only)|
|daytype|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The type of day of the week in which ridership was collected|
|location|object|CTA-Ridership-Avg Weekday Bus Stop Boardings in Oct 2012|The longitude and latitude of bus stop|
|year|integer|Where Workers Work|The year in which the observation was reported|
|60601, 60602, ... , 60666|integer|Where Workers Work|All of the 55 features that represent the ZIP code where a particular number of jobs was reported|
|zip|string|Chicago 2019 Population Counts by ZIP Code|The Zip code for which a population was recorded in 2019|
|pop|integer|Chicago 2019 Population Counts by ZIP Code|The population of a particular ZIP code in 2019|





## Modeling

### K-Means Clustering
In order to add dimensionality to the data to give the models more information, unsupervised learning methods such as KMeans Clustering were implemented. K-Means Clustering was used on location data in order to use lattitude/longitude data more effectively.

The data was clustered by longitude and latitude and a grid search loop was used to optimize for best number of k clusters that was evaluated by silhouette score. Silhouette score is a method of evaluating our results. When looking at silhouette score, we are looking for a high score between 0 and 1 which. The higher the score, the more similar to other points in its cluster it is and dissimilar from points in neighboring clusters it is. The best number of clusters was 16 which yielded a silhouette score of 0.42. 

The clusters were then appended onto the data and OneHotEncoder was used to transform the clusters and the data was split into train and test sets to run through a Linear Regression Model. 
The Linear Regression model yielded an $R^2$ score of 0.97 on the training and testing data. This means that the train and test set explains 97% of the variability of the response data around its mean. The model is not overfit, therefore able to account for unseen data. The data is able to both accuarately capture the regularities in the training data but also generalizes well to unseen data with 97% accuracy.


### Time Series: ARIMA Model
Time series models such as ARIMA and VAR models were used to generate forecasts for future values of ridership based off of time data within the dataset. 
Three paramters: p, q, and d were optimized in order to fit the ARIMA model which was evaluated by AIC score, an estimator of prediction error. The lower the AIC score, the better. P represents the number of timesteps to correlate with, q is the number of prior error terms to regress on and d is how much to difference our model. 
Preprocessing: Data collected after March 2020 was removed from the dataset due to COVID-19 pandemic causing nation-wide closures which will misrepresent our data. 
Paramater d: Differencing Paramter
This paramter controls how much we 'difference' our time series by. Differencing is important as stationarity is required for all time series models. Stationarity means there are no systemic changes in our time series over time, our means stay the same, and there is no trend. 
The augmented Dickey-Fukker test was used to test for stationarity and p values were scored against an alpha score of 0.05 to accept or reject stationarity of the data. Average monthly total was first-differenced which revealed a p value of 0.01 and were able to accept stationarity of first differenced average monthly ridership. 
Next, a manual gridsearch was used to evaluate combinations of p and q paramters, along with our known d parameter (1) that would give us the best model with lowest AIC score. 
The gridsearch revealed best combination of p,d,q for the lowest AIC score was 10,1,8 which gave us an AIC score of 3487.56. 

### Time Series: VAR Model
Additionally the VAR times series model was used to predict average monthly ridership, average weekly ridership, average saturday ridership, and average sunday/holiday ridership on train and bus ridership. VAR model allows us to forecast forward many variables simultaneously.
Again, data collected after March 2020 was removed from the dataset due to COVID-19 pandemic causing nation-wide closures which misrepresents the data. The stationarity was accepted at first differenced for average total monthly ridership and average weekday ridership and the stationarity was accepted at second differenced for average saturday ridership and average sunday/holiday ridership. The forecast produced high MSE scores for each variable and the model was not able to forecast well on unseen data. 

### Timeseries: Linear Models

We tackled the average ridership data for CTA buses and trains. We were able to determine seasonality by looking at the auto correlation and partial auto correlation plots, as well as by interpreting stationarity through the Dicky-Fuller Test p-values with and without differencing our target of monthly total ridership.

This was by far the best model for forecasting, which is not surprising since the data itself is sequentially linear. We got an r2 score of 0.89, and a mean squared error of 3605.66 for the bus data. We got an $R^2$ score of 0.93, and a mean squared error of 2514.46 for the train data. Since auto correlation was taken into account, we were able to predict the slightly downward trend in both models.



### Timeseries: SARIMA

A grid search was performed to find the ideal, p, d, q, and m (periodicity) for the bus and train data. After fitting our model, we found the ideal seasonal order for bus data to be (1, 1, 7, 6) which is semiannual seasonality, and for train data we found (3, 1, 5, 12) which is annual seasonality. The RMSE scores were 12537.14 and 16851.8 respectively. We were surprised that this is not the best model since it did not accurately follow the downward trend. With some tweaking and a larger grid search, this can become the best model.

### Bus Ridership Clustering
There are couple of ways to cluster the bus stop ridership data. 
- The first way is to cluster base on location (lat & long). The KMEAN algorithm will randomly select starting point every time it runs, and because the bus stops are uniformly distributed across Chicago, we might have a different cluster each time. 

<img src="https://i.postimg.cc/Tw9G7dG1/cluster-only-loc.png" width="500">

- The second way is to cluster base on ridership (boardings + alightings) from each bus stop. From the graph, we can roughly tell which area or intersection has a high amount of ridership.

<img src="https://i.postimg.cc/c46ZhGz1/cluster-rider.png" width="500">

- The most optimal way is to cluster base on both location and ridership combine. Comparing it to the ridership heatmap shows that the method keeps the features of ridership, while also take location into account.

<p float="left">
  <img src="https://i.postimg.cc/26mr7qsg/cluster-loc-rider.png" width="450" />
  <img src="https://i.postimg.cc/jd9TkkVH/ridership.png" width="450" />
</p>

If we have more data and plan to predict ridership of certain areas in the future, having each bus stop clustered will result in a stronger model. 

### Trends of each Bus Route
The graph below shows the total combined monthly ridership vs time. Between 2000 and 2012, the average ridership maintained roughly the same level. Between 2012 and 2020, the demand seems to slowly decrease. In 2020, the pandemic totally changed the landscape of public transportation. 

<img src="https://i.postimg.cc/C5x093LN/total-rider-vs-time.png" width="700" />
In order to get a better estimation of the ridership trend of each bus route, we dropped the data after 2020. Then, we ran a linear regression model for each bus route and saved the coefficient into a data frame. We are then able to sort the data frame to find the most and least trending bus route. 

<img src="https://i.postimg.cc/RhpmmgWz/highest-demand.png" width="700" />

- Most and least trending route 
<p float="left">
  <img src="https://i.postimg.cc/x1KvFhkh/trend-top.png" height="300" />
  <img src="https://i.postimg.cc/sgFPms25/trend-bottom.png" height="300" />
</p>

## Recommendations
### 1. Ashland BRT (Bus Rapid Transit)
The idea of creating dedicated bus lanes and signal priority along Ashland Ave between Irving Park and 95th is [well researched](https://www.transitchicago.com/ashlandbrt/) by the CTA and is in the final stages of obtaining funding. The results of our research coincide with those of previously completed research concerning this project. This route runs 1-2 miles west of the Red Line and fills a significant gap in North-South transit. Additionally, there is notable population density and job availability in these neighborhoods. About 10% of Chicago lives within a ½ mile of this route while 1 out of every 4 of these houses have no car. The positive effect is clear and attainable and this will also set a precedent for future, more ambitious projects.
### 2. 83rd St. Bus
It's well known that transit accessibility on the South Side is far more sparse than on the North side. On the North Side, there is a bus route on nearly every major street (every ½ mile), while the South Side normally only has a bus route every other major street (every mile). The 79th and 87th st busses (that run parallel to 83rd) have had decreasing ridership numbers in the recent past, likely due to the lack of complementary service in the area. This prposed route [(detailed here)](https://www.google.com/maps/d/u/0/edit?mid=1Ia0z6OTLdgjv7FeUBcf1IXW-akpFoiLt&ll=41.7434652416821%2C-87.70991063959718&z=14) would fill gap on the South Side that has higher than average population and job density. It also provides direct connections to 2 Metra (commuter rail) lines (SWS - Ashburn,  ME - 83rd (Avalon Park) and 83rd (eastern stop)), as well as passing by (but not directly stopping at) Metra RI - Gresham. There will also be direct connections to the 79th St. Red Line station and the Jeffery Jump Express (Chicago stop).
### 3. Increased Service on the Following Routes:
- 79th St. Bus __79__
- 63rd St. Bus __63__
- __151__ Sheridan
    - to balance out increasing demond on the __146__ Inner Drive Express and the __147__ Outer Drive Express, all three of which run parallel to one another
- __J14__ Jeffery Jump
    - hybrid BRT betweeen deep South Side and Downtown
    - complements addition of an 83rd St. bus
- __Green Line__ trains to/from the __Ashland branch__
    - to complement Ashland BRT, as well as increase general service to the South and West Sides
    
It is self-evident that the cheapest way to increase access to public transit is to simply increase the number of daily runs on already existing routes/infrastructure. These routes were selected specifically because they met all of our criterium (low/decreasing ridership, higher population density, current lack of substantial service).

## Conclusions
The analysis and modeling was successful in predicting total monthly ridership at a given train station which can serve as an extremely useful tool when evaluating future projects and changes the CTA can make when optimizing its services. We would recommend further research to compare the trends of ridership prior to March 2020 (pre COVID-19 pandemic) with ridership after March 2020 (intra and post COVID-19 pandemic) to assess for any changes to improve services, routes, and train station lines that can be made to account for the unprecedented event that changed many people's lives. Forecasting future trends of ridership is more important now more than ever and will allow the CTA to make better, more informed decicions during such an uncertain time.
