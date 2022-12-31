---
title: An Analysis of Derivatives Strategies
author: Daniel Sineus
date: '2022-12-30'
slug: an-analysis-of-derivatives-strategies
categories: []
tags:
  - Academic
subtitle: ''
summary: 'The purpose of this paper is to examine the payoffs and trading strategies referring to a portfolio that consists of options on given assets. The underlying assets are Apple, Meta (Before called Facebook) and Tesla, which later I will be presenting below. Furthermore, the paper examines three options strategies that are the following: covered calls, protective puts, and spread.  The aim of this paper is to examine how we can use the strategies to mitigate risk of losses and to gain from the call-put parity. It will also present a risk assessment of the portfolio’s volatility through some parameters.
Keywords: Covered calls, protective puts, spreads, gamma, delta, theta, volatility, options.'
authors: []
lastmod: '2022-12-30T20:01:52-05:00'
featured: no
draft: no
image:
  caption: 'image credit: [**businessline**](featured)'
  focal_point: ''
  preview_only: no
projects: []
---

# AN ANALYSIS OF OPTIONS TRADING STRATEGIES


This term paper examines the payoffs and trading strategies referring to a portfolio that consists of options on given assets such as, Apple, Meta, and Tesla. We will consider three option strategies to mitigate losses and gain from the tradeoff. The three option trading strategies are: covered calls, protective puts, and vertical bearish spreads. This paper will also be accompanied of an Excel Sheet in which the steps to the results are documented and presented in this paper in the form of tables. We will also design some Greek-neutral strategies. Some parameters such Rho, Theta, Gamma will be computed to predict the effect of variation or change of volatility, time to maturity, and interest rates on the option price. The last thing that will be expected is to present the Gamma-Theta Trade off. First, it is important to briefly outline the characteristics of the underlying assets. Apples, Inc (ticker: AAPL) engages in the design, manufacture, and sales of smartphones, personal computers, tablets wearables and accessories, and other varieties of related services. According to Wall Street, its sales revenue amounts to 394.33 billion dollars. Tesla, Inc. Engages in the design, development, manufacture, and sale of fully electric vehicles and energy generation and storage systems. It has a market cap of 615.3 billion dollars.

## METHODOLOGY OF THE PROJECT

Considering hedging or pricing put options or call options regardless the models either through a binomial or a more complex one such as Black Scholes, pricing options generally depend on the fundamental parameters, volatility, interest rate, maturity, and free interest rate (Sundaram & Das, 2016, pp.145 - 427). We will use these parameters to determine the prices, the options values, and predict the variation or influence of each parameter on the options. Generally, volatility is a primary determinant of option values. the adjusted closed data of each asset from Yahoo Finance. In order to estimate historical volatility, we estimate the standard deviation of monthly log returns or price changes (stds.s as function) and then multiply this by the appropriate factor (which is the square root of 12 months) to convert it into an annualized form (Sundaram & Das, 2016, p.307).  We used the Excel VBA sheets, related to Black Scholes and Greek parameters, designed by the Professor Giannetti (2022) to compute the parameters. According to Bloomberg, the treasury yield for a 3 month-bond (GB3:GOV) is 4.17%. This is the free interest rate that will be used in our options analysis. 

## CONSTRUCTION OF THE PORTFOLIO AND THE ALLOCATION OF FUNDS

 	Apple, Meta, and Tesla stock are currently trading on 11/26/2022 respectively at $148.11, 115.61 and 173.44 listed on Yahoo Finance at the time building our portfolio. In table 1, we have provided the preliminary characteristics of the portfolio in which we outline the volatility of the underlying assets, the strike, the calls, the puts, and the essential parameters that constitute the portfolio. Based on my predictions, I believe that prices will be soon declining most likely below $ 100. In this case, my call options will be out of the money, and therefore the portfolio will occur losses. I am bearish on directions regarding the stock price movements. To mitigate losses, I decided to short call and long put positions. Below presented these following positions:
