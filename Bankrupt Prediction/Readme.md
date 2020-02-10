## Bankrupt Prediction

### Abstruct
Predict companies’ bankrupt probability of given unbalanced financial data by Logistic Regression. Set different weights and thresholds to aviod unbalanced data and unsymmetrical influence and used Random Forest to choose features and AUC to choose models.

### Solution
1. how to process the missing data?  
> I try two ways, one is processing the features, make some similar features with no missing to replace; another is to delete or fill the missing samples.    
> I think the first way is better. Because for financial indicators, it is not reasonable to use average or midean to replace the missing value. So I generate many features to replace features with many missing.

2. how to choose useful features?
> I use logical analysis: I believe we majorly need three factors: asset and leverage, operating situation, sales and profit. And the financial indicator which is divededy by total asset is better, because if it is divededy by sales, but sales can be very small or even negative. So I make and choose features in show these information and are devided by totally asset.   
> I also use Random Forest to see the importance of features and delete some.   

3. how to deal with imbalanced data?
> I use AUC to show judge the model.  
> I set different weights to 0 and 1.

### Conclusion
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrrdefd1xj318o0nmgmr.jpg)
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrrdkrx9kj317y0jmt9z.jpg)
![](https://tva1.sinaimg.cn/large/0082zybpgy1gbrrdvs5lmj319k0bggmn.jpg)

