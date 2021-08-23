# Bus Ridership Clustering
There are couple of ways to cluster the bus stop ridership data. 
- The first way is to cluster base on location (lat & long). The KMEAN algorithm will randomly select starting point every time it runs, and because the bus stops are uniformly distributed across Chicago, we might have a different cluster each time. 
<img src="https://i.postimg.cc/Tw9G7dG1/cluster-only-loc.png" width="48">
- The second way is to cluster base on ridership (boardings + alightings) from each bus stop. From the graph, we can roughly tell which area or intersection has a high amount of ridership.
![alt text](https://i.postimg.cc/c46ZhGz1/cluster-rider.png)
- The most optimal way is to cluster base on both location and ridership combine. Comparing it to the ridership heatmap shows that the method keeps the features of ridership, while also take location into account.
![alt text](https://i.postimg.cc/26mr7qsg/cluster-loc-rider.png)
![alt text](https://i.postimg.cc/jd9TkkVH/ridership.png)
If we have more data and plan to predict ridership of certain areas in the future, having each bus stop clustered will result in a stronger model. 

# Trends of each Bus Route
The graph below shows the total combined monthly ridership vs time. Between 2000 and 2012, the average ridership maintained roughly the same level. Between 2012 and 2020, the demand seems to slowly decrease. In 2020, the pandemic totally changed the landscape of public transportation. 
![alt text](https://i.postimg.cc/C5x093LN/total-rider-vs-time.png)
In order to get a better estimation of the ridership trend of each bus route, we dropped the data after 2020. Then, we ran a linear regression model for each bus route and saved the coefficient into a data frame. We are then able to sort the data frame to find the most and least trending bus route. 
![alt text](https://i.postimg.cc/RhpmmgWz/highest-demand.png)
- Most trending route 
![alt text](https://i.postimg.cc/x1KvFhkh/trend-top.png)
- Least trending route 
![alt text](https://i.postimg.cc/sgFPms25/trend-bottom.png)