•	Long 120 shares of Apple, Meta, and Tesla stocks;
•	Long 100 puts with strike of 115 and 85; and 200 puts with strike of 80
•	Short 100 calls with strike 100; and short 200 calls with a strike of 130 and 120


contrat date	11/26/2022			CONSTRUCTION OF PORTFOLIO

		 VOLATILITY 	INSTRUMENT	STRIKE	B/S PRICE	DELTA (per $ )	GAMMA (per $)	VEGA (%)	THETA per day	RHO (%)
APPLE PRICE	 $  148.11 	31.17%	APPLE	CALL 	100	49.09	                 0.99637 	         0.00047 	       0.00770 	    (4.64500)	   0.22650 
META PRICE	 $  115.61 	34.98%		PUT	115	0.3637	                (0.03759)	         0.00358 	       0.58190 	    (3.82200)	  (0.01360)
TESLA PRICE	 $    173.44 	53.95%		 			 	 	 	 	 
			META	CALL 	130	3.21	                 0.28834 	         0.01760 	      18.92700 	  (15.64930)	   6.92743 
contract maturity	2/17/2023			PUT	85	0.187	                (0.02400)	         0.00290 	       3.14930 	    (2.27100)	  (0.68600)
time to maturity	          0.23 			 			 	 	 	 	 
risk free rate	4.17%		TESLA	CALL	120	55.768	                 0.94410 	         0.00250 	       9.37380 	  (15.49640)	 24.83410 
CALL at the money	St>K			PUT	100	0.1816	                (0.01090)	         0.00060 	       2.38500 	    (2.71090)	  (0.47560)
Table 1 - Construction of the options portfolio with 3 assets


## THE THREE OPTIONS STRATEGIES CONSIDERED

In the lines below, the three trading options strategies will be presented with examples given through the portfolio excel sheet. 

•	**Covered Call**: the covered call is an income generation strategy for equity owners who do not anticipate their stock will go higher in the future (Butler, 2022). For the covered call strategy, we assume that the three underlying assets considered in this paper drop to $ 100% each. Butler presented the formula for covered call: 

**Suppose the stocks get to be at the time of maturity $ 100**

---
**_NOTE_**
Max Profit Potential: (Short Call + Credit received for call - Share purchase) x number of shares

Max Loss Potential : (Share Purchase Price - Credit Received for call ) x number of shares

Expiration Breakeven: Share purchase price - Credit received for call

---
	 
	 
| **stocks**        | Max profit          |	 Max Loss   	            | Breakeven  |
|-------------------|:------------------ |-------------------------:  |-----------:|
|  APPLE	          |          5,890.80 	|         6,109.20 	        |  50.91     |
|  META	            |         7,195.20 	  |          8,404.80 	      |    70.04   |
|  TESLA	          |         4,881.60 	  |        9,518.40           |	79.32      |
| PORTFOLIO	        |      17,967.60 	     |       24,032.40 	        |   $ 200.27 |
|                   |                     |                           |            |
Table 2- covered call


For Apple Stock, the breakeven is $ 50.91. If this stock falls below the breakeven price, one will lose money on the option call. Same consideration for Meta and Tesla. With a covered call when this stock falls to $ 100, the Apple will make a max profit of $ 5890.80, etc. The portfolio will make a max profit in case the three stocks fall to $ 100 (see table 2)

•	**Protective Puts**:  Butler (2022) defines it as the strategy that consists of buying a put option against shares of long stock. A protective put is a defensive strategy that reduces the risk of owning shares of stock. Now, we make the two premises: I) We suppose that we did not have short positions in calls but instead we had long the calls; ii) the long puts position will offset the losses on the long call position we take.

---
**_NOTE:_** 

Max Profit Potential: Unlimited

Max Loss Potential : [(Share Purchase Price - Put Strike Price )+debit paid for PUT] x number of shares

Expiration Breakeven: Share purchase price + debit paid for put

