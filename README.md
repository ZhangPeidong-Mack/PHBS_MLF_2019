# PHBS_MLF_2019
MLF Team Project

## Team members:
Name                   |     Student ID    |     GitHub ID
-----------------------|-------------------|---------------------------------
Hu Tianrui(胡天锐) | 1901212587 | [PeterHuTHU](https://github.com/PeterHuTHU)
Yu Haiyang(余海洋) | 1901212663 | [Yavin-1018](https://github.com/Yavin-1018)
Zhang Peidong(张培栋) | 1901212671 | [ZhangPeidong-Mack](https://github.com/ZhangPeidong-Mack)
Zhong Lin(钟林) | 1801212992 | [zhong-lin-pku](https://github.com/zhong-lin-pku)

## Project goal
Our goal is to predict trends of stocks and their future prices. We will use classifiers such as SVM, decision tree and random forest to predict trends of stocks and then compare advantages and disadvantages of each algorithm. Then we will use models such as linear regression, SVM, random forest and Multi-Layer Perceptron to predict specific prices, again we will compare advantages and disadvantages of each model. Other skills such as k-fold cross-validation will also be applied.

## Data Description
We use trading data of Shenzhen Stock Exchange and Shanghai Stock Exchange from 2017-01-01 to 2019-12-31. Features include the opening price, closing price, highest price, lowest price, trading volume and turnover. The dataset is too large so we only upload part of it. Click [here](https://pan.baidu.com/s/1aaYOzaOtSxtKzsZU-PMNlg) with extraction code "nspy" if you want to see a complete version of our data.

## Data Preprocessing
Raw data collected from JQ-Quant Database needs to be cleaned and features can therefore be derived from processed data. 

Several stocks was delisted during the past 3 years, for those stocks which are not qualified for trading, we removed them from the stock pool. For the remaining stocks, their nan data due to trade suspension are filled using the previously most close available data. In this way, we finally get rid of all the nan values and can proceed to the next session.

Then we import the package 'talib'. Using this package, we calculated several popular technical factors, including MOM stands for Momentum, RSI stands for Relative Strength Index, EMA stands for Exponential Moving Average, MACD stands for Moving Average Convergence / Divergence and ATR stands for Average true range. These factors will be used to build our models to predict trends of stock prices according to their factor loadings.

Finally, we turn the daily frequency data into week frequency data. In the transformation, we view every 5 trading days as a week. Then we classify weeks into odd number weeks and even number weeks. For example, week 1, week 3 belong to the former class and week2, week 4 belong to the latter class. If stock return in one particular even number week, namely week 2t is negative, then we label corresponding Yt to be -1, and vise versa. Factors in week 2t-1 are viewed as Xt, we make pairs of (Xt, Yt) and our goal is to build models to predict Yt based on corresponding Xt.
## TEST YU
hello

## Applying SVM model
The purpose of this part is to derive an SVM model to predict trends of stock prices using the factors stated above.

We devide our data set into training set and test set. According to datetime, the former 80% belongs to the training set and the rest belongs to test set. We devide data according to datetime in order to avoid the influence of so called future information.

In order to reduce the time of computing, we use pca method to deduct dimensions. We observed that the 3 most import features can explain almost 90% of all the variance, so we used pca method and set components equal to 3. 

Then we tried to use linear kernel to build our model, but several problems occured. First of all, size of training data is too big(almost 180000 sample points), making the model building process very slow.Secondly, because the market behaved very bad in Year 2018, the label '-1' in training set appears much more often than the label '1', which will lead to the problem of sample imbalance.

To solve the problems stated above, we changed the training set. We randomly select 1000 sample points whose Y is labeled as '1' and 1000 another labeled as '-1', along with X corresponding to those Y we form a new 'training set'. We tested kernels like 'rbf' and 'linear', along with different parameters. We found that when using 'linear' kernel and set C=10.0, the model behaved fairly well. The result of it is listed as follows. We can see that the accuracy is about 57.9% on the test set and the precision and recall rate are all at a acceptable level. Also accuracy of 57.9% seems to be not to high, but if we employ a investing strategy based on this model, because of law of large numbers, we can expect the stratrgy to receive a nice return.
![](https://github.com/PeterHuTHU/PHBS_MLF_2019/blob/master/1.png)

![](https://github.com/PeterHuTHU/PHBS_MLF_2019/blob/master/2.png)
