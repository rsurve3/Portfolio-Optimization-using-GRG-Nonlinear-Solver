# Portfolio-Optimization-using-GRG-Nonlinear-Solver

 
**Abstract**

Diversification is the practice of spreading your investments to ensure that the exposure to any one type of asset is limited. This practice is designed to reduce the volatility of your portfolio over time.

The key to successful investing is learning how to balance your portfolio’s comfort level with risk against your time horizon. The best way to balance risk and reward in your investment portfolio is to diversify your assets. This will help ensure that you do not put all your eggs in one basket and lay everything on the line, but rather mitigate the risk and volatility of your portfolio.

Therefore, there is the necessity for us to research about ways to correctly identify how to go about diversifying your investments. In this report, we will explore how utilizing the solver function in Excel can help us achieve this goal. While excel has previously been used to identify which stocks to invest in, we took it a step further by additionally leveraging it to decide how much to invest in each stock we do decide to invest in.




**Introduction**

A mutual fund is a type of financial vehicle made up of a pool of money collected from many investors to invest in securities like stocks, bonds, money market instruments, and other assets. Mutual funds give small or individual investors access to diversified, professionally managed portfolios at a low price. As a mutual fund investor, you don’t directly own the stock in the companies the fund purchases but share equally in the profits or losses of the fund’s total holdings, one of the reasons they’re called “mutual funds.”

The prospect of not investing all your money in a single stock, but rather in a pooled collection of assets is what makes it the perfect model to work on for our analysis.

The theme of this project is to optimize the weight of the stocks involved in a mutual fund portfolio on the basis of their returns over a period of time, while also not concentrating our investment in just a few stocks to make it as risk-averse as possible.  

**Overview of Axis Bank Mutual Fund**

For the purpose of our research, we picked the Axis Bank Mutual Fund. It’s a mutual fund which is a collection of stocks of 12 different companies - namely HDFC, ICICI Bank, SBI, Kotak Mahindra Bank Ltd, Axis Bank Ltd, Indusind, AU Small Finance Bank, Bandhan Bank Ltd, Federal Bank, RBL Bank, PNB Bank, IDFC First Bank. 

Axis Mutual Fund launched its first scheme in October 2009. And since then, Axis Mutual fund has grown strongly. They attribute their success thus far to 3 founding principles - Long term wealth creation, customer view and Long term relationship. 

We picked this fund as we were able to easily procure all the historical data for this fund from Yahoo Finance, as well as the fact that a great performing fund such as this one gave us a great benchmark to work with to assess how our optimization algorithm performs. 

**Motivation & Hypothesis**

While the AXIS Bank Mutual Fund has been performing admirably over the past years, we observed that the distribution of the investments is slightly risky, with ~86% of the proportion of the investments being currently held by just 5 out of the 12 companies. 

Thus, we wanted to use the solver function in Excel to redistribute the weights of the investments with constraints that limit the weightage of the stocks within a permissible limit that will allow the risk to be reduced. 

Our hypothesis is that using the past returns of the stocks would allow us to ensure that we are investing higher in the more profitable stocks, while the constraints on the investment weights would ensure that we do not invest all our resources in just the most profitable stocks. 

Even if this allows us to match the portfolio’s current returns, we would consider our algorithm a success as we were to match those returns with much lower risk. And if we’re able to improve the returns, it would definitely add a feather to the cap.

**Data Collection**

Input data used for this analysis includes opening price of stock for particular trading day and daily percentage change in price of stock as compared to previous day. This data was collected from various sources like moneycontrol website, National Stock Exchange (NSE India), Bombay Stock Exchange (BSE India), Securities and Exchange Board of India(SEBI), Axis Bank Mutual Fund - Banking Fund Monthly statements and Yahoo finance. Data from Axis Bank Mutual Fund was used to determine which stocks are included in the mutual fund portfolio and the ratio of investing the net investments into all the stocks is also fetched from the mutual fund statements provided by mutual fund house i.e., Axis bank. The NSE, BSE and Yahoo Finance provided the accurate data of opening prices of stocks from January 1, 2021 to June 15, 2021. NAV of each unit of mutual fund was fetched from Yahoo Finance webpage to calculate the returns from January 1, 2021 to June 15, 2021.


We fetched data of stocks from June 30, 2021 to October 1, 2021 to compute the expected results after investing in optimized allocation ratios of investing, in all the stocks present in the mutual fund portfolio. 


**Data preparation**

**Covariance**

Excel has two functions to calculate variance Covariance.P and Covariance.S. Function Covariance.P is used to calculate covariance of population data and Covariance.S is used to calculate covariance of sample data. We have used Covariance.S since we have to calculate sample covariance.
Formula to calculate Covariance.S is:

