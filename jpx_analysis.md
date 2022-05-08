# JPX Growth Board Analysis

## Background

This analysis focuses on the growth board of JPX and will look at the valuation difference, price and fundamental performance of companies listed on the growth board vs the rest of the market and try to give suggestions on actions post IPO for a company that provides power bank services. We will also look at some comparable companies (Smart Charge, formerly known as [EN Monster](https://www.enmonster.com/)) listed elsewhere and see what implications can be drawn.

## 1. Compare growth board valuation vs the overall market

### 1.1 Valuation comparion

We can first look at the overall valuation on the growth board vs the overall market in Japan. 

As there are many unprofitable companies on the growth board, given the early stage nature, apart from the price/earnings ratios, we also look at the price/sales and price/book.

Ideally we would also look at FCF yield and EV/EBITDA, but these were not available for the Nikkei 225.


As figure 1 shows, growth board stocks in general are a order of magnitude more expensive compared with the rest of the market, and is also much more expensive than the growth‑oriented JASDAQ section. This is in part due to the early stage nature of the companies on the board, which tend to have faster growth and depressed margins due to investment in growth.

- Valuation trends tend to be similar, but growth board tend to be a bit more volatile and have seen more pull back recently.


    
![png](jpx_analysis_files/jpx_analysis_5_0.png)
    


Looking at both P/S and P/B, the growth board overall is about 10x more expensive than the rest of the market.


    
![png](jpx_analysis_files/jpx_analysis_7_0.png)
    



    
![png](jpx_analysis_files/jpx_analysis_8_0.png)
    


If we control for only the electrics appliance & internet services sector, the valuation gap continues to hold. I could only get the MSCI IT sector index that represent, so the meaningful comparison would be to compare it with the IT services, hardware, electronics, and semiconductor sectors on the growth board. 

- Also worth noting that there has not been a pullback in valuation recently in the IT sector on the growth board, contrary to the other indices.


    
![png](jpx_analysis_files/jpx_analysis_11_0.png)
    


### 1.3 Difference in fundamentals

As figure 4 shows, the growth board has a faster growth rate than JASDAQ, as expected, but growth in new listings in the recent 2 years have been easing off.


    
![png](jpx_analysis_files/jpx_analysis_14_0.png)
    


Looking at the margins, we can see that the growth board stocks are generally loss making even on the EBITDA line. This partially explains the high average P/E. 


    
![png](jpx_analysis_files/jpx_analysis_16_0.png)
    


We can also look at gross margin as ebitda margin tends to be distorted by a few very loss making companies. These could be pharmaceutical companies that have a high R&D cost but did not have a meaningful revenue yet. 

As the chart below shows, growth board on average actually has a better gross margin than JASDAQ. This makes sense given the technology-focus on the board. 


    
![png](jpx_analysis_files/jpx_analysis_18_0.png)
    


Slightly surprisingly though, the average market cap on the growth board is actually higher than the JASDAQ, between JPY10-20bn. 


    
![png](jpx_analysis_files/jpx_analysis_20_0.png)
    


## 2. Performance since IPO

We can now look at the performance since IPO. We will look at this through the following angles:
1) General performance since IPO;
2) Performance by sector;
3) General market condiction, interest rates, and company characteristics and their impact to IPO performance;

Looking at the share price performance on the growth board, we can observe a few interesting trends, some of which are generally true with IPOs:

1) After 2013, the average IPOs rise more than 25% from the issue price.

2) It seems like the secondary market is fairly efficient at pricing IPOs, with share prices stablizing after IPOs. The average share price performance 1/4/12 weeks after IPO don't differ that much from the IPO price. 

3) Except for 2019 which was an unusual year (trade war, macro shocks), share price after a year almost always to IPO levels on average. 

4) There are a few bad years such as 2015 when IPOs performed poorly and generally did not rise above the issue prices. Given the macro uncertainties 2022 is likely going to be such a year. 


    
![png](jpx_analysis_files/jpx_analysis_25_0.png)
    


### 2.1 An analysis into the factors driving IPO performance

We can now look at the IPOs and try to predict IPO price, incorporating the various macro and market data as factors contributing to the performance. 

