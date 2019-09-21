# FinTA (Financial Technical Analysis)

[![License: LGPL v3](https://img.shields.io/badge/License-LGPL%20v3-blue.svg)](https://www.gnu.org/licenses/lgpl-3.0)
[![PyPI](https://img.shields.io/pypi/v/finta.svg?style=flat-square)](https://pypi.python.org/pypi/finta/)
[![](https://img.shields.io/badge/python-3.4+-blue.svg)](https://www.python.org/download/releases/3.4.0/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black)
[![Build Status](https://travis-ci.org/peerchemist/finta.svg?branch=master)](https://travis-ci.org/peerchemist/finta)

Common financial technical indicators implemented in Pandas.

*This is work in progress, bugs are expected and results of some indicators
may not be accurate.*

## Supported indicators:

Finta supports 75 trading indicators:

```
* Accumulation-Distribution Line 'ADL'
* Adaptive Price Zone 'APZ'
* Average Directional Index 'ADX'
* Average True Range 'ATR'
* Awesome Oscillator 'AO'
* Bollinger Bands 'BBANDS'
* Bollinger Bands Width 'BBWIDTH'
* Bull power and Bear Power 'EBBP'
* Buy and Sell Pressure 'BASP'
* Chaikin Oscillator 'CHAIKIN'
* Chande Momentum Oscillator 'CMO'
* Chandelier Exit 'CHANDELIER'
* Commodity Channel Index 'CCI'
* Coppock Curve 'COPP'
* Cummulative Force Index 'CFI'
* Directional Movement Indicator 'DMI'
* Donchian Channel 'DO'
* Double Exponential Moving Average 'DEMA'
* Ease of Movement 'EMV'
* Elastic Volume Moving Average 'EVWMA'
* Elastic-Volume weighted MACD 'EV_MACD'
* Elder's Force Index 'EFI'
* Exponential Moving Average 'EMA'
* Fibonacci Pivot Points 'PIVOT_FIB'
* Finite Volume Element 'FVE'
* Fisher Transform 'FISH'
* Hull Moving Average 'HMA'
* Ichimoku Cloud 'ICHIMOKU'
* Inverse Fisher Transform RSI 'IFT_RSI'
* Kaufman Efficiency Indicator 'ER'
* Kaufman's Adaptive Moving Average 'KAMA'
* Keltner Channels 'KC'
* Know Sure Thing 'KST'
* Market Momentum 'MOM'
* Mass Index 'MI'
* Money Flow Index 'MFI'
* Moving Average Convergence Divergence 'MACD'
* Moving Standard deviation 'MSD'
* Normalized BASP 'BASPN'
* On Balance Volume 'OBV'
* Percent B 'PERCENT_B'
* Percentage Price Oscillator 'PPO'
* Pivot Points 'PIVOT'
* Price Zone Oscillator 'PZO'
* Qstick 'QSTICK'
* Rate-of-Change 'ROC'
* Relative Strenght Index 'RSI'
* Simple Moving Average 'SMA'
* Simple Moving Median 'SMM'
* Smoothed Moving Average 'SMMA'
* Smoothed Simple Moving Average 'SSMA'
* Squeeze Momentum Indicator 'SQZMI'
* Stochastic oscillator %D 'STOCHD'
* Stochastic Oscillator %K 'STOCH'
* Stochastic RSI 'STOCHRSI'
* Stop-and-Reverse 'SAR'
* Triangular Moving Average 'TRIMA'
* Triple Exponential Moving Average 'TEMA'
* Triple Exponential Moving Average Oscillator 'TRIX'
* True Range 'TR'
* True Strength Index 'TSI'
* Twiggs Money Index 'TMF'
* Typical Price 'TP'
* Ultimate Oscillator 'UO'
* Vector Size Indicator 'VR'
* Volume Adjusted Moving Average 'VAMA'
* Volume Flow Indicator 'VFI'
* Volume Price Trend 'VPT'
* Volume Weighted Average Price 'VWAP'
* Volume Zone Oscillator 'VZO'
* Volume-Weighted MACD 'VW_MACD'
* Vortex Indicator 'VORTEX'
* Wave Trend Oscillator 'WTO'
* Weighted Moving Average 'WMA'
* Weighter OBV 'WOBV'
* Williams %R 'WILLIAMS'
* Zero Lag Exponential Moving Average 'ZLEMA'

```

## Dependencies:

-   python (3.4+)
-   pandas (0.21.1+)

TA class is very well documented and there should be no trouble
exploring it and using with your data. Each class method expects proper `ohlc` DataFrame as input.

## Install:

`pip install finta`

or latest development version:

`pip install git+git://github.com/peerchemist/finta.git`

## Import

`from finta import TA`

Prepare data to use with finta:

finta expects properly formated `ohlc` DataFrame, with column names in `lowercase`:
["open", "high", "low", close"] and ["volume"] for indicators that expect `ohlcv` input.

To prepare the DataFrame into `ohlc` format you can do something as following:

### standardize column names of your source
`df.columns = ["date", 'close', 'volume']`

### set index on the date column, which is requirement to sort it by time periods
`df.set_index('date', inplace=True)`

### select only price column, resample by time period and return daily ohlc (you can choose different time period)
`ohlc = df["close"].resample("24h").ohlc()`


`ohlc()` method applied on the Series above will automatically format the dataframe in format expected by the library so resulting `ohlc` Series is ready to use.
____________________________________________________________________________

## Examples:

### will return Pandas Series object with the Simple moving average for 42 periods
`TA.SMA(ohlc, 42)`

### will return Pandas Series object with "Awesome oscillator" values
`TA.AO(ohlc)`

### expects ["volume"] column as input
`TA.OBV(ohlc)`

### will return Series with Bollinger Bands columns [BB_UPPER, BB_LOWER]
`TA.BBANDS(ohlc)`

### will return Series with calculated BBANDS values but will use KAMA instead of MA for calculation, other types of Moving Averages are allowed as well.
`TA.BBANDS(ohlc, TA.KAMA(ohlc, 20))`

------------------------------------------------------------------------

I welcome pull requests with new indicators or fixes for existing ones.
Please submit only indicators that belong in public domain and are
royalty free.

## Contributing

1. Fork it (https://github.com/peerchemist/finta/fork)
2. Study how it's implemented.
3. Create your feature branch (`git checkout -b my-new-feature`).
4. Run [black](https://github.com/ambv/black) code formatter on the finta.py to ensure uniform code style.
5. Commit your changes (`git commit -am 'Add some feature'`).
6. Push to the branch (`git push origin my-new-feature`).
7. Create a new Pull Request.

------------------------------------------------------------------------

## Donate

Buy me a beer 🍺:

Bitcoin: 39PdX8jhXvUpzpkDibwMAVHVs6ZtoHCjnm

Peercoin: PRn448Km1ZJ2BhdPQfiSS3q4Af2vkjwwvH