---

	
| Stocks     	|Max profit 	 |   Max Loss Potential  	|         BREAKEVEN|
|:-------------|:-------------------:| :----------------------:|------------------:|
|APPLE	      |UNLIMITED 	   | (1,756.36)	            |       100.3637   |
|META	        |UNLIMITED 	  |   1,876.04              |	      100.6337   |
|TESLA	      |UNLIMITED 	   |     2,587.62           |     	101.5635   |
|PORTFOLIO	  |UNLIMITED   |	 $ 2,707.31           |	 $    302.56    |
			
Table 3 - Protective Puts


With the protective puts, there is no limit to your profits. As I said it is a defensive strategy, the portfolio will lose less whichever puts are considered compared the covered call. The portfolio will lose. A position like that is when you go long on calls, and you would like to minimize your losses by buying puts against the long calls.

•	**Bear Call Spread**: Butler (2022) argues that the bear call spread is a bearish options strategy that consists of simultaneously selling a call and buying a call at higher strike price (same expiration cycle). A bear call credit spread is entered when the seller believes the price of the underlying asset will be below the short call option’s strike price on or before the expiration date.

---
**_NOTE_**

Maximum Profit Potential: Credit received * 100

Maximum Loss Potential: (Width of call strikes – credit received) X 100

Expiration breakeven Price: Short call price + Credit received

---

				
|            |Positions in Apple	 | Strike 	| Price  |	
|:-----------|:-------------------:|----------|--------|
|*Assumption*	 |Short Call           |$ 100.00 	|$ 49.09 |	
|            | Long call            |  120.00 	|30.2	   |
|	          |NET CREDIT	 $         |  18.89 	|	       |
|		         |                     | Wide bear Call|20.00| 	
|**Stock**|**Max profit** |**Max Loss Potential** |**Breakeven**|
|	APPLE|  1,889.00 	|             111.00 	|      118.89  |
				
Table 4- Bear Call Spread


In a bear call spread, the loss for apple will $ 111 and the profit will be $ 1889. Buying the higher call option will reduce the overall premium collected to enter the trade but will define the position's risk to the width of the spread minus the credit received.
INTERPRETATION OF THE PARAMETERS (DELTA, GAMMA, THETA)
One of the parameters to firstly estimate is the delta of the calls or puts. The delta is evidently central to the pricing of options by replication. Calls gain value when the price of the underlying increases but puts lose value in this case. Our comment regarding the parameters of the portfolio is defined as such: delta of the portfolio is $ 4.23, that is to say, the portfolio will increase by $ 4.23 whenever there is a price change of $ 1 whether it comes from Apple, Tesla, Meta. It means also that the portfolio is positively sensitive to the price change of the underlying assets. 
Position Greek of the Portfolio		SIMULATION	
			if Apple Stock gets to be	Increase
Value of the Portfolio 	 $          30,959.20 		 $                          170.00 	 $      21.89 
				
Delta of the Portfolio	                     4.23 		New Delta -Portfolio	        92.51 
 				
Gamma of Portfolio	                 356.93 			
			change in the portfolio 	  87,540.56 
VEGA	              (4,734.38)			
				
Theta of Portfolio	               5,586.15 			
				
Rho of Portfolio	              (6,561.08)			
				
GAMMA NEUTRAL			
	short position of the calls	New Position of DELTA	Cumulative	
Call with K=100	           752,066.03 	   (749,331.81)	                          2,734.23 	
Call with K=130	             20,280.14 	         (352.70)	                        19,927.44 	
Call with K =120	           142,772.22 	         (352.70)	                      142,419.51 	
Table 5 - Greek positions and simulation

Gamma 

Damaradan and Das (2016, p. 412) presented Gamma as the parameter that measures the change in the option delta for a given change in the price of the underlying. The same authors advanced that the gamma can be used to estimate both the impact of large price movements on aggregate portfolio value, and the impact on the position delta of a change in the underlying price. So to speak, a large value of gamma, for instance, the gamma of the portfolio of $ 356.96 (see table 4) implies that the delta of the portfolio will change substantially even for a relatively small change in one of the underlying assets. Given only the Apple stock increases by $ 21.89 because of the new Apple price is $ 170, the new delta of the portfolio jumps from $ 4.23 to $ 92.51. Therefore, it also translates a huge change of $87,540.56 in the portfolio.