We are NOT going to look at 'similar' companies and assume this IPO to be similar, due to a few reasons:

1) There are virtually not similar company;

2) As we will see below, the most important factor is actually not the company's business, but how it's valued and the market conditions for IPOs. Over a longer horizon, stock performance will revert back to trend with its fundamentals, but IPOs don't usually reflect the underlying fundamentals;

3) Market condition, valuation, and many other random variables could affect the IPO performance. 

As a result, we need to look at the many factors deciding IPO performance, while also acknolwedging that IPO performance has a large random/stochastic component to it.

In order to look at the factors affecting IPOs in JPX's growth board, we can first create a dataset containing the features we want about the company - sector, valuation, index performance before the IPO.

The created dataset looks like this (data is provided, I transposed the data to make it more viewable. This includes the first 5 rows and companies only as an example):




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th>index</th>
      <th>1400 JP Equity</th>
      <th>1401 JP Equity</th>
      <th>1431 JP Equity</th>
      <th>1436 JP Equity</th>
      <th>1447 JP Equity</th>
    </tr>
    <tr>
      <th>short_name</th>
      <th>RUDEN HD</th>
      <th>MBS INC</th>
      <th>LIB WORK CO LTD</th>
      <th>FIT CORP</th>
      <th>ITBOOK HOLDINGS</th>
    </tr>
    <tr>
      <th>cie_des</th>
      <th>Ruden Holdings Co., Ltd. constructs and remodels buildings, apartments, and houses. The Company specializes in interior design reforms. Also, Ruden Holdings sells interior products and securities products.</th>
      <th>mbs. inc. repairs and renovates outer walls and interiors for housings and buildings.  The Company also provides consulting services on renovation work.</th>
      <th>Lib Work Co. Ltd. operates as a custom homebuilder. The Company designs, constructs, and sells single-family homes. Lib Work also renovates and remodels homes.</th>
      <th>Fit Corporation builds homes. The Company builds and sells single family houses, apartments, prefabricated houses, and other buildings. Fit provides its services throughout Japan.</th>
      <th>ITbook Holdings Co., LTD offers IT services. The Company provides IT and system procurement support, technology consulting, and other services. ITbook Holdings offers services in Japan.</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>gics_industry_name</th>
      <td>Construction &amp; Engineering</td>
      <td>Household Durables</td>
      <td>Real Estate Management &amp; Devel</td>
      <td>Independent Power and Renewabl</td>
      <td>IT Services</td>
    </tr>
    <tr>
      <th>gics_sub_industry_name</th>
      <td>Construction &amp; Engineering</td>
      <td>Homebuilding</td>
      <td>Real Estate Development</td>
      <td>Independent Power Producers &amp;</td>
      <td>IT Consulting &amp; Other Services</td>
    </tr>
    <tr>
      <th>eqy_init_po_dt</th>
      <td>2005-04-06 00:00:00</td>
      <td>2005-04-26 00:00:00</td>
      <td>2015-08-05 00:00:00</td>
      <td>2016-03-11 00:00:00</td>
      <td></td>
    </tr>
    <tr>
      <th>ipo_ps</th>
      <td>21.093566</td>
      <td>733.072665</td>
      <td>3.452758</td>
      <td>0.836822</td>
      <td></td>
    </tr>
    <tr>
      <th>ipo_pe</th>
      <td>-95.947804</td>
      <td>7438.262422</td>
      <td>98.674067</td>
      <td>9.580778</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>



* Note category meanings 

- gics_industry is the GICS industry classification from S&P. 

- cie_des is the description of the company's main business.

- eqy_init_po_dt is the IPO date of the stock.

- ipo_pe/ps/pb are the valuations at IPO for the companies.

We have examined the IPO performance grouped by year, but we didn't look at the distribution of performance. We can now take a look:

- The mode is about 0% increase at IPO, which is a lot lower than the mean, which is generally positive as discussed above. This is due to the long tail towards the right skewing the distribution, meaning majority of the IPOs are actually flat.

- Shares tend to perform better at IPO date and within 1 week of IPO than afterwards. 


    
![png](jpx_analysis_files/jpx_analysis_36_0.png)
    


Let's first look at the correlation among different factors determining IPO performance. 

