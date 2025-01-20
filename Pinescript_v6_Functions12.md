Orders from this command, unlike those from strategy.order, are affected by the pyramiding parameter of the strategy declaration statement. Pyramiding specifies the number of concurrent open entries allowed per position. For example, with pyramiding = 3, the strategy can have up to three open trades, and the command cannot create orders to open additional trades until at least one existing trade closes.
By default, when a strategy executes an order from this command in the opposite direction of the current market position, it reverses that position. For example, if there is an open long position of five shares, an order from this command with a qty of 5 and a direction of strategy.short triggers the sale of 10 shares to close the long position and open a new five-share short position. Users can change this behavior by specifying an allowed direction with the strategy.risk_allow_entry_in function.
SYNTAX
strategy.entry(id, direction, qty, limit, stop, oca_name, oca_type, comment, alert_message, disable_alert) → void
ARGUMENTS
id (series string) The identifier of the order, which corresponds to an entry ID in the strategy's trades after the order fills. If the strategy opens a new position after filling the order, the order's ID becomes the strategy.position_entry_name value. Strategy commands can reference the order ID to cancel or modify pending orders and generate exit orders for specific open trades. The Strategy Tester and the chart display the order ID unless the command specifies a comment value.
direction (series strategy_direction) The direction of the trade. Possible values: strategy.long for a long trade, strategy.short for a short one.
qty (series int/float) Optional. The number of contracts/shares/lots/units in the resulting open trade when the order fills. The default is na, which means that the command uses the default_qty_type and default_qty_value parameters of the strategy declaration statement to determine the quantity.
limit (series int/float) Optional. The limit price of the order. If specified, the command creates a limit or stop-limit order, depending on whether the stop value is also specified. The default is na, which means the resulting order is not of the limit or stop-limit type.
stop (series int/float) Optional. The stop price of the order. If specified, the command creates a stop or stop-limit order, depending on whether the limit value is also specified. The default is na, which means the resulting order is not of the stop or stop-limit type.
oca_name (series string) Optional. The name of the order's One-Cancels-All (OCA) group. When a pending order with the same oca_name and oca_type parameters executes, that order affects all unfilled orders in the group. The default is an empty string, which means the order does not belong to an OCA group.
oca_type (input string) Optional. Specifies how an unfilled order behaves when another pending order with the same oca_name and oca_type values executes. Possible values: strategy.oca.cancel, strategy.oca.reduce, strategy.oca.none. The default is strategy.oca.none.
comment (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the specified id. The default is an empty string.
alert_message (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. The default is an empty string.
disable_alert (series bool) Optional. If true when the command creates an order, the strategy does not trigger an alert when that order fills. This parameter accepts a "series" value, meaning users can control which orders trigger alerts when they execute. The default is false.
EXAMPLE
//@version=6
strategy("Market order strategy", overlay = true)

// Calculate a 14-bar and 28-bar moving average of `close` prices.
float sma14 = ta.sma(close, 14)
float sma28 = ta.sma(close, 28)

// Place a market order to close the short trade and enter a long position when `sma14` crosses over `sma28`.
if ta.crossover(sma14, sma28)
    strategy.entry("My Long Entry ID", strategy.long)

// Place a market order to close the long trade and enter a short position when `sma14` crosses under `sma28`.
if ta.crossunder(sma14, sma28)
    strategy.entry("My Short Entry ID", strategy.short)
EXAMPLE
//@version=6
strategy("Limit order strategy", overlay=true, margin_long=100, margin_short=100)

//@variable The distance from the `close` price for each limit order.
float limitOffsetInput = input.int(100, "Limit offset, in ticks", 1) * syminfo.mintick

//@function Draws a label and line at the specified `price` to visualize a limit order's level. 
drawLimit(float price, bool isLong) =>
    color col = isLong ? color.blue : color.red
    label.new(
         bar_index, price, (isLong ? "Long" : "Short") + " limit order created", 
         style = label.style_label_right, color = col, textcolor = color.white
     )
    line.new(bar_index, price, bar_index + 1, price, extend = extend.right, style = line.style_dashed, color = col)

//@function Stops the `l` line from extending further.
method stopExtend(line l) =>
    l.set_x2(bar_index)
    l.set_extend(extend.none)

// Initialize two `line` variables to reference limit line IDs.
var line longLimit  = na
var line shortLimit = na

// Calculate a 14-bar and 28-bar moving average of `close` prices.
float sma14 = ta.sma(close, 14)
float sma28 = ta.sma(close, 28)

if ta.crossover(sma14, sma28)
    // Cancel any unfilled sell orders with the specified ID.
    strategy.cancel("My Short Entry ID")
    //@variable The limit price level. Its value is `limitOffsetInput` ticks below the current `close`.
    float limitLevel = close - limitOffsetInput
    // Place a long limit order to close the short trade and enter a long position at the `limitLevel`.
    strategy.entry("My Long Entry ID", strategy.long, limit = limitLevel)
    // Make new drawings for the long limit and stop extending the `shortLimit` line.
    longLimit := drawLimit(limitLevel, isLong = true)
    shortLimit.stopExtend()
    
if ta.crossunder(sma14, sma28)
    // Cancel any unfilled buy orders with the specified ID.
    strategy.cancel("My Long Entry ID")
    //@variable The limit price level. Its value is `limitOffsetInput` ticks above the current `close`.
    float limitLevel = close + limitOffsetInput
    // Place a short limit order to close the long trade and enter a short position at the `limitLevel`.
    strategy.entry("My Short Entry ID", strategy.short, limit = limitLevel)
    // Make new drawings for the short limit and stop extending the `shortLimit` line.
    shortLimit := drawLimit(limitLevel, isLong = false)
    longLimit.stopExtend()
strategy.exit()
Creates price-based orders to exit from an open position. If unfilled exit orders with the same id exist, calls to this command modify those orders. This command can generate more than one type of exit order, depending on the specified parameters. However, it does not create market orders. To exit from a position with a market order, use strategy.close or strategy.close_all.
If a call to this command contains a profit or limit argument, it creates take-profit orders to exit from applicable trades at the determined price levels or better values (higher for long trades and lower for short ones). If the call contains loss or stop arguments, it creates stop-loss orders to exit from applicable trades at the determined levels or worse values (lower for long trades and higher for short ones). Calling this command with profit or limit and loss or stop arguments creates an order bracket with both order types.
This command can create trailing stop orders when its call specifies a trail_price or trail_points argument and a trail_offset argument. A trailing stop order activates when the price moves trail_points ticks past the entry price or touches the trail_price level. Once activated, the stop follows trail_offset ticks behind the market price each time the trade's profit reaches a new high. The stop does not move when the trade does not achieve a new best value.
Each call to this command reserves a portion of the position to close until the strategy fills or cancels its orders. For example, if there is an open position of 50 contracts and a strategy.exit call specifies a qty of 20, that call's orders reserve 20 contracts out of the position. A second call can close a maximum of 30 contracts, even if its qty is 50 and one of its orders executes first. This behavior does not affect the orders from other commands, such as strategy.close or strategy.order.
If a call to this command occurs before a created entry order's execution, the strategy waits and does not create the exit orders until after the entry order executes.
SYNTAX
strategy.exit(id, from_entry, qty, qty_percent, profit, limit, loss, stop, trail_price, trail_points, trail_offset, oca_name, comment, comment_profit, comment_loss, comment_trailing, alert_message, alert_profit, alert_loss, alert_trailing, disable_alert) → void
ARGUMENTS
id (series string) The identifier of the orders, which corresponds to an exit ID in the strategy's trades after an order fills. Strategy commands can reference the order ID to cancel or modify pending exit orders. The Strategy Tester and the chart display the order ID unless the command includes a comment* argument that applies to the filled order.
from_entry (series string) Optional. The entry order ID of the trade to exit from. If there is more than one open trade with the specified entry ID, the command generates exit orders for all the entries from before or at the time of the call. The default is an empty string, which means the command generates exit orders for all open trades until the position closes.
qty (series int/float) Optional. The number of contracts/lots/shares/units to close when an exit order fills. If specified, the command uses this value instead of qty_percent to determine the order size. The exit orders reserve this quantity from the position, meaning other calls to this command cannot close this portion until the strategy fills or cancels those orders. The default is na, which means the order size depends on the qty_percent value.
qty_percent (series int/float) Optional. A value between 0 and 100 representing the percentage of the open trade quantity to close when an exit order fills. The exit orders reserve this percentage from the applicable open trades, meaning other calls to this command cannot close this portion until the strategy fills or cancels those orders. The percentage calculation depends on the total size of the applicable open trades without considering the reserved amount from other strategy.exit calls. The command ignores this parameter if the qty value is not na. The default is 100.
profit (series int/float) Optional. The take-profit distance, expressed in ticks. If specified, the command creates a limit order to exit the trade profit ticks away from the entry price in the favorable direction. The order executes at the calculated price or a better value. If this parameter and limit are not na, the command places a take-profit order only at the price level expected to trigger an exit first. The default is na.
limit (series int/float) Optional. The take-profit price. If this parameter and profit are not na, the command places a take-profit order only at the price level expected to trigger an exit first. The default is na.
loss (series int/float) Optional. The stop-loss distance, expressed in ticks. If specified, the command creates a stop order to exit the trade loss ticks away from the entry price in the unfavorable direction. The order executes at the calculated price or a worse value. If this parameter and stop are not na, the command places a stop-loss order only at the price level expected to trigger an exit first. The default is na.
stop (series int/float) Optional. The stop-loss price. If this parameter and loss are not na, the command places a stop-loss order only at the price level expected to trigger an exit first. The default is na.
trail_price (series int/float) Optional. The price of the trailing stop activation level. If the value is more favorable than the entry price, the command creates a trailing stop when the market price reaches that value. If less favorable than the entry price, the command creates the trailing stop immediately when the current market price is equal to or more favorable than the value. If this parameter and trail_points are not na, the command sets the activation level using the value expected to activate the stop first. The default is na.
trail_points (series int/float) Optional. The trailing stop activation distance, expressed in ticks. If the value is positive, the command creates a trailing stop order when the market price moves trail_points ticks away from the trade's entry price in the favorable direction. If the value is negative, the command creates the trailing stop immediately when the market price is equal to or more favorable than the level trail_points ticks away from the entry price in the unfavorable direction. The default is na.
trail_offset (series int/float) Optional. The trailing stop offset. When the market price reaches the activation level determined by the trail_price or trail_points parameter, or exceeds the level in the favorable direction, the command creates a trailing stop with an initial value trail_offset ticks away from that level in the unfavorable direction. After activation, the trailing stop moves toward the market price each time the trade's profit reaches a better value, maintaining the specified distance behind the best price. The default is na.
oca_name (series string) Optional. The name of the One-Cancels-All (OCA) group that the command's take-profit, stop-loss, and trailing stop orders belong to. All orders from this command are of the strategy.oca.reduce OCA type. When an order of this OCA type with the same oca_name executes, the strategy reduces the sizes of other unfilled orders in the OCA group by the filled quantity. The default is an empty string, which means the strategy assigns the OCA name automatically, and the resulting orders cannot reduce or be reduced by the orders from other commands.
comment (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the specified id. The command ignores this value if the call includes an argument for a comment_* parameter that applies to the order. The default is an empty string.
comment_profit (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the specified id or comment. This comment applies only to the command's take-profit orders created using the profit or limit parameter. The default is an empty string.
comment_loss (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the specified id or comment. This comment applies only to the command's stop-loss orders created using the loss or stop parameter. The default is an empty string.
comment_trailing (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the specified id or comment. This comment applies only to the command's trailing stop orders created using the trail_price or trail_points and trail_offset parameters. The default is an empty string.
alert_message (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. The command ignores this value if the call includes an argument for the other alert_* parameter that applies to the order. The default is an empty string.
alert_profit (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. This message applies only to the command's take-profit orders created using the profit or limit parameter. The default is an empty string.
alert_loss (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. This message applies only to the command's stop-loss orders created using the loss or stop parameter. The default is an empty string.
alert_trailing (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. This message applies only to the command's trailing stop orders created using the trail_price or trail_points and trail_offset parameters. The default is an empty string.
disable_alert (series bool) Optional. If true when the command creates an order, the strategy does not trigger an alert when that order fills. This parameter accepts a "series" value, meaning users can control which orders trigger alerts when they execute. The default is false.
EXAMPLE
//@version=6
strategy("Exit bracket strategy", overlay = true)

// Inputs that define the profit and loss amount of each trade as a tick distance from the entry price.
int profitDistanceInput = input.int(100, "Profit distance, in ticks", 1)
int lossDistanceInput   = input.int(100, "Loss distance, in ticks", 1)

// Variables to track the take-profit and stop-loss price. 
var float takeProfit = na
var float stopLoss   = na

// Calculate a 14-bar and 28-bar moving average of `close` prices.
float sma14 = ta.sma(close, 14)
float sma28 = ta.sma(close, 28)

if ta.crossover(sma14, sma28) and strategy.opentrades == 0
    // Place a market order to enter a long position.
    strategy.entry("My Long Entry ID", strategy.long)
    // Place a take-profit and stop-loss order when the entry order fills. 
    strategy.exit("My Long Exit ID", "My Long Entry ID", profit = profitDistanceInput, loss = lossDistanceInput)

if ta.change(strategy.opentrades) == 1
    //@variable The long entry price.
    float entryPrice = strategy.opentrades.entry_price(0)
    // Update the `takeProfit` and `stopLoss` values.
    takeProfit := entryPrice + profitDistanceInput * syminfo.mintick
    stopLoss   := entryPrice - lossDistanceInput * syminfo.mintick

if ta.change(strategy.closedtrades) == 1
    // Reset the `takeProfit` and `stopLoss`.
    takeProfit := na
    stopLoss   := na

// Plot the `takeProfit` and `stopLoss`.
plot(takeProfit, "Take-profit level", color.green, 2, plot.style_linebr)
plot(stopLoss, "Stop-loss level", color.red, 2, plot.style_linebr)
EXAMPLE
//@version=6
strategy("Trailing stop strategy", overlay = true)

//@variable The distance required to activate the trailing stop.
float activationDistanceInput = input.int(100, "Trail activation distance, in ticks") * syminfo.mintick 
//@variable The number of ticks the trailing stop follows behind the price as it reaches new peaks. 
int trailDistanceInput = input.int(100, "Trail distance, in ticks")

//@function Draws a label and line at the specified `price` to visualize a trailing stop order's activation level. 
drawActivation(float price) =>
    label.new(
         bar_index, price, "Activation level", style = label.style_label_right, 
         color = color.gray, textcolor = color.white
     )
    line.new(
         bar_index, price, bar_index + 1, price, extend = extend.right, style = line.style_dashed, color = color.gray
     )

//@function Stops the `l` line from extending further.
method stopExtend(line l) =>
    l.set_x2(bar_index)
    l.set_extend(extend.none)

// The activation line, active trailing stop price, and active trailing stop flag. 
var line activationLine     = na
var float trailingStopPrice = na
var bool isActive           = false

if bar_index % 100 == 0 and strategy.opentrades == 0
    trailingStopPrice := na
    isActive          := false
    // Place a market order to enter a long position.
    strategy.entry("My Long Entry ID", strategy.long)
    //@variable The activation level's price. 
    float activationPrice = close + activationDistanceInput
    // Create a trailing stop order that activates the defined number of ticks above the entry price.
    strategy.exit(
         "My Long Exit ID", "My Long Entry ID", trail_price = activationPrice, trail_offset = trailDistanceInput,
         oca_name = "Exit"
     )
    // Create new drawings at the `activationPrice`.
    activationLine := drawActivation(activationPrice)

// Logic for trailing stop visualization. 
if strategy.opentrades == 1
    // Stop extending the `activationLine` when the stop activates.
    if not isActive and high > activationLine.get_price(bar_index)
        isActive := true
        activationLine.stopExtend()
    // Update the `trailingStopPrice` while the trailing stop is active. 
    if isActive
        float offsetPrice = high - trailDistanceInput * syminfo.mintick
        trailingStopPrice := math.max(nz(trailingStopPrice, offsetPrice), offsetPrice)

// Close the trade with a market order if the trailing stop does not activate before the next 300th bar. 
if not isActive and bar_index % 300 == 0
    strategy.close_all("Market close")

// Reset the `trailingStopPrice` and `isActive` flags when the trade closes, and stop extending the `activationLine`.
if ta.change(strategy.closedtrades) > 0
    if not isActive
        activationLine.stopExtend()
    trailingStopPrice := na
    isActive          := false

// Plot the `trailingStopPrice`.
plot(trailingStopPrice, "Trailing stop", color.red, 3, plot.style_linebr)
REMARKS
A single call to the strategy.exit command can generate exit orders for several entries in an open position, depending on the call's from_entry value. If the call does not include a from_entry argument, it creates exit orders for all open trades, even the ones opened after the call, until the position closes. See this section of our User Manual to learn more.
When a position consists of several open trades, and the close_entries_rule in the strategy declaration statement is "FIFO" (default), the orders from a strategy.exit call exit from the position starting with the first open trade. This behavior applies even if the from_entry value is the entry ID of different open trades. However, in that case, the maximum size of the exit orders still depends on the trades opened by orders with the from_entry ID. For more information, see this section of our User Manual.
If a strategy.exit call includes arguments for creating stop-loss and trailing stop orders, the command places only the order that is supposed to fill first, because both orders are of the "stop" type.
strategy.opentrades.commission()
Returns the sum of entry and exit fees paid in the open trade, expressed in strategy.account_currency.
SYNTAX
strategy.opentrades.commission(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
// Calculates the gross profit or loss for the current open position.
//@version=6
strategy("`strategy.opentrades.commission` Example", commission_type = strategy.commission.percent, commission_value = 0.1)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Calculate gross profit or loss for open positions only.
tradeOpenGrossPL() =>
    sumOpenGrossPL = 0.0
    for tradeNo = 0 to strategy.opentrades - 1
        sumOpenGrossPL += strategy.opentrades.profit(tradeNo) - strategy.opentrades.commission(tradeNo)
    result = sumOpenGrossPL
    
plot(tradeOpenGrossPL())
SEE ALSO
strategystrategy.closedtrades.commission
strategy.opentrades.entry_bar_index()
Returns the bar_index of the open trade's entry.
SYNTAX
strategy.opentrades.entry_bar_index(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
// Wait 10 bars and then close the position.
//@version=6
strategy("`strategy.opentrades.entry_bar_index` Example")

barsSinceLastEntry() =>
    strategy.opentrades > 0 ? bar_index - strategy.opentrades.entry_bar_index(strategy.opentrades - 1) : na

// Enter a long position if there are no open positions.
if strategy.opentrades == 0
    strategy.entry("Long", strategy.long)

// Close the long position after 10 bars. 
if barsSinceLastEntry() >= 10
    strategy.close("Long")
SEE ALSO
strategy.closedtrades.entry_bar_indexstrategy.closedtrades.exit_bar_index
strategy.opentrades.entry_comment()
Returns the comment message of the open trade's entry, or na if there is no entry with this trade_num.
SYNTAX
strategy.opentrades.entry_comment(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.opentrades.entry_comment()` Example", overlay = true)

stopPrice = open * 1.01

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))

if (longCondition)
    strategy.entry("Long", strategy.long, stop = stopPrice, comment = str.tostring(stopPrice, "#.####"))

var testTable = table.new(position.top_right, 1, 3, color.orange, border_width = 1)

if barstate.islastconfirmedhistory or barstate.isrealtime
    table.cell(testTable, 0, 0, 'Last entry stats')
    table.cell(testTable, 0, 1, "Order stop price value: " + strategy.opentrades.entry_comment(strategy.opentrades - 1))
    table.cell(testTable, 0, 2, "Actual Entry Price: " + str.tostring(strategy.opentrades.entry_price(strategy.opentrades - 1)))
SEE ALSO
strategystrategy.entrystrategy.opentrades
strategy.opentrades.entry_id()
Returns the id of the open trade's entry.
SYNTAX
strategy.opentrades.entry_id(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.opentrades.entry_id` Example", overlay = true)

// We enter a long position when 14 period sma crosses over 28 period sma.
// We enter a short position when 14 period sma crosses under 28 period sma.
longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
shortCondition = ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))

// Strategy calls to enter a long or short position when the corresponding condition is met.
if longCondition
    strategy.entry("Long entry at bar #" + str.tostring(bar_index), strategy.long)
if shortCondition
    strategy.entry("Short entry at bar #" + str.tostring(bar_index), strategy.short)

// Display ID of the latest open position.
if barstate.islastconfirmedhistory
    label.new(bar_index, high + (2 * ta.tr), "Last opened position is \n " + strategy.opentrades.entry_id(strategy.opentrades - 1))
RETURNS
Returns the id of the open trade's entry.
REMARKS
The function returns na if trade_num is not in the range: 0 to strategy.opentrades-1.
SEE ALSO
strategy.opentrades.entry_bar_indexstrategy.opentrades.entry_pricestrategy.opentrades.entry_time
strategy.opentrades.entry_price()
Returns the price of the open trade's entry.
SYNTAX
strategy.opentrades.entry_price(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.opentrades.entry_price Example 1", overlay = true)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if ta.crossover(close, ta.sma(close, 14))
    strategy.entry("Long", strategy.long)

// Return the entry price for the latest closed trade.
currEntryPrice = strategy.opentrades.entry_price(strategy.opentrades - 1)
currExitPrice = currEntryPrice * 1.05

if high >= currExitPrice
    strategy.close("Long")

plot(currEntryPrice, "Long entry price", style = plot.style_linebr)
plot(currExitPrice, "Long exit price", color.green, style = plot.style_linebr)
EXAMPLE
// Calculates the average price for the open position.
//@version=6
strategy("strategy.opentrades.entry_price Example 2", pyramiding = 2)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Calculates the average price for the open position.
avgOpenPositionPrice() =>
    sumOpenPositionPrice = 0.0
    for tradeNo = 0 to strategy.opentrades - 1
        sumOpenPositionPrice += strategy.opentrades.entry_price(tradeNo) * strategy.opentrades.size(tradeNo) / strategy.position_size
    result = nz(sumOpenPositionPrice / strategy.opentrades)

plot(avgOpenPositionPrice())
SEE ALSO
strategy.closedtrades.exit_price
strategy.opentrades.entry_time()
Returns the UNIX time of the open trade's entry, expressed in milliseconds.
SYNTAX
strategy.opentrades.entry_time(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.opentrades.entry_time Example")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Calculates duration in milliseconds since the last position was opened.
timeSinceLastEntry()=>
    strategy.opentrades > 0 ? (time - strategy.opentrades.entry_time(strategy.opentrades - 1)) : na

plot(timeSinceLastEntry() / 1000 * 60 * 60 * 24, "Days since last entry")
SEE ALSO
strategy.closedtrades.entry_timestrategy.closedtrades.exit_time
strategy.opentrades.max_drawdown()
Returns the maximum drawdown of the open trade, i.e., the maximum possible loss during the trade, expressed in strategy.account_currency.
SYNTAX
strategy.opentrades.max_drawdown(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.opentrades.max_drawdown Example 1")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Plot the max drawdown of the latest open trade.
plot(strategy.opentrades.max_drawdown(strategy.opentrades - 1), "Max drawdown of the latest open trade")
EXAMPLE
// Calculates the max trade drawdown value for all open trades.
//@version=6
strategy("`strategy.opentrades.max_drawdown` Example 2", pyramiding = 100)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Get the biggest max trade drawdown value from all of the open trades.
maxTradeDrawDown() =>
    maxDrawdown = 0.0
    for tradeNo = 0 to strategy.opentrades - 1
        maxDrawdown := math.max(maxDrawdown, strategy.opentrades.max_drawdown(tradeNo))
    result = maxDrawdown

plot(maxTradeDrawDown(), "Biggest max drawdown")
REMARKS
The function returns na if trade_num is not in the range: 0 to strategy.closedtrades - 1.
SEE ALSO
strategy.closedtrades.max_drawdownstrategy.max_drawdown
strategy.opentrades.max_drawdown_percent()
Returns the maximum drawdown of the open trade, i.e., the maximum possible loss during the trade, expressed as a percentage and calculated by formula: Lowest Value During Trade / (Entry Price x Quantity) * 100.
SYNTAX
strategy.opentrades.max_drawdown_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.opentrades.max_drawdownstrategy.max_drawdown
strategy.opentrades.max_runup()
Returns the maximum run up of the open trade, i.e., the maximum possible profit during the trade, expressed in strategy.account_currency.
SYNTAX
strategy.opentrades.max_runup(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.opentrades.max_runup Example 1")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Plot the max runup of the latest open trade.
plot(strategy.opentrades.max_runup(strategy.opentrades - 1), "Max runup of the latest open trade")
EXAMPLE
// Calculates the max trade runup value for all open trades.
//@version=6
strategy("strategy.opentrades.max_runup Example 2", pyramiding = 100)

// Enter a long position every 30 bars.
if bar_index % 30 == 0
    strategy.entry("Long", strategy.long)

// Calculate biggest max trade runup value from all of the open trades.
maxOpenTradeRunUp() =>
    maxRunup = 0.0
    for tradeNo = 0 to strategy.opentrades - 1
        maxRunup := math.max(maxRunup, strategy.opentrades.max_runup(tradeNo))
    result = maxRunup

plot(maxOpenTradeRunUp(), "Biggest max runup of all open trades")
SEE ALSO
strategy.closedtrades.max_runupstrategy.max_drawdown
strategy.opentrades.max_runup_percent()
Returns the maximum run-up of the open trade, i.e., the maximum possible profit during the trade, expressed as a percentage and calculated by formula: Highest Value During Trade / (Entry Price x Quantity) * 100.
SYNTAX
strategy.opentrades.max_runup_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.opentrades.max_runupstrategy.max_runup
strategy.opentrades.profit()
Returns the profit/loss of the open trade, expressed in strategy.account_currency. Losses are expressed as negative values.
SYNTAX
strategy.opentrades.profit(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
// Returns the profit of the last open trade.
//@version=6
strategy("`strategy.opentrades.profit` Example 1", commission_type = strategy.commission.percent, commission_value = 0.1)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

plot(strategy.opentrades.profit(strategy.opentrades - 1), "Profit of the latest open trade")
EXAMPLE
// Calculates the profit for all open trades.
//@version=6
strategy("`strategy.opentrades.profit` Example 2", pyramiding = 5)

// Strategy calls to enter 5 long positions every 2 bars.
if bar_index % 2 == 0
    strategy.entry("Long", strategy.long, qty = 5)

// Calculate open profit or loss for the open positions.
tradeOpenPL() =>
    sumProfit = 0.0
    for tradeNo = 0 to strategy.opentrades - 1
        sumProfit += strategy.opentrades.profit(tradeNo)
    result = sumProfit
    
plot(tradeOpenPL(), "Profit of all open trades")
SEE ALSO
strategy.closedtrades.profitstrategy.openprofitstrategy.netprofitstrategy.grossprofit
strategy.opentrades.profit_percent()
Returns the profit/loss of the open trade, expressed as a percentage. Losses are expressed as negative values.
SYNTAX
strategy.opentrades.profit_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.opentrades.profit
strategy.opentrades.size()
Returns the direction and the number of contracts traded in the open trade. If the value is > 0, the market position was long. If the value is < 0, the market position was short.
SYNTAX
strategy.opentrades.size(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the open trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.opentrades.size` Example 1")

// We calculate the max amt of shares we can buy.
amtShares = math.floor(strategy.equity / close)
// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long, qty = amtShares)
if bar_index % 20 == 0
    strategy.close("Long")

// Plot the number of contracts in the latest open trade.
plot(strategy.opentrades.size(strategy.opentrades - 1), "Amount of contracts in latest open trade")
EXAMPLE
// Calculates the average profit percentage for all open trades.
//@version=6
strategy("`strategy.opentrades.size` Example 2")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Calculate profit for all open trades.
profitPct = 0.0
for tradeNo = 0 to strategy.opentrades - 1
    entryP = strategy.opentrades.entry_price(tradeNo)
    exitP = close
    profitPct += (exitP - entryP) / entryP * strategy.opentrades.size(tradeNo) * 100
    
// Calculate average profit percent for all open trades.
avgProfitPct = nz(profitPct / strategy.opentrades)
plot(avgProfitPct)
SEE ALSO
strategy.closedtrades.sizestrategy.position_sizestrategy.opentradesstrategy.closedtrades
strategy.order()
Creates a new order to open, add to, or exit from a position. If an unfilled order with the same id exists, a call to this command modifies that order.
The resulting order's type depends on the limit and stop parameters. If the call does not contain limit or stop arguments, it creates a market order that executes on the next tick. If the call specifies a limit value but no stop value, it places a limit order that executes after the market price reaches the limit value or a better price (lower for buy orders and higher for sell orders). If the call specifies a stop value but no limit value, it places a stop order that executes after the market price reaches the stop value or a worse price (higher for buy orders and lower for sell orders). If the call contains limit and stop arguments, it creates a stop-limit order, which generates a limit order at the limit price only after the market price reaches the stop value or a worse price.
Pinescript_v6_Functions11.md
table.cleartable.deletetable.newtable.set_frame_colortable.set_frame_widthtable.set_bgcolortable.set_border_colortable.set_position
table.set_frame_color()
The function sets the color of the outer frame of a table.
SYNTAX
table.set_frame_color(table_id, frame_color) → void
ARGUMENTS
table_id (series table) A table object.
frame_color (series color) The color of the frame of the table. Optional. The default is no color.
SEE ALSO
table.cleartable.deletetable.newtable.set_border_colortable.set_border_widthtable.set_bgcolortable.set_frame_widthtable.set_position
table.set_frame_width()
The function set the width of the outer frame of a table.
SYNTAX
table.set_frame_width(table_id, frame_width) → void
ARGUMENTS
table_id (series table) A table object.
frame_width (series int) The width of the outer frame of the table. Optional. The default is 0.
SEE ALSO
table.cleartable.deletetable.newtable.set_frame_colortable.set_border_widthtable.set_bgcolortable.set_border_colortable.set_position
table.set_position()
The function sets the position of a table.
SYNTAX
table.set_position(table_id, position) → void
ARGUMENTS
table_id (series table) A table object.
position (series string) Position of the table. Possible values are: position.top_left, position.top_center, position.top_right, position.middle_left, position.middle_center, position.middle_right, position.bottom_left, position.bottom_center, position.bottom_right.
SEE ALSO
table.cleartable.deletetable.newtable.set_bgcolortable.set_border_colortable.set_border_widthtable.set_frame_colortable.set_frame_width
ticker.heikinashi()2 overloads
Creates a ticker identifier for requesting Heikin Ashi bar values.
SYNTAX & OVERLOADS
ticker.heikinashi(symbol) → simple string
ticker.heikinashi(symbol) → series string
ARGUMENTS
symbol (simple string) Symbol ticker identifier.
EXAMPLE
//@version=6
indicator("ticker.heikinashi", overlay=true) 
heikinashi_close = request.security(ticker.heikinashi(syminfo.tickerid), timeframe.period, close)

heikinashi_aapl_60_close = request.security(ticker.heikinashi("AAPL"), "60", close)
plot(heikinashi_close)
plot(heikinashi_aapl_60_close)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickerrequest.securityticker.renkoticker.linebreakticker.kagiticker.pointfigure
ticker.inherit()2 overloads
Constructs a ticker ID for the specified symbol with additional parameters inherited from the ticker ID passed into the function call, allowing the script to request a symbol's data using the same modifiers that the from_tickerid has, including extended session, dividend adjustment, currency conversion, non-standard chart types, back-adjustment, settlement-as-close, etc.
SYNTAX & OVERLOADS
ticker.inherit(from_tickerid, symbol) → simple string
ticker.inherit(from_tickerid, symbol) → series string
ARGUMENTS
from_tickerid (simple string) The ticker ID to inherit modifiers from.
symbol (simple string) The symbol to construct the new ticker ID for.
EXAMPLE
//@version=6
indicator("ticker.inherit")

//@variable A "NASDAQ:AAPL" ticker ID with Extender Hours enabled.
tickerExtHours = ticker.new("NASDAQ", "AAPL", session.extended)
//@variable A Heikin Ashi ticker ID for "NASDAQ:AAPL" with Extended Hours enabled.
HAtickerExtHours = ticker.heikinashi(tickerExtHours)
//@variable The "NASDAQ:MSFT" symbol with no modifiers.
testSymbol = "NASDAQ:MSFT"
//@variable A ticker ID for "NASDAQ:MSFT" with inherited Heikin Ashi and Extended Hours modifiers.
testSymbolHAtickerExtHours = ticker.inherit(HAtickerExtHours, testSymbol)

//@variable The `close` price requested using "NASDAQ:MSFT" with inherited modifiers. 
secData = request.security(testSymbolHAtickerExtHours, "60", close, ignore_invalid_symbol = true)
//@variable The `close` price requested using "NASDAQ:MSFT" without modifiers. 
compareData = request.security(testSymbol, "60", close, ignore_invalid_symbol = true)

plot(secData, color = color.green)
plot(compareData)
REMARKS
If the constructed ticker ID inherits a modifier that doesn't apply to the symbol (e.g., if the from_tickerid has Extended Hours enabled, but no such option is available for the symbol), the script will ignore the modifier when requesting data using the ID.
ticker.kagi()2 overloads
Creates a ticker identifier for requesting Kagi values.
SYNTAX & OVERLOADS
ticker.kagi(symbol, reversal) → simple string
ticker.kagi(symbol, reversal) → series string
ARGUMENTS
symbol (simple string) Symbol ticker identifier.
reversal (simple int/float) Reversal amount (absolute price value).
EXAMPLE
//@version=6
indicator("ticker.kagi", overlay=true) 
kagi_tickerid = ticker.kagi(syminfo.tickerid, 3)
kagi_close = request.security(kagi_tickerid, timeframe.period, close)
plot(kagi_close)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickerrequest.securityticker.heikinashiticker.renkoticker.linebreakticker.pointfigure
ticker.linebreak()2 overloads
Creates a ticker identifier for requesting Line Break values.
SYNTAX & OVERLOADS
ticker.linebreak(symbol, number_of_lines) → simple string
ticker.linebreak(symbol, number_of_lines) → series string
ARGUMENTS
symbol (simple string) Symbol ticker identifier.
number_of_lines (simple int) Number of line.
EXAMPLE
//@version=6
indicator("ticker.linebreak", overlay=true) 
linebreak_tickerid = ticker.linebreak(syminfo.tickerid, 3)
linebreak_close = request.security(linebreak_tickerid, timeframe.period, close)
plot(linebreak_close)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickerrequest.securityticker.heikinashiticker.renkoticker.kagiticker.pointfigure
ticker.modify()2 overloads
Creates a ticker identifier for requesting additional data for the script.
SYNTAX & OVERLOADS
ticker.modify(tickerid, session, adjustment) → series string
ticker.modify(tickerid, session, adjustment, backadjustment, settlement_as_close) → simple string
ARGUMENTS
tickerid (series string) Symbol name with exchange prefix, e.g. 'BATS:MSFT', 'NASDAQ:MSFT' or tickerid with session and adjustment from the ticker.new function.
session (series string) Session type. Optional argument. Possible values: session.regular, session.extended. Session type of the current chart is syminfo.session. If session is not given, then syminfo.session value is used.
adjustment (series string) Adjustment type. Optional argument. Possible values: adjustment.none, adjustment.splits, adjustment.dividends. If adjustment is not given, then default adjustment value is used (can be different depending on particular instrument).
EXAMPLE
//@version=6
indicator("ticker_modify", overlay=true)
t1 = ticker.new(syminfo.prefix, syminfo.ticker, session.regular, adjustment.splits)
c1 = request.security(t1, "D", close)
t2 = ticker.modify(t1, session.extended)
c2 = request.security(t2, "2D", close)
plot(c1)
plot(c2)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickersyminfo.sessionsession.extendedsession.regularticker.heikinashiadjustment.noneadjustment.splitsadjustment.dividendsbackadjustment.inheritbackadjustment.onbackadjustment.offsettlement_as_close.inheritsettlement_as_close.onsettlement_as_close.off
ticker.new()2 overloads
Creates a ticker identifier for requesting additional data for the script.
SYNTAX & OVERLOADS
ticker.new(prefix, ticker, session, adjustment) → series string
ticker.new(prefix, ticker, session, adjustment, backadjustment, settlement_as_close) → simple string
ARGUMENTS
prefix (series string) Exchange prefix. For example: 'BATS', 'NYSE', 'NASDAQ'. Exchange prefix of main series is syminfo.prefix.
ticker (series string) Ticker name. For example 'AAPL', 'MSFT', 'EURUSD'. Ticker name of the main series is syminfo.ticker.
session (series string) Session type. Optional argument. Possible values: session.regular, session.extended. Session type of the current chart is syminfo.session. If session is not given, then syminfo.session value is used.
adjustment (series string) Adjustment type. Optional argument. Possible values: adjustment.none, adjustment.splits, adjustment.dividends. If adjustment is not given, then default adjustment value is used (can be different depending on particular instrument).
EXAMPLE
//@version=6
indicator("ticker.new", overlay=true) 
t = ticker.new(syminfo.prefix, syminfo.ticker, session.regular, adjustment.splits)
t2 = ticker.heikinashi(t)
c = request.security(t2, timeframe.period, low, barmerge.gaps_on)
plot(c, style=plot.style_linebr)
RETURNS
String value of ticker id, that can be supplied to request.security function.
REMARKS
You may use return value of ticker.new function as input argument for ticker.heikinashi, ticker.renko, ticker.linebreak, ticker.kagi, ticker.pointfigure functions.
SEE ALSO
syminfo.tickeridsyminfo.tickersyminfo.sessionsession.extendedsession.regularticker.heikinashiadjustment.noneadjustment.splitsadjustment.dividendsbackadjustment.inheritbackadjustment.onbackadjustment.offsettlement_as_close.inheritsettlement_as_close.onsettlement_as_close.off
ticker.pointfigure()2 overloads
Creates a ticker identifier for requesting Point & Figure values.
SYNTAX & OVERLOADS
ticker.pointfigure(symbol, source, style, param, reversal) → simple string
ticker.pointfigure(symbol, source, style, param, reversal) → series string
ARGUMENTS
symbol (simple string) Symbol ticker identifier.
source (simple string) The source for calculating Point & Figure. Possible values are: 'hl', 'close'.
style (simple string) Box Size Assignment Method: 'ATR', 'Traditional'.
param (simple int/float) ATR Length if style is equal to 'ATR', or Box Size if style is equal to 'Traditional'.
reversal (simple int) Reversal amount.
EXAMPLE
//@version=6
indicator("ticker.pointfigure", overlay=true) 
pnf_tickerid = ticker.pointfigure(syminfo.tickerid, "hl", "Traditional", 1, 3)
pnf_close = request.security(pnf_tickerid, timeframe.period, close)
plot(pnf_close)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickerrequest.securityticker.heikinashiticker.renkoticker.linebreakticker.kagi
ticker.renko()2 overloads
Creates a ticker identifier for requesting Renko values.
SYNTAX & OVERLOADS
ticker.renko(symbol, style, param, request_wicks, source) → simple string
ticker.renko(symbol, style, param, request_wicks, source) → series string
ARGUMENTS
symbol (simple string) Symbol ticker identifier.
style (simple string) Box Size Assignment Method: 'ATR', 'Traditional'.
param (simple int/float) ATR Length if style is equal to 'ATR', or Box Size if style is equal to 'Traditional'.
request_wicks (simple bool) Specifies if wick values are returned for Renko bricks. When true, high and low values requested from a symbol using the ticker formed by this function will include wick values when they are present. When false, high and low will always be equal to either open or close. Optional. The default is false. A detailed explanation of how Renko wicks are calculated can be found in our Help Center.
source (simple string) The source used to calculate bricks. Optional. Possible values: "Close", "OHLC". The default is "Close".
EXAMPLE
//@version=6
indicator("ticker.renko", overlay=true) 
renko_tickerid = ticker.renko(syminfo.tickerid, "ATR", 10)
renko_close = request.security(renko_tickerid, timeframe.period, close)
plot(renko_close)
EXAMPLE
//@version=6
indicator("Renko candles", overlay=false)
renko_tickerid = ticker.renko(syminfo.tickerid, "ATR", 10)
[renko_open, renko_high, renko_low, renko_close] = request.security(renko_tickerid, timeframe.period, [open, high, low, close])
plotcandle(renko_open, renko_high, renko_low, renko_close, color = renko_close > renko_open ? color.green : color.red)
RETURNS
String value of ticker id, that can be supplied to request.security function.
SEE ALSO
syminfo.tickeridsyminfo.tickerrequest.securityticker.heikinashiticker.linebreakticker.kagiticker.pointfigure
ticker.standard()2 overloads
Creates a ticker to request data from a standard chart that is unaffected by modifiers like extended session, dividend adjustment, currency conversion, and the calculations of non-standard chart types: Heikin Ashi, Renko, etc. Among other things, this makes it possible to retrieve standard chart values when the script is running on a non-standard chart.
SYNTAX & OVERLOADS
ticker.standard(symbol) → simple string
ticker.standard(symbol) → series string
ARGUMENTS
symbol (simple string) A ticker ID to be converted into its standard form. Optional. The default is syminfo.tickerid.
EXAMPLE
//@version=6
indicator("ticker.standard", overlay = true)
// This script should be run on a non-standard chart such as HA, Renko...

// Requests data from the chart type the script is running on.
chartTypeValue = request.security(syminfo.tickerid, "1D", close)

// Request data from the standard chart type, regardless of the chart type the script is running on.
standardChartValue = request.security(ticker.standard(syminfo.tickerid), "1D", close)

// This will not use a standard ticker ID because the `symbol` argument contains only the ticker — not the prefix (exchange).
standardChartValue2 = request.security(ticker.standard(syminfo.ticker), "1D", close)

plot(chartTypeValue)
plot(standardChartValue, color = color.green)
RETURNS
A string representing the ticker of a standard chart in the "prefix:ticker" format. If the symbol argument does not contain the prefix and ticker information, the function returns the supplied argument as is.
SEE ALSO
request.security
time()3 overloads
The time function returns the UNIX time of the current bar for the specified timeframe and session or NaN if the time point is out of session.
SYNTAX & OVERLOADS
time(timeframe, bars_back) → series int
time(timeframe, session, bars_back) → series int
time(timeframe, session, timezone, bars_back) → series int
ARGUMENTS
timeframe (series string) Timeframe. An empty string is interpreted as the current timeframe of the chart.
bars_back (series int) Optional. The bar offset on the script's main timeframe. If the value is positive, the function retrieves the timestamp of the bar N bars back relative to the current bar on the main timeframe. If the value is a negative number from -1 to -500, the function retrieves the expected time of a future bar on that timeframe. The default is 0.
EXAMPLE
//@version=6
indicator("Time", overlay=true)
// Try this on chart AAPL,1
timeinrange(res, sess) => not na(time(res, sess, "America/New_York")) ? 1 : 0
plot(timeinrange("1", "1300-1400"), color=color.red)

// This plots 1.0 at every start of 10 minute bar on a 1 minute chart:
newbar(res) => ta.change(time(res)) == 0 ? 0 : 1
plot(newbar("10"))
While setting up a session you can specify not just the hours and minutes but also the days of the week that will be included in that session.
If the days aren't specified, the session is considered to have been set from Sunday (1) to Saturday (7), i.e. "1100-2000" is the same as "1100-1200:1234567".
You can change that by specifying the days. For example, on a symbol that is traded seven days a week with the 24-hour trading session the following script will not color Saturdays and Sundays:
EXAMPLE
//@version=6
indicator("Time", overlay=true)
t1 = time(timeframe.period, "0000-0000:23456")
bgcolor(not na(t1) ? color.new(color.blue, 90) : na)
One session argument can include several different sessions, separated by commas. For example, the following script will highlight the bars from 10:00 to 11:00 and from 14:00 to 15:00 (workdays only):
EXAMPLE
//@version=6
indicator("Time", overlay=true)
t1 = time(timeframe.period, "1000-1100,1400-1500:23456")
bgcolor(not na(t1) ? color.new(color.blue, 90) : na)
RETURNS
UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
time
time_close()3 overloads
Returns the UNIX time of the current bar's close for the specified timeframe and session, or na if the time point is outside the session. On non-standard price-based chart types (Renko, Line break, Kagi, Point & Figure, and Range), this function returns na on the chart's realtime bars.
SYNTAX & OVERLOADS
time_close(timeframe, bars_back) → series int
time_close(timeframe, session, bars_back) → series int
time_close(timeframe, session, timezone, bars_back) → series int
ARGUMENTS
timeframe (series string) Resolution. An empty string is interpreted as the current resolution of the chart.
bars_back (series int) Optional. The bar offset on the script's main timeframe. If the value is positive, the function retrieves the timestamp of the bar N bars back relative to the current bar on the main timeframe. If the value is a negative number from -1 to -500, the function retrieves the expected time of a future bar on that timeframe. The default is 0.
EXAMPLE
//@version=6
indicator("Time", overlay=true)
t1 = time_close(timeframe.period, "1200-1300", "America/New_York")
bgcolor(not na(t1) ? color.new(color.blue, 90) : na)
RETURNS
UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
time_close
timeframe.change()
Detects changes in the specified timeframe.
SYNTAX
timeframe.change(timeframe) → series bool
ARGUMENTS
timeframe (series string) String formatted according to the User manual's timeframe string specifications.
EXAMPLE
//@version=6
// Run this script on an intraday chart.
indicator("New day started", overlay = true)
// Highlights the first bar of the new day.
isNewDay = timeframe.change("1D")
bgcolor(isNewDay ? color.new(color.green, 80) : na)
RETURNS
Returns true on the first bar of a new timeframe, false otherwise.
timeframe.from_seconds()2 overloads
Converts a number of seconds into a valid timeframe string.
SYNTAX & OVERLOADS
timeframe.from_seconds(seconds) → simple string
timeframe.from_seconds(seconds) → series string
ARGUMENTS
seconds (simple int) The number of seconds in the timeframe.
EXAMPLE
//@version=6
indicator("HTF Close", "", true)
int chartTf = timeframe.in_seconds()
string tfTimes5 = timeframe.from_seconds(chartTf * 5)
float htfClose = request.security(syminfo.tickerid, tfTimes5, close)
plot(htfClose)
RETURNS
A timeframe string compliant with timeframe string specifications.
REMARKS
If no valid timeframe exists for the quantity of seconds supplied, the next higher valid timeframe will be returned. Accordingly, one second or less will return "1S", 2-5 seconds will return "5S", and 604,799 seconds (one second less than 7 days) will return "7D".
If the seconds exactly represent two or more valid timeframes, the one with the larger base unit will be used. Thus 604,800 seconds (7 days) returns "1W", not "7D".
All values above 31,622,400 (366 days) return "12M".
SEE ALSO
timeframe.in_secondsrequest.securityrequest.security_lower_tf
timeframe.in_seconds()2 overloads
Converts a timeframe string into seconds.
SYNTAX & OVERLOADS
timeframe.in_seconds(timeframe) → simple int
timeframe.in_seconds(timeframe) → series int
ARGUMENTS
timeframe (simple string) Timeframe string in timeframe string specifications format. Optional. The default is timeframe.period.
EXAMPLE
//@version=6
indicator("`timeframe_in_seconds()`")

// Get a user-selected timeframe.
tfInput = input.timeframe("1D")

// Convert it into an "int" number of seconds.
secondsInTf = timeframe.in_seconds(tfInput)

plot(secondsInTf)
RETURNS
The "int" representation of the number of seconds in the timeframe string.
REMARKS
When the timeframe is "1M" or more, calculations use 2628003 as the number of seconds in one month, which represents 30.4167 (365/12) days.
SEE ALSO
input.timeframetimeframe.periodtimeframe.from_seconds
timestamp()5 overloads
Function timestamp returns UNIX time of specified date and time.
SYNTAX & OVERLOADS
timestamp(dateString) → const int
timestamp(year, month, day, hour, minute, second) → simple int
timestamp(year, month, day, hour, minute, second) → series int
timestamp(timezone, year, month, day, hour, minute, second) → simple int
timestamp(timezone, year, month, day, hour, minute, second) → series int
ARGUMENTS
dateString (const string) A string containing the date and, optionally, the time and time zone. Its format must comply with either the IETF RFC 2822 or ISO 8601 standards ("DD MMM YYYY hh:mm:ss ±hhmm" or "YYYY-MM-DDThh:mm:ss±hh:mm", so "20 Feb 2020" or "2020-02-20"). If no time is supplied, "00:00" is used. If no time zone is supplied, GMT+0 will be used. Note that this diverges from the usual behavior of the function where it returns time in the exchange's timezone.
EXAMPLE
//@version=6
indicator("timestamp")
plot(timestamp(2016, 01, 19, 09, 30), linewidth=3, color=color.green)
plot(timestamp(syminfo.timezone, 2016, 01, 19, 09, 30), color=color.blue)
plot(timestamp(2016, 01, 19, 09, 30), color=color.yellow)
plot(timestamp("GMT+6", 2016, 01, 19, 09, 30))
plot(timestamp(2019, 06, 19, 09, 30, 15), color=color.lime)
plot(timestamp("GMT+3", 2019, 06, 19, 09, 30, 15), color=color.fuchsia)
plot(timestamp("Feb 01 2020 22:10:05"))
plot(timestamp("2011-10-10T14:48:00"))
plot(timestamp("04 Dec 1995 00:12:00 GMT+5"))
RETURNS
UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
time
weekofyear()2 overloads
SYNTAX & OVERLOADS
weekofyear(time) → series int
weekofyear(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Week of year (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
Note that this function returns the week based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the week of the trading day.
SEE ALSO
weekofyeartimeyearmonthdayofmonthdayofweekhourminutesecond
year()2 overloads
SYNTAX & OVERLOADS
year(time) → series int
year(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Year (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
Note that this function returns the year based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00 UTC-4) this value can be lower by 1 than the year of the trading day.
SEE ALSO
yeartimemonthdayofmonthdayofweekhourminutesecond
Keywords
and
Logical AND. Applicable to boolean expressions.
SYNTAX
expr1 and expr2
RETURNS
Boolean value, or series of boolean values.
REMARKS
If expr1 evaluates to false, the and operator returns false without evaluating expr2.
enum
This keyword allows the creation of an enumeration, enum for short. Enums are unique constructs that hold groups of predefined constants.
Each field in an enum has a const string title. Scripts can access the fields in an enum using dot notation, similar to accessing the fields of a user-defined type.
Each field represents a value of the enumName enum. Scripts can declare each field in an enum with an optional const string title. If a field's title is not specified, its title is the string representation of its name. Use str.tostring on an enum field to retrieve its title.
SYNTAX
[export ]enum <enumName> 
<field_1> [= <title_1>] 
<field_2> [= <title_2>] 
... 
<field_N> [= <title_N>]
One can use an enum to quickly create a dropdown input with the help of the input.enum function. The options that appear in the dropdown represent the titles of the enum fields.
EXAMPLE
//@version=6
indicator("Session highlight", overlay = true)

//@enum       Contains fields with popular timezones as titles.
//@field exch Has an empty string as the title to represent the chart timezone.
enum tz
    utc  = "UTC"
    exch = ""
    ny   = "America/New_York"
    chi  = "America/Chicago"
    lon  = "Europe/London"
    tok  = "Asia/Tokyo"

//@variable The session string.
selectedSession = input.session("1200-1500", "Session")
//@variable The selected timezone. The input's dropdown contains the fields in the `tz` enum.
selectedTimezone = input.enum(tz.utc, "Session Timezone")

//@variable Is `true` if the current bar's time is in the specified session.
bool inSession = false
if not na(time("", selectedSession, str.tostring(selectedTimezone)))
    inSession := true

// Highlight the background when `inSession` is `true`.
bgcolor(inSession ? color.new(color.green, 90) : na, title = "Active session highlight")
Additionally, one can use an enum in a collection's type template to restrict the values it will allow as elements. When used inside a type template, the collection will only accept fields that belong to the specified enum.
EXAMPLE
//@version=6
indicator("Map with enum keys")

//@enum        Contains fields with titles representing ticker IDs.
//@field aapl  Has an Apple ticker ID as its title.
//@field tsla  Has a Tesla ticker ID as its title.
//@field amzn  Has an Amazon ticker ID as its title.
enum symbols
    aapl = "NASDAQ:AAPL"
    tsla = "NASDAQ:TSLA"
    amzn = "NASDAQ:AMZN"

//@variable A map that accepts fields from the `symbols` enum as keys and "float" values.
map<symbols, float> data = map.new<symbols, float>()
// Put key-value pairs into the `data` map.
data.put(symbols.aapl, request.security(str.tostring(symbols.aapl), timeframe.period, close))
data.put(symbols.tsla, request.security(str.tostring(symbols.tsla), timeframe.period, close))
data.put(symbols.amzn, request.security(str.tostring(symbols.amzn), timeframe.period, close))
// Plot the value from the `data` map accessed by the `symbols.aapl` key.
plot(data.get(symbols.aapl))
export
Used in libraries to prefix the declaration of functions or user-defined type definitions that will be available from other scripts importing the library.
EXAMPLE
//@version=6
//@description Library of debugging functions.
library("Debugging_library", overlay = true)
//@function Displays a string as a table cell for debugging purposes.
//@param txt String to display.
//@returns Void.
export print(string txt) => 
    var table t = table.new(position.middle_right, 1, 1)
    table.cell(t, 0, 0, txt, bgcolor = color.yellow)
// Using the function from inside the library to show an example on the published chart.
// This has no impact on scripts using the library.
print("Library Test")
REMARKS
Each library must have at least one exported function or user-defined type (UDT).
Exported functions cannot use variables from the global scope if they are arrays, mutable variables (reassigned with :=), or variables of 'input' form.
Exported functions cannot use request.*() functions.
Exported functions must explicitly declare each parameter's type and all parameters must be used in the function's body. By default, all arguments passed to exported functions are of the series form, unless they are explicitly specified as simple in the function's signature.
The @description, @function, @param, @type, @field, and @returns compiler annotations are used to automatically generate the library's description and release notes, and in the Pine Script® Editor's tooltips.
SEE ALSO
libraryimportsimpleseriestype
for
The 'for' structure allows the repeated execution of a number of statements:
SYNTAX
[var_declaration =] for counter = from_num to to_num [by step_num]
    statements | continue | break
    return_expression
var_declaration - An optional variable declaration that will be assigned the value of the loop's return_expression.
counter - A variable holding the value of the loop's counter, which is incremented/decremented by 1 or by the step_num value on each iteration of the loop.
from_num - The starting value of the counter. "series int/float" values/expressions are allowed.
to_num - The end value of the counter. When the counter becomes greater than to_num (or less than to_num in cases where from_num > to_num) the loop is broken. "series int/float" values/expressions are allowed, but they are evaluated only on the loop's first iteration.
step_num - The increment/decrement value of the counter. It is optional. The default value is +1 or -1, depending on which of from_num or to_num is the greatest. When a value is used, the counter is also incremented/decremented depending on which of from_num or to_num is the greatest, so the +/- sign of step_num is optional.
statements | continue | break - Any number of statements, or the 'continue' or 'break' keywords, indented by 4 spaces or a tab.
return_expression - The loop's return value which is assigned to the variable in var_declaration if one is present. If the loop exits because of a 'continue' or 'break' keyword, the loop's return value is that of the last variable assigned a value before the loop's exit.
continue - A keyword that can only be used in loops. It causes the next iteration of the loop to be executed.
break - A keyword that exits the loop.
EXAMPLE
//@version=6
indicator("for")
// Here, we count the quantity of bars in a given 'lookback' length which closed above the current bar's close
qtyOfHigherCloses(lookback) =>
    int result = 0
    for i = 1 to lookback
        if close[i] > close
            result += 1
    result
plot(qtyOfHigherCloses(14))
EXAMPLE
//@version=6
indicator("`for` loop with a step")

a = array.from(0, 1, 2, 3, 4, 5, 6, 7, 8, 9)
sum = 0.0

for i = 0 to 9 by 5
    // Because the step is set to 5, we are adding only the first (0) and the sixth (5) value from the array `a`.
    sum += array.get(a, i)

plot(sum)
SEE ALSO
for...inwhile
for...in
The for...in structure allows the repeated execution of a number of statements for each element in an array. It can be used with either one argument: array_element, or with two: [index, array_element]. The second form doesn't affect the functionality of the loop. It tracks the current iteration's index in the tuple's first variable.
SYNTAX
[var_declaration =] for array_element in array_id
    statements | continue | break
    return_expression

[var_declaration =] for [index, array_element] in array_id
    statements | continue | break
    return_expression
var_declaration - An optional variable declaration that will be assigned the value of the loop's return_expression.
index - An optional variable that tracks the current iteration's index. Indexing starts at 0. The variable is immutable in the loop's body. When used, it must be included in a tuple also containing array_element.
array_element - A variable containing each successive array element to be processed in the loop. The variable is immutable in the loop's body.
array_id - The ID of the array over which the loop is iterated.
statements | continue | break - Any number of statements, or the 'continue' or 'break' keywords, indented by 4 spaces or a tab.
return_expression - The loop's return value assigned to the variable in var_declaration, if one is present. If the loop exits because of a 'continue' or 'break' keyword, the loop's return value is that of the last variable assigned a value before the loop's exit.
continue - A keyword that can only be used in loops. It causes the next iteration of the loop to be executed.
break - A keyword that exits the loop.
Scripts can modify arrays and matrices while iterating over their elements with this structure. However, maps cannot change while looping through their key-value pairs. To modify a map within a for...in loop, iterate over the key-value pairs of a copy or over the elements in its map.keys array.
Here, we use the single-argument form of for...in to determine on each bar how many of the bar's OHLC values are greater than the SMA of 'close' values:
EXAMPLE
//@version=6
indicator("for...in")
// Here we determine on each bar how many of the bar's OHLC values are greater than the SMA of 'close' values
float[] ohlcValues = array.from(open, high, low, close)
qtyGreaterThan(value, array) =>
    int result = 0
    for currentElement in array
        if currentElement > value
            result += 1
        result
plot(qtyGreaterThan(ta.sma(close, 20), ohlcValues))
Here, we use the two-argument form of for...in to set the values of our isPos array to true when their corresponding value in our valuesArray array is positive:
EXAMPLE
//@version=6
indicator("for...in")
var valuesArray = array.from(4, -8, 11, 78, -16, 34, 7, 99, 0, 55)
var isPos = array.new_bool(10, false)

for [index, value] in valuesArray
    if value > 0
        array.set(isPos, index, true)

if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(isPos))
Iterate through matrix rows as arrays.
EXAMPLE
//@version=6
indicator("`for ... in` matrix Example")

// Create a 2x3 matrix with values `4`.
matrix1 = matrix.new<int>(2, 3, 4)

sum = 0.0
// Loop through every row of the matrix.
for rowArray in matrix1
    // Sum values of the every row 
    sum += array.sum(rowArray)

plot(sum)
SEE ALSO
forwhilearray.sumarray.minarray.max
if
If statement defines what block of statements must be executed when conditions of the expression are satisfied.
To have access to and use the if statement, one should specify the version >= 2 of Pine Script® language in the very first line of code, for example: //@version=6
The 4th version of Pine Script® Language allows you to use “else if” syntax.
General code form:
SYNTAX
var_declarationX = if condition
    var_decl_then0
    var_decl_then1
    …
    var_decl_thenN
else if [optional block]
    var_decl_else0
    var_decl_else1
    …
    var_decl_elseN
else
    var_decl_else0
    var_decl_else1
    …
    var_decl_elseN
    return_expression_else
where
var_declarationX — this variable gets the value of the if statement
condition — if the condition is true, the logic from the block 'then' (var_decl_then0, var_decl_then1, etc.) is used.
If the condition is false, the logic from the block 'else' (var_decl_else0, var_decl_else1, etc.) is used.
return_expression_then, return_expression_else — the last expression from the block then or from the block else will return the final value of the statement. If declaration of the variable is in the end, its value will be the result.
The type of returning value of the if statement depends on return_expression_then and return_expression_else type (their types must match: it is not possible to return an integer value from then, while you have a string value in else block).
EXAMPLE
//@version=6
indicator("if")
// This code compiles
x = if close > open
    close
else
    open

// This code doesn’t compile
// y = if close > open
//     close
// else
//     "open"
plot(x)
It is possible to omit the else block. In this case if the condition is false, an “empty” value (na, false, or “”) will be assigned to the var_declarationX variable:
EXAMPLE
//@version=6
indicator("if")
x = if close > open
    close
// If current close > current open, then x = close.
// Otherwise the x = na.
plot(x)
It is possible to use either multiple “else if” blocks or none at all. The blocks “then”, “else if”, “else” are shifted by four spaces:
EXAMPLE
//@version=6
indicator("if")
x = if open > close
    5
else if high > low
    close
else
    open
plot(x)
It is possible to ignore the resulting value of an if statement (“var_declarationX=“ can be omitted). It may be useful if you need the side effect of the expression, for example in strategy trading:
EXAMPLE
//@version=6
strategy("if")
if (ta.crossover(high, low))
    strategy.entry("BBandLE", strategy.long, stop=low, oca_name="BollingerBands", oca_type=strategy.oca.cancel, comment="BBandLE")
else
    strategy.cancel(id="BBandLE")
If statements can include each other:
EXAMPLE
//@version=6
indicator("if")
float x = na
if close > open
    if close > close[1]
        x := close
    else
        x := close[1]
else
    x := open
plot(x)
import
Used to load an external library into a script and bind its functions to a namespace. The importing script can be an indicator, a strategy, or another library. A library must be published (privately or publicly) before it can be imported.
SYNTAX
import {username}/{libraryName}/{libraryVersion} as {alias}
ARGUMENTS
username (literal string) User name of the library's author.
libraryName (literal string) Name of the imported library, which corresponds to the title argument used by the author in his library script.
libraryVersion (literal int) Version number of the imported library.
alias (literal string) A non-numeric identifier used as a namespace to refer to the library's functions. Optional. The default is the libraryName string.
EXAMPLE
//@version=6
indicator("num_methods import")
// Import the first version of the username’s "num_methods" library and assign it to the "m" namespace",
import username/num_methods/1 as m
// Call the “sinh()” function from the imported library
y = m.sinh(3.14)
// Plot value returned by the "sinh()" function",
plot(y)
REMARKS
Using an alias that replaces a built-in namespace such as math.* or strategy.* is allowed, but if the library contains function names that shadow Pine Script®'s built-in functions, the built-ins will become unavailable. The same version of a library can only be imported once. Aliases must be distinct for each imported library. When calling library functions, casting their arguments to types other than their declared type is not allowed. An import statement cannot use 'as' or 'import' as username, libraryName, or alias identifiers.
SEE ALSO
libraryexport
method
This keyword is used to prefix a function declaration, indicating it can then be invoked using dot notation by appending its name to a variable of the type of its first parameter and omitting that first parameter. Alternatively, functions declared as methods can also be invoked like normal user-defined functions. In that case, an argument must be supplied for its first parameter.
The first parameter of a method declaration must be explicitly typified.
SYNTAX
[export] method <functionName>(<paramType> <paramName> [= <defaultValue>], …) =>
    <functionBlock>
EXAMPLE
//@version=6
indicator("")

var prices = array.new<float>()

//@function Pushes a new value into the array and removes the first one if the resulting array is greater than `maxSize`. Can be used as a method.
method maintainArray(array<float> id, maxSize, value) =>
    id.push(value)
    if id.size() > maxSize
        id.shift()

prices.maintainArray(50, close)
// The method can also be called like a function, without using dot notation.
// In this case an argument must be supplied for its first parameter.
// maintainArray(prices, 50, close)

// This calls the `array.avg()` built-in using dot notation with the `prices` array.
// It is possible because built-in functions belonging to some namespaces that are a special Pine type
// can be invoked with method notation when the function's first parameter is an ID of that type.
// Those namespaces are: `array`, `matrix`, `line`, `linefill`, `label`, `box`, and `table`.
plot(prices.avg())
not
Logical negation (NOT). Applicable to boolean expressions.
SYNTAX
not expr1
RETURNS
Boolean value, or series of boolean values.
or
Logical OR. Applicable to boolean expressions.
SYNTAX
expr1 or expr2
RETURNS
Boolean value, or series of boolean values.
REMARKS
If expr1 evaluates to true, the or operator returns true without evaluating expr2.
switch
The switch operator transfers control to one of the several statements, depending on the values of a condition and expressions.
SYNTAX
[variable_declaration = ] switch expression
    value1 => local_block
    value2 => local_block
    …
    => default_local_block

[variable_declaration = ] switch
    condition1 => local_block
    condition2 => local_block
    …
    => default_local_block
Switch with an expression:
EXAMPLE
//@version=6
indicator("Switch using an expression")

string i_maType = input.string("EMA", "MA type", options = ["EMA", "SMA", "RMA", "WMA"])

float ma = switch i_maType
    "EMA" => ta.ema(close, 10)
    "SMA" => ta.sma(close, 10)
    "RMA" => ta.rma(close, 10)
    // Default used when the three first cases do not match.
    => ta.wma(close, 10)

plot(ma)
Switch without an expression:
EXAMPLE
//@version=6
strategy("Switch without an expression", overlay = true)

bool longCondition  = ta.crossover( ta.sma(close, 14), ta.sma(close, 28))
bool shortCondition = ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))

switch
    longCondition  => strategy.entry("Long ID", strategy.long)
    shortCondition => strategy.entry("Short ID", strategy.short)
RETURNS
The value of the last expression in the local block of statements that is executed.
REMARKS
Only one of the local_block instances or the default_local_block can be executed. The default_local_block is introduced with the => token alone and is only executed when none of the preceding blocks are executed. If the result of the switch statement is assigned to a variable and a default_local_block is not specified, the statement returns na if no local_block is executed. When assigning the result of the switch statement to a variable, all local_block instances must return the same type of value.
SEE ALSO
if?:
type
This keyword allows the declaration of user-defined types (UDT) from which scripts can instantiate objects. UDTs are composite types that contain an arbitrary number of fields of any built-in or user-defined type, including the defined UDT itself. The syntax to define a UDT is:
SYNTAX
[export ]type <UDT_identifier>
    [varip ]<field_type> <field_name> [= <value>]
    …
Once a UDT is defined, scripts can instantiate objects from it with the UDT_identifier.new() construct. When creating a new type instance, the fields of the resulting object will initialize with the default values from the UDT's definition. Any type fields without specified defaults will initialize as na. Alternatively, users can pass initial values as arguments in the *.new() method to override the type's defaults. For example, newFooObject = foo.new(x = true) assigns a new foo object to the newFooObject variable with its x field initialized using a value of true.
Field declarations can include the varip keyword, in which case the field values persist between successive script iterations on the same bar.
For more information see the User Manual's sections on defining UDTs and using objects.
Libraries can export UDTs. See the Libraries page of our User Manual to learn more.
EXAMPLE
//@version=6
indicator("Multi Time Period Chart", overlay = true)

timeframeInput = input.timeframe("1D")

type bar
    float o = open
    float h = high
    float l = low
    float c = close
    int   t = time

drawBox(bar b, right) =>
    bar s = bar.new()
    color boxColor = b.c >= b.o ? color.green : color.red
    box.new(b.t, b.h, right, b.l, boxColor, xloc = xloc.bar_time, bgcolor = color.new(boxColor, 90))

updateBox(box boxId, bar b) =>
    color boxColor = b.c >= b.o ? color.green : color.red
    box.set_border_color(boxId, boxColor)
    box.set_bgcolor(boxId, color.new(boxColor, 90))
    box.set_top(boxId, b.h)
    box.set_bottom(boxId, b.l)
    box.set_right(boxId, time)

secBar = request.security(syminfo.tickerid, timeframeInput, bar.new())

if not na(secBar)
    // To avoid a runtime error, only process data when an object exists.
    if not barstate.islast
        if timeframe.change(timeframeInput)
            // On historical bars, draw a new box in the past when the HTF closes.
            drawBox(secBar, time[1])
    else
        var box lastBox = na
        if na(lastBox) or timeframe.change(timeframeInput)
            // On the last bar, only draw a new current box the first time we get there or when HTF changes.
            lastBox := drawBox(secBar, time)
        else
            // On other chart updates, use setters to modify the current box.
            updateBox(lastBox, secBar)
var
var is the keyword used for assigning and one-time initializing of the variable.
Normally, a syntax of assignment of variables, which doesn’t include the keyword var, results in the value of the variable being overwritten with every update of the data. Contrary to that, when assigning variables with the keyword var, they can “keep the state” despite the data updating, only changing it when conditions within if-expressions are met.
SYNTAX
var variable_name = expression
where:
variable_name - any name of the user’s variable that’s allowed in Pine Script® (can contain capital and lowercase Latin characters, numbers, and underscores (_), but can’t start with a number).
expression - any arithmetic expression, just as with defining a regular variable. The expression will be calculated and assigned to a variable once.
EXAMPLE
//@version=6
indicator("Var keyword example")
var a = close
var b = 0.0
var c = 0.0
var green_bars_count = 0
if close > open
