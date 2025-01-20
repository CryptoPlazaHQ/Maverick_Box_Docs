nafixnannz
nz()12 overloads
Replaces NaN values with zeros (or given value) in a series.
SYNTAX & OVERLOADS
nz(source) → simple color
nz(source) → simple int
nz(source) → series color
nz(source) → series int
nz(source) → simple float
nz(source) → series float
nz(source, replacement) → simple color
nz(source, replacement) → simple int
nz(source, replacement) → series color
nz(source, replacement) → series int
nz(source, replacement) → simple float
nz(source, replacement) → series float
ARGUMENTS
source (simple color) Series of values to process.
EXAMPLE
//@version=6
indicator("nz", overlay=true)
plot(nz(ta.sma(close, 100)))
RETURNS
The value of source if it is not na. If the value of source is na, returns zero, or the replacement argument when one is used.
SEE ALSO
nanafixnan
plot()
Plots a series of data on the chart.
SYNTAX
plot(series, title, color, linewidth, style, trackprice, histbase, offset, join, editable, show_last, display, format, precision, force_overlay) → plot
ARGUMENTS
series (series int/float) Series of data to be plotted. Required argument.
title (const string) Title of the plot.
color (series color) Color of the plot. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
linewidth (input int) Width of the plotted line. Default value is 1. Not applicable to every style.
style (input plot_style) Type of plot. Possible values are: plot.style_line, plot.style_stepline, plot.style_stepline_diamond, plot.style_histogram, plot.style_cross, plot.style_area, plot.style_columns, plot.style_circles, plot.style_linebr, plot.style_areabr, plot.style_steplinebr. Default value is plot.style_line.
trackprice (input bool) If true then a horizontal price line will be shown at the level of the last indicator value. Default is false.
histbase (input int/float) The price value used as the reference level when rendering plot with plot.style_histogram, plot.style_columns or plot.style_area style. Default is 0.0.
offset (simple int) Shifts the plot to the left or to the right on the given number of bars. Default is 0.
join (input bool) If true then plot points will be joined with line, applicable only to plot.style_cross and plot.style_circles styles. Default is false.
editable (input bool) If true then plot style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plot")
plot(high+low, title='Title', color=color.new(#00ffaa, 70), linewidth=2, style=plot.style_area, offset=15, trackprice=true)

// You may fill the background between any two plots with a fill() function:
p1 = plot(open)
p2 = plot(close)
fill(p1, p2, color=color.new(color.green, 90))
RETURNS
A plot object, that can be used in fill
SEE ALSO
plotshapeplotcharplotarrowbarcolorbgcolorfill
plotarrow()
Plots up and down arrows on the chart. Up arrow is drawn at every indicator positive value, down arrow is drawn at every negative value. If indicator returns na then no arrow is drawn. Arrows has different height, the more absolute indicator value the longer arrow is drawn.
SYNTAX
plotarrow(series, title, colorup, colordown, offset, minheight, maxheight, editable, show_last, display, format, precision, force_overlay) → void
ARGUMENTS
series (series int/float) Series of data to be plotted as arrows. Required argument.
title (const string) Title of the plot.
colorup (series color) Color of the up arrows. Optional argument.
colordown (series color) Color of the down arrows. Optional argument.
offset (simple int) Shifts arrows to the left or to the right on the given number of bars. Default is 0.
minheight (input int) Minimal possible arrow height in pixels. Default is 5.
maxheight (input int) Maximum possible arrow height in pixels. Default is 100.
editable (input bool) If true then plotarrow style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plotarrow example", overlay=true)
codiff = close - open
plotarrow(codiff, colorup=color.new(color.teal,40), colordown=color.new(color.orange, 40))
REMARKS
Use plotarrow function in conjunction with 'overlay=true' indicator parameter!
SEE ALSO
plotplotshapeplotcharbarcolorbgcolor
plotbar()
Plots ohlc bars on the chart.
SYNTAX
plotbar(open, high, low, close, title, color, editable, show_last, display, format, precision, force_overlay) → void
ARGUMENTS
open (series int/float) Open series of data to be used as open values of bars. Required argument.
high (series int/float) High series of data to be used as high values of bars. Required argument.
low (series int/float) Low series of data to be used as low values of bars. Required argument.
close (series int/float) Close series of data to be used as close values of bars. Required argument.
title (const string) Title of the plotbar. Optional argument.
color (series color) Color of the ohlc bars. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
editable (const bool) If true then plotbar style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plotbar example", overlay=true)
plotbar(open, high, low, close, title='Title', color = open < close ? color.green : color.red)
REMARKS
Even if one value of open, high, low or close equal NaN then bar no draw.
The maximal value of open, high, low or close will be set as 'high', and the minimal value will be set as 'low'.
SEE ALSO
plotcandle
plotcandle()
Plots candles on the chart.
SYNTAX
plotcandle(open, high, low, close, title, color, wickcolor, editable, show_last, bordercolor, display, format, precision, force_overlay) → void
ARGUMENTS
open (series int/float) Open series of data to be used as open values of candles. Required argument.
high (series int/float) High series of data to be used as high values of candles. Required argument.
low (series int/float) Low series of data to be used as low values of candles. Required argument.
close (series int/float) Close series of data to be used as close values of candles. Required argument.
title (const string) Title of the plotcandles. Optional argument.
color (series color) Color of the candles. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
wickcolor (series color) The color of the wick of candles. An optional argument.
editable (const bool) If true then plotcandle style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
bordercolor (series color) The border color of candles. An optional argument.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plotcandle example", overlay=true)
plotcandle(open, high, low, close, title='Title', color = open < close ? color.green : color.red, wickcolor=color.black)
REMARKS
Even if one value of open, high, low or close equal NaN then bar no draw.
The maximal value of open, high, low or close will be set as 'high', and the minimal value will be set as 'low'.
SEE ALSO
plotbar
plotchar()
Plots visual shapes using any given one Unicode character on the chart.
SYNTAX
plotchar(series, title, char, location, color, offset, text, textcolor, editable, size, show_last, display, format, precision, force_overlay) → void
ARGUMENTS
series (series int/float/bool) Series of data to be plotted as shapes. Series is treated as a series of boolean values for all location values except location.absolute. Required argument.
title (const string) Title of the plot.
char (input string) Character to use as a visual shape.
location (input string) Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.abovebar.
color (series color) Color of the shapes. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
offset (simple int) Shifts shapes to the left or to the right on the given number of bars. Default is 0.
text (const string) Text to display with the shape. You can use multiline text, to separate lines use '\n' escape sequence. Example: 'line one\nline two'.
textcolor (series color) Color of the text. You can use constants like 'textcolor=color.red' or 'textcolor=#ff001a' as well as complex expressions like 'textcolor = close >= open ? color.green : color.red'. Optional argument.
editable (const bool) If true then plotchar style will be editable in Format dialog. Default is true.
size (const string) Size of characters on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plotchar example", overlay=true)
data = close >= open
plotchar(data, char='❄')
REMARKS
Use plotchar function in conjunction with 'overlay=true' indicator parameter!
SEE ALSO
plotplotshapeplotarrowbarcolorbgcolor
plotshape()
Plots visual shapes on the chart.
SYNTAX
plotshape(series, title, style, location, color, offset, text, textcolor, editable, size, show_last, display, format, precision, force_overlay) → void
ARGUMENTS
series (series int/float/bool) Series of data to be plotted as shapes. Series is treated as a series of boolean values for all location values except location.absolute. Required argument.
title (const string) Title of the plot.
style (input string) Type of plot. Possible values are: shape.xcross, shape.cross, shape.triangleup, shape.triangledown, shape.flag, shape.circle, shape.arrowup, shape.arrowdown, shape.labelup, shape.labeldown, shape.square, shape.diamond. Default value is shape.xcross.
location (input string) Location of shapes on the chart. Possible values are: location.abovebar, location.belowbar, location.top, location.bottom, location.absolute. Default value is location.abovebar.
color (series color) Color of the shapes. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
offset (simple int) Shifts shapes to the left or to the right on the given number of bars. Default is 0.
text (const string) Text to display with the shape. You can use multiline text, to separate lines use '\n' escape sequence. Example: 'line one\nline two'.
textcolor (series color) Color of the text. You can use constants like 'textcolor=color.red' or 'textcolor=#ff001a' as well as complex expressions like 'textcolor = close >= open ? color.green : color.red'. Optional argument.
editable (const bool) If true then plotshape style will be editable in Format dialog. Default is true.
size (const string) Size of shapes on the chart. Possible values are: size.auto, size.tiny, size.small, size.normal, size.large, size.huge. Default is size.auto.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
display (input plot_display) Controls where the plot's information is displayed. Display options support addition and subtraction, meaning that using display.all - display.status_line will display the plot's information everywhere except in the script's status line. display.price_scale + display.status_line will display the plot only in the price scale and status line. When display arguments such as display.price_scale have user-controlled chart settings equivalents, the relevant plot information will only appear when all settings allow for it. Possible values: display.none, display.pane, display.data_window, display.price_scale, display.status_line, display.all. Optional. The default is display.all.
format (input string) Determines whether the script formats the plot's values as prices, percentages, or volume values. The argument passed to this parameter supersedes the format parameter of the indicator, and strategy functions. Optional. The default is the format value used by the indicator/strategy function. Possible values: format.price, format.percent, format.volume.
precision (input int) The number of digits after the decimal point the plot's values show on the chart pane's y-axis, the script's status line, and the Data Window. Accepts a non-negative integer less than or equal to 16. The argument passed to this parameter supersedes the precision parameter of the indicator and strategy functions. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is the precision value used by the indicator/strategy function.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("plotshape example 1", overlay=true)
data = close >= open
plotshape(data, style=shape.xcross)
REMARKS
Use plotshape function in conjunction with 'overlay=true' indicator parameter!
SEE ALSO
plotplotcharplotarrowbarcolorbgcolor
polyline.delete()
Deletes the specified polyline object. It has no effect if the id doesn't exist.
SYNTAX
polyline.delete(id) → void
ARGUMENTS
id (series polyline) The polyline ID to delete.
polyline.new()
Creates a new polyline instance and displays it on the chart, sequentially connecting all of the points in the points array with line segments. The segments in the drawing can be straight or curved depending on the curved parameter.
SYNTAX
polyline.new(points, curved, closed, xloc, line_color, fill_color, line_style, line_width, force_overlay) → series polyline
ARGUMENTS
points (array<chart.point>) An array of chart.point objects for the drawing to sequentially connect.
curved (series bool) If true, the drawing will connect all points from the points array using curved line segments. Optional. The default is false.
closed (series bool) If true, the drawing will also connect the first point to the last point from the points array, resulting in a closed polyline. Optional. The default is false.
xloc (series string) Determines the field of the chart.point objects in the points array that the polyline will use for its x-coordinates. If xloc.bar_index, the polyline will use the index field from each point. If xloc.bar_time, it will use the time field. Optional. The default is xloc.bar_index.
line_color (series color) The color of the line segments. Optional. The default is color.blue.
fill_color (series color) The fill color of the polyline. Optional. The default is na.
line_style (series string) The style of the polyline. Possible values: line.style_solid, line.style_dotted, line.style_dashed, line.style_arrow_left, line.style_arrow_right, line.style_arrow_both. Optional. The default is line.style_solid.
line_width (series int) The width of the line segments, expressed in pixels. Optional. The default is 1.
force_overlay (const bool) If true, the drawing will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("Polylines example", overlay = true)

//@variable If `true`, connects all points in the polyline with curved line segments. 
bool curvedInput = input.bool(false, "Curve Polyline")
//@variable If `true`, connects the first point in the polyline to the last point.
bool closedInput = input.bool(true, "Close Polyline")
//@variable The color of the space filled by the polyline.
color fillcolor = input.color(color.new(color.blue, 90), "Fill Color")

// Time and price inputs for the polyline's points. 
p1x = input.time(0,  "p1", confirm = true, inline = "p1")
p1y = input.price(0, "  ", confirm = true, inline = "p1")
p2x = input.time(0,  "p2", confirm = true, inline = "p2")
p2y = input.price(0, "  ", confirm = true, inline = "p2")
p3x = input.time(0,  "p3", confirm = true, inline = "p3")
p3y = input.price(0, "  ", confirm = true, inline = "p3")
p4x = input.time(0,  "p4", confirm = true, inline = "p4")
p4y = input.price(0, "  ", confirm = true, inline = "p4")
p5x = input.time(0,  "p5", confirm = true, inline = "p5")
p5y = input.price(0, "  ", confirm = true, inline = "p5")

if barstate.islastconfirmedhistory
    //@variable An array of `chart.point` objects for the new polyline.
    var points = array.new<chart.point>()
    // Push new `chart.point` instances into the `points` array.
    points.push(chart.point.from_time(p1x, p1y))
    points.push(chart.point.from_time(p2x, p2y))
    points.push(chart.point.from_time(p3x, p3y))
    points.push(chart.point.from_time(p4x, p4y))
    points.push(chart.point.from_time(p5x, p5y))
    // Add labels for each `chart.point` in `points`.
    l1p1 = label.new(points.get(0), text = "p1", xloc = xloc.bar_time, color = na)
    l1p2 = label.new(points.get(1), text = "p2", xloc = xloc.bar_time, color = na)
    l2p1 = label.new(points.get(2), text = "p3", xloc = xloc.bar_time, color = na)
    l2p2 = label.new(points.get(3), text = "p4", xloc = xloc.bar_time, color = na)
    // Create a new polyline that connects each `chart.point` in the `points` array, starting from the first.
    polyline.new(points, curved = curvedInput, closed = closedInput, fill_color = fillcolor, xloc = xloc.bar_time)
RETURNS
The ID of a new polyline object that a script can use in other polyline.*() functions.
SEE ALSO
chart.point.new
request.currency_rate()
Provides a daily rate that can be used to convert a value expressed in the from currency to another in the to currency.
SYNTAX
request.currency_rate(from, to, ignore_invalid_currency) → series float
ARGUMENTS
from (series string) The currency in which the value to be converted is expressed. Possible values: a three-letter string with the currency code in the ISO 4217 format (e.g. "USD"), or one of the built-in variables that return currency codes, like syminfo.currency or currency.USD.
to (series string) The currency in which the value is to be converted. Possible values: a three-letter string with the currency code in the ISO 4217 format (e.g. "USD"), or one of the built-in variables that return currency codes, like syminfo.currency or currency.USD.
ignore_invalid_currency (series bool) Determines the behavior of the function if a conversion rate between the two currencies cannot be calculated: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. Optional. The default is false.
EXAMPLE
//@version=6
indicator("Close in British Pounds")
rate = request.currency_rate(syminfo.currency, "GBP")
plot(close * rate)
REMARKS
If from and to arguments are equal, function returns 1. Please note that using this variable/function can cause indicator repainting.
request.dividends()
Requests dividends data for the specified symbol.
SYNTAX
request.dividends(ticker, field, gaps, lookahead, ignore_invalid_symbol, currency) → series float
ARGUMENTS
ticker (series string) Symbol. Note that the symbol should be passed with a prefix. For example: "NASDAQ:AAPL" instead of "AAPL". Using syminfo.ticker will cause an error. Use syminfo.tickerid instead.
field (series string) Input string. Possible values include: dividends.net, dividends.gross. Default value is dividends.gross.
gaps (simple barmerge_gaps) Merge strategy for the requested data (requested data automatically merges with the main series OHLC data). Possible values: barmerge.gaps_on, barmerge.gaps_off. barmerge.gaps_on - requested data is merged with possible gaps (na values). barmerge.gaps_off - requested data is merged continuously without gaps, all the gaps are filled with the previous nearest existing values. Default value is barmerge.gaps_off.
lookahead (simple barmerge_lookahead) Merge strategy for the requested data position. Possible values: barmerge.lookahead_on, barmerge.lookahead_off. Default value is barmerge.lookahead_off starting from version 3. Note that behavour is the same on real-time, and differs only on history.
ignore_invalid_symbol (input bool) An optional parameter. Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. The default value is false.
currency (series string) Currency into which the symbol's currency-related dividends values (e.g. dividends.gross) are to be converted. The conversion rate depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
EXAMPLE
//@version=6
indicator("request.dividends")
s1 = request.dividends("NASDAQ:BELFA")
plot(s1)
s2 = request.dividends("NASDAQ:BELFA", dividends.net, gaps=barmerge.gaps_on, lookahead=barmerge.lookahead_on)
plot(s2)
RETURNS
Requested series, or n/a if there is no dividends data for the specified symbol.
SEE ALSO
request.earningsrequest.splitsrequest.securitysyminfo.tickerid
request.earnings()
Requests earnings data for the specified symbol.
SYNTAX
request.earnings(ticker, field, gaps, lookahead, ignore_invalid_symbol, currency) → series float
ARGUMENTS
ticker (series string) Symbol. Note that the symbol should be passed with a prefix. For example: "NASDAQ:AAPL" instead of "AAPL". Using syminfo.ticker will cause an error. Use syminfo.tickerid instead.
field (series string) Input string. Possible values include: earnings.actual, earnings.estimate, earnings.standardized. Default value is earnings.actual.
gaps (simple barmerge_gaps) Merge strategy for the requested data (requested data automatically merges with the main series OHLC data). Possible values: barmerge.gaps_on, barmerge.gaps_off. barmerge.gaps_on - requested data is merged with possible gaps (na values). barmerge.gaps_off - requested data is merged continuously without gaps, all the gaps are filled with the previous nearest existing values. Default value is barmerge.gaps_off.
lookahead (simple barmerge_lookahead) Merge strategy for the requested data position. Possible values: barmerge.lookahead_on, barmerge.lookahead_off. Default value is barmerge.lookahead_off starting from version 3. Note that behavour is the same on real-time, and differs only on history.
ignore_invalid_symbol (input bool) An optional parameter. Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. The default value is false.
currency (series string) Currency into which the symbol's currency-related earnings values (e.g. earnings.actual) are to be converted. The conversion rate depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
EXAMPLE
//@version=6
indicator("request.earnings")
s1 = request.earnings("NASDAQ:BELFA")
plot(s1)
s2 = request.earnings("NASDAQ:BELFA", earnings.actual, gaps=barmerge.gaps_on, lookahead=barmerge.lookahead_on)
plot(s2)
RETURNS
Requested series, or n/a if there is no earnings data for the specified symbol.
SEE ALSO
request.dividendsrequest.splitsrequest.securitysyminfo.tickerid
request.economic()
Requests economic data for a symbol. Economic data includes information such as the state of a country's economy (GDP, inflation rate, etc.) or of a particular industry (steel production, ICU beds, etc.).
SYNTAX
request.economic(country_code, field, gaps, ignore_invalid_symbol) → series float
ARGUMENTS
country_code (series string) The code of the country (e.g. "US") or the region (e.g. "EU") for which the economic data is requested. The Help Center article lists the countries and their codes. The countries for which information is available vary with metrics. The Help Center article for each metric lists the countries for which the metric is available.
field (series string) The code of the requested economic metric (e.g., "GDP"). The Help Center article lists the metrics and their codes.
gaps (simple barmerge_gaps) Specifies how the returned values are merged on chart bars. Possible values: barmerge.gaps_off, barmerge.gaps_on. With barmerge.gaps_on, a value only appears on the current chart bar when it first becomes available from the function's context, otherwise na is returned (thus a "gap" occurs). With barmerge.gaps_off, what would otherwise be gaps are filled with the latest known value returned, avoiding na values. Optional. The default is barmerge.gaps_off.
ignore_invalid_symbol (input bool) Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. Optional. The default is false.
EXAMPLE
//@version=6
indicator("US GDP")
e = request.economic("US", "GDP")
plot(e)
RETURNS
Requested series.
REMARKS
Economic data can also be accessed from charts, just like a regular symbol. Use "ECONOMIC" as the exchange name and {country_code}{field} as the ticker. The name of US GDP data is thus "ECONOMIC:USGDP".
SEE ALSO
request.financial
request.financial()
Requests financial series for symbol.
SYNTAX
request.financial(symbol, financial_id, period, gaps, ignore_invalid_symbol, currency) → series float
ARGUMENTS
symbol (series string) Symbol. Note that the symbol should be passed with a prefix. For example: "NASDAQ:AAPL" instead of "AAPL".
financial_id (series string) Financial identifier. You can find the list of available ids via our Help Center.
period (series string) Reporting period. Possible values are "TTM", "FY", "FQ", "FH", "D".
gaps (simple barmerge_gaps) Merge strategy for the requested data (requested data automatically merges with the main series: OHLC data). Possible values include: barmerge.gaps_on, barmerge.gaps_off. barmerge.gaps_on - requested data is merged with possible gaps (na values). barmerge.gaps_off - requested data is merged continuously without gaps, all the gaps are filled with the previous, nearest existing values. Default value is barmerge.gaps_off.
ignore_invalid_symbol (input bool) An optional parameter. Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. The default value is false.
currency (series string) Optional. Currency into which the symbol's financial metrics (e.g. Net Income) are to be converted. The conversion rate depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
EXAMPLE
//@version=6
indicator("request.financial")
f = request.financial("NASDAQ:MSFT", "ACCOUNTS_PAYABLE", "FY")
plot(f)
RETURNS
Requested series.
SEE ALSO
request.securitysyminfo.tickerid
request.quandl()
Note: This function has been deprecated due to the API change from NASDAQ Data Link. Requests for "QUANDL" symbols are no longer valid and requests for them return a runtime error.
Some of the data previously provided by this function is available on TradingView through other feeds, such as "BCHAIN" or "FRED". Use Symbol Search to look for such data based on its description. Commitment of Traders (COT) data can be requested using the official LibraryCOT library.
Requests Nasdaq Data Link (formerly Quandl) data for a symbol.
SYNTAX
request.quandl(ticker, gaps, index, ignore_invalid_symbol) → series float
ARGUMENTS
ticker (series string) Symbol. Note that the name of a time series and Quandl data feed should be divided by a forward slash. For example: "CFTC/SB_FO_ALL".
gaps (simple barmerge_gaps) Merge strategy for the requested data (requested data automatically merges with the main series: OHLC data). Possible values include: barmerge.gaps_on, barmerge.gaps_off. barmerge.gaps_on - requested data is merged with possible gaps (na values). barmerge.gaps_off - requested data is merged continuously without gaps, all the gaps are filled with the previous, nearest existing values. Default value is barmerge.gaps_off.
index (series int) A Quandl time-series column index.
ignore_invalid_symbol (input bool) An optional parameter. Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. The default value is false.
EXAMPLE
//@version=6
indicator("request.quandl")
f = request.quandl("CFTC/SB_FO_ALL", barmerge.gaps_off, 0)
plot(f)
RETURNS
Requested series.
REMARKS
You can learn more about how to find ticker and index values in our Help Center.
SEE ALSO
request.securitysyminfo.tickerid
request.security()
Requests the result of an expression from a specified context (symbol and timeframe).
SYNTAX
request.security(symbol, timeframe, expression, gaps, lookahead, ignore_invalid_symbol, currency, calc_bars_count) → series <type>
ARGUMENTS
symbol (series string) Symbol or ticker identifier of the requested data. Use an empty string or syminfo.tickerid to request data using the chart's symbol. To retrieve data with additional modifiers (extended sessions, dividend adjustments, non-standard chart types like Heikin Ashi and Renko, etc.), create a custom ticker ID for the request using the functions in the ticker.* namespace.
timeframe (series string) Timeframe of the requested data. Use an empty string or timeframe.period to request data from the chart's timeframe or the timeframe specified in the indicator function. To request data from a different timeframe, supply a valid timeframe string. See here to learn about specifying timeframe strings.
expression (variable, function, object, array, matrix, or map of series int/float/bool/string/color/enum, or a tuple of these) The expression to calculate and return from the requested context. It can accept a built-in variable like close, a user-defined variable, an expression such as ta.change(close) / (high - low), a function call that does not use Pine Script® drawings, an object, a collection, or a tuple of expressions.
gaps (simple barmerge_gaps) Specifies how the returned values are merged on chart bars. Possible values: barmerge.gaps_on, barmerge.gaps_off. With barmerge.gaps_on a value only appears on the current chart bar when it first becomes available from the function's context, otherwise na is returned (thus a "gap" occurs). With barmerge.gaps_off what would otherwise be gaps are filled with the latest known value returned, avoiding na values. Optional. The default is barmerge.gaps_off.
lookahead (simple barmerge_lookahead) On historical bars only, returns data from the timeframe before it elapses. Possible values: barmerge.lookahead_on, barmerge.lookahead_off. Has no effect on realtime values. Optional. The default is barmerge.lookahead_off starting from Pine Script® v3. The default is barmerge.lookahead_on in v1 and v2. WARNING: Using barmerge.lookahead_on at timeframes higher than the chart's without offsetting the expression argument like in close[1] will introduce future leak in scripts, as the function will then return the close price before it is actually known in the current context. As is explained in the User Manual's page on Repainting this will produce misleading results.
ignore_invalid_symbol (input bool) Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and throw a runtime error; if true, the function will return na and execution will continue. Optional. The default is false.
currency (series string) Optional. Specifies the target currency for converting values expressed in currency units (e.g., open, high, low, close) or expressions involving such values. Literal values such as 200 are not converted. The conversion rate for monetary values depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
calc_bars_count (simple int) If specified, the function will only request this number of values from the end of the symbol's history and calculate expression as if these values are the only available data, which might improve calculation speed in some cases. Optional. The default is 100,000, which is the limit for all non-professional TradingView plans.
EXAMPLE
//@version=6
indicator("Simple `request.security()` calls")
// Returns 1D close of the current symbol.
dailyClose = request.security(syminfo.tickerid, "1D", close)
plot(dailyClose)

// Returns the close of "AAPL" from the same timeframe as currently open on the chart.
aaplClose = request.security("AAPL", timeframe.period, close)
plot(aaplClose)
EXAMPLE
//@version=6
indicator("Advanced `request.security()` calls")
// This calculates a 10-period moving average on the active chart.
sma = ta.sma(close, 10)
// This sends the `sma` calculation for execution in the context of the "AAPL" symbol at a "240" (4 hours) timeframe.
aaplSma = request.security("AAPL", "240", sma)
plot(aaplSma)

// To avoid differences on historical and realtime bars, you can use this technique, which only returns a value from the higher timeframe on the bar after it completes:
indexHighTF = barstate.isrealtime ? 1 : 0
indexCurrTF = barstate.isrealtime ? 0 : 1
nonRepaintingClose = request.security(syminfo.tickerid, "1D", close[indexHighTF])[indexCurrTF]
plot(nonRepaintingClose, "Non-repainting close")

// Returns the 1H close of "AAPL", extended session included. The value is dividend-adjusted.
extendedTicker = ticker.modify("NASDAQ:AAPL", session = session.extended, adjustment = adjustment.dividends)
aaplExtAdj = request.security(extendedTicker, "60", close)
plot(aaplExtAdj)

// Returns the result of a user-defined function.
// The `max` variable is mutable, but we can pass it to `request.security()` because it is wrapped in a function.
allTimeHigh(source) =>
    var max = source
    max := math.max(max, source)
allTimeHigh1D = request.security(syminfo.tickerid, "1D", allTimeHigh(high))

// By using a tuple `expression`, we obtain several values with only one `request.security()` call.
[open1D, high1D, low1D, close1D, ema1D] = request.security(syminfo.tickerid, "1D", [open, high, low, close, ta.ema(close, 10)])
plotcandle(open1D, high1D, low1D, close1D)
plot(ema1D)

// Returns an array containing the OHLC values of the chart's symbol from the 1D timeframe.
ohlcArray = request.security(syminfo.tickerid, "1D", array.from(open, high, low, close))
plotcandle(array.get(ohlcArray, 0), array.get(ohlcArray, 1), array.get(ohlcArray, 2), array.get(ohlcArray, 3))
RETURNS
A result determined by expression.
REMARKS
Scripts using this function might calculate differently on historical and realtime bars, leading to repainting.
A single script can contain no more than 40 unique request.*() function calls. A call is unique only if it does not call the same function with the same arguments.
When using two calls to a request.*() function to evaluate the same expression from the same context with different calc_bars_count values, the second call requests the same number of historical bars as the first. For example, if a script calls request.security("AAPL", "", close, calc_bars_count = 3) after it calls request.security("AAPL", "", close, calc_bars_count = 5), the second call also uses five bars of historical data, not three.
The symbol of a request.() call can be inherited if it is not specified precisely, i.e., if the symbol argument is an empty string or syminfo.tickerid. Similarly, the timeframe of a request.() call can be inherited if the timeframe argument is an empty string or timeframe.period. These values are normally taken from the chart on which the script is running. However, if request.*() function A is called from within the expression of request.*() function B, then function A can inherit the values from function B. See here for more information.
SEE ALSO
syminfo.tickersyminfo.tickeridtimeframe.periodticker.newticker.modifyrequest.security_lower_tfrequest.dividendsrequest.earningsrequest.splitsrequest.financial
request.security_lower_tf()
Requests the results of an expression from a specified symbol on a timeframe lower than or equal to the chart's timeframe. It returns an array containing one element for each lower-timeframe bar within the chart bar. On a 5-minute chart, requesting data using a timeframe argument of "1" typically returns an array with five elements representing the value of the expression on each 1-minute bar, ordered by time with the earliest value first.
SYNTAX
request.security_lower_tf(symbol, timeframe, expression, ignore_invalid_symbol, currency, ignore_invalid_timeframe, calc_bars_count) → array<type>
ARGUMENTS
symbol (series string) Symbol or ticker identifier of the requested data. Use an empty string or syminfo.tickerid to request data using the chart's symbol. To retrieve data with additional modifiers (extended sessions, dividend adjustments, non-standard chart types like Heikin Ashi and Renko, etc.), create a custom ticker ID for the request using the functions in the ticker.* namespace.
timeframe (series string) Timeframe of the requested data. Use an empty string or timeframe.period to request data from the chart's timeframe or the timeframe specified in the indicator function. To request data from a different timeframe, supply a valid timeframe string. See here to learn about specifying timeframe strings.
expression (variable, object or function of series int/float/bool/string/color/enum, or a tuple of these) The expression to calculate and return from the requested context. It can accept a built-in variable like close, a user-defined variable, an expression such as ta.change(close) / (high - low), a function call that does not use Pine Script® drawings, an object, or a tuple of expressions. Collections are not allowed unless they are within the fields of an object
ignore_invalid_symbol (series bool) Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and throw a runtime error; if true, the function will return na and execution will continue. Optional. The default is false.
currency (series string) Optional. Specifies the target currency for converting values expressed in currency units (e.g., open, high, low, close) or expressions involving such values. Literal values such as 200 are not converted. The conversion rate for monetary values depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
ignore_invalid_timeframe (series bool) Determines the behavior of the function when the chart's timeframe is smaller than the timeframe used in the function call. If false, the script will halt and throw a runtime error. If true, the function will return na and execution will continue. Optional. The default is false.
calc_bars_count (simple int) If specified, the function will only request this number of values from the end of the symbol's history and calculate expression as if these values are the only available data, which might improve calculation speed in some cases. Optional. The default is 100,000, which is the limit for all non-professional TradingView plans.
EXAMPLE
//@version=6
indicator("`request.security_lower_tf()` Example", overlay = true)

// If the current chart timeframe is set to 120 minutes, then the `arrayClose` array will contain two 'close' values from the 60 minute timeframe for each bar.
arrClose = request.security_lower_tf(syminfo.tickerid, "60", close)

if bar_index == last_bar_index - 1
    label.new(bar_index, high, str.tostring(arrClose))
RETURNS
An array of a type determined by expression, or a tuple of these.
REMARKS
Scripts using this function might calculate differently on historical and realtime bars, leading to repainting.
Please note that spreads (e.g., "AAPL+MSFT*TSLA") do not always return reliable data with this function.
A single script can contain no more than 40 unique request.*() function calls. A call is unique only if it does not call the same function with the same arguments.
When using two calls to a request.*() function to evaluate the same expression from the same context with different calc_bars_count values, the second call requests the same number of historical bars as the first. For example, if a script calls request.security("AAPL", "", close, calc_bars_count = 3) after it calls request.security("AAPL", "", close, calc_bars_count = 5), the second call also uses five bars of historical data, not three.
The symbol of a request.() call can be inherited if it is not specified precisely, i.e., if the symbol argument is an empty string or syminfo.tickerid. Similarly, the timeframe of a request.() call can be inherited if the timeframe argument is an empty string or timeframe.period. These values are normally taken from the chart that the script is running on. However, if request.*() function A is called from within the expression of request.*() function B, then function A can inherit the values from function B. See here for more information.
SEE ALSO
request.securitysyminfo.tickersyminfo.tickeridtimeframe.periodticker.newrequest.dividendsrequest.earningsrequest.splitsrequest.financial
request.seed()
Requests data from a user-maintained GitHub repository and returns it as a series. An in-depth tutorial on how to add new data can be found here.
SYNTAX
request.seed(source, symbol, expression, ignore_invalid_symbol, calc_bars_count) → series <type>
ARGUMENTS
source (series string) Name of the GitHub repository.
symbol (series string) Name of the file in the GitHub repository containing the data. The ".csv" file extension must not be included.
expression (<arg_expr_type>) An expression to be calculated and returned from the requested symbol's context. It can be a built-in variable like close, an expression such as ta.sma(close, 100), a non-mutable variable previously calculated in the script, a function call that does not use Pine Script® drawings, an array, a matrix, or a tuple. Mutable variables are not allowed, unless they are enclosed in the body of a function used in the expression.
ignore_invalid_symbol (input bool) Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and throw a runtime error; if true, the function will return na and execution will continue. Optional. The default is false.
calc_bars_count (simple int) If specified, the function will only request this number of values from the end of the symbol's history and calculate expression as if these values are the only available data, which might improve calculation speed in some cases. Optional. The default is 100,000, which is the limit for all non-professional TradingView plans.
EXAMPLE
//@version=6
indicator("BTC Development Activity")

[devAct, devActSMA] = request.seed("seed_crypto_santiment", "BTC_DEV_ACTIVITY", [close, ta.sma(close, 10)])

plot(devAct, "BTC Development Activity")
plot(devActSMA, "BTC Development Activity SMA10", color = color.yellow)
RETURNS
Requested series or tuple of series, which may include array/matrix IDs.
request.splits()
Requests splits data for the specified symbol.
SYNTAX
request.splits(ticker, field, gaps, lookahead, ignore_invalid_symbol) → series float
ARGUMENTS
ticker (series string) Symbol. Note that the symbol should be passed with a prefix. For example: "NASDAQ:AAPL" instead of "AAPL". Using syminfo.ticker will cause an error. Use syminfo.tickerid instead.
field (series string) Input string. Possible values include: splits.denominator, splits.numerator.
gaps (simple barmerge_gaps) Merge strategy for the requested data (requested data automatically merges with the main series OHLC data). Possible values: barmerge.gaps_on, barmerge.gaps_off. barmerge.gaps_on - requested data is merged with possible gaps (na values). barmerge.gaps_off - requested data is merged continuously without gaps, all the gaps are filled with the previous nearest existing values. Default value is barmerge.gaps_off.
lookahead (simple barmerge_lookahead) Merge strategy for the requested data position. Possible values: barmerge.lookahead_on, barmerge.lookahead_off. Default value is barmerge.lookahead_off starting from version 3. Note that behavour is the same on real-time, and differs only on history.
ignore_invalid_symbol (input bool) An optional parameter. Determines the behavior of the function if the specified symbol is not found: if false, the script will halt and return a runtime error; if true, the function will return na and execution will continue. The default value is false.
EXAMPLE
//@version=6
indicator("request.splits")
s1 = request.splits("NASDAQ:BELFA", splits.denominator)
plot(s1)
s2 = request.splits("NASDAQ:BELFA", splits.denominator, gaps=barmerge.gaps_on, lookahead=barmerge.lookahead_on)
plot(s2)
RETURNS
Requested series, or n/a if there is no splits data for the specified symbol.
SEE ALSO
request.earningsrequest.dividendsrequest.securitysyminfo.tickerid
runtime.error()
When called, causes a runtime error with the error message specified in the message argument.
SYNTAX
runtime.error(message) → void
ARGUMENTS
message (series string) Error message.
second()2 overloads
SYNTAX & OVERLOADS
second(time) → series int
second(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Second (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
secondtimeyearmonthdayofmonthdayofweekhourminute
str.contains()3 overloads
Returns true if the source string contains the str substring, false otherwise.
SYNTAX & OVERLOADS
str.contains(source, str) → const bool
str.contains(source, str) → simple bool
str.contains(source, str) → series bool
ARGUMENTS
source (const string) Source string.
str (const string) The substring to search for.
EXAMPLE
//@version=6
indicator("str.contains")
// If the current chart is a continuous futures chart, e.g “BTC1!”, then the function will return true, false otherwise.
var isFutures = str.contains(syminfo.tickerid, "!")
plot(isFutures ? 1 : 0)
RETURNS
True if the str was found in the source string, false otherwise.
SEE ALSO
str.posstr.match
str.endswith()3 overloads
Returns true if the source string ends with the substring specified in str, false otherwise.
SYNTAX & OVERLOADS
str.endswith(source, str) → const bool
str.endswith(source, str) → simple bool
str.endswith(source, str) → series bool
ARGUMENTS
source (const string) Source string.
str (const string) The substring to search for.
RETURNS
True if the source string ends with the substring specified in str, false otherwise.
SEE ALSO
str.startswith
str.format()2 overloads
Converts the formatting string and value(s) into a formatted string. The formatting string can contain literal text and one placeholder in curly braces {} for each value to be formatted. Each placeholder consists of the index of the required argument (beginning at 0) that will replace it, and an optional format specifier. The index represents the position of that argument in the str.format argument list.
SYNTAX & OVERLOADS
str.format(formatString, arg0, arg1, ...) → simple string
str.format(formatString, arg0, arg1, ...) → series string
ARGUMENTS
formatString (simple string) Format string.
arg0, arg1, ... (simple int/float/bool/string) Values to format.
EXAMPLE
//@version=6
indicator("str.format", overlay=true)
// The format specifier inside the curly braces accepts certain modifiers:
// - Specify the number of decimals to display:
s1 = str.format("{0,number,#.#}", 1.34) // returns: 1.3
label.new(bar_index, close, text=s1)
// - Round a float value to an integer:
s2 = str.format("{0,number,integer}", 1.34) // returns: 1
label.new(bar_index - 1, close, text=s2)
// - Display a number in currency:
s3 = str.format("{0,number,currency}", 1.34) // returns: $1.34
label.new(bar_index - 2, close, text=s3)
// - Display a number as a percentage:
s4 = str.format("{0,number,percent}", 0.5) // returns: 50%
label.new(bar_index - 3, close, text=s4)
// EXAMPLES WITH SEVERAL ARGUMENTS
// returns: Number 1 is not equal to 4
s5 = str.format("Number {0} is not {1} to {2}", 1, "equal", 4)
label.new(bar_index - 4, close, text=s5)
// returns: 1.34 != 1.3
s6 = str.format("{0} != {0, number, #.#}", 1.34)
label.new(bar_index - 5, close, text=s6)
// returns: 1 is equal to 1, but 2 is equal to 2
s7 = str.format("{0, number, integer} is equal to 1, but {1, number, integer} is equal to 2", 1.34, 1.52)
label.new(bar_index - 6, close, text=s7)
// returns: The cash turnover amounted to $1,340,000.00
s8 = str.format("The cash turnover amounted to {0, number, currency}", 1340000)
label.new(bar_index - 7, close, text=s8)
// returns: Expected return is 10% - 20%
s9 = str.format("Expected return is {0, number, percent} - {1, number, percent}", 0.1, 0.2)
label.new(bar_index - 8, close, text=s9)
RETURNS
The formatted string.
REMARKS
By default, formatted numbers will display up to three decimals with no trailing zeros.
The string used as the formatString argument can contain single quote characters ('). However, one must pair all single quotes in that string to avoid unexpected formatting results.
Any curly braces within an unquoted pattern must be balanced. For example, "ab {0} de" and "ab '}' de" are valid patterns, but "ab {0'}' de", "ab } de" and "''{''" are not.
str.format_time()
Converts the time timestamp into a string formatted according to format and timezone.
SYNTAX
str.format_time(time, format, timezone) → series string
ARGUMENTS
time (series int) UNIX time, in milliseconds.
format (series string) A format string specifying the date/time representation of the time in the returned string. All letters used in the string, except those escaped by single quotation marks ', are considered formatting tokens and will be used as a formatting instruction. Refer to the Remarks section for a list of the most useful tokens. Optional. The default is "yyyy-MM-dd'T'HH:mm:ssZ", which represents the ISO 8601 standard.
timezone (series string) Allows adjusting the returned value to a time zone specified in either UTC/GMT notation (e.g., "UTC-5", "GMT+0530") or as an IANA time zone database name (e.g., "America/New_York"). Optional. The default is syminfo.timezone.
EXAMPLE
//@version=6
indicator("str.format_time")
if timeframe.change("1D")
    formattedTime = str.format_time(time, "yyyy-MM-dd HH:mm", syminfo.timezone)
    label.new(bar_index, high, formattedTime)
RETURNS
The formatted string.
REMARKS
The M, d, h, H, m and s tokens can all be doubled to generate leading zeros. For example, the month of January will display as 1 with M, or 01 with MM.
The most frequently used formatting tokens are:
y - Year. Use yy to output the last two digits of the year or yyyy to output all four. Year 2000 will be 00 with yy or 2000 with yyyy.
M - Month. Not to be confused with lowercase m, which stands for minute.
d - Day of the month.
a - AM/PM postfix.
h - Hour in the 12-hour format. The last hour of the day will be 11 in this format.
H - Hour in the 24-hour format. The last hour of the day will be 23 in this format.
m - Minute.
s - Second.
S - Fractions of a second.
Z - Timezone, the HHmm offset from UTC, preceded by either + or -.
str.length()3 overloads
Returns an integer corresponding to the amount of chars in that string.
SYNTAX & OVERLOADS
str.length(string) → const int
str.length(string) → simple int
str.length(string) → series int
ARGUMENTS
string (const string) Source string.
RETURNS
The number of chars in source string.
str.lower()3 overloads
Returns a new string with all letters converted to lowercase.
SYNTAX & OVERLOADS
str.lower(source) → const string
str.lower(source) → simple string
str.lower(source) → series string
ARGUMENTS
source (const string) String to be converted.
RETURNS
A new string with all letters converted to lowercase.
SEE ALSO
str.upper
str.match()2 overloads
Returns the new substring of the source string if it matches a regex regular expression, an empty string otherwise.
SYNTAX & OVERLOADS
str.match(source, regex) → simple string
str.match(source, regex) → series string
ARGUMENTS
source (simple string) Source string.
regex (simple string) The regular expression to which this string is to be matched.
EXAMPLE
//@version=6
indicator("str.match")

s = input.string("It's time to sell some NASDAQ:AAPL!")

// finding first substring that matches regular expression "[\w]+:[\w]+"
var string tickerid = str.match(s, "[\\w]+:[\\w]+")

if barstate.islastconfirmedhistory
    label.new(bar_index, high, text = tickerid) // "NASDAQ:AAPL"
RETURNS
The new substring of the source string if it matches a regex regular expression, an empty string otherwise.
REMARKS
Function returns first occurrence of the regular expression in the source string.
The backslash "\" symbol in theregex string needs to be escaped with additional backslash, e.g. "\\d" stands for regular expression "\d".
SEE ALSO
str.containsstr.substring
str.pos()3 overloads
Returns the position of the first occurrence of the str string in the source string, 'na' otherwise.
SYNTAX & OVERLOADS
str.pos(source, str) → const int
str.pos(source, str) → simple int
str.pos(source, str) → series int
ARGUMENTS
source (const string) Source string.
str (const string) The substring to search for.
RETURNS
Position of the str string in the source string.
REMARKS
Strings indexing starts at 0.
SEE ALSO
str.containsstr.matchstr.substring
str.repeat()4 overloads
Constructs a new string containing the source string repeated repeat times with the separator injected between each repeated instance.
SYNTAX & OVERLOADS
str.repeat(source, repeat, separator) → const string
str.repeat(source, repeat, separator) → input string
str.repeat(source, repeat, separator) → simple string
str.repeat(source, repeat, separator) → series string
ARGUMENTS
source (const string) String to repeat.
repeat (const int) Number of times to repeat the source string. Must be greater than or equal to 0.
separator (const string) String to inject between repeated values. Optional. The default is empty string.
EXAMPLE
//@version=6
indicator("str.repeat")
repeat = str.repeat("?", 3, ",") // Returns "?,?,?"
label.new(bar_index,close,repeat)
REMARKS
Returns na if the source is na.
str.replace()3 overloads
Returns a new string with the Nth occurrence of the target string replaced by the replacement string, where N is specified in occurrence.
SYNTAX & OVERLOADS
str.replace(source, target, replacement, occurrence) → const string
str.replace(source, target, replacement, occurrence) → simple string
str.replace(source, target, replacement, occurrence) → series string
ARGUMENTS
source (const string) Source string.
target (const string) String to be replaced.
replacement (const string) String to be inserted instead of the target string.
occurrence (const int) N-th occurrence of the target string to replace. Indexing starts at 0 for the first match. Optional. Default value is 0.
EXAMPLE
//@version=6
indicator("str.replace")
var source = "FTX:BTCUSD / FTX:BTCEUR"

// Replace first occurrence of "FTX" with "BINANCE" replacement string
var newSource = str.replace(source, "FTX", "BINANCE", 0)

if barstate.islastconfirmedhistory
    // Display "BINANCE:BTCUSD / FTX:BTCEUR"
    label.new(bar_index, high, text = newSource)
RETURNS
Processed string.
SEE ALSO
str.replace_allstr.match
str.replace_all()2 overloads
Replaces each occurrence of the target string in the source string with the replacement string.
SYNTAX & OVERLOADS
str.replace_all(source, target, replacement) → simple string
str.replace_all(source, target, replacement) → series string
ARGUMENTS
source (simple string) Source string.
target (simple string) String to be replaced.
replacement (simple string) String to be substituted for each occurrence of target string.
RETURNS
Processed string.
str.split()
Divides a string into an array of substrings and returns its array id.
SYNTAX
str.split(string, separator) → array<string>
ARGUMENTS
string (series string) Source string.
separator (series string) The string separating each substring.
RETURNS
The id of an array of strings.
str.startswith()3 overloads
Returns true if the source string starts with the substring specified in str, false otherwise.
SYNTAX & OVERLOADS
str.startswith(source, str) → const bool
str.startswith(source, str) → simple bool
str.startswith(source, str) → series bool
ARGUMENTS
source (const string) Source string.
str (const string) The substring to search for.
RETURNS
True if the source string starts with the substring specified in str, false otherwise.
SEE ALSO
str.endswith
str.substring()6 overloads
Returns a new string that is a substring of the source string. The substring begins with the character at the index specified by begin_pos and extends to 'end_pos - 1' of the source string.
SYNTAX & OVERLOADS
str.substring(source, begin_pos) → const string
str.substring(source, begin_pos) → simple string
str.substring(source, begin_pos) → series string
str.substring(source, begin_pos, end_pos) → const string
str.substring(source, begin_pos, end_pos) → simple string
str.substring(source, begin_pos, end_pos) → series string
ARGUMENTS
source (const string) Source string from which to extract the substring.
begin_pos (const int) The beginning position of the extracted substring. It is inclusive (the extracted substring includes the character at that position).
EXAMPLE
//@version=6
indicator("str.substring", overlay = true)
sym= input.symbol("NASDAQ:AAPL")
pos = str.pos(sym, ":") // Get position of ":" character
tkr= str.substring(sym, pos+1) // "AAPL"
if barstate.islastconfirmedhistory
    label.new(bar_index, high, text = tkr)
RETURNS
The substring extracted from the source string.
REMARKS
Strings indexing starts from 0. If begin_pos is equal to end_pos, the function returns an empty string.
SEE ALSO
str.containsstr.posstr.match
str.tonumber()4 overloads
Converts a value represented in string to its "float" equivalent.
SYNTAX & OVERLOADS
str.tonumber(string) → const float
str.tonumber(string) → input float
str.tonumber(string) → simple float
str.tonumber(string) → series float
ARGUMENTS
string (const string) String containing the representation of an integer or floating point value.
RETURNS
A "float" equivalent of the value in string. If the value is not a properly formed integer or floating point value, the function returns na.
str.tostring()4 overloads
SYNTAX & OVERLOADS
str.tostring(value, format) → simple string
str.tostring(value, format) → series string
str.tostring(value) → simple string
str.tostring(value) → series string
ARGUMENTS
value (simple int/float) Value or array ID whose elements are converted to a string.
format (simple string) Format string. Accepts these format.* constants: format.mintick, format.percent, format.volume. Optional. The default value is '#.##########'.
RETURNS
The string representation of the value argument.
If the value argument is a string, it is returned as is.
When the value is na, the function returns the string "NaN".
REMARKS
The formatting of float values will also round those values when necessary, e.g. str.tostring(3.99, '#') will return "4".
To display trailing zeros, use '0' instead of '#'. For example, '#.000'.
When using format.mintick, the value will be rounded to the nearest number that can be divided by syminfo.mintick without the remainder. The string is returned with trailing zeros.
If the x argument is a string, the same string value will be returned.
Bool type arguments return "true" or "false".
When x is na, the function returns "NaN".
str.trim()4 overloads
Constructs a new string with all consecutive whitespaces and other control characters (e.g., “\n”, “\t”, etc.) removed from the left and right of the source.
SYNTAX & OVERLOADS
str.trim(source) → const string
str.trim(source) → input string
str.trim(source) → simple string
str.trim(source) → series string
ARGUMENTS
source (const string) String to trim.
EXAMPLE
//@version=6
indicator("str.trim")
trim = str.trim("    abc    ") // Returns "abc"
label.new(bar_index,close,trim)
REMARKS
Returns an empty string ("") if the result is empty after the trim or if the source is na.
str.upper()3 overloads
Returns a new string with all letters converted to uppercase.
SYNTAX & OVERLOADS
str.upper(source) → const string
str.upper(source) → simple string
str.upper(source) → series string
ARGUMENTS
source (const string) String to be converted.
RETURNS
A new string with all letters converted to uppercase.
SEE ALSO
str.lower
strategy()
This declaration statement designates the script as a strategy and sets a number of strategy-related properties.
SYNTAX
strategy(title, shorttitle, overlay, format, precision, scale, pyramiding, calc_on_order_fills, calc_on_every_tick, max_bars_back, backtest_fill_limits_assumption, default_qty_type, default_qty_value, initial_capital, currency, slippage, commission_type, commission_value, process_orders_on_close, close_entries_rule, margin_long, margin_short, explicit_plot_zorder, max_lines_count, max_labels_count, max_boxes_count, calc_bars_count, risk_free_rate, use_bar_magnifier, fill_orders_on_standard_ohlc, max_polylines_count, dynamic_requests, behind_chart) → void
ARGUMENTS
title (const string) The title of the script. It is displayed on the chart when no shorttitle argument is used, and becomes the publication's default title when publishing the script.
shorttitle (const string) The script's display name on charts. If specified, it will replace the title argument in most chart-related windows. Optional. The default is the argument used for title.
overlay (const bool) If true, the strategy will be displayed over the chart. If false, it will be added in a separate pane. Strategy-specific labels that display entries and exits will be displayed over the main chart regardless of this setting. Optional. The default is false.
format (const string) Specifies the formatting of the script's displayed values. Possible values: format.inherit, format.price, format.volume, format.percent. Optional. The default is format.inherit.
precision (const int) Specifies the number of digits after the floating point of the script's displayed values. Must be a non-negative integer no greater than 16. If format is set to format.inherit and precision is specified, the format will instead be set to format.price. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is inherited from the precision of the chart's symbol.
scale (const scale_type) The price scale used. Possible values: scale.right, scale.left, scale.none. The scale.none value can only be applied in combination with overlay = true. Optional. By default, the script uses the same scale as the chart.
pyramiding (const int) The maximum number of entries allowed in the same direction. If the value is 0, only one entry order in the same direction can be opened, and additional entry orders are rejected. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is 0.
calc_on_order_fills (const bool) Specifies whether the strategy should be recalculated after an order is filled. If true, the strategy recalculates after an order is filled, as opposed to recalculating only when the bar closes. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is false.
calc_on_every_tick (const bool) Specifies whether the strategy should be recalculated on each realtime tick. If true, when the strategy is running on a realtime bar, it will recalculate on each chart update. If false, the strategy only calculates when the realtime bar closes. The argument used does not affect strategy calculation on historical data. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is false.
max_bars_back (const int) The length of the historical buffer the script keeps for every variable and function, which determines how many past values can be referenced using the [] history-referencing operator. The required buffer size is automatically detected by the Pine Script® runtime. Using this parameter is only necessary when a runtime error occurs because automatic detection fails. More information on the underlying mechanics of the historical buffer can be found in our Help Center. Optional. The default is 0.
backtest_fill_limits_assumption (const int) Limit order execution threshold in ticks. When it is used, limit orders are only filled if the market price exceeds the order's limit level by the specified number of ticks. Optional. The default is 0.
default_qty_type (const string) Specifies the units used for default_qty_value. Possible values are: strategy.fixed for contracts/shares/lots, strategy.cash for currency amounts, or strategy.percent_of_equity for a percentage of available equity. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is strategy.fixed.
default_qty_value (const int/float) The default quantity to trade, in units determined by the argument used with the default_qty_type parameter. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is 1.
initial_capital (const int/float) The amount of funds initially available for the strategy to trade, in units of currency. Optional. The default is 1000000.
currency (const string) Currency used by the strategy in currency-related calculations. Market positions are still opened by converting currency into the chart symbol's currency. The conversion rate depends on the previous daily value of a corresponding currency pair from the most popular exchange. A spread symbol is used if no exchange provides the rate directly. Possible values: a "string" representing a valid currency code (e.g., "USD" or "USDT") or a constant from the currency.* namespace (e.g., currency.USD or currency.USDT). The default is syminfo.currency.
slippage (const int) Slippage expressed in ticks. This value is added to or subtracted from the fill price of market/stop orders to make the fill price less favorable for the strategy. E.g., if syminfo.mintick is 0.01 and slippage is set to 5, a long market order will enter at 5 * 0.01 = 0.05 points above the actual price. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is 0.
commission_type (const string) Determines what the number passed to the commission_value expresses: strategy.commission.percent for a percentage of the cash volume of the order, strategy.commission.cash_per_contract for currency per contract, strategy.commission.cash_per_order for currency per order. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is strategy.commission.percent.
commission_value (const int/float) Commission applied to the strategy's orders in units determined by the argument passed to the commission_type parameter. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is 0.
process_orders_on_close (const bool) When set to true, generates an additional attempt to execute orders after a bar closes and strategy calculations are completed. If the orders are market orders, the broker emulator executes them before the next bar's open. If the orders are price-dependent, they will only be filled if the price conditions are met. This option is useful if you wish to close positions on the current bar. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. The default is false.
close_entries_rule (const string) Determines the order in which trades are closed. Possible values are: "FIFO" (First-In, First-Out) if the earliest exit order must close the earliest entry order, or "ANY" if the orders are closed based on the from_entry parameter of the strategy.exit function. "FIFO" can only be used with stocks, futures and US forex (NFA Compliance Rule 2-43b), while "ANY" is allowed in non-US forex. Optional. The default is "FIFO".
margin_long (const int/float) Margin long is the percentage of the purchase price of a security that must be covered by cash or collateral for long positions. Must be a non-negative number. The logic used to simulate margin calls is explained in the Help Center. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. If the value is 0, the strategy does not enforce any limits on position size. The default is 100, in which case the strategy only uses its own funds and the long positions cannot be margin called.
margin_short (const int/float) Margin short is the percentage of the purchase price of a security that must be covered by cash or collateral for short positions. Must be a non-negative number. The logic used to simulate margin calls is explained in the Help Center. This setting can also be changed in the strategy's "Settings/Properties" tab. Optional. If the value is 0, the strategy does not enforce any limits on position size. The default is 100, in which case the strategy only uses its own funds. Note that even with no margin used, short positions can be margin called if the loss exceeds available funds.
explicit_plot_zorder (const bool) Specifies the order in which the script's plots, fills, and hlines are rendered. If true, plots are drawn in the order in which they appear in the script's code, each newer plot being drawn above the previous ones. This only applies to plot*() functions, fill, and hline. Optional. The default is false.
max_lines_count (const int) The number of last line drawings displayed. Possible values: 1-500. Optional. The default is 50.
max_labels_count (const int) The number of last label drawings displayed. Possible values: 1-500. Optional. The default is 50.
max_boxes_count (const int) The number of last box drawings displayed. Possible values: 1-500. Optional. The default is 50.
calc_bars_count (const int) Limits the initial calculation of a script to the last number of bars specified. When specified, a "Calculated bars" field will be included in the "Calculation" section of the script's "Settings/Inputs" tab. Optional. The default is 0, in which case the script executes on all available bars.
risk_free_rate (const int/float) The risk-free rate of return is the annual percentage change in the value of an investment with minimal or zero risk. It is used to calculate the Sharpe and Sortino ratios. Optional. The default is 2.
use_bar_magnifier (const bool) Optional. When true, the Broker Emulator uses lower timeframe data during backtesting on historical bars to achieve more realistic results. The default is false. Only Premium and higher-tier plans have access to this feature.
fill_orders_on_standard_ohlc (const bool) When true, forces strategies running on Heikin Ashi charts to fill orders using actual OHLC prices, for more realistic results. Optional. The default is false.
max_polylines_count (const int) The number of last polyline drawings displayed. Possible values: 1-100. The count is approximate; more drawings than the specified count may be displayed. Optional. The default is 50.
dynamic_requests (const bool) Specifies whether the script can dynamically call functions from the request.*() namespace. Dynamic request.*() calls are allowed within the local scopes of conditional structures (e.g., if), loops (e.g., for), and exported functions. Additionally, such calls allow "series" arguments for many of their parameters. Optional. The default is true. See the User Manual's Dynamic requests section for more information.
behind_chart (const bool) Controls whether the script's plots and drawings in the main chart pane appear behind the chart display (if true), or in front of it (if false). Optional. The default is true.
EXAMPLE
//@version=6
strategy("My strategy", overlay = true)

// Enter long by market if current open is greater than previous high.
if open > high[1]
    strategy.entry("Long", strategy.long, 1)
// Generate a full exit bracket (profit 10 points, loss 5 points per contract) from the entry named "Long".
strategy.exit("Exit", "Long", profit = 10, loss = 5)
REMARKS
You can learn more about strategies in our User Manual.
Every strategy script must have one strategy call.
Strategies using calc_on_every_tick = true parameter may calculate differently on historical and realtime bars, which causes repainting.
Strategies always use the chart's prices to enter and exit positions. Using them on non-standard chart types (Heikin Ashi, Renko, etc.) will produce misleading results, as their prices are synthetic. Backtesting on non-standard charts is thus not recommended.
The maximum number of orders a strategy can open, unless it uses Deep Backtesting mode, is 9000. If the strategy exceeds this limit, it removes the oldest order's information when a new entry appears in the "List of Trades" tab. The strategy.closedtrades.*() functions return na for trades opened or closed by removed orders. To retrieve the index of the oldest available closed trade, use the strategy.closedtrades.first_index variable.
SEE ALSO
indicatorlibrary
strategy.cancel()
Cancels a pending or unfilled order with a specific identifier. If multiple unfilled orders share the same ID, calling this command with that ID as the id argument cancels all of them. If a script calls this command with an id representing the ID of a filled order, it has no effect.
This command is most useful when working with price-based orders (e.g., limit orders). Calls to this command can also cancel market orders, but only if they execute on the same ticks as the order placement commands.
SYNTAX
strategy.cancel(id) → void
ARGUMENTS
id (series string) The identifier of the unfilled order to cancel.
EXAMPLE
//@version=6
strategy(title = "Order cancellation demo")

conditionForBuy = open > high[1]
if conditionForBuy
    strategy.entry("Long", strategy.long, 1, limit = low) // Enter long using limit order at low price of current bar if `conditionForBuy` is `true`.
if not conditionForBuy
    strategy.cancel("Long") // Cancel the entry order with name "Long" if `conditionForBuy` is `false`.
strategy.cancel_all()
Cancels all pending or unfilled orders, regardless of their identifiers.
This command is most useful when working with price-based orders (e.g., limit orders). Calls to this command can also cancel market orders, but only if they execute on the same ticks as the order placement commands.
SYNTAX
strategy.cancel_all() → void
EXAMPLE
//@version=6
strategy(title = "Cancel all orders demo")
conditionForBuy1 = open > high[1]
if conditionForBuy1
    strategy.entry("Long entry 1", strategy.long, 1, limit = low) // Enter long using a limit order if `conditionForBuy1` is `true`.
conditionForBuy2 = conditionForBuy1 and open[1] > high[2]
float lowest2 = ta.lowest(low, 2)
if conditionForBuy2
    strategy.entry("Long entry 2", strategy.long, 1, limit = lowest2) // Enter long using a limit order if `conditionForBuy2` is `true`.
conditionForStopTrading = open < lowest2
if conditionForStopTrading
    strategy.cancel_all() // Cancel both limit orders if `conditionForStopTrading` is `true`.
strategy.close()
Creates an order to exit from the part of a position opened by entry orders with a specific identifier. If multiple entries in the position share the same ID, the orders from this command apply to all those entries, starting from the first open trade, when its calls use that ID as the id argument.
This command always generates market orders. To exit from a position using price-based orders (e.g., stop-loss orders), use the strategy.exit command.
SYNTAX
strategy.close(id, comment, qty, qty_percent, alert_message, immediately, disable_alert) → void
ARGUMENTS
id (series string) The entry identifier of the open trades to close.
comment (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the automatically generated exit identifier. The default is an empty string.
qty (series int/float) Optional. The number of contracts/lots/shares/units to close when an exit order fills. If specified, the command uses this value instead of qty_percent to determine the order size. The default is na, which means the order size depends on the qty_percent value.
qty_percent (series int/float) Optional. A value between 0 and 100 representing the percentage of the open trade quantity to close when an exit order fills. The percentage calculation depends on the total size of the open trades with the id entry identifier. The command ignores this parameter if the qty value is not na. The default is 100.
alert_message (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. The default is an empty string.
immediately (series bool) Optional. If true, the closing order executes on the same tick when the strategy places it, ignoring the strategy properties that restrict execution to the opening tick of the following bar. The default is false.
disable_alert (series bool) Optional. If true when the command creates an order, the strategy does not trigger an alert when that order fills. This parameter accepts a "series" value, meaning users can control which orders trigger alerts when they execute. The default is false.
EXAMPLE
//@version=6
strategy("Partial close strategy")

// Calculate a 14-bar and 28-bar moving average of `close` prices.
float sma14 = ta.sma(close, 14)
float sma28 = ta.sma(close, 28)

// Place a market order to enter a long position when `sma14` crosses over `sma28`.
if ta.crossover(sma14, sma28)
    strategy.entry("My Long Entry ID", strategy.long)

// Place a market order to close the long trade when `sma14` crosses under `sma28`. 
if ta.crossunder(sma14, sma28)
    strategy.close("My Long Entry ID", "50% market close", qty_percent = 50)

// Plot the position size.
plot(strategy.position_size)
REMARKS
When a position consists of several open trades and the close_entries_rule in the strategy declaration statement is "FIFO" (default), a strategy.close call exits from the position starting with the first open trade. This behavior applies even if the id value is the entry ID of different open trades. However, in that case, the maximum exit order size still depends on the trades opened by orders with the id identifier. For more information, see this section of our User Manual.
strategy.close_all()2 overloads
Creates an order to close an open position completely, regardless of the identifiers of the entry orders that opened or added to it.
This command always generates market orders. To exit from a position using price-based orders (e.g., stop-loss orders), use the strategy.exit command.
SYNTAX & OVERLOADS
strategy.close_all(comment, alert_message) → void
strategy.close_all(comment, alert_message, immediately, disable_alert) → void
ARGUMENTS
comment (series string) Optional. Additional notes on the filled order. If the value is not an empty string, the Strategy Tester and the chart show this text for the order instead of the automatically generated exit identifier. The default is an empty string.
alert_message (series string) Optional. Custom text for the alert that fires when an order fills. If the "Message" field of the "Create Alert" dialog box contains the {{strategy.order.alert_message}} placeholder, the alert message replaces the placeholder with this text. The default is an empty string.
EXAMPLE
//@version=6
strategy("Multi-entry close strategy")

// Calculate a 14-bar and 28-bar moving average of `close` prices.
float sma14 = ta.sma(close, 14)
float sma28 = ta.sma(close, 28)

// Place a market order to enter a long trade every time `sma14` crosses over `sma28`.
if ta.crossover(sma14, sma28)
    strategy.order("My Long Entry ID " + str.tostring(strategy.opentrades), strategy.long)

// Place a market order to close the entire position every 500 bars. 
if bar_index % 500 == 0
    strategy.close_all()

// Plot the position size.
plot(strategy.position_size)
strategy.closedtrades.commission()
Returns the sum of entry and exit fees paid in the closed trade, expressed in strategy.account_currency.
SYNTAX
strategy.closedtrades.commission(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.commission` Example", commission_type = strategy.commission.percent, commission_value = 0.1)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Plot total fees for the latest closed trade.
plot(strategy.closedtrades.commission(strategy.closedtrades - 1))
SEE ALSO
strategystrategy.opentrades.commission
strategy.closedtrades.entry_bar_index()
Returns the bar_index of the closed trade's entry.
SYNTAX
strategy.closedtrades.entry_bar_index(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.entry_bar_index Example")
// Enter long trades on three rising bars; exit on two falling bars.
if ta.rising(close, 3)
    strategy.entry("Long", strategy.long)
if ta.falling(close, 2)
    strategy.close("Long")
// Function that calculates the average amount of bars in a trade.
avgBarsPerTrade() =>
    sumBarsPerTrade = 0
    for tradeNo = 0 to strategy.closedtrades - 1
        // Loop through all closed trades, starting with the oldest.
        sumBarsPerTrade += strategy.closedtrades.exit_bar_index(tradeNo) - strategy.closedtrades.entry_bar_index(tradeNo) + 1
    result = nz(sumBarsPerTrade / strategy.closedtrades)
plot(avgBarsPerTrade())
SEE ALSO
strategy.closedtrades.exit_bar_indexstrategy.opentrades.entry_bar_index
strategy.closedtrades.entry_comment()
Returns the comment message of the closed trade's entry, or na if there is no entry with this trade_num.
SYNTAX
strategy.closedtrades.entry_comment(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.entry_comment()` Example", overlay = true)

stopPrice = open * 1.01

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))

if (longCondition)
    strategy.entry("Long", strategy.long, stop = stopPrice, comment = str.tostring(stopPrice, "#.####"))
    strategy.exit("EXIT", trail_points = 1000, trail_offset = 0)

var testTable = table.new(position.top_right, 1, 3, color.orange, border_width = 1)

if barstate.islastconfirmedhistory or barstate.isrealtime
    table.cell(testTable, 0, 0, 'Last closed trade:')
    table.cell(testTable, 0, 1, "Order stop price value: " + strategy.closedtrades.entry_comment(strategy.closedtrades - 1))
    table.cell(testTable, 0, 2, "Actual Entry Price: " + str.tostring(strategy.closedtrades.entry_price(strategy.closedtrades - 1)))
SEE ALSO
strategystrategy.entrystrategy.closedtrades
strategy.closedtrades.entry_id()
Returns the id of the closed trade's entry.
SYNTAX
strategy.closedtrades.entry_id(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.entry_id Example", overlay = true)

// Enter a short position and close at the previous to last bar.
if bar_index == 1
    strategy.entry("Short at bar #" + str.tostring(bar_index), strategy.short)
if bar_index == last_bar_index - 2
    strategy.close_all()
    
// Display ID of the last entry position.
if barstate.islastconfirmedhistory
    label.new(last_bar_index, high, "Last Entry ID is: " + strategy.closedtrades.entry_id(strategy.closedtrades - 1))
RETURNS
Returns the id of the closed trade's entry.
REMARKS
The function returns na if trade_num is not in the range: 0 to strategy.closedtrades-1.
SEE ALSO
strategy.closedtrades.entry_bar_indexstrategy.closedtrades.entry_pricestrategy.closedtrades.entry_time
strategy.closedtrades.entry_price()
Returns the price of the closed trade's entry.
SYNTAX
strategy.closedtrades.entry_price(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.entry_price Example 1")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Return the entry price for the latest entry.
entryPrice = strategy.closedtrades.entry_price(strategy.closedtrades - 1)

plot(entryPrice, "Long entry price")
EXAMPLE
// Calculates the average profit percentage for all closed trades.
//@version=6
strategy("strategy.closedtrades.entry_price Example 2")

// Strategy calls to create single short and long trades
if bar_index == last_bar_index - 15
    strategy.entry("Long Entry", strategy.long)
else if bar_index == last_bar_index - 10
    strategy.close("Long Entry")
    strategy.entry("Short", strategy.short)
else if bar_index == last_bar_index - 5
    strategy.close("Short")

// Calculate profit for both closed trades.
profitPct = 0.0
for tradeNo = 0 to strategy.closedtrades - 1
    entryP = strategy.closedtrades.entry_price(tradeNo)
    exitP = strategy.closedtrades.exit_price(tradeNo)
    profitPct += (exitP - entryP) / entryP * strategy.closedtrades.size(tradeNo) * 100
    
// Calculate average profit percent for both closed trades.
avgProfitPct = nz(profitPct / strategy.closedtrades)

plot(avgProfitPct)
SEE ALSO
strategy.closedtrades.entry_pricestrategy.closedtrades.exit_pricestrategy.closedtrades.sizestrategy.closedtrades
strategy.closedtrades.entry_time()
Returns the UNIX time of the closed trade's entry, expressed in milliseconds..
SYNTAX
strategy.closedtrades.entry_time(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.entry_time Example", overlay = true)

// Enter long trades on three rising bars; exit on two falling bars.
if ta.rising(close, 3)
    strategy.entry("Long", strategy.long)
if ta.falling(close, 2)
    strategy.close("Long")

// Calculate the average trade duration 
avgTradeDuration() =>
    sumTradeDuration = 0
    for i = 0 to strategy.closedtrades - 1
        sumTradeDuration += strategy.closedtrades.exit_time(i) - strategy.closedtrades.entry_time(i)
    result = nz(sumTradeDuration / strategy.closedtrades)

// Display average duration converted to seconds and formatted using 2 decimal points
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(avgTradeDuration() / 1000, "#.##") + " seconds")
SEE ALSO
strategy.opentrades.entry_timestrategy.closedtrades.exit_timetime
strategy.closedtrades.exit_bar_index()
Returns the bar_index of the closed trade's exit.
SYNTAX
strategy.closedtrades.exit_bar_index(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.exit_bar_index Example 1")

// Strategy calls to place a single short trade. We enter the trade at the first bar and exit the trade at 10 bars before the last chart bar.
if bar_index == 0
    strategy.entry("Short", strategy.short)
if bar_index == last_bar_index - 10
    strategy.close("Short")

// Calculate the amount of bars since the last closed trade.
barsSinceClosed = strategy.closedtrades > 0 ? bar_index - strategy.closedtrades.exit_bar_index(strategy.closedtrades - 1) : na

plot(barsSinceClosed, "Bars since last closed trade")
EXAMPLE
// Calculates the average amount of bars per trade.
//@version=6
strategy("strategy.closedtrades.exit_bar_index Example 2")

// Enter long trades on three rising bars; exit on two falling bars.
if ta.rising(close, 3)
    strategy.entry("Long", strategy.long)
if ta.falling(close, 2)
    strategy.close("Long")

// Function that calculates the average amount of bars per trade.
avgBarsPerTrade() =>
    sumBarsPerTrade = 0
    for tradeNo = 0 to strategy.closedtrades - 1
        // Loop through all closed trades, starting with the oldest.
        sumBarsPerTrade += strategy.closedtrades.exit_bar_index(tradeNo) - strategy.closedtrades.entry_bar_index(tradeNo) + 1
    result = nz(sumBarsPerTrade / strategy.closedtrades)

plot(avgBarsPerTrade())
SEE ALSO
bar_indexlast_bar_index
strategy.closedtrades.exit_comment()
Returns the comment message of the closed trade's exit, or na if there is no entry with this trade_num.
SYNTAX
strategy.closedtrades.exit_comment(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.exit_comment()` Example", overlay = true)

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit", stop = open * 0.95, limit = close * 1.05, trail_points = 100, trail_offset = 0, comment_profit = "TP", comment_loss = "SL", comment_trailing = "TRAIL")

exitStats() =>
    int slCount = 0
    int tpCount = 0
    int trailCount = 0
    
    if strategy.closedtrades > 0
        for i = 0 to strategy.closedtrades - 1
            switch strategy.closedtrades.exit_comment(i)
                "TP"    => tpCount    += 1
                "SL"    => slCount    += 1
                "TRAIL" => trailCount += 1
    [slCount, tpCount, trailCount]

var testTable = table.new(position.top_right, 1, 4, color.orange, border_width = 1)

if barstate.islastconfirmedhistory
    [slCount, tpCount, trailCount] = exitStats()
    table.cell(testTable, 0, 0, "Closed trades (" + str.tostring(strategy.closedtrades) +") stats:")
    table.cell(testTable, 0, 1, "Stop Loss: " + str.tostring(slCount))
    table.cell(testTable, 0, 2, "Take Profit: " + str.tostring(tpCount))
    table.cell(testTable, 0, 3, "Trailing Stop: " + str.tostring(trailCount))
SEE ALSO
strategystrategy.exitstrategy.closestrategy.closedtrades
strategy.closedtrades.exit_id()
Returns the id of the closed trade's exit.
SYNTAX
strategy.closedtrades.exit_id(trade_num) → series string
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.exit_id Example", overlay = true)

// Strategy calls to create single short and long trades
if bar_index == last_bar_index - 15
    strategy.entry("Long Entry", strategy.long)
else if bar_index == last_bar_index - 10
    strategy.entry("Short Entry", strategy.short)
    
// When a new open trade is detected then we create the exit strategy corresponding with the matching entry id
// We detect the correct entry id by determining if a position is long or short based on the position quantity
if ta.change(strategy.opentrades) != 0
    posSign = strategy.opentrades.size(strategy.opentrades - 1)
    strategy.exit(posSign > 0 ? "SL Long Exit" : "SL Short Exit", strategy.opentrades.entry_id(strategy.opentrades - 1), stop = posSign > 0 ? high - ta.tr : low + ta.tr)

// When a new closed trade is detected then we place a label above the bar with the exit info
if ta.change(strategy.closedtrades) != 0
    msg = "Trade closed by: " + strategy.closedtrades.exit_id(strategy.closedtrades - 1)
    label.new(bar_index, high + (3 * ta.tr), msg)
RETURNS
Returns the id of the closed trade's exit.
REMARKS
The function returns na if trade_num is not in the range: 0 to strategy.closedtrades-1.
SEE ALSO
strategy.closedtrades.exit_bar_indexstrategy.closedtrades.exit_pricestrategy.closedtrades.exit_time
strategy.closedtrades.exit_price()
Returns the price of the closed trade's exit.
SYNTAX
strategy.closedtrades.exit_price(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.exit_price Example 1")

// We are creating a long trade every 5 bars
if bar_index % 5 == 0
    strategy.entry("Long", strategy.long)
strategy.close("Long")

// Return the exit price from the latest closed trade.
exitPrice = strategy.closedtrades.exit_price(strategy.closedtrades - 1)

plot(exitPrice, "Long exit price")
EXAMPLE
// Calculates the average profit percentage for all closed trades.
//@version=6
strategy("strategy.closedtrades.exit_price Example 2")

// Strategy calls to create single short and long trades.
if bar_index == last_bar_index - 15
    strategy.entry("Long Entry", strategy.long)
else if bar_index == last_bar_index - 10
    strategy.close("Long Entry")
    strategy.entry("Short", strategy.short)
else if bar_index == last_bar_index - 5
    strategy.close("Short")

// Calculate profit for both closed trades.
profitPct = 0.0
for tradeNo = 0 to strategy.closedtrades - 1
    entryP = strategy.closedtrades.entry_price(tradeNo)
    exitP = strategy.closedtrades.exit_price(tradeNo)
    profitPct += (exitP - entryP) / entryP * strategy.closedtrades.size(tradeNo) * 100
    
// Calculate average profit percent for both closed trades.
avgProfitPct = nz(profitPct / strategy.closedtrades)

plot(avgProfitPct)
SEE ALSO
strategy.closedtrades.entry_price
strategy.closedtrades.exit_time()
Returns the UNIX time of the closed trade's exit, expressed in milliseconds.
SYNTAX
strategy.closedtrades.exit_time(trade_num) → series int
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("strategy.closedtrades.exit_time Example 1")

// Enter long trades on three rising bars; exit on two falling bars.
if ta.rising(close, 3)
    strategy.entry("Long", strategy.long)
if ta.falling(close, 2)
    strategy.close("Long")

// Calculate the average trade duration. 
avgTradeDuration() =>
    sumTradeDuration = 0
    for i = 0 to strategy.closedtrades - 1
        sumTradeDuration += strategy.closedtrades.exit_time(i) - strategy.closedtrades.entry_time(i)
    result = nz(sumTradeDuration / strategy.closedtrades)

// Display average duration converted to seconds and formatted using 2 decimal points.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(avgTradeDuration() / 1000, "#.##") + " seconds")
EXAMPLE
// Reopens a closed trade after X seconds.
//@version=6
strategy("strategy.closedtrades.exit_time Example 2")

// Strategy calls to emulate a single long trade at the first bar.
if bar_index == 0
    strategy.entry("Long", strategy.long)

reopenPositionAfter(timeSec) =>
    if strategy.closedtrades > 0
        if time - strategy.closedtrades.exit_time(strategy.closedtrades - 1) >= timeSec * 1000
            strategy.entry("Long", strategy.long)

// Reopen last closed position after 120 sec.                
reopenPositionAfter(120)

if ta.change(strategy.opentrades) != 0
    strategy.exit("Long", stop = low * 0.9, profit = high * 2.5)
SEE ALSO
strategy.closedtrades.entry_time
strategy.closedtrades.max_drawdown()
Returns the maximum drawdown of the closed trade, i.e., the maximum possible loss during the trade, expressed in strategy.account_currency.
SYNTAX
strategy.closedtrades.max_drawdown(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.max_drawdown` Example")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Get the biggest max trade drawdown value from all of the closed trades.
maxTradeDrawDown() =>
    maxDrawdown = 0.0
    for tradeNo = 0 to strategy.closedtrades - 1
        maxDrawdown := math.max(maxDrawdown, strategy.closedtrades.max_drawdown(tradeNo))
    result = maxDrawdown

plot(maxTradeDrawDown(), "Biggest max drawdown")
REMARKS
The function returns na if trade_num is not in the range: 0 to strategy.closedtrades - 1.
SEE ALSO
strategy.opentrades.max_drawdownstrategy.max_drawdown
strategy.closedtrades.max_drawdown_percent()
Returns the maximum drawdown of the closed trade, i.e., the maximum possible loss during the trade, expressed as a percentage and calculated by formula: Lowest Value During Trade / (Entry Price x Quantity) * 100.
SYNTAX
strategy.closedtrades.max_drawdown_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.closedtrades.max_drawdownstrategy.max_drawdown
strategy.closedtrades.max_runup()
Returns the maximum run up of the closed trade, i.e., the maximum possible profit during the trade, expressed in strategy.account_currency.
SYNTAX
strategy.closedtrades.max_runup(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.max_runup` Example")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Get the biggest max trade runup value from all of the closed trades.
maxTradeRunUp() =>
    maxRunup = 0.0
    for tradeNo = 0 to strategy.closedtrades - 1
        maxRunup := math.max(maxRunup, strategy.closedtrades.max_runup(tradeNo))
    result = maxRunup

plot(maxTradeRunUp(), "Max trade runup")
SEE ALSO
strategy.opentrades.max_runupstrategy.max_runup
strategy.closedtrades.max_runup_percent()
Returns the maximum run-up of the closed trade, i.e., the maximum possible profit during the trade, expressed as a percentage and calculated by formula: Highest Value During Trade / (Entry Price x Quantity) * 100.
SYNTAX
strategy.closedtrades.max_runup_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.closedtrades.max_runupstrategy.max_runup
strategy.closedtrades.profit()
Returns the profit/loss of the closed trade, expressed in strategy.account_currency. Losses are expressed as negative values.
SYNTAX
strategy.closedtrades.profit(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.profit` Example")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")

// Calculate average gross profit by adding the difference between gross profit and commission.
avgGrossProfit() =>
    sumGrossProfit = 0.0
    for tradeNo = 0 to strategy.closedtrades - 1
        sumGrossProfit += strategy.closedtrades.profit(tradeNo) - strategy.closedtrades.commission(tradeNo)
    result = nz(sumGrossProfit / strategy.closedtrades)
    
plot(avgGrossProfit(), "Average gross profit")
SEE ALSO
strategy.opentrades.profitstrategy.closedtrades.commission
strategy.closedtrades.profit_percent()
Returns the profit/loss value of the closed trade, expressed as a percentage. Losses are expressed as negative values.
SYNTAX
strategy.closedtrades.profit_percent(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
SEE ALSO
strategy.closedtrades.profit
strategy.closedtrades.size()
Returns the direction and the number of contracts traded in the closed trade. If the value is > 0, the market position was long. If the value is < 0, the market position was short.
SYNTAX
strategy.closedtrades.size(trade_num) → series float
ARGUMENTS
trade_num (series int) The trade number of the closed trade. The number of the first trade is zero.
EXAMPLE
//@version=6
strategy("`strategy.closedtrades.size` Example 1")

// We calculate the max amt of shares we can buy.
amtShares = math.floor(strategy.equity / close)
// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long, qty = amtShares)
if bar_index % 20 == 0
    strategy.close("Long")

// Plot the number of contracts traded in the last closed trade.     
plot(strategy.closedtrades.size(strategy.closedtrades - 1), "Number of contracts traded")
EXAMPLE
// Calculates the average profit percentage for all closed trades.
//@version=6
strategy("`strategy.closedtrades.size` Example 2")

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long)
if bar_index % 20 == 0
    strategy.close("Long")


// Calculate profit for both closed trades.
profitPct = 0.0
for tradeNo = 0 to strategy.closedtrades - 1
    entryP = strategy.closedtrades.entry_price(tradeNo)
    exitP = strategy.closedtrades.exit_price(tradeNo)
    profitPct += (exitP - entryP) / entryP * strategy.closedtrades.size(tradeNo) * 100
    
// Calculate average profit percent for both closed trades.
avgProfitPct = nz(profitPct / strategy.closedtrades)

plot(avgProfitPct)
SEE ALSO
strategy.opentrades.sizestrategy.position_sizestrategy.closedtradesstrategy.opentrades
strategy.convert_to_account()
Converts the value from the currency that the symbol on the chart is traded in (syminfo.currency) to the currency used by the strategy (strategy.account_currency).
SYNTAX
strategy.convert_to_account(value) → series float
ARGUMENTS
value (series int/float) The value to be converted.
EXAMPLE
//@version=6
strategy("`strategy.convert_to_account` Example 1", currency = currency.EUR)

plot(close, "Close price using default currency")
plot(strategy.convert_to_account(close), "Close price converted to strategy currency")
EXAMPLE
// Calculates the "Buy and hold return" using your account's currency.
//@version=6
strategy("`strategy.convert_to_account` Example 2", currency = currency.EUR)

dateInput = input.time(timestamp("20 Jul 2021 00:00 +0300"), "From Date", confirm = true)

buyAndHoldReturnPct(fromDate) =>
    if time >= fromDate
        money = close * syminfo.pointvalue
        var initialBal = strategy.convert_to_account(money)
        (strategy.convert_to_account(money) - initialBal) / initialBal * 100
        
plot(buyAndHoldReturnPct(dateInput))
SEE ALSO
strategystrategy.convert_to_symbol
strategy.convert_to_symbol()
Converts the value from the currency used by the strategy (strategy.account_currency) to the currency that the symbol on the chart is traded in (syminfo.currency).
SYNTAX
strategy.convert_to_symbol(value) → series float
ARGUMENTS
value (series int/float) The value to be converted.
EXAMPLE
//@version=6
strategy("`strategy.convert_to_symbol` Example", currency = currency.EUR)

// Calculate the max qty we can buy using current chart's currency.
calcContracts(accountMoney) =>
    math.floor(strategy.convert_to_symbol(accountMoney) / syminfo.pointvalue / close)

// Return max qty we can buy using 300 euros
qt = calcContracts(300)

// Strategy calls to enter long trades every 15 bars and exit long trades every 20 bars using our custom qty.
if bar_index % 15 == 0
    strategy.entry("Long", strategy.long, qty = qt)
if bar_index % 20 == 0
    strategy.close("Long")
SEE ALSO
strategystrategy.convert_to_account
strategy.default_entry_qty()
Calculates the default quantity, in units, of an entry order from strategy.entry or strategy.order if it were to fill at the specified fill_price value. The calculation depends on several strategy properties, including default_qty_type, default_qty_value, currency, and other parameters in the strategy function and their representation in the "Properties" tab of the strategy's settings.
SYNTAX
strategy.default_entry_qty(fill_price) → series float
ARGUMENTS
fill_price (series int/float) The fill price for which to calculate the default order quantity.
EXAMPLE
//@version=6
strategy("Supertrend Strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 15)

//@variable The length of the ATR calculation.
atrPeriod = input(10, "ATR Length")
//@variable The ATR multiplier.
factor = input.float(3.0, "Factor", step = 0.01)
//@variable The tick offset of the stop order.
stopOffsetInput = input.int(100, "Tick offset for entry stop")

// Get the direction of the SuperTrend.
[_, direction] = ta.supertrend(factor, atrPeriod)

if ta.change(direction) < 0
    //@variable The stop price of the entry order.
    stopPrice = close + syminfo.mintick * stopOffsetInput
    //@variable The expected default fill quantity at the `stopPrice`. This value may not reflect actual qty of the filled order, because fill price may be different.
    calculatedQty = strategy.default_entry_qty(stopPrice)
    strategy.entry("My Long Entry Id", strategy.long, stop = stopPrice)
    label.new(bar_index, stopPrice, str.format("Stop set at {0}\nExpected qty at {0}: {1}", math.round_to_mintick(stopPrice), calculatedQty))

if ta.change(direction) > 0
    strategy.close_all()
REMARKS
This function does not consider open positions simulated by a strategy. For example, if a strategy script has an open position from a long order with a qty of 10 units, using the strategy.entry function to simulate a short order with a qty of 5 will prompt the script to sell 15 units to reverse the position. This function will still return 5 in such a case since it doesn't consider an open trade.
This value represents the default calculated quantity of an order.
Order placement commands can override the default value by explicitly passing a new qty value in the function call.
strategy.entry()
Creates a new order to open or add to a position. If an unfilled order with the same id exists, a call to this command modifies that order.
The resulting order's type depends on the limit and stop parameters. If the call does not contain limit or stop arguments, it creates a market order that executes on the next tick. If the call specifies a limit value but no stop value, it places a limit order that executes after the market price reaches the limit value or a better price (lower for buy orders and higher for sell orders). If the call specifies a stop value but no limit value, it places a stop order that executes after the market price reaches the stop value or a worse price (higher for buy orders and lower for sell orders). If the call contains limit and stop arguments, it creates a stop-limit order, which generates a limit order at the limit price only after the market price reaches the stop value or a worse price.
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