Table below summerizes factors' correlation with the price performance at and after IPO. Table is sorted in descending order by the IPO day performance. We can see that:

1) US interest rate change in the previous 4 and 12 weeks is positively correlated to IPO performance, and the 2 main indices in Japan, Nikkei 225 and TOPIX are both positively correlated with performance. These correlations tend to fade longer after the IPO (expected, known as alpha decay in quantitative trading). This basicaly means in a bull market, IPOs tend to do better, which is self explanatory. 

2) Only gross margin seemed positively correltated with IPO performance. Sales growth, ebitda margin nd ebit margin did not show much correlation - this could be due to extreme values in the dataset - earlier I have shown that in some years IPOs tend to have extremely loss making companies on the ebitda line. 

3) Valuation is negatively correlated with IPO performance. 

4) Sector has a weak correlation with performance (positive or negative doesn't matter, these are dummy variables). 

For example, usgg10yr index_chg_12wk (usgg10yr is the 10 year US govt bond, this is the trailing 12 weeks price change in US govt bond - see note below) has 15.28% correlation with the IPO same day performance and is the most positively correlated factor. On the other hand, ipo_pe, ipo_ps, and ipo_pb are the most negatively correlated factors - this makes sense as the most expensive IPOs generally tend not to perform very well on the IPO day. 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0weeks after IPO</th>
      <th>1weeks after IPO</th>
      <th>4weeks after IPO</th>
      <th>12weeks after IPO</th>
      <th>26weeks after IPO</th>
      <th>52weeks after IPO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>usgg10yr index_chg_12wks</th>
      <td>15.28%</td>
      <td>16.37%</td>
      <td>14.26%</td>
      <td>10.33%</td>
      <td>9.09%</td>
      <td>0.86%</td>
    </tr>
    <tr>
      <th>nky index_chg_12wks</th>
      <td>15.09%</td>
      <td>18.68%</td>
      <td>18.14%</td>
      <td>13.84%</td>
      <td>11.65%</td>
      <td>6.41%</td>
    </tr>
    <tr>
      <th>tpx index_chg_12wks</th>
      <td>13.59%</td>
      <td>17.05%</td>
      <td>15.45%</td>
      <td>10.62%</td>
      <td>8.71%</td>
      <td>5.38%</td>
    </tr>
    <tr>
      <th>nky index_chg_26wks</th>
      <td>10.58%</td>
      <td>13.63%</td>
      <td>9.72%</td>
      <td>3.05%</td>
      <td>1.96%</td>
      <td>-1.55%</td>
    </tr>
    <tr>
      <th>usgg10yr index_chg_4wks</th>
      <td>10.13%</td>
      <td>13.50%</td>
      <td>10.28%</td>
      <td>5.08%</td>
      <td>2.87%</td>
      <td>-1.64%</td>
    </tr>
    <tr>
      <th>gross_margin</th>
      <td>9.70%</td>
      <td>9.78%</td>
      <td>12.57%</td>
      <td>13.36%</td>
      <td>10.99%</td>
      <td>14.17%</td>
    </tr>
    <tr>
      <th>nky index_chg_4wks</th>
      <td>9.00%</td>
      <td>10.64%</td>
      <td>8.44%</td>
      <td>0.97%</td>
      <td>-0.73%</td>
      <td>0.39%</td>
    </tr>
    <tr>
      <th>tpx index_chg_4wks</th>
      <td>8.88%</td>
      <td>11.18%</td>
      <td>8.54%</td>
      <td>0.71%</td>
      <td>-0.79%</td>
      <td>0.01%</td>
    </tr>
    <tr>
      <th>nky index_chg_52wks</th>
      <td>7.48%</td>
      <td>8.53%</td>
      <td>6.98%</td>
      <td>0.90%</td>
      <td>0.06%</td>
      <td>-0.95%</td>
    </tr>
    <tr>
      <th>usgg10yr index_chg_26wks</th>
      <td>7.30%</td>
      <td>6.47%</td>
      <td>4.91%</td>
      <td>0.71%</td>
      <td>-3.66%</td>
      <td>-9.83%</td>
    </tr>
    <tr>
      <th>tpx index_chg_26wks</th>
      <td>6.81%</td>
      <td>9.42%</td>
      <td>5.43%</td>
      <td>-1.76%</td>
      <td>-1.95%</td>
      <td>-2.07%</td>
    </tr>
    <tr>
      <th>listing_mkt_cap</th>
      <td>4.77%</td>
      <td>2.38%</td>
      <td>5.10%</td>
      <td>3.30%</td>
      <td>3.00%</td>
      <td>5.89%</td>
    </tr>
    <tr>
      <th>gics_industry_name_encoded</th>
      <td>4.34%</td>
      <td>8.73%</td>
      <td>6.71%</td>
      <td>6.37%</td>
      <td>3.49%</td>
      <td>7.26%</td>
    </tr>
    <tr>
      <th>tpx index_chg_52wks</th>
      <td>3.34%</td>
      <td>4.52%</td>
      <td>2.15%</td>
      <td>-4.18%</td>
      <td>-3.65%</td>
      <td>-2.40%</td>
    </tr>
    <tr>
      <th>usgg10yr index_chg_1wks</th>
      <td>2.73%</td>
      <td>5.29%</td>
      <td>3.91%</td>
      <td>0.34%</td>
      <td>3.18%</td>
      <td>0.31%</td>
    </tr>
    <tr>
      <th>sales_3yr_avg_growth</th>
      <td>1.84%</td>
      <td>2.38%</td>
      <td>2.01%</td>
      <td>3.54%</td>
      <td>3.44%</td>
      <td>3.21%</td>
    </tr>
    <tr>
      <th>jpy curncy_chg_1wks</th>
      <td>1.38%</td>
      <td>4.35%</td>
      <td>2.64%</td>
      <td>0.87%</td>
      <td>3.69%</td>
      <td>3.27%</td>
    </tr>
    <tr>
      <th>tpx index_chg_1wks</th>
      <td>0.30%</td>
      <td>3.38%</td>
      <td>3.12%</td>
      <td>1.70%</td>
      <td>-0.25%</td>
      <td>1.10%</td>
    </tr>
    <tr>
      <th>nky index_chg_1wks</th>
      <td>0.07%</td>
      <td>3.57%</td>
      <td>3.10%</td>
      <td>1.43%</td>
      <td>-0.76%</td>
      <td>0.58%</td>
    </tr>
    <tr>
      <th>jpy curncy_chg_12wks</th>
      <td>-0.11%</td>
      <td>1.18%</td>
      <td>1.85%</td>
      <td>0.42%</td>
      <td>1.27%</td>
      <td>0.37%</td>
    </tr>
    <tr>
      <th>usgg10yr index_chg_52wks</th>
      <td>-0.32%</td>
      <td>-4.27%</td>
      <td>-5.54%</td>
      <td>-9.78%</td>
      <td>-15.10%</td>
      <td>-15.76%</td>
    </tr>
    <tr>
      <th>ebitda_margin</th>
      <td>-0.38%</td>
      <td>1.16%</td>
      <td>0.35%</td>
      <td>1.76%</td>
      <td>4.31%</td>
      <td>3.25%</td>
    </tr>
    <tr>
      <th>ebit_margin</th>
      <td>-0.39%</td>
      <td>1.15%</td>
      <td>0.33%</td>
      <td>1.73%</td>
      <td>4.30%</td>
      <td>3.23%</td>
    </tr>
    <tr>
      <th>jpy curncy_chg_4wks</th>
      <td>-1.25%</td>
      <td>-0.64%</td>
      <td>0.81%</td>
      <td>1.60%</td>
      <td>-0.06%</td>
      <td>-1.32%</td>
    </tr>
    <tr>
      <th>jpy curncy_chg_26wks</th>
      <td>-2.78%</td>
      <td>-2.02%</td>
      <td>-0.18%</td>
      <td>-0.87%</td>
      <td>-3.30%</td>
      <td>-2.20%</td>
    </tr>
    <tr>
      <th>trailing_12m_sales_growth</th>
      <td>-3.91%</td>
      <td>-1.17%</td>
      <td>0.88%</td>
      <td>1.01%</td>
      <td>2.25%</td>
      <td>1.81%</td>
    </tr>
    <tr>
      <th>jpy curncy_chg_52wks</th>
      <td>-3.98%</td>
      <td>-1.19%</td>
      <td>-2.57%</td>
      <td>-4.08%</td>
      <td>-3.47%</td>
      <td>-3.30%</td>
    </tr>
    <tr>
      <th>gics_sub_industry_name_encoded</th>
      <td>-6.56%</td>
      <td>-7.78%</td>
      <td>-10.79%</td>
      <td>-7.86%</td>
      <td>-7.28%</td>
      <td>-4.12%</td>
    </tr>
    <tr>
      <th>sales_rev_turn</th>
      <td>-8.22%</td>
      <td>-8.92%</td>
      <td>-7.95%</td>
      <td>-8.15%</td>
      <td>-6.88%</td>
      <td>-5.30%</td>
    </tr>
    <tr>
      <th>ipo_pe</th>
      <td>-9.94%</td>
      <td>-10.45%</td>
      <td>-10.65%</td>
      <td>-9.98%</td>
      <td>-9.82%</td>
      <td>-7.70%</td>
    </tr>
    <tr>
      <th>ipo_ps</th>
      <td>-10.09%</td>
      <td>-10.49%</td>
      <td>-10.75%</td>
      <td>-10.39%</td>
      <td>-10.17%</td>
      <td>-7.85%</td>
    </tr>
    <tr>
      <th>ipo_pb</th>
      <td>-17.46%</td>
      <td>-17.88%</td>
      <td>-18.47%</td>
      <td>-17.54%</td>
      <td>-16.73%</td>
      <td>-12.95%</td>
    </tr>
  </tbody>
</table>
</div>



Note - meaning of the top factors:
- ipo_pb means price/book at IPO; ipo_ps/ipo_pe means the p/s and p/e at IPO. 
- usgg10yr is the 10 year us government bond yield.
- jpy curncy is the JPYUSD exchange rate.
- nky index is the Nikkei 225 and tpx is the TOPIX index. 

We can visualize this to see the trend more clearly.


    
![png](jpx_analysis_files/jpx_analysis_42_0.png)
    


### 2.2 Predicting IPO performance

With the training data we can do some more interesting predictions now. Our dataset is quite small (467 IPOs) so we don't need to consider neural networks. We can try random forests, adaboost and bayesian classifier given the noisy nature of the data. To make the predictions a bit more meaningful, we are also going to bin the performance into categories so we don't have to worry about forecasting the actual performance.

After training the model we can check the accuracy score on the testing data set. 

Note that we have 4 classes we are trying to predict - return <-20%, -20% to 20%, 20% to 100%, and above 100%. This means that if we were to randomly guess, our success rate (accuracy) would be 25%, in reality it will be a slightly different as some classes are more common.

We can see that our AdaBoost model performs best, with an accuracy of 42%. We shouldn't push the accuracy too high, as that would cause overfitting (model looking at small details particular to the historical data but don't have predictive power) - our data set is small and there are a lot of noise, so this is about as good as we can do. IPO performance, as mentioned, have a large random component to it, as mentioned.

