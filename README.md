# Residual-momentum-calc
Residual momentum calculator for equities, for use on Quantopian.com's research notebook feature.

The following script is meant to be used in the research notebook section of quant finance website ‘Quantopian’. It takes on certain time frame and equity selection criteria and will output a value factor for stocks in that selection.

This script is inspired by ideas put forward in the following papers:

Hongwei Chuang; ‘Time Series Residual Momentum’

Blitz, Huij, Martens; ‘Residual Momentum

Which in turn build on...

Fama, French; ‘Common risk factors in the returns on stocks and bonds’

Carhart; ‘On Persistence in Mutual Fund Performance’

In short, advocates for residual momentum market strategy argue purely momentum-based long/short equity strategy is likely to be ineffective when implemented in current markets. This is mainly for 2 reasons. The first, and weaker argument is that the momentum effect for equities is extremely well documented, and traditional pricing theory would dictate that little, if any, risk-free return can be gleaned from these particular rising or falling stocks since this effect should be priced into certain equities accordingly. The second is that, while you may hold an equal quantity of long and short positions in a portfolio to achieve market neutrality, the portfolio will inevitably be very exposed to any kind of structural break in the market which it is based. For example, if your portfolio is constructed in a rising market, highly positive momentum equities will likely have a large market correlation, and those with low momentum will likely have a small market correlation, hence you will still have significantly positive market exposure. This applies to the other Fama French factors in turn and means market reversals usually yield highly negative returns for momentum portfolios. This risk can be mitigated, to some extent, by incorporating a metric similar to that outlined below.

## The script in short:

#### A certain stock’s correlation to market returns of the 3 Fama French factors is calculated over a long time-frame. In the case below, 3 years.

* The overall market and risk-free returns are calculated by ETF proxies throughout the 3 year period to approximate the excess return of the overall market.

* Grouped sub-portfolios returns are compared to approximate the excess returns of the other 2 Fama French factors. Market capitalization and Book to Price ratio. This method of constructing sub-portfolios of stocks high and low in a factor we are looking to assess allows us to, on average, isolate the effect of the factor on stock returns.

* Linear regression is used over the period to compare a stock’s daily returns to that of the factor mimicking portfolios. The correlations calculated is now our estimate of a stock's exposure to that factor.


#### A certain stock’s predicted returns over a more recent time frame, in this case, 1 year, is calculated. 

* Risk-free and market returns proxies are again found 

* Grouped sub-portfolios seen previously again mimick isolated returns offered by Fama French factors

* An expected returns metric is then calculated by multiplying a stock's exposure to a factor by the returns of the corresponding factor mimicking portfolio. 


* The expected returns of a stock based on Fama French factor exposure alone is then calculated

#### The stock’s predicted returns are compared to its actual returns in the recent time frame to give a residual momentum value.

This is z-scored and combined with a momentum z-score, to produce a real number evaluation metric. Momentum has a positive effect on the metric, and residual momentum has a negative effect. Intuitively this means that high momentum equities are valued, (this is still a momentum strategy), however, equities whose returns have vastly exceeded what would be expected of them given factor exposure, are punished. 



*This metric is by no means a perfect representation of value and is not meant for use to select equities on its own.* 

First, it should be tweaked depending on the particular output you are looking for. For example, picks could be more or less shielded from the potential pitfalls of high momentum stocks depending on how you weight the final evaluation metric. It could also be adjusted to seek mean reversion opportunities. 

Time frames of analysis should also be adjusted depending on your investment horizon. 

The script can also be adapted for use to analyse individual equities, and compare their residual momentum to a particular tranche of the market, to aid investment decisions.
