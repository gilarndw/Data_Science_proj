# Data Science Tesla Stock Analysis per August 2021: Overview
* Created plot to analyze Tesla stock market movement
* Calculated market capital
* attempted to create basic linear regression model 
* Analized tesla stock price volatility

## Tools and Resources
* **Python**: Version 3.7
* **Notebook**: Google Colab
* **Libraries**: pandas, matplotlib, numpy, statsmodel, scipy
* **Datasets**: https://finance.yahoo.com/quote/TSLA/history?p=TSLA

## Data Preparation
### Attributes
* Date: Date of stock data recorded
* Open: Opening stock price 
* High: Highest stock price traded during a period
* Low: Lowest stock price traded during a period
* Close: Closing stock price 
* Adj. Close: Adjusted stock price for dividend distributions
* Volume: Stock's volume during a period

## Data Cleaning
* Checked null values, in this case there was no null value in this datasets
* Because the Adj. Close is identical with Close, I cleared the Adj. Close column

![image](https://user-images.githubusercontent.com/60825743/137606705-6f87440b-824d-45a4-a5fa-e113b24db2ef.png)

## Data Visualization
* Visualized Close price and Volume trend
![image](https://user-images.githubusercontent.com/60825743/137606738-cd504ef2-3623-4c43-857c-9d631f175046.png)
![image](https://user-images.githubusercontent.com/60825743/137606888-4cdd8df0-5b64-42bd-a199-c158b4d55d23.png)
* Created Market Cap column by multiplying Open price and Volume
![image](https://user-images.githubusercontent.com/60825743/137606929-cc23ee1b-f06e-46a8-bd34-c9bfd6bcba86.png)
![image](https://user-images.githubusercontent.com/60825743/137606986-0013a487-37ec-48dc-8ec3-f337d9edfcb3.png)

## Creating Prediction Model
* I attemped to try creating a simple and basic linear regression model using statsmodel library to predict the price of tesla stock

```
model = smf.ols('Close ~ Market_Cap + Volume', data = tsla_raw)
results = model.fit()
print(results.summary())
```
![image](https://user-images.githubusercontent.com/60825743/137607169-40ca0d94-1ee9-47f3-bf35-6a9fff240e87.png)

* From the model showed that all of the features are related
* However, I tested the model manually, and the results are barely close to the actual value
```
def Predict_Close(Market_Cap,Volume):
 return(2.015e-08 * Market_Cap - 3.852e-06 * Volume + 77.2798)

print(Predict_Close(9.297897e+09,13083100)) #Market Cap and Volume on 2021-08-24
print(Predict_Close(1.373380e+08,34334500)) #Market Cap and Volume on 2010-07-06
print(Predict_Close(1.322403e+10,18502400)) #Market Cap and Volume on 2021-08-30
```
the results are:

214.23632334999996 (Actual Value 708.489)

-52.2093333 (Actual Value 3.222)

272.4727597 (Actual Value 730.909)
* I have to fix and develop another model in order to use it as prediction 

## Analyzing Tesla stock volatility
* Added volatility column
```
#Now we going to find the Volatility of Tesla Stock
tsla_raw['Vol'] = tsla_raw['Close']/tsla_raw['Close'].shift(1) - 1
tsla_raw
```
![image](https://user-images.githubusercontent.com/60825743/137607560-c25c37bc-236a-4866-9919-861a4972b25d.png)
* From the trend above we can see that tesla stock is quite volatile
* Tesla stock average gain percentage from 2010 until 2021 is around 0.2%
* The maximum gain percentage is up to 20% 
* The maximum loss percentage is up to 20% also