Our model performas as follows:

    Accuracy:
    Random Forest: 0.42
    AdaBoost: 0.42
    Naive Bayes: 0.28


We can also check the confusion matrix of our model to see how it perform. The y axis represents the true class (of IPO performance), and the x axis prepresents the predicted classes.

A perfect model would have only the diagnal - all classes predicted correctly. Ours is not, but we can see it has reasonable performance.


    
![png](jpx_analysis_files/jpx_analysis_51_0.png)
    


Our random forest classifier is not as good, but it has an important use case - figuring the factor importances.

Slightly different from the correlation matrix, we can see that the most important feature included valuation, listing market cap, trailing index performance, and interest rates.


    
![png](jpx_analysis_files/jpx_analysis_55_0.png)
    


### Stock performance prediction

As I don't have the detailed financial information and potential listing price for this company, I can only assume a few scenarios based on similar companies. 

Globally listed portable power bank companies are actually quite rare, the most directably comparable company is [Smart Charge](https://www.enmonster.com/) (EM US, formerly known as EN Monster), a China based company which sales and rents portable chargers, listed in the US. Smart Charge operates predominantly in China. 

Below is a snap shop of its income statement (in millions):




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>asOfDate</th>
      <th>2019-12-31</th>
      <th>2020-12-31</th>
      <th>2021-12-31</th>
      <th>2021-12-31</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>periodType</th>
      <td>12M</td>
      <td>12M</td>
      <td>12M</td>
      <td>TTM</td>
    </tr>
    <tr>
      <th>currencyCode</th>
      <td>CNY</td>
      <td>CNY</td>
      <td>CNY</td>
      <td>CNY</td>
    </tr>
    <tr>
      <th>TotalRevenue</th>
      <td>2022.3</td>
      <td>2809.4</td>
      <td>3585.4</td>
      <td>3585.4</td>
    </tr>
    <tr>
      <th>GrossProfit</th>
      <td>1729.8</td>
      <td>2378.6</td>
      <td>3028.2</td>
      <td>3028.2</td>
    </tr>
    <tr>
      <th>OperatingExpense</th>
      <td>1497.8</td>
      <td>2246.8</td>
      <td>3137.2</td>
      <td>3137.2</td>
    </tr>
    <tr>
      <th>EBITDA</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>310.3</td>
    </tr>
    <tr>
      <th>NormalizedEBITDA</th>
      <td>436.4</td>
      <td>485.9</td>
      <td>318.3</td>
      <td>318.3</td>
    </tr>
    <tr>
      <th>EBIT</th>
      <td>239.4</td>
      <td>134.6</td>
      <td>-86.6</td>
      <td>-86.6</td>
    </tr>
    <tr>
      <th>NetIncome</th>
      <td>166.6</td>
      <td>75.4</td>
      <td>-124.6</td>
      <td>-124.6</td>
    </tr>
  </tbody>
</table>
</div>



Smart Charge been growing at ~40% annual since listing, and as a 85% gross margin / 10% EBITDA margin. I'm assuming similar financials for this portable charger company to be listed in Japan (target company). 

Below is the valuation metrics for Smart Charge. Its valuations have been depressed to a great extent due to a few reasons: 

1) shrinking margins; 

