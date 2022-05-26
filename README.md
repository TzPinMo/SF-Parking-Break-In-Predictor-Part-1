# SF-Parking-Break-In-Predictor
Building a classification models to train on 5 years of SFPD data to predict level of break-in risk when parking

Data Source: https://data.sfgov.org/Public-Safety/Police-Department-Incident-Reports-2018-to-Present/wg3w-h783
Dataset: https://drive.google.com/file/d/1nV9_STKb-F0zhr_iQmkPIbVVEUs1Djpg/view?usp=sharing

“The car break-in capital of the world”, which is another name for San Francisco. Even right now, there are many cars broken-in and stolen stuff out of cars. According to articles, car break-ins happen 74 cars in a day (NBC, 2021), and more than 3,000 cars in a month, November 2021 (CBS, 2021). It undermines San Francisco’s reputation, which is a representative city in the US, and damages the social community. In addition, criminals of car break-ins mainly target tourists because most of them are struggling from handling the cases and they are having more valuables in a car. Due to these reasons, bad reputations of San Francisco have been widespread in the world. Drivers should consider safety from car break-in when they park in the city. We are coming up with a social good product which informs people about the danger level of the current location, so that drivers can avoid dangerous places and park their cars at safer places.

To give driver's a “peace of mind,” the best way could be by showing users whether their selected spot would be safe for parking. 

To help drivers estimate whether a parking spot is risky or not, we will be implementing a classification model that can learn from historical data to recognize patterns and identify which “class” the input data belongs to, i.e. low risk/medium risk/high risk to park. We have obtained public data from SFPD that could be leveraged to help train the model. The data includes valuable potential variables such as crime type, location, coordinates, day of week, and time of crime - we assume these factors contribute to whether an area is safe to park. 

## Part 1: Model Training

To train the classification model, labels (Y variable) were added to our datasets so that the model can learn how different X variables might lead to specific classes. In this scenario, the labels include “low risk”, “medium risk”, and “high risk” based on where  and when the break-in happened. Using PySpark, we were able to label the data and the methodology and rules are as follows: 

1) We first conducted EDA to see what the break-in counts are per neighborhood / day of week / time of day.
2) Based on the break-in incident counts, the percentile is used to label an area and corresponding time details as “low risk”, “medium risk”, and “high risk” - the higher the percentile, the riskier it is. The cut off for respective categories are 33rd percentile and 66th percentile. 

The following steps were taken to arrive at the final model:
1) Data cleaning: NAs were removed and categorical variables were converted using One Hot Encoder
2) Train Test split: 70% of the data was used to train the model, and the 30% was preserved for testing
3) Classification Model training: Both Random Forest and Multinomial Logistic Regression algorithms were used to train the model.
4) Classification Model testing: The model was tested with the reserved data and accuracy rate was calculated for both algorithms.
