## Bankrupt Prediction

### Abstruct
According to the AAPL's return and related stock return, using Machine Learning, combining LSTM, GRU and Logistic Regression to predict AAPL's future return. 

### Solution
1. Data Cleaning

2. I use **three different ways** to predict return of AAPL and combine them toghter to give the final prediction. The Final result just include the first and the second one.
> 1. I fisrtly try to predict return by different models. (choose LSTM model)   
> 2. Secondly, I predict stock price and use prediction to get predicted return. (GRU)
> 3. Finally, I use a classification model to predict the return. (Logistic Regression)

3. Combined this three models to predict daily return by feature engineering and error analysis. The result shows, the model mostly learned the average trend, and merely volatility.

### Conclusion
1. Predict return directly could only learn average trend.
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrqxhseufj30yw0gm75f.jpg)

2. Predict price and then calculate return
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrqyd6p9kj30y60eut98.jpg)
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrqywluidj30xq0ecgml.jpg)

3. Turn it into a classification problems. Predict the category of returns.
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrr0p7w9mj30xs0g40tq.jpg)