2) challenging environment in China with sluggish smartphone sales; 

3) regulatory pressure on the sector from the Chinese government; and 

4) uncertainties around potential delisting due to accounting/auditing debates between the US's PCAOB and China's CSRC. 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>asOfDate</th>
      <th>periodType</th>
      <th>EnterpriseValue</th>
      <th>EnterprisesValueEBITDARatio</th>
      <th>EnterprisesValueRevenueRatio</th>
      <th>MarketCap</th>
      <th>PbRatio</th>
      <th>PsRatio</th>
    </tr>
    <tr>
      <th>symbol</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>EM</th>
      <td>2021-06-30</td>
      <td>3M</td>
      <td>2092.5</td>
      <td>102.3</td>
      <td>2.2</td>
      <td>1514.1</td>
      <td></td>
      <td>2.9</td>
    </tr>
    <tr>
      <th>EM</th>
      <td>2021-09-30</td>
      <td>3M</td>
      <td>1410.9</td>
      <td>-18.7</td>
      <td>1.5</td>
      <td>833.1</td>
      <td>1.6</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>EM</th>
      <td>2021-12-31</td>
      <td>3M</td>
      <td>950.8</td>
      <td>-15.6</td>
      <td>1.1</td>
      <td>364.2</td>
      <td>0.7</td>
      <td>0.7</td>
    </tr>
    <tr>
      <th>EM</th>
      <td>2022-05-06</td>
      <td>TTM</td>
      <td>434.3</td>
      <td></td>
      <td></td>
      <td>276.6</td>
      <td>0.6</td>
      <td>0.4</td>
    </tr>
    <tr>
      <th>EM</th>
      <td>2022-05-07</td>
      <td>TTM</td>
      <td></td>
      <td>1.4</td>
      <td>0.1</td>
      <td></td>
      <td></td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>