Theta
Position Theta is expressed as a negative number that indicates how much your account can lose or make daily due to time decay (Sundaram & Das, 2016, pp.145 - 427). The options in the portfolio, calls and puts, have negative values. The portfolio might lose value, at least $ 5,586.15, every day that passes. The portfolio through its calls and puts is negatively sensitive to time to maturity. 

THE GAMMA NEUTRAL AND DELTA NEUTRAL 
A large value of gamma implies that the delta will change substantially even for a relatively small change in S, so the portfolio needs to be rebalanced to keep it delta-hedged. We short the calls options and delta-hedged, see the table below to see how much money for the short positions for each call. To delta-hedge, we can only increase the long positions in the underlying assets to a certain level in order to increase the delta of the portfolio in to benefit more from a price increase. The excel sheet will help simulate this one, increase the “N for the stock to 200, you will see the change in the portfolio delta.
GAMMA NEUTRAL		
	short position of the calls	New Position of DELTA	Cumulative
Call with K=100	           752,066.03 	    (749,331.81)	                          2,734.23 
Call with K=130	             20,280.14 	          (352.70)	                        19,927.44 
Call with K =120	           142,772.22 	          (352.70)	                      142,419.51 
Table 6 - Gamma Neutral

## CONCLUSION A ND RECOMMENDATIONS

In sum, this term paper presents the analysis of three option strategies, covered call, protective put, and spread by considering three underlying assets: Apple, Meta, and Tesla stocks. The Portfolio has been constructed by taking short positions on the calls and long position from a bearish perspective. The covered call strategy will minimize losses in case the stock price increases. If the three stocks fall to $ 100 each, the portfolio will lose a maximum of $ 24,032. But with the strategy, since we short calls on the three stocks, the portfolio might incur a gain of $ 17, 977 dollars. In the same vein, the defensive strategy, the protective puts help limit losses in case we long calls instead. The profit is limited but the losses will amount to $ 2,707. But in the case of this portfolio the covered call is more appropriate.
At last, we have assessed the risk areas of the options in a specific manner and the portfolio in a broad way by considering the Greek parameters. We concluded that the gamma of Apple is very sensitive to the price change of the stocks positively. The Gamma of the portfolio is substantial in the same a dollar change in the portfolio will reflect to a big change in the portfolio (see table 4 – Simulation). It translates that a price change of a dollar will bring a huge change in the portfolio. The portfolio is positively sensitive to price while it is negatively sensitive to time decay. 
 

##   BIBLIOGRAPHY
   
Bank of America. (2022, December 02). Vega: Options Involve risk and are not suitable for all investors. Retrieved December 02, 2022, from Bank of America: https://www.merrilledge.com/investment-products/options/learn-understand-vega-options

Bloomberg. (2022, December 12). United States Rates & Bonds. Retrieved December 04, 2022, from Bloomberg: https://www.bloomberg.com/markets/rates-bonds/government-bonds/us

BUTLER, C. (2022, FEBRUARY 10). Bear Call Spread Option . Retrieved from ProjectFinance: https://www.projectfinance.com/bear-call/

Butler, C. (2022, March 22). Covered Call Options Strategy: Complete Guide With Visuals. Retrieved from Project Finance: https://www.projectfinance.com/buy-write/

Sundaram, R. K., & Das, S. R. (2016). Derivatives: Principles and Practice. New York: McGraw -Hill Education.
Wall Street Journal. (2022, December 02). Apple Inc. Retrieved 12 02, 2022, from Wall Street Journal Markets: https://www.wsj.com/market-data/quotes/AAPL/company-people

Wall Street Journal. (2022, November 22). mata Plaforms Inc. Retrieved from Wall Street Journal: https://www.wsj.com/market-data/quotes/MX/XMEX/META/company-people