Sample Covariance = Σ(xij – x’)2 / (n-1)
In this formula
1. Σ   : Denotes Summation this is a Greek symbol
2. Xij : The value of dataset which is in Row i and Column j
3. X’  : Denotes Mean value of the dataset
4. N  : The total number of observations

![image](https://user-images.githubusercontent.com/122759737/214118652-b407138e-9e5c-4e31-8b76-28ce669cc230.png)


**Correlation coefficient**

Correlation coefficient is the statistical unit that measures the degree to which two stocks are related to each other. Correlation coefficient can be in the range of -1 to +1. Where 0 represents no correlation between two stocks. 0 to +1 denotes positive correlation which means both the stocks are positively correlated if the price of one stock increases the the price of other stock will also increase. If the Correlation coefficient lies between -1 to 0 this means that both the stocks are negatively correlated, which means price of both the stocks would travel in opposite direction.

-1  : Perfect negative correlation 
0   : No correlation
+1 : Perfect Positive correlation
 
Correlation coefficient Formula:

![image](https://user-images.githubusercontent.com/122759737/214118695-f89cb291-9bb6-4ca8-8460-a809b4c418a7.png)
 

Where:
1. n   : Total of observations
2. x   : Array 1 
3. y   : Array 2
4. Σx : Summation of all the observations in Array 1
5. Σy : Summation of all the observations in Array 2
6. Σxy : Summation of products of observations in Array 1 and Array 2

![image](https://user-images.githubusercontent.com/122759737/214119021-9b3a59a8-03fb-47ec-8a36-0b49b31a9f9f.png)

**Model development** 

![image](https://user-images.githubusercontent.com/122759737/214119839-c928b74f-21fb-459a-9902-faeb3ca165e2.png)


After preparing the data and calculating the covariance of stocks, we calculate the average returns of all the 12 stocks in the Axis Bank mutual fund. The average return is basically the average of the daily percentage change of all the stocks over the period of 6.5 months.
                    
The further step would be to calculate the returns of each stock over the time period. To do so, we subtract the price of the stock on 15 June 2021 (which is the last data point in our dataset) and price of stock on 1st January 2021 which is then divided by the 1st day stock price. This would give us the percentage of the returns that a particular stock has given from January 1, 2021 to June 15, 2021. 

![image](https://user-images.githubusercontent.com/122759737/214119137-c11807f1-de7b-4497-88a4-67b8f122f1cc.png)


As shown in the figure above, we can see that the 6 months return of HDFC bank is 3% over the period of 6 months from January 2021 at which the price was INR 1440 to June 2021 on which price of stock hiked to INR 1486, ICICI Bank gave a return of 19% and so on.

Weights of the stocks are the percentages of stocks bought in the mutual fund. The 12 stocks collectively comprise 100% of the portfolio. The optimized weight of the stock column are the decision variables for our portfolio optimization model. Decision variables are changing variables wherein the excel's solver function adjusts the values in these cells to satisfy the given constraints and further produce the optimal result from the objective cell.


![image](https://user-images.githubusercontent.com/122759737/214119357-0809e3c7-5bf9-463e-9ebe-86907abf2089.png)


We calculated the total portfolio return over the period of 6 months, this can be done using the sumproduct formula in excel wherein the two parameters are: Return of individual stocks and the decision variables i.e. Optimized weights of stocks. 

The portfolio return turns out to be 28% over the given period of time. The risk aversion component of a portfolio is expressed as variance of the portfolio which is found by using the same sumproduct function using the optimized weight of stocks and the covariance of each stock with each other. Covariance is the statistical measure of relationship between two stock prices and a positive covariance implies that the stocks generally move in the same direction. 

By taking the square root of the variance we get the standard deviation which is used to measure the volatility of an investment. The standard deviation for our model turns out to be 2.079%. 

Lastly, Sharpe ratio is calculated which measures the performance of an investment such as a portfolio to a risk free asset. In other words, it is a metric to compare the risk free rate to the designed portfolio. Maximum the sharpe ratio, higher is the return on the investment. 

![image](https://user-images.githubusercontent.com/122759737/214119384-7c82dcd4-b5b6-4a03-999a-6a0433355831.png)
                            

Objective of the portfolio optimization model is to maximize the sharpe ratio to earn higher returns  on our investment. In order to do so, we use excel's solver function to optimize the portfolio by setting the objective to maximize as sharpe ratio with constraints such as no investment should be less than 5% and greater than 15% in order to avoid over allocation of funds in any single stock which would result in reducing the risk by diversifying the portfolio.
With the help of the GRG NonLinear algorithm we solve our model and compute the maximum sharpe ratio as 10.634 while all the constraints are satisfied. It is necessary to use the GRG nonlinear method of solver in this case rather than simplex or evolutionary methods because the portfolio optimization model is a nonlinear problem and can be only solved by GRG Nonlinear algorithm
                                     


![image](https://user-images.githubusercontent.com/122759737/214119418-ddbb7810-bec5-48d8-8c84-4a6ab8893f13.png)

   
   
**Results**

From Jan 1, 2021 to June 15, 2021, the Axis Bank Mutual Fund is giving 13.274% return. After running GRG - Nonlinear solver on our model, where the risk free rate is 6% and the standard deviation i.e. volatility of the stock is 2.0769%, we get the sharpe ratio as 10.6334. Also, after running the solver, the weights of the stocks i.e. the changing variables of our model are optimized while adhering to the model constraints as follows:-


![image](https://user-images.githubusercontent.com/122759737/214119503-e9c61696-8537-4cbc-8f1f-4610568379a0.png)


After the stock weights are optimized, the portfolio return rises from 13.274% to 28.085%. That is a whopping 111% increase. 





The biggest changes in the stock weight allocation can be seen in HDFC and ICICI bank whose weights were reduced from 27.50% and 22.85% to a meagre 5%. However, subsequently the weights of IDFC First Bank, Federal Bank and AU Small Finance Bank were increased from 1.22%, 1.53% and 2.34% to 15%, 13% and 14% respectively. 

Now after finding the weights of the stocks to be invested in, we compared the optimized weights of stocks versus the original weights of the stocks in Axis Bank Mutual Fund for the next three months i.e. from 30 June, 2021 to 1 October, 2022. 

After calculation, we found out that the compound annual growth rate and the monthly compound rate of the original weights of stock is 25% and 2.09% respectively, while that of optimized weights of stocks is 39.14% and 3.26% respectively. 


![image](https://user-images.githubusercontent.com/122759737/214119529-43ba7b3d-1296-4e50-9d82-73e421c89571.png)


**Assumptions** 

1. The investment horizon is fixed for all the investors which is from June 30, 2021 to October 1, 2021, which means every investor does his investment on 30th of June 2021 and returns are calculated on 1st of October 2021.
2. For optimization of allocation ratios of stocks we have used data from January 1, 2021 to June 15, 2021 which is roughly about five and half months of data. Whereas all the companies present in the portfolio were listed on the stock market more than 10 years ago. So considering the five and half months of data to optimize the allocation percentages would not provide the best possible allocation ratios.
3. We are also not taking into account major Socio-Economic series of events which might have considerable impact on the stock market, these can include a lot of events like global recession, outbreak of pandemic like Covid-19, geopolitical events etc.
4. Another assumption is there are no changes in rules and regulations by governing bodies like Reserve Bank of India (RBI) and Securities and Exchange Board of India (SEBI). Any changes or measures by these governing bodies can also have an impact on the performance of stocks in the stock market.
5. Also the grants and packages offered by the government of India for a particular industry can have significant impact on the performance of a particular sector or industry, these events are also not taken into consideration.







**Limitations**

1. This optimization model cannot factor arbitrage opportunities because such opportunities are for shorter investment horizons and we have a fixed investment horizon of about 3 months.
2. Various ratios such as Repo rate and Reverse Repo rate are also not factored into the model because these rates are dynamic and they are regulated by the Reserve Bank of India (RBI).
3. Various Stock market events like offering of Bonus shares, Stock splits, merger of two or more companies, foreign investments, performance of Indian economy as compared to performance of global economy, delisting of stock, offer of FPO by company, promoters reducing their stake, announcement of dividends, etc which can have considerable impact on the stocks in mutual fund portfolio, are also not considered in this analysis model due to lack of resources.
4. Addition of new stock due to exceptional performance of stock during investment horizon or removal of stock due to poor performance are also not considered during the entire investment window which is from June 30, 2021 to October 1, 2021.










**Conclusion**

![image](https://user-images.githubusercontent.com/122759737/214119574-f6a5bb25-4960-43f6-b58f-9a8e5b21f7a8.png)


Upon computing the allocation returns of the optimized portfolio it can be concluded that the CAGR Compounding Annual Growth Rate) of the original portfolio was 25% and the CAGR (Compounding Annual Growth Rate) of the optimized portfolio was 39.12%, which is approximately 14% higher than the original portfolio.

The graph illustrates returns on investment if $1000 were invested in a risk free asset, original portfolio and optimized portfolio. If an investor invests in  a risk free asset, original portfolio and optimized portfolio they would receive $1,060, $1,250, $1,391.2 respectively after one year. In this case the investor is receiving $141.2 higher returns on the principal amount of $1,000 if invested in the optimized portfolio.



