Smart Charge's share price (see chart below) has been performing miserably due to the aforementioned reasons. 

As our target company operates in Japan, it's unlikely going to see these pressure EM US sees, but the valuation should be lower than the multiples EM went public at. My base case takes reference from EM's valuation in mid-2021, before the regulatory pressure kicked in. 

We can plug in EM's financials and check a few scenarios for target company:

1) High valuation - ipo_ps = 20.0x; ipo_pe = -100.0x; ipo_pb = 10.0x; all still lower than the average valuation in the growth board.

2) Similar to EM valuation last year - ipo_ps = 4.0x; ipo_pe = -20.0x; ipo_pb = 2.0x;

3) Very low valuation similar to EM now - ipo_ps = 1.0x; ipo_pe = -5.0x; ipo_pb = 1.0x



    
![png](jpx_analysis_files/jpx_analysis_61_0.png)
    


Now let's look at what our high valuation case implicates. We assumt 10x p/s, -100x p/e, and 20x p/b in the base case, as see what the models predict.




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>target company</th>
    </tr>
    <tr>
      <th></th>
      <th>Electronic Equipment &amp; Instrum</th>
    </tr>
    <tr>
      <th></th>
      <th>This is the company we are trying to do prediction for</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ipo_ps</th>
      <td>10.0</td>
    </tr>
    <tr>
      <th>ipo_pe</th>
      <td>-100.0</td>
    </tr>
    <tr>
      <th>ipo_pb</th>
      <td>20.0</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](jpx_analysis_files/jpx_analysis_66_0.png)
    


In the high valuation case, both random forest and adaboost models are predicting the -20% to 20% performance class (the chart means the adaboost is predicting 100% chance that the IPO will rise -20% to 20%, and randomforest is predicting about 35% chance that the IPO rise -20% to 20%). Both models agree, so the high valuation case is very likely goign to see -20% to 20% return on the IPO day, based on the historical data.

We can take a look at the base case also. 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>target company</th>
    </tr>
    <tr>
      <th></th>
      <th>Electronic Equipment &amp; Instrum</th>
    </tr>
    <tr>
      <th></th>
      <th>This is the company we are trying to do prediction for</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ipo_ps</th>
      <td>2.0</td>
    </tr>
    <tr>
      <th>ipo_pe</th>
      <td>-20.0</td>
    </tr>
    <tr>
      <th>ipo_pb</th>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](jpx_analysis_files/jpx_analysis_70_0.png)
    


In the base case where valuation is slightly higher than EM US but extremely cheap by growth board standards, the stock could perform well. Our models are prediction either 20-100% increase or even more than 100% increase at IPO. 

Finally, let's look at the bear/low valution case. 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>target company</th>
    </tr>
    <tr>
      <th></th>
      <th>Electronic Equipment &amp; Instrum</th>
    </tr>
    <tr>
      <th></th>
      <th>This is the company we are trying to do prediction for</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ipo_ps</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>ipo_pe</th>
      <td>-5.0</td>
    </tr>
    <tr>
      <th>ipo_pb</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




    
![png](jpx_analysis_files/jpx_analysis_74_0.png)
    


In the bear valuation case, both models are prediction high probability of very high returns. Intuitively this would make sense, as low valuation could revert to its true valuation if market is sufficiently efficient. 

## Conclusion

We have looked at the valuations and fundamental difference between growth board and the wider market, and noticed a wide valuation gap, with the growth board being generally very expensive with >100x P/E, ~40x P/S, and close to 10x P/B, all much more expensive than the overall market. It's also high growth and more volatile.

We then explored the IPO performance and know that IPOs on the growth board have on average been generating postive return since 2014, but in bear market years it's generally flat on IPO day. Return tend to ease off longer after the IPO and most IPOs drop to their offering prices after a year. 

We also explored the factors impacting IPO performance, and know that valuation at IPO, market performance, and interest rates are the most important factors affecting IPO performance.

For our target company itself, there are not many companies directly comparable so we could only look at EM US, which offers similar services. However, the idiosyncrasies of EM US from operating in China means that most of the metrics/performance cannot be directly applied to our target company. I have created 3 valuation scenarios with assumed financial that are similar to EM US, and have provided the predicted performance on the IPO day for each scenario. IPO performance tend to not differ too much from the IPO date within 6 months on average. 1 year after the IPO, however, expensive IPO almost always drop back and cheaper IPOs tend to revert to its true value.  




    126


