#Create a dataframe holding the closing price for each stock in the last year.
#By how much (in percents) did the price of each stock vary over the last year? Draw a barplot, in which the x-axis represents stocks, and the y-axis represents the change in percents.
#Generate a random array of 5 integers between 10-100 that represent the number of stocks in your protfolio.
#Draw a pie chart representing the composition of your protfolio at the beginning of year (in US$).
#Plot the daily value of your protfolio over the last year.
#Plot a scatter matrix to check for correlations in the daily changes of stock prices.


from pandas_datareader import data, wb
import pandas_datareader.data as web
import datetime
import matplotlib.pyplot as plt
import pandas as pd
from pandas import Series, DataFrame
%matplotlib inline
from pandas.tools.plotting import scatter_matrix
import numpy as np

#PART 1 Create a dataframe holding the closing price for each stock in the last year

start = datetime.datetime(2016, 1, 1)
end = datetime.datetime(2016, 12, 31)
stocksdf = DataFrame() #New dataframe to store the prices
symbols = [["AAPL"],["GOOG"],["FB"],["XOM"],["NFLX"]] #List with the stocks

for i in range(5):
    f = web.DataReader(symbols[i], 'yahoo', start, end)
    df= f.minor_xs(symbols[i][0])
    stocksdf[symbols[i][0]] = df['Close']
stocksdf.head()

#PART 2 By how much (in percents) did the price of each stock vary over the last year?
prices_start = stocksdf.iloc[0]
prices_end = stocksdf.iloc[-1]
((prices_end-prices_start)/prices_start*100).plot.bar()
plt.gca().axhline(0,color='k')

#PART 3a #Draw a pie chart representing the composition of your protfolio at the beginning of year (in US$).

NumberStocks = np.random.randint(10,100, size=5)
Portfolio = pd.Series(NumberStocks*prices_start,name='Portfolio',)
Portfolio.plot.pie(figsize=(4,4),autopct='%.2f')
print('Price of stocks')
print(prices_start)
print('\n')
print('Number of Stocks')
print(NumberStocks)
print('\n')
print('Composition of portfolio in USD')
print(Portfolio)

#PART 3B Plot the daily value of your protfolio over the last year.
dfPortfolio = stocksdf * NumberStocks
dfPortfolio['TOTAL'] = dfPortfolio['AAPL'] + dfPortfolio['GOOG'] + dfPortfolio['FB'] + dfPortfolio['XOM'] + dfPortfolio['NFLX']
dfPortfolio.head()
dfPortfolio['TOTAL'].plot()

#PART 4 Plot a scatter matrix to check for correlations in the daily changes of stock prices
dfDailyChange = stocksdf.pct_change(1)
scatter1= scatter_matrix(dfDailyChange)
scatter2 = scatter_matrix(dfDailyChange, alpha=0.2, figsize=(6, 6), diagonal='kde')
