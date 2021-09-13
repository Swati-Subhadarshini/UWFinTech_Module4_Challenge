# UWFinTech_Module4_Challenge
## Risk Return Analysis

This project is designed for quantitative analysis used in FinTech investing platform. This project aims to offer clients a one-stop online investment solution for their retirement portfolios that’s both inexpensive and high quality by evaluating four new investment options for inclusion in the client portfolios. The code and analysis of different graphs and visualization helps in determining whether the fund with the most investment potential based on key risk-management metrics: the daily returns, standard deviations, Sharpe ratios, and betas.


---

## Technologies Used

Leveraging Jupyter Notebook
Gitbash CLI is used to pull and push the code from local repository to remote repository
Code written with the help of Jupyter Notebook.
Using the .csv file for the data.

---

## Libraries and Dependencies

import pandas as pd
from pathlib import Path
import numpy as np
%matplotlib inline

---
## Analysis 

To analyse the data first import a CSV file and prepare your daily returns DataFrame for analysis. Then, you’ll do a quantitative analysis that includes the following:

import and read the whale_navs.csv file.
 `whale_df = pd.read_csv(Path("whale_navs.csv"), index_col="date", parse_dates=True, infer_datetime_format=True)`
Use the Pandas pct_change function together with dropna to create the daily returns DataFrame.
  `whale_daily_returns = whale_df.pct_change().dropna()`
  `whale_cumulative_returns = (1 + whale_daily_returns).cumprod()`

1. Performance

2. Volatility

3. Risk

4. Risk-return profile

5. Portfolio diversification

### Performance Analysis:

Analyze the data to determine if any of the portfolios outperform the broader stock market, which the S&P 500 represents.
Through plots visualise the daily return values

`whale_daily_returns.plot(figsize=(15,10), title="Whale NAVs Daily Retun Dataframe Plot")`

Use the Pandas cumprod function to calculate the cumulative returns for the four fund portfolios and the S&P 500.

`whale_cumulative_returns.plot(figsize= (15,10), title="Cumulative Returns Plot")`

### Volatility Analysis:

Use the Pandas plot function and the kind="box" parameter to visualize the daily return data for each of the four portfolios and for the S&P 500 in a box plot
`whale_daily_returns.plot(kind='box', figsize=(15,10), title="Box Plot of Daily Returns")`

### Risk Analysis:

- Evaluate the risk profile of each portfolio by using the standard deviation and the beta. 
- Use the Pandas std function to calculate the standard deviation for each of the four portfolios and for the S&P 500. 
    `whale_std_df = whale_daily_returns.std()`
    
- Calculate the annualized standard deviation for each of the four portfolios and for the S&P 500 (formula standard deviation * the square root of     the number of trading days)
    `whale_annual_std = whale_std_df * np.sqrt(trading_days)`
    
- Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of the four fund portfolios and of the S&P 500   index

  `whale_std_21.plot(figsize=(15,10), title="21 days Rolling Standard Deviation of 4 portfolios and S&P 500")`
  
- Use the daily returns DataFrame and a 21-day rolling window to plot the rolling standard deviations of only the four fund portfolios. 

  `new_whale_std_21.plot(figsize=(15,10), title="21 days Rolling Standard Deviation of 4 portfolios")`
  
### Risk-Return Analysis:

To determine the overall risk of an asset or portfolio, quantitative analysts and investment managers consider not only its risk metrics but also its risk-return profile. After all, if you have two portfolios that each offer a 10% return but one has less risk, you’d probably invest in the smaller-risk portfolio. For this reason, you need to consider the Sharpe ratios for each portfolio. 

- Use the daily return DataFrame to calculate the annualized average return data for the four fund portfolios and for the S&P 500. Use 252 for the number of trading days. 

    `annual_average_return = whale_daily_returns.mean() * trading_days`
    
- Calculate the Sharpe ratios for the four fund portfolios and for the S&P 500. To do that, divide the annualized average return by the annualized standard deviation for each.

    `sharpe_ratio = annual_average_return / whale_annual_std`
    
- Visualize the Sharpe ratios for the four funds and for the S&P 500 in a bar chart. 
    `sharpe_ratio.plot(kind='bar', figsize =(15,10), title="Bar Chart for Sharpe Ratios of 4 funds and the S&P 500") `
    
### Diversify the portfolio:
- Use the Pandas var function to calculate the variance of the S&P 500 by using a 60-day rolling window
    
    `market_variance = whale_daily_returns['S&P 500'].rolling(window=60).var()`
    
- Using the 60-day rolling window, the daily return data, and the S&P 500 returns, calculate the covariance
    `bh_rolling_60_covariance = whale_daily_returns['BERKSHIRE HATHAWAY INC'].rolling(window=60).cov(whale_daily_returns['S&P 500'])`

- Calculate the beta of bh_beta_rolling_60 = bh_rolling_60_covariance / market_variancef the portfolio. To do that, divide the covariance of the portfolio by the variance of the S&P 500.
    `bh_beta_rolling_60 = bh_rolling_60_covariance / market_variance`

-Use the Pandas mean function to calculate the average value of the 60-day rolling beta of the portfolio.
    `bh_avg_rolling_60_beta = bh_beta_rolling_60.mean()`
    
- Plot the 60-day rolling beta.
   `bh_beta_rolling_60.plot(figsize=(15,10), title= "Berkshire Hathaway INC 60 Days rolling beta", color="purple")`
   
With similar way we can get beta value, sharpe values of the no of portfolios we wanted to include.
By analysing daily returns, standard deviation, sharpe ratio, beta values we can decide which stock is more volatile in the market and also rewarding good returns. Those stocks can be included in the firm's suite for the clients fund investment. 
    
## Contributors

This project is designed by Swati Subhadarshini 
Emaid id: sereneswati@gmail.com
LinkedIn link: https://www.linkedin.com/in/swati-subhadarshini-89a8a538?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3BhUCLlUYCSc2jK4x4khPVUQ%3D%3D

---