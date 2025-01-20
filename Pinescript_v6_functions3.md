line.all
Returns an array filled with all the current lines drawn by the script.
TYPE
array<line>
EXAMPLE
//@version=6
indicator("line.all")
//delete all lines
line.new(bar_index - 10, close, bar_index, close)
a_allLines = line.all
if array.size(a_allLines) > 0
    for i = 0 to array.size(a_allLines) - 1
        line.delete(array.get(a_allLines, i))
REMARKS
The array is read-only. Index zero of the array is the ID of the oldest object on the chart.
SEE ALSO
line.newlabel.allbox.alltable.all
linefill.all
Returns an array filled with all the current linefill objects drawn by the script.
TYPE
array<linefill>
REMARKS
The array is read-only. Index zero of the array is the ID of the oldest object on the chart.
low
Current low price.
TYPE
series float
REMARKS
Previous values may be accessed with square brackets operator [], e.g. low[1], low[2].
SEE ALSO
openhighclosevolumetimehl2hlc3hlcc4ohlc4
minute
Current bar minute in exchange timezone.
TYPE
series int
SEE ALSO
minutetimeyearmonthweekofyeardayofmonthdayofweekhoursecond
month
Current bar month in exchange timezone.
TYPE
series int
REMARKS
Note that this variable returns the month based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the month of the trading day.
SEE ALSO
monthtimeyearweekofyeardayofmonthdayofweekhourminutesecond
na
A keyword signifying "not available", indicating that a variable has no assigned value.
TYPE
simple na
EXAMPLE
//@version=6
indicator("na")
// CORRECT
// Plot no value when on bars zero to nine. Plot `close` on other bars.
plot(bar_index < 10 ? na : close)
// CORRECT ALTERNATIVE
// Initialize `a` to `na`. Reassign `close` to `a` on bars 10 and later.
float a = na
if bar_index >= 10
    a := close
plot(a)

// INCORRECT
// Trying to test the preceding bar's `close` for `na`.
// The next line, if uncommented, will cause a compilation error, because direct comparison with `na` is not allowed.
// plot(close[1] == na ? close : close[1])
// CORRECT
// Use the `na()` function to test for `na`.
plot(na(close[1]) ? close : close[1])
// CORRECT ALTERNATIVE
// `nz()` tests `close[1]` for `na`. It returns `close[1]` if it is not `na`, and `close` if it is.
plot(nz(close[1], close))
REMARKS
Do not use this variable with comparison operators to test values for na, as it might lead to unexpected behavior. Instead, use the na function. Note that na can be used to initialize variables when the initialization statement also specifies the variable's type.
SEE ALSO
nanzfixnan
ohlc4
Is a shortcut for (open + high + low + close)/4
TYPE
series float
SEE ALSO
openhighlowclosevolumetimehl2hlc3hlcc4
open
Current open price.
TYPE
series float
REMARKS
Previous values may be accessed with square brackets operator [], e.g. open[1], open[2].
SEE ALSO
highlowclosevolumetimehl2hlc3hlcc4ohlc4
polyline.all
Returns an array containing all current polyline instances drawn by the script.
TYPE
array<polyline>
REMARKS
The array is read-only. Index zero of the array references the ID of the oldest polyline object on the chart.
second
Current bar second in exchange timezone.
TYPE
series int
SEE ALSO
secondtimeyearmonthweekofyeardayofmonthdayofweekhourminute
session.isfirstbar
Returns true if the current bar is the first bar of the day's session, false otherwise. If extended session information is used, only returns true on the first bar of the pre-market bars.
TYPE
series bool
EXAMPLE
//@version=6
strategy("`session.isfirstbar` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition 
    strategy.entry("Long", strategy.long)

// Close the long position at the `close` of the trading session's last bar.
if session.islastbar and barstate.isconfirmed
    strategy.close("Long", immediately = true)
SEE ALSO
session.isfirstbar_regularsession.islastbarsession.islastbar_regular
session.isfirstbar_regular
Returns true on the first regular session bar of the day, false otherwise. The result is the same whether extended session information is used or not.
TYPE
series bool
EXAMPLE
//@version=6
strategy("`session.isfirstbar_regular` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition
    strategy.entry("Long", strategy.long)
// Close the long position at the `close` of the trading session's last bar.
if session.islastbar_regular and barstate.isconfirmed
    strategy.close("Long", immediately = true)
SEE ALSO
session.isfirstbarsession.islastbar
session.islastbar
Returns true if the current bar is the last bar of the day's session, false otherwise. If extended session information is used, only returns true on the last bar of the post-market bars.
TYPE
series bool
EXAMPLE
//@version=6
strategy("`session.islastbar` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's last bar.
// The position will enter on the `open` of next session's first bar.
if session.islastbar and longCondition
    strategy.entry("Long", strategy.long)
 // Close 'Long' position at the close of the last bar of the trading session
if session.islastbar and barstate.isconfirmed
    strategy.close("Long", immediately = true)
REMARKS
This variable is not guaranteed to return true once in every session because the last bar of the session might not exist if no trades occur during what should be the session's last bar.
This variable is not guaranteed to work as expected on non-standard chart types, e.g., Renko.
SEE ALSO
session.isfirstbarsession.islastbar_regular
session.islastbar_regular
Returns true on the last regular session bar of the day, false otherwise. The result is the same whether extended session information is used or not.
TYPE
series bool
EXAMPLE
//@version=6
strategy("`session.islastbar_regular` Example", overlay = true)
longCondition = year >= 2022
// Place a long order at the `close` of the trading session's first bar.
if session.isfirstbar and longCondition
    strategy.entry("Long", strategy.long)
// Close the long position at the `close` of the trading session's last bar.
if session.islastbar_regular and barstate.isconfirmed
    strategy.close("Long", immediately = true)
REMARKS
This variable is not guaranteed to return true once in every session because the last bar of the session might not exist if no trades occur during what should be the session's last bar.
This variable is not guaranteed to work as expected on non-standard chart types, e.g., Renko.
SEE ALSO
session.isfirstbarsession.islastbarsession.isfirstbar_regular
session.ismarket
Returns true if the current bar is a part of the regular trading hours (i.e. market hours), false otherwise.
TYPE
series bool
SEE ALSO
session.ispremarketsession.ispostmarket
session.ispostmarket
Returns true if the current bar is a part of the post-market, false otherwise. On non-intraday charts always returns false.
TYPE
series bool
SEE ALSO
session.ismarketsession.ispremarket
session.ispremarket
Returns true if the current bar is a part of the pre-market, false otherwise. On non-intraday charts always returns false.
TYPE
series bool
SEE ALSO
session.ismarketsession.ispostmarket
strategy.account_currency
Returns the currency used to calculate results, which can be set in the strategy's properties.
TYPE
simple string
SEE ALSO
strategystrategy.convert_to_accountstrategy.convert_to_symbol
strategy.avg_losing_trade
Returns the average amount of money lost per losing trade. Calculated as the sum of losses divided by the number of losing trades.
TYPE
series float
SEE ALSO
strategy.avg_losing_trade_percent
strategy.avg_losing_trade_percent
Returns the average percentage loss per losing trade. Calculated as the sum of loss percentages divided by the number of losing trades.
TYPE
series float
SEE ALSO
strategy.avg_losing_trade
strategy.avg_trade
Returns the average amount of money gained or lost per trade. Calculated as the sum of all profits and losses divided by the number of closed trades.
TYPE
series float
SEE ALSO
strategy.avg_trade_percent
strategy.avg_trade_percent
Returns the average percentage gain or loss per trade. Calculated as the sum of all profit and loss percentages divided by the number of closed trades.
TYPE
series float
SEE ALSO
strategy.avg_trade
strategy.avg_winning_trade
Returns the average amount of money gained per winning trade. Calculated as the sum of profits divided by the number of winning trades.
TYPE
series float
SEE ALSO
strategy.avg_winning_trade_percent
strategy.avg_winning_trade_percent
Returns the average percentage gain per winning trade. Calculated as the sum of profit percentages divided by the number of winning trades.
TYPE
series float
SEE ALSO
strategy.avg_winning_trade
strategy.closedtrades
Number of trades, which were closed for the whole trading range.
TYPE
series int
SEE ALSO
strategy.position_sizestrategy.opentradesstrategy.wintradesstrategy.losstradesstrategy.eventrades
strategy.closedtrades.first_index
The index, or trade number, of the first (oldest) trade listed in the List of Trades. This number is usually zero. If more trades than the allowed limit have been closed, the oldest trades are removed, and this number is the index of the oldest remaining trade.
TYPE
series int
SEE ALSO
strategy.position_sizestrategy.opentradesstrategy.wintradesstrategy.losstradesstrategy.eventrades
strategy.equity
Current equity (strategy.initial_capital + strategy.netprofit + strategy.openprofit).
TYPE
series float
SEE ALSO
strategy.netprofitstrategy.openprofitstrategy.position_size
strategy.eventrades
Number of breakeven trades for the whole trading range.
TYPE
series int
SEE ALSO
strategy.position_sizestrategy.opentradesstrategy.closedtradesstrategy.wintradesstrategy.losstrades
strategy.grossloss
Total currency value of all completed losing trades.
TYPE
series float
SEE ALSO
strategy.netprofitstrategy.grossprofit
strategy.grossloss_percent
The total value of all completed losing trades, expressed as a percentage of the initial capital.
TYPE
series float
SEE ALSO
strategy.grossloss
strategy.grossprofit
Total currency value of all completed winning trades.
TYPE
series float
SEE ALSO
strategy.netprofitstrategy.grossloss
strategy.grossprofit_percent
The total currency value of all completed winning trades, expressed as a percentage of the initial capital.
TYPE
series float
SEE ALSO
strategy.grossprofit
strategy.initial_capital
The amount of initial capital set in the strategy properties.
TYPE
series float
SEE ALSO
strategy
strategy.losstrades
Number of unprofitable trades for the whole trading range.
TYPE
series int
SEE ALSO
strategy.position_sizestrategy.opentradesstrategy.closedtradesstrategy.wintradesstrategy.eventrades
strategy.margin_liquidation_price
When margin is used in a strategy, returns the price point where a simulated margin call will occur and liquidate enough of the position to meet the margin requirements.
TYPE
series float
EXAMPLE
//@version=6
strategy("Margin call management", overlay = true, margin_long = 25, margin_short = 25, 
  default_qty_type = strategy.percent_of_equity, default_qty_value = 395)

float maFast = ta.sma(close, 14)
float maSlow = ta.sma(close, 28)

if ta.crossover(maFast, maSlow)
    strategy.entry("Long", strategy.long)

if ta.crossunder(maFast, maSlow)
    strategy.entry("Short", strategy.short)

changePercent(v1, v2) => 
    float result = (v1 - v2) * 100 / math.abs(v2)

// exit when we're 10% away from a margin call, to prevent it.
if math.abs(changePercent(close, strategy.margin_liquidation_price)) <= 10
    strategy.close("Long")
    strategy.close("Short")
REMARKS
The variable returns na if the strategy does not use margin, i.e., the strategy declaration statement does not specify an argument for the margin_long or margin_short parameter.
strategy.max_contracts_held_all
Maximum number of contracts/shares/lots/units in one trade for the whole trading range.
TYPE
series float
SEE ALSO
strategy.position_sizestrategy.max_contracts_held_longstrategy.max_contracts_held_short
strategy.max_contracts_held_long
Maximum number of contracts/shares/lots/units in one long trade for the whole trading range.
TYPE
series float
SEE ALSO
strategy.position_sizestrategy.max_contracts_held_allstrategy.max_contracts_held_short
strategy.max_contracts_held_short
Maximum number of contracts/shares/lots/units in one short trade for the whole trading range.
TYPE
series float
SEE ALSO
strategy.position_sizestrategy.max_contracts_held_allstrategy.max_contracts_held_long
strategy.max_drawdown
Maximum equity drawdown value for the whole trading range.
TYPE
series float
SEE ALSO
strategy.netprofitstrategy.equitystrategy.max_runup
strategy.max_drawdown_percent
The maximum equity drawdown value for the whole trading range, expressed as a percentage and calculated by formula: Lowest Value During Trade / (Entry Price x Quantity) * 100.
TYPE
series float
SEE ALSO
strategy.max_drawdown
strategy.max_runup
Maximum equity run-up value for the whole trading range.
TYPE
series float
SEE ALSO
strategy.netprofitstrategy.equitystrategy.max_drawdown
strategy.max_runup_percent
The maximum equity run-up value for the whole trading range, expressed as a percentage and calculated by formula: Highest Value During Trade / (Entry Price x Quantity) * 100.
TYPE
series float
SEE ALSO
strategy.max_runup
strategy.netprofit
Total currency value of all completed trades.
TYPE
series float
SEE ALSO
strategy.openprofitstrategy.position_sizestrategy.grossprofitstrategy.grossloss
strategy.netprofit_percent
The total value of all completed trades, expressed as a percentage of the initial capital.
TYPE
series float
SEE ALSO
strategy.netprofit
strategy.openprofit
Current unrealized profit or loss for all open positions.
TYPE
series float
SEE ALSO
