---
title: 'FACTOR ANALYSIS'
author: Daniel Sineus
date: '2022-11-03'
slug: ''
categories: []
tags:
  - Academic
  - Deep Learning
  - FACTOR ANALYSIS
  - PORTFOLIO
summary: ''
authors: []
external_link: ''
image:
  caption: "Image credit:[**unsplash**](featured)"
  focal_point: ''
  preview_only: no
url_code: ''
url_pdf: ''
url_slides: ''
url_video: ''
slides: ''
---


This exercise has been thought to help anyone who like to create a **basic, quantitative multi-factor investment strategy**. The sample universe of stocks has been in csv format retrieved from Ycharts.The idea and the methods came from a class of Portfolio management taken with a brilliant Professor, Mr.  Matthews [link text](https://www.linkedin.com/search/results/all/?keywords=michael%20j.%20matthews%2C%20cfa&origin=RICH_QUERY_SUGGESTION&position=1&searchId=2cbc037d-52d2-43f3-9557-edecb8f78b83&sid=fYg)



# **INVESTMENT DECISION BASED ON FACTOR ANALYSIS**

---
The purpose of this document is to bring a factor analysis toward a portfolio by using a great deal of securities reflecting the S&P500. Anyone will be able to see all the steps from begining to the end. One thing that you will need to expect is that there will not be theories about Quantitative Portfolio Management. You will discover the routes taken to get the results.


---




```python
#upload the file
import pandas as pd
from pandas import Series, DataFrame

```


```python
from google.colab import files
uploaded=files.upload()
```



    Saving MultifactorDaniel.csv to MultifactorDaniel.csv
    


```python
factor=pd.read_csv("MultifactorDaniel.csv")
factor1=pd.DataFrame(factor)
factor1.drop(["Name", "Industry"], inplace=True, axis=1) # Delete the collumns Name and Industry
factor1.head()#Check the result
```




Above, you can notice 6 factors. The following factors are 

*   **Value Factors**: Price to Earnings ratio;
*   **Quality Factors**: Return on Equity and Profit margin;
*   **Momentum Factors**: Past 12 month return;
*   **Volatility** : Standard deviation;
*   **Size** : Market Capitalization




```python
print(factor1.isnull().sum()) #to compute the sum of empty cells per variables
```

    Symbol                   0
    Sector                   0
    PE Ratio                39
    Profit Margin            3
    1 Year Total Returns     1
    Std_Monthly Returns      0
    Market Cap               0
    dtype: int64
    

The variable PE ratio alone has 39 missing values. We infer that there are many missing values, so we need to deal with the missing values. we can't afford to drop the empty cells. We resort to the stategy of replacing the empty cells by the median.


```python
# Replace missing values. we could've dropped the missing values by using dropna() because they are too much in the column P/E ratio
print(factor1.isnull().sum().sum())
```

    43
    


```python
#use fillna()
medi=factor1["PE Ratio"].median()
medi

```




    26.0248




```python
#Replace missing values with the median number
factor1["PE Ratio"].fillna(medi,inplace=True)
#Check to see if there is any missing value in the column **PE Ratio**
factor1["PE Ratio"].isnull().values.any()
factor1.isnull().sum()
```




    Symbol                  0
    Sector                  0
    PE Ratio                0
    Profit Margin           3
    1 Year Total Returns    1
    Std_Monthly Returns     0
    Market Cap              0
    dtype: int64




```python
factor1.dropna(how="any")
```



We still have a few missing values. Nothing to impede us analysis. We find it correct to drop the few missing values left. It would not impact our analysis substantially. 


```python
factor1.head()
```


```python
# use the factor method to rank
factor1["rank_Profit"]=factor1["Profit Margin"].rank(ascending=False)
factor1["rank_MarketCap"]=factor1["Market Cap"].rank(ascending=False)
factor1["rank_riskvalue"]=factor1["Std_Monthly Returns"].rank(ascending=False)
factor1["rank_returns"]=factor1["1 Year Total Returns"].rank(ascending=False)
factor1["rank_PE"]=factor1["PE Ratio"].rank(ascending=True)

```


```python
factor1.head()
fact=factor1.index
fact1=len(fact)# count the number of rows in a Pandas dataframe.
fact1# the higher the PE Ratio the riskier the firm might be. this is the reason why we use the ascending=True, it means the lower PE ratio the better

```




    505




```python
# Computer the average of the rank
factor1["average_rank"]=factor1[["rank_Profit", "rank_MarketCap", "rank_riskvalue", "rank_returns", "rank_PE"]].mean(axis=1)
factor1.head()
```



```python
factor1["rank"]=factor1["average_rank"].rank(ascending=False)
factor1.sort_values(by="average_rank").head(10)

```



```python
#Convert the data into a spreadsheet in case you would like to share it with non-python users
factor1.to_csv("Mathew1.csv", index=False)

```

# Investment decision
We invest 30% in stocks in the given universe. TO determine the neutral weight. it is 30%  * 502


```python
stocksel=round(.28*505,ndigits=0)#Let's select the first 152 stocks
stocksel
weight=round(1/stocksel, ndigits=3)
weight
```




    0.007



each stock will have a weight of 0.007.



```python
securities=factor1["Symbol"].iloc[:150]
securities
```




    0         A
    1       AAL
    2       AAP
    3      AAPL
    4      ABBV
           ... 
    145     DRI
    146     DTE
    147     DUK
    148     DVA
    149     DVN
    Name: Symbol, Length: 150, dtype: object



##FACTOR MODEL BY SECTOR
To proceed with the factor model, we are going to group the data by sectors particularly when doing the factor ranking. 


```python

factor2=factor1
factor2=factor1[["Symbol", "Sector", "PE Ratio", "Profit Margin", "1 Year Total Returns", "Std_Monthly Returns", "Market Cap"]]
factor2.head(10)
```




```python
factor2.set_index("Sector")
factor2.head(30)
factor2.tail(30)
dat=factor2.sort_values("Sector", ascending=True)
```


```python
dat.head(10)
```





```python

factor2["rank1_PE"]=factor2.groupby("Sector")["PE Ratio"].rank(ascending=True)
factor2["rank1_Profit"]=factor2.groupby("Sector")["Profit Margin"].rank(ascending=False)
factor2["rank1_Return"]=factor2.groupby("Sector")["1 Year Total Returns"].rank(ascending=False)
factor2["rank1_risk"]=factor2.groupby("Sector")["Std_Monthly Returns"].rank(ascending=False)
factor2["rank1_cap"]=factor2.groupby("Sector")["Market Cap"].rank(ascending=False)
```


```python
df.head()
```



```python
df=pd.DataFrame(factor2.sort_values("Sector"))
#Convert the data into a spreadsheet in case you would like to share it with non-python users
df.to_csv("Mathew2.csv", index=False)
# number of stock per sectors to invest in
number=df.groupby(["Sector"])["Symbol"].count()
number.tail(13)
dframe=pd.DataFrame(number, index=None)
dframe

```





We are going to keep the investment decision the same way. We will invest 30% in stocks in the given universe given all the sectors. To
 determine the neutral weight. it is 30% * by the quatity of stocks per sector




```python
dframe["Stock_per_sector"]=round(dframe["Symbol"]*0.3, ndigits=None)
dframe
```



```python

Symol1=df.loc[df["Sector"]=="Basic Materials","Symbol"].head(6)
Symol2=df.loc[df["Sector"]=="Comunications Services","Symbol"].head(8)
Symol3=df.loc[df["Sector"]=="Consumer Cyclical","Symbol"].head(20)   
Symol4=df.loc[df["Sector"]=="Consumer Defensive","Symbol"].head(10) 
Symol5=df.loc[df["Sector"]=="Energy","Symbol"].head(6)
Symol6=df.loc[df["Sector"]=="Financial Services","Symbol"].head(21)
Symol7=df.loc[df["Sector"]=="Healthcare","Symbol"].head(20)
Symol8=df.loc[df["Sector"]=="Industrials","Symbol"].head(22)
Symol9=df.loc[df["Sector"]=="Real Estate","Symbol"].head(9)
Symol10=df.loc[df["Sector"]=="Technology","Symbol"].head(21)
Symol11=df.loc[df["Sector"]=="Utilities","Symbol"].head(8)
```

The investable universe when considering the top stock per sector. Please see the list of the 143 securities. in case you want to see 140 securities. use the function result.head(143)


```python
frames=[Symol1, Symol2,Symol3, Symol4,Symol5, Symol6, Symol7,Symol8,Symol9,Symol10,Symol11]
result=pd.concat(frames)
result.head(30)

```




    340     NUE
    154     ECL
    409     SHW
    306     MLM
    41      APD
    469     VMC
    390     RCL
    125     CZR
    325    NCLH
    143     DPZ
    397      RL
    331     NKE
    377    POOL
    73      BWA
    400     ROL
    180    FBHS
    362    PENN
    84      CCL
    176       F
    342     NVR
    174    EXPE
    145     DRI
    370     PKG
    369     PHM
    408     SEE
    169    ETSY
    229     HSY
    304     MKC
    288      LW
    363     PEP
    Name: Symbol, dtype: object
