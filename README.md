## ML-Finance
some projects about finance in machine learning


### Bankrupt Prediction
1. The problem is asked to predict companies’ bankrupt probability of given unbalanced financial data. But the bankrupt sample is unbalanced, and predict a to-be bankrupted company into not bankrupted will get worse loss.
2. Cleaned data and chose features by Random Forest, used Logistic Regression to predict. Set different weights and thresholds to aviod unbalanced data and unsymmetrical influence and choose features and AUC to choose models.


### Return Prediction
1. According to the AAPL's return and related stock return, using Machine Learning, combining LSTM, GRU and Logistic Regression to predict AAPL's future return.
2. Combined LSTM (to predict return directly), GRU (to predict stock price and use prediction to get predicted return) and Linear Regression models (use a classification model to predict the return)  to predicted AAPL’s daily return by feature engineering and error analysis.


### Titanic Problem
1. It a problem in Kaggle, about the Titanic disaster. Given some basic data of all the people on this ship, we should give a solution to predict a person was survived or not.
2. Devised feature engineering and Random Forest to predict Titanic passenger’s survival situation
