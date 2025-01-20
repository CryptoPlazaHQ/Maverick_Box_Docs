TYPE
series int
EXAMPLE
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
REMARKS
If analysts supply the targets when the market is closed, the variable can return na until the market opens.
SEE ALSO
syminfo.target_price_averagesyminfo.target_price_estimatessyminfo.target_price_highsyminfo.target_price_lowsyminfo.target_price_median
syminfo.target_price_estimates
The latest total number of price target predictions for the current symbol.
TYPE
series float
EXAMPLE
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
REMARKS
If analysts supply the targets when the market is closed, the variable can return na until the market opens.
SEE ALSO
syminfo.target_price_averagesyminfo.target_price_datesyminfo.target_price_highsyminfo.target_price_lowsyminfo.target_price_median
syminfo.target_price_high
The last highest yearly price target for the symbol predicted by analysts.
TYPE
series float
EXAMPLE
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
REMARKS
If analysts supply the targets when the market is closed, the variable can return na until the market opens.
SEE ALSO
syminfo.target_price_averagesyminfo.target_price_datesyminfo.target_price_estimatessyminfo.target_price_lowsyminfo.target_price_median
syminfo.target_price_low
The last lowest yearly price target for the symbol predicted by analysts.
TYPE
series float
EXAMPLE
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
REMARKS
If analysts supply the targets when the market is closed, the variable can return na until the market opens.
SEE ALSO
syminfo.target_price_averagesyminfo.target_price_datesyminfo.target_price_estimatessyminfo.target_price_highsyminfo.target_price_median
syminfo.target_price_median
The median of the last yearly price targets for the symbol predicted by analysts.
TYPE
series float
EXAMPLE
//@version=6
indicator("syminfo target_price")
if barstate.islastconfirmedhistory
    //@variable The time value one year from the date of the last analyst recommendations.
    int YTD = syminfo.target_price_date + timeframe.in_seconds("12M") * 1000
    //@variable A line connecting the current `close` to the highest yearly price estimate.
    highLine = line.new(time, close, YTD, syminfo.target_price_high, color = color.green, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the lowest yearly price estimate.
    lowLine = line.new(time, close, YTD, syminfo.target_price_low, color = color.red, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the median yearly price estimate.
    medianLine = line.new(time, close, YTD, syminfo.target_price_median, color = color.gray, xloc = xloc.bar_time)
    //@variable A line connecting the current `close` to the average yearly price estimate.
    averageLine = line.new(time, close, YTD, syminfo.target_price_average, color = color.orange, xloc = xloc.bar_time)
    // Fill the space between targets
    linefill.new(lowLine, medianLine, color.new(color.red, 90))
    linefill.new(medianLine, highLine, color.new(color.green, 90))
    // Create a label displaying the total number of analyst estimates.
    string estimatesText = str.format("Number of estimates: {0}", syminfo.target_price_estimates)
    label.new(bar_index, close, estimatesText, textcolor = color.white, size = size.large)
REMARKS
If analysts supply the targets when the market is closed, the variable can return na until the market opens.
SEE ALSO
syminfo.target_price_averagesyminfo.target_price_datesyminfo.target_price_estimatessyminfo.target_price_highsyminfo.target_price_low
syminfo.ticker
Symbol name without exchange prefix, e.g. 'MSFT'.
TYPE
simple string
SEE ALSO
syminfo.tickeridtimeframe.periodtimeframe.multipliersyminfo.root
syminfo.tickerid
A ticker identifier representing the chart's symbol or a requested symbol, depending on how the script uses it. The variable's value represents a requested dataset's ticker ID when used in the expression argument of a request.*() function call. Otherwise, it represents the chart's ticker ID. The value contains an exchange prefix and a symbol name, separated by a colon (e.g., "NASDAQ:AAPL"). It can also include information about data modifications such as dividend adjustment, non-standard chart type, currency conversion, etc.
TYPE
simple string
REMARKS
Because the value of this variable does not always use a simple "prefix:ticker" format, it is a poor candidate for use in boolean comparisons or string manipulation functions. In those contexts, run the variable's result through ticker.standard to purify it. This will remove any extraneous information and return a ticker ID consistently formatted using the "prefix:ticker" structure.
To always access the script's main ticker ID, even within another context, use the syminfo.main_tickerid variable.
SEE ALSO
ticker.newsyminfo.main_tickeridtimeframe.main_periodsyminfo.tickertimeframe.periodtimeframe.multipliersyminfo.root
syminfo.timezone
Timezone of the exchange of the chart main series. Possible values see in timestamp.
TYPE
simple string
SEE ALSO
timestamp
syminfo.type
The type of market the symbol belongs to. The values are "stock", "fund", "dr", "right", "bond", "warrant", "structured", "index", "forex", "futures", "spread", "economic", "fundamental", "crypto", "spot", "swap", "option", "commodity".
TYPE
simple string
SEE ALSO
syminfo.ticker
syminfo.volumetype
Volume type of the current symbol. Possible values are: "base" for base currency, "quote" for quote currency, "tick" for the number of transactions, and "n/a" when there is no volume or its type is not specified.
TYPE
simple string
REMARKS
Only some data feed suppliers provide information qualifying volume. As a result, the variable will return a value on some symbols only, mostly in the crypto sector.
SEE ALSO
syminfo.type
ta.accdist
Accumulation/distribution index.
TYPE
series float
ta.iii
Intraday Intensity Index.
TYPE
series float
EXAMPLE
//@version=6
indicator("Intraday Intensity Index")
plot(ta.iii, color=color.yellow)

// the same on pine
f_iii() =>
    (2 * close - high - low) / ((high - low) * volume)

plot(f_iii())
ta.nvi
Negative Volume Index.
TYPE
series float
EXAMPLE
//@version=6
indicator("Negative Volume Index")

plot(ta.nvi, color=color.yellow)

// the same on pine
f_nvi() =>
    float ta_nvi = 1.0
    float prevNvi = (nz(ta_nvi[1], 0.0) == 0.0) ? 1.0 : ta_nvi[1]
    if nz(close, 0.0) == 0.0 or nz(close[1], 0.0) == 0.0
        ta_nvi := prevNvi
    else
        ta_nvi := (volume < nz(volume[1], 0.0)) ? prevNvi + ((close - close[1]) / close[1]) * prevNvi : prevNvi
    result = ta_nvi

plot(f_nvi())
ta.obv
On Balance Volume.
TYPE
series float
EXAMPLE
//@version=6
indicator("On Balance Volume")
plot(ta.obv, color=color.yellow)

// the same on pine
f_obv() =>
    ta.cum(math.sign(ta.change(close)) * volume)

plot(f_obv())
ta.pvi
Positive Volume Index.
TYPE
series float
EXAMPLE
//@version=6
indicator("Positive Volume Index")

plot(ta.pvi, color=color.yellow)

// the same on pine
f_pvi() =>
    float ta_pvi = 1.0
    float prevPvi = (nz(ta_pvi[1], 0.0) == 0.0) ? 1.0 : ta_pvi[1]
    if nz(close, 0.0) == 0.0 or nz(close[1], 0.0) == 0.0
        ta_pvi := prevPvi
    else
        ta_pvi := (volume > nz(volume[1], 0.0)) ? prevPvi + ((close - close[1]) / close[1]) * prevPvi : prevPvi
    result = ta_pvi

plot(f_pvi())
ta.pvt
Price-Volume Trend.
TYPE
series float
EXAMPLE
//@version=6
indicator("Price-Volume Trend")
plot(ta.pvt, color=color.yellow)

// the same on pine
f_pvt() =>
    ta.cum((ta.change(close) / close[1]) * volume)

plot(f_pvt())
ta.tr
True range, equivalent to ta.tr(handle_na = false). It is calculated as math.max(high - low, math.abs(high - close[1]), math.abs(low - close[1])).
TYPE
series float
SEE ALSO
ta.trta.atr
ta.vwap
Volume Weighted Average Price. It uses hlc3 as its source series.
TYPE
series float
SEE ALSO
ta.vwap
ta.wad
Williams Accumulation/Distribution.
TYPE
series float
EXAMPLE
//@version=6
indicator("Williams Accumulation/Distribution")
plot(ta.wad, color=color.yellow)

// the same on pine
f_wad() =>
    trueHigh = math.max(high, close[1])
    trueLow = math.min(low, close[1])
    mom = ta.change(close)
    gain = (mom > 0) ? close - trueLow : (mom < 0) ? close - trueHigh : 0
    ta.cum(gain)

plot(f_wad())
ta.wvad
Williams Variable Accumulation/Distribution.
TYPE
series float
EXAMPLE
//@version=6
indicator("Williams Variable Accumulation/Distribution")
plot(ta.wvad, color=color.yellow)

// the same on pine
f_wvad() =>
    (close - open) / (high - low) * volume

plot(f_wvad())
table.all
Returns an array filled with all the current tables drawn by the script.
TYPE
array<table>
EXAMPLE
//@version=6
indicator("table.all")
//delete all tables
table.new(position = position.top_right, columns = 2, rows = 1, bgcolor = color.yellow, border_width = 1)
a_allTables = table.all
if array.size(a_allTables) > 0
    for i = 0 to array.size(a_allTables) - 1
        table.delete(array.get(a_allTables, i))
REMARKS
The array is read-only. Index zero of the array is the ID of the oldest object on the chart.
SEE ALSO
table.newline.alllabel.allbox.all
time
Current bar time in UNIX format. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
TYPE
series int
REMARKS
Note that this variable returns the timestamp based on the time of the bar's open. Because of that, for overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this variable can return time before the specified date of the trading day. For example, on EURUSD, dayofmonth(time) can be lower by 1 than the date of the trading day, because the bar for the current day actually opens one day prior.
SEE ALSO
timetime_closetimenowyearmonthweekofyeardayofmonthdayofweekhourminutesecond
time_close
The time of the current bar's close in UNIX format. It represents the number of milliseconds elapsed since 00:00:00 UTC, 1 January 1970. On non-standard price-based chart types (Renko, Line break, Kagi, Point & Figure, and Range), this variable returns na on the chart's realtime bars.
TYPE
series int
SEE ALSO
timetimenowyearmonthweekofyeardayofmonthdayofweekhourminutesecond
time_tradingday
The beginning time of the trading day the current bar belongs to, in UNIX format (the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970).
TYPE
series int
REMARKS
The variable is useful for overnight sessions, where the current day's session can start on the previous calendar day (e.g., on FXCM:EURUSD the Monday session will start on Sunday, 17:00 in the exchange timezone). Unlike time, which would return the timestamp for Sunday at 17:00 for the Monday daily bar, time_tradingday will return the timestamp for Monday, 00:00 UTC.
When used on timeframes higher than 1D, time_tradingday returns the trading day of the last day inside the bar (e.g. on 1W, it will return the last trading day of the week).
SEE ALSO
timetime_close
timeframe.isdaily
Returns true if current resolution is a daily resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.isminutestimeframe.issecondstimeframe.istickstimeframe.isweeklytimeframe.ismonthly
timeframe.isdwm
Returns true if current resolution is a daily or weekly or monthly resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isintradaytimeframe.isminutestimeframe.issecondstimeframe.istickstimeframe.isdailytimeframe.isweeklytimeframe.ismonthly
timeframe.isintraday
Returns true if current resolution is an intraday (minutes or seconds) resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isminutestimeframe.issecondstimeframe.istickstimeframe.isdwmtimeframe.isdailytimeframe.isweeklytimeframe.ismonthly
timeframe.isminutes
Returns true if current resolution is a minutes resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.issecondstimeframe.istickstimeframe.isdailytimeframe.isweeklytimeframe.ismonthly
timeframe.ismonthly
Returns true if current resolution is a monthly resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.isminutestimeframe.issecondstimeframe.istickstimeframe.isdailytimeframe.isweekly
timeframe.isseconds
Returns true if current resolution is a seconds resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.isminutestimeframe.istickstimeframe.isdailytimeframe.isweeklytimeframe.ismonthly
timeframe.isticks
Returns true if current resolution is a ticks resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.isminutestimeframe.issecondstimeframe.isdailytimeframe.isweeklytimeframe.ismonthly
timeframe.isweekly
Returns true if current resolution is a weekly resolution, false otherwise.
TYPE
simple bool
SEE ALSO
timeframe.isdwmtimeframe.isintradaytimeframe.isminutestimeframe.issecondstimeframe.istickstimeframe.isdailytimeframe.ismonthly
timeframe.main_period
A string representation of the script's main timeframe. If the script is an indicator that specifies a timeframe value in its declaration statement, this variable holds that value. Otherwise, its value represents the chart's timeframe. Unlike timeframe.period, this variable's value does not change when used in the expression argument of a request.*() function call.
The string's format is "<quantity>[<unit>]", where <unit> is "T" for ticks, "S" for seconds, "D" for days, "W" for weeks, and "M" for months, but is absent for minutes. No <unit> exists for hours: hourly timeframes are expressed in minutes.
The variable's value is: "10S" for 10 seconds, "30" for 30 minutes, "240" for four hours, "1D" for one day, "2W" for two weeks, and "3M" for one quarter.
TYPE
simple string
SEE ALSO
timeframe.periodsyminfo.main_tickeridsyminfo.tickersyminfo.tickeridtimeframe.multiplier
timeframe.multiplier
Multiplier of resolution, e.g. '60' - 60, 'D' - 1, '5D' - 5, '12M' - 12.
TYPE
simple int
SEE ALSO
syminfo.tickersyminfo.tickeridtimeframe.period
timeframe.period
A string representation of the script's main timeframe or a requested timeframe, depending on how the script uses it. The variable's value represents the timeframe of a requested dataset when used in the expression argument of a request.*() function call. Otherwise, its value represents the script's main timeframe (timeframe.main_period), which equals either the timeframe argument of the indicator declaration statement or the chart's timeframe.
The string's format is "<quantity>[<unit>]", where <unit> is "T" for ticks, "S" for seconds, "D" for days, "W" for weeks, and "M" for months, but is absent for minutes. No <unit> exists for hours: hourly timeframes are expressed in minutes.
The variable's value is: "10S" for 10 seconds, "30" for 30 minutes, "240" for four hours, "1D" for one day, "2W" for two weeks, and "3M" for one quarter.
TYPE
simple string
REMARKS
To always access the script's main timeframe, even within another context, use the timeframe.main_period variable.
SEE ALSO
timeframe.main_periodsyminfo.main_tickeridsyminfo.tickersyminfo.tickeridtimeframe.multiplier
timenow
Current time in UNIX format. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
TYPE
series int
REMARKS
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
timestamptimetime_closeyearmonthweekofyeardayofmonthdayofweekhourminutesecond
volume
Current bar volume.
TYPE
series float
REMARKS
Previous values may be accessed with square brackets operator [], e.g. volume[1], volume[2].
SEE ALSO
openhighlowclosetimehl2hlc3hlcc4ohlc4
weekofyear
Week number of current bar time in exchange timezone.
TYPE
series int
REMARKS
Note that this variable returns the week based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the week of the trading day.
SEE ALSO
weekofyeartimeyearmonthdayofmonthdayofweekhourminutesecond
year
Current bar year in exchange timezone.
TYPE
series int
REMARKS
Note that this variable returns the year based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the year of the trading day.
SEE ALSO
yeartimemonthweekofyeardayofmonthdayofweekhourminutesecond
Constants
adjustment.dividends
Constant for dividends adjustment type (dividends adjustment is applied).
TYPE
const string
SEE ALSO
adjustment.noneadjustment.splitsticker.new
adjustment.none
Constant for none adjustment type (no adjustment is applied).
TYPE
const string
SEE ALSO
adjustment.splitsadjustment.dividendsticker.new
adjustment.splits
Constant for splits adjustment type (splits adjustment is applied).
TYPE
const string
SEE ALSO
adjustment.noneadjustment.dividendsticker.new
alert.freq_all
A named constant for use with the freq parameter of the alert() function.
All function calls trigger the alert.
TYPE
const string
SEE ALSO
alert
alert.freq_once_per_bar
A named constant for use with the freq parameter of the alert() function.
The first function call during the bar triggers the alert.
TYPE
const string
SEE ALSO
alert
alert.freq_once_per_bar_close
A named constant for use with the freq parameter of the alert() function.
The function call triggers the alert only when it occurs during the last script iteration of the real-time bar, when it closes.
TYPE
const string
SEE ALSO
alert
backadjustment.inherit
A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.
TYPE
const backadjustment
SEE ALSO
ticker.newticker.modifybackadjustment.onbackadjustment.off
backadjustment.off
A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.
TYPE
const backadjustment
SEE ALSO
ticker.newticker.modifybackadjustment.onbackadjustment.inherit
backadjustment.on
A constant to specify the value of the backadjustment parameter in ticker.new and ticker.modify functions.
TYPE
const backadjustment
SEE ALSO
ticker.newticker.modifybackadjustment.inheritbackadjustment.off
barmerge.gaps_off
Merge strategy for requested data. Data is merged continuously without gaps, all the gaps are filled with the previous nearest existing value.
TYPE
const barmerge_gaps
SEE ALSO
request.securitybarmerge.gaps_on
barmerge.gaps_on
Merge strategy for requested data. Data is merged with possible gaps (na values).
TYPE
const barmerge_gaps
SEE ALSO
request.securitybarmerge.gaps_off
barmerge.lookahead_off
Merge strategy for the requested data position. Requested barset is merged with current barset in the order of sorting bars by their close time. This merge strategy disables effect of getting data from "future" on calculation on history.
TYPE
const barmerge_lookahead
SEE ALSO
request.securitybarmerge.lookahead_on
barmerge.lookahead_on
Merge strategy for the requested data position. Requested barset is merged with current barset in the order of sorting bars by their opening time. This merge strategy can lead to undesirable effect of getting data from "future" on calculation on history. This is unacceptable in backtesting strategies, but can be useful in indicators.
TYPE
const barmerge_lookahead
SEE ALSO
request.securitybarmerge.lookahead_off
