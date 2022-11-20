---
title: "Spatiotemporal Forecasting of Traffic Flow Data using GNN (Ongoing)"
excerpt: "In recent times, the development of transport infrastructure has had a great boom, however, traffic problems continue to spread due to an increase in the population in urban areas  which ultimately increases pressure on transport networks. Thus, we develop a GNN model (SST-GNN currently) which provides forecasts of traffic flow data such as velocity, etc. Additionally, we introduce DIVE dataset created by collecting traffic data over 20 nodes within the Old Panvel, Maharashtra of the Indian Province. The model achieved an RMSE of 1.76, 1.69 and 1.69 on the DIVE dataset at 15, 30 and 45 mins intervals for prediction.
<br/><img src='/images/speed_each_node.png'>"
collection: portfolio
---

According to a study, India suffers a huge loss of $21.3 billion annually because of delays and additional fuel consumption due to poor road conditions and frequent halts. The occurrence of congestion on the city roads prevents the movement of traffic and leads to an intolerable increase in the trip delay. The time wasted in congestion could effectively be used in doing some productive work. The sudden stop-and-go driving pattern in the congestion leads to more fuel consumption in the city, thereby increasing the pollution level in the city by emitting more carbon into the environment. Traffic congestion causes noise of high level (more than 90 dB) which causes the environment to turn unpleasant.

All of the factors mentioned above made us realize the importance of reducing the time required to reach your destination in addition to the harmful effects of congestion on the environment and the country’s economy. This led to the creation of a solution to predict an optimal path to avoid traffic congestion altogether.

It was found that PeMSD7and PeMSD8 as the two main datasets used in the development of the traffic forecast models. But both of them were based on the foreign setting which is unsuitable for utilization in the Indian Province thus, a need to create our own dataset was realized. Thus, the area to be considered was finalized and explored. Finally, 20 distinct points were selected.

<img height="600" width="400" src='/images/node_map.PNG'><br/>

Thus, a Nodejs script which uses the TomTom API was deployed on Heroku to create our own API server. This server collects traffic data at the selected nodes at a regular interval of 15 mins.

<img src='/images/heroku.PNG'><br/>

The exploratory data analysis on the collected data showcased the heavy correlation between the free flow velocity at every node at a given instance.

<img src='/images/speed_each_node.png'><br/>

Now the data engineering was done to change the data into a similar form to that of PeMSD7, and PeMSD8. Thus, Dive (Dataset for Indian Vehicular Traffic Evaluation) is created which is a dataset based on the Indian setting for traffic forecasting and evaluation. It currently consists of 2 CSV files:-

- Node.adj.csv: 
    - The adjacency matrix where each node represents euclidean distance among two nodes.

    <img src='/images/speed.png'><br/>

- FreeFlowVelocity.csv: 
    - The free flow velocity of 20 sensors at 15-minute intervals.

    <img src='/images/adj.png'><br/>

Currently, we have trained the SST-GNN which is the current state of the art on our dataset and got similar results to that of PeMDS7. The results are competitive with the ones trained on PeMSD7.

| Dataset          | <====   |  15 mins |  ====>   | <====   | 30 mins  |  ====>   | <====   |  45 mins | ====>    | <====   |  60 mins | ====>    |
|                  | ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
|                  |   MAE   |   RMSE   |   MAPE   |   MAE   |   RMSE   |   MAPE   |   MAE   |   RMSE   |   MAPE   |   MAE   |   RMSE   |   MAPE   |
| ---------------- | ------- | -------- | -------- | ------- | -------- | -------- | ------- | -------- | -------- | ------- | -------- | -------- |
| PEMSD7           | 2.04    | 3.53     | 4.77     | 2.67    | 4.80     | 6.60     | 3.17    | 5.79     | 8.00     | 3.48    | 6.39     | 9.04     |
| PEMSD8           | 1.03    | 2.08     | 1.86     | 1.39    | 2.80     | 2.67     | 1.62    | 3.28     | 2.67     | 1.74    | 3.57     | 3.50     |
| DIVE             | 0.95    | 1.76     | 2.01     | 0.96    | 1.69     | 2.03     | 0.91    | 1.69     | 1.94     | 12.61   | 26.23    | 26.23    |

