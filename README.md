# Visibility_CLimate

## Table of Content
    * Demo
    * Overview
    * Process
    
    
## Demo

Data Description: This dataset predicts the visibility distance based on the different indicators as below:

1.	VISIBILITY - Distance from which an object can be seen.
2.	DRYBULBTEMPF-Dry bulb temperature (degrees Fahrenheit). Most commonly reported standard temperature.
3.	WETBULBTEMPF-Wet bulb temperature (degrees Fahrenheit).
4.	DewPointTempF-Dew point temperature (degrees Fahrenheit).
5.	RelativeHumidity-Relative humidity (percent).
6.	WindSpeed-Wind speed (miles per hour).
7.	WindDirection-Wind direction from true north using compass directions.
8.	StationPressure-Atmospheric pressure (inches of Mercury; or ‘in Hg’).
9.	SeaLevelPressure- Sea level pressure (in Hg).
10.	Precip	Total-precipitation in the past hour (in inches).





## Overview

1.Data Validation 
2.Model Training 
3.Prediction Data Description
4.Prediction 

## Code details

1) Data Export from Db - The data in a stored database is exported as a CSV file to be used for model training.
2) Data Preprocessing   
   a) Drop columns not useful for training the model. Such columns were selected while doing the EDA.
   b) Replace the invalid values with numpy “nan” so we can use imputer on such values.
   d) Check for null values in the columns. If present, impute the null values using the KNN imputer
   e) Scale the training and test data separately 
3) Clustering - KMeans algorithm is used to create clusters in the preprocessed data. The optimum number of clusters is selected by plotting the elbow plot, and for the dynamic selection of the number of clusters, we are using "KneeLocator" function. The idea behind clustering is to implement different algorithms
   To train data in different clusters. The Kmeans model is trained over preprocessed data and the model is saved for further use in prediction.
4) Model Selection - After clusters are created, we find the best model for each cluster. We are using two algorithms, "Decision Tree Regressor" and "XGBoost regressor". For each cluster, both the algorithms are passed with the best parameters derived from GridSearch. We calculate the Rsquared scores for both models and select the model with the best score. Similarly, the model is selected for each cluster. All the models for every cluster are saved for use in prediction. 


# Prediction 
 
1) Data Export from Db - The data in the stored database is exported as a CSV file to be used for prediction.
2) Data Preprocessing   
   a) Drop columns not useful for training the model. Such columns were selected while doing the EDA.
   b) Replace the invalid values with numpy “nan” so we can use imputer on such values.
   c) Check for null values in the columns. If present, impute the null values using the KNN imputer.
   d) Scale the training data.
3) Clustering - KMeans model created during training is loaded, and clusters for the preprocessed prediction data is predicted.
4) Prediction - Based on the cluster number, the respective model is loaded and is used to predict the data for that cluster.
5) Once the prediction is made for all the clusters, the predictions along with the original names before label encoder are saved in a CSV file at a given location and the location is returned to the client.



























