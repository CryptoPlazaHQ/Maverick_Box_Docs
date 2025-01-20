SEE ALSO
floatintboolstringlinelabel
color.b()4 overloads
Retrieves the value of the color's blue component.
SYNTAX & OVERLOADS
color.b(color) → const float
color.b(color) → input float
color.b(color) → simple float
color.b(color) → series float
ARGUMENTS
color (const color) Color.
EXAMPLE
//@version=6
indicator("color.b", overlay=true)
plot(color.b(color.blue))
RETURNS
The value (0 to 255) of the color's blue component.
color.from_gradient()
Based on the relative position of value in the bottom_value to top_value range, the function returns a color from the gradient defined by bottom_color to top_color.
SYNTAX
color.from_gradient(value, bottom_value, top_value, bottom_color, top_color) → series color
ARGUMENTS
value (series int/float) Value to calculate the position-dependent color.
bottom_value (series int/float) Bottom position value corresponding to bottom_color.
top_value (series int/float) Top position value corresponding to top_color.
bottom_color (series color) Bottom position color.
top_color (series color) Top position color.
EXAMPLE
//@version=6
indicator("color.from_gradient", overlay=true)
color1 = color.from_gradient(close, low, high, color.yellow, color.lime)
color2 = color.from_gradient(ta.rsi(close, 7), 0, 100, color.rgb(255, 0, 0), color.rgb(0, 255, 0, 50))
plot(close, color=color1)
plot(ta.rsi(close,7), color=color2)
RETURNS
A color calculated from the linear gradient between bottom_color to top_color.
REMARKS
Using this function will have an impact on the colors displayed in the script's "Settings/Style" tab. See the User Manual for more information.
color.g()4 overloads
Retrieves the value of the color's green component.
SYNTAX & OVERLOADS
color.g(color) → const float
color.g(color) → input float
color.g(color) → simple float
color.g(color) → series float
ARGUMENTS
color (const color) Color.
EXAMPLE
//@version=6
indicator("color.g", overlay=true)
plot(color.g(color.green))
RETURNS
The value (0 to 255) of the color's green component.
color.new()4 overloads
Function color applies the specified transparency to the given color.
SYNTAX & OVERLOADS
color.new(color, transp) → const color
color.new(color, transp) → input color
color.new(color, transp) → simple color
color.new(color, transp) → series color
ARGUMENTS
color (const color) Color to apply transparency to.
transp (const int/float) Possible values are from 0 (not transparent) to 100 (invisible).
EXAMPLE
//@version=6
indicator("color.new", overlay=true)
plot(close, color=color.new(color.red, 50))
RETURNS
Color with specified transparency.
REMARKS
Using arguments that are not constants (e.g., 'simple', 'input' or 'series') will have an impact on the colors displayed in the script's "Settings/Style" tab. See the User Manual for more information.
color.r()4 overloads
Retrieves the value of the color's red component.
SYNTAX & OVERLOADS
color.r(color) → const float
color.r(color) → input float
color.r(color) → simple float
color.r(color) → series float
ARGUMENTS
color (const color) Color.
EXAMPLE
//@version=6
indicator("color.r", overlay=true)
plot(color.r(color.red))
RETURNS
The value (0 to 255) of the color's red component.
color.rgb()4 overloads
Creates a new color with transparency using the RGB color model.
SYNTAX & OVERLOADS
color.rgb(red, green, blue, transp) → const color
color.rgb(red, green, blue, transp) → input color
color.rgb(red, green, blue, transp) → simple color
color.rgb(red, green, blue, transp) → series color
ARGUMENTS
red (const int/float) Red color component. Possible values are from 0 to 255.
green (const int/float) Green color component. Possible values are from 0 to 255.
blue (const int/float) Blue color component. Possible values are from 0 to 255.
transp (const int/float) Optional. Color transparency. Possible values are from 0 (opaque) to 100 (invisible). Default value is 0.
EXAMPLE
//@version=6
indicator("color.rgb", overlay=true)
plot(close, color=color.rgb(255, 0, 0, 50))
RETURNS
Color with specified transparency.
REMARKS
Using arguments that are not constants (e.g., 'simple', 'input' or 'series') will have an impact on the colors displayed in the script's "Settings/Style" tab. See the User Manual for more information.
color.t()4 overloads
Retrieves the color's transparency.
SYNTAX & OVERLOADS
color.t(color) → const float
color.t(color) → input float
color.t(color) → simple float
color.t(color) → series float
ARGUMENTS
color (const color) Color.
EXAMPLE
//@version=6
indicator("color.t", overlay=true)
plot(color.t(color.new(color.red, 50)))
RETURNS
The value (0-100) of the color's transparency.
dayofmonth()2 overloads
SYNTAX & OVERLOADS
dayofmonth(time) → series int
dayofmonth(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Day of month (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
Note that this function returns the day based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00 UTC-4) this value can be lower by 1 than the day of the trading day.
SEE ALSO
dayofmonthtimeyearmonthdayofweekhourminutesecond
dayofweek()2 overloads
SYNTAX & OVERLOADS
dayofweek(time) → series int
dayofweek(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Day of week (in exchange timezone) for provided UNIX time.
REMARKS
Note that this function returns the day based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the day of the trading day.
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
dayofweektimeyearmonthdayofmonthhourminutesecond
fill()3 overloads
Fills background between two plots or hlines with a given color.
SYNTAX & OVERLOADS
fill(hline1, hline2, color, title, editable, fillgaps, display) → void
fill(plot1, plot2, color, title, editable, show_last, fillgaps, display) → void
fill(plot1, plot2, top_value, bottom_value, top_color, bottom_color, title, display, fillgaps, editable) → void
ARGUMENTS
hline1 (hline) The first hline object. Required argument.
hline2 (hline) The second hline object. Required argument.
color (series color) Color of the background fill. You can use constants like 'color=color.red' or 'color=#ff001a' as well as complex expressions like 'color = close >= open ? color.green : color.red'. Optional argument.
title (const string) Title of the created fill object. Optional argument.
editable (const bool) If true then fill style will be editable in Format dialog. Default is true.
fillgaps (const bool) Controls continuing fills on gaps, i.e., when one of the plot() calls returns an na value. When true, the last fill will continue on gaps. The default is false.
display (input plot_simple_display) Controls where the fill is displayed. Possible values are: display.none, display.all. Default is display.all.
Fill between two horizontal lines
EXAMPLE
//@version=6
indicator("Fill between hlines", overlay = false)
h1 = hline(20)
h2 = hline(10)
fill(h1, h2, color = color.new(color.blue, 90))
Fill between two plots
EXAMPLE
//@version=6
indicator("Fill between plots", overlay = true)
p1 = plot(open)
p2 = plot(close)
fill(p1, p2, color = color.new(color.green, 90))
Gradient fill between two horizontal lines
EXAMPLE
//@version=6
indicator("Gradient Fill between hlines", overlay = false)
topVal = input.int(100)
botVal = input.int(0)
topCol = input.color(color.red)
botCol = input.color(color.blue)
topLine = hline(100, color = topCol, linestyle = hline.style_solid)
botLine = hline(0,   color = botCol, linestyle = hline.style_solid)
fill(topLine, botLine, topVal, botVal, topCol, botCol)
SEE ALSO
plotbarcolorbgcolorhlinecolor.new
fixnan()3 overloads
For a given series replaces NaN values with previous nearest non-NaN value.
SYNTAX & OVERLOADS
fixnan(source) → series color
fixnan(source) → series int
fixnan(source) → series float
ARGUMENTS
source (series color) Source used for the calculation.
RETURNS
Series without na gaps.
SEE ALSO
nananz
float()4 overloads
Casts na to float
SYNTAX & OVERLOADS
float(x) → const float
float(x) → input float
float(x) → simple float
float(x) → series float
ARGUMENTS
x (const int/float) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to float.
SEE ALSO
intboolcolorstringlinelabel
hline()
Renders a horizontal line at a given fixed price level.
SYNTAX
hline(price, title, color, linestyle, linewidth, editable, display) → hline
ARGUMENTS
price (input int/float) Price value at which the object will be rendered. Required argument.
title (const string) Title of the object.
color (input color) Color of the rendered line. Must be a constant value (not an expression). Optional argument.
linestyle (input hline_style) Style of the rendered line. Possible values are: hline.style_solid, hline.style_dotted, hline.style_dashed. Optional argument.
linewidth (input int) Width of the rendered line. Default value is 1.
editable (const bool) If true then hline style will be editable in Format dialog. Default is true.
display (input plot_simple_display) Controls where the hline is displayed. Possible values are: display.none, display.all. Default is display.all.
EXAMPLE
//@version=6
indicator("input.hline", overlay=true)
hline(3.14, title='Pi', color=color.blue, linestyle=hline.style_dotted, linewidth=2)

// You may fill the background between any two hlines with a fill() function:
h1 = hline(20)
h2 = hline(10)
fill(h1, h2, color=color.new(color.green, 90))
RETURNS
An hline object, that can be used in fill
SEE ALSO
fill
hour()2 overloads
SYNTAX & OVERLOADS
hour(time) → series int
hour(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Hour (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
hourtimeyearmonthdayofmonthdayofweekminutesecond
indicator()
This declaration statement designates the script as an indicator and sets a number of indicator-related properties.
SYNTAX
indicator(title, shorttitle, overlay, format, precision, scale, max_bars_back, timeframe, timeframe_gaps, explicit_plot_zorder, max_lines_count, max_labels_count, max_boxes_count, calc_bars_count, max_polylines_count, dynamic_requests, behind_chart) → void
ARGUMENTS
title (const string) The title of the script. It is displayed on the chart when no shorttitle argument is used, and becomes the publication's default title when publishing the script.
shorttitle (const string) The script's display name on charts. If specified, it will replace the title argument in most chart-related windows. Optional. The default is the argument used for title.
overlay (const bool) If true, the indicator will be displayed over the chart. If false, it will be added in a separate pane. Optional. The default is false.
format (const string) Specifies the formatting of the script's displayed values. Possible values: format.inherit, format.price, format.volume, format.percent. Optional. The default is format.inherit.
precision (const int) Specifies the number of digits after the floating point of the script's displayed values. Must be a non-negative integer no greater than 16. If format is set to format.inherit and precision is specified, the format will instead be set to format.price. When the function's format parameter uses format.volume, the precision parameter will not affect the result, as the decimal precision rules defined by format.volume supersede other precision settings. Optional. The default is inherited from the precision of the chart's symbol.
scale (const scale_type) The price scale used. Possible values: scale.right, scale.left, scale.none. The scale.none value can only be applied in combination with overlay = true. Optional. By default, the script uses the same scale as the chart.
max_bars_back (const int) The length of the historical buffer the script keeps for every variable and function, which determines how many past values can be referenced using the [] history-referencing operator. The required buffer size is automatically detected by the Pine Script® runtime. Using this parameter is only necessary when a runtime error occurs because automatic detection fails. More information on the underlying mechanics of the historical buffer can be found in our Help Center. Optional. The default is 0.
timeframe (const string) Adds multi-timeframe functionality to simple scripts. When specified, a "Timeframe" field will be included in the "Calculation" section of the script's "Settings/Inputs" tab. The field's default value will be the argument supplied, whose format must conform to timeframe string specifications. To specify the chart's timeframe, use an empty string or the timeframe.period variable. The parameter cannot be used with scripts using Pine Script® drawings. Optional. The default is timeframe.period.
timeframe_gaps (const bool) Specifies how the indicator's values are displayed on chart bars when the timeframe is higher than the chart's. If true, a value only appears on a chart bar when the higher timeframe value becomes available, otherwise na is returned (thus a "gap" occurs). With false, what would otherwise be gaps are filled with the latest known value returned, avoiding na values. When specified, a "Wait for timeframe closes" checkbox will be included in the "Calculation" section of the script's "Settings/Inputs" tab. Optional. The default is true.
explicit_plot_zorder (const bool) Specifies the order in which the script's plots, fills, and hlines are rendered. If true, plots are drawn in the order in which they appear in the script's code, each newer plot being drawn above the previous ones. This only applies to plot*() functions, fill, and hline. Optional. The default is false.
max_lines_count (const int) The number of last line drawings displayed. Possible values: 1-500. The count is approximate; more drawings than the specified count may be displayed. Optional. The default is 50.
max_labels_count (const int) The number of last label drawings displayed. Possible values: 1-500. The count is approximate; more drawings than the specified count may be displayed. Optional. The default is 50.
max_boxes_count (const int) The number of last box drawings displayed. Possible values: 1-500. The count is approximate; more drawings than the specified count may be displayed. Optional. The default is 50.
calc_bars_count (const int) Limits the initial calculation of a script to the last number of bars specified. When specified, a "Calculated bars" field will be included in the "Calculation" section of the script's "Settings/Inputs" tab. Optional. The default is 0, in which case the script executes on all available bars.
max_polylines_count (const int) The number of last polyline drawings displayed. Possible values: 1-100. The count is approximate; more drawings than the specified count may be displayed. Optional. The default is 50.
dynamic_requests (const bool) Specifies whether the script can dynamically call functions from the request.*() namespace. Dynamic request.*() calls are allowed within the local scopes of conditional structures (e.g., if), loops (e.g., for), and exported functions. Additionally, such calls allow "series" arguments for many of their parameters. Optional. The default is true. See the User Manual's Dynamic requests section for more information.
behind_chart (const bool) Controls whether the script's plots and drawings in the main chart pane appear behind the chart display (if true), or in front of it (if false). Optional. The default is true.
EXAMPLE
//@version=6
indicator("My script", shorttitle="Script")
plot(close)
REMARKS
Every indicator script must have one indicator call.
SEE ALSO
strategylibrary
input()6 overloads
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function automatically detects the type of the argument used for 'defval' and uses the corresponding input widget.
SYNTAX & OVERLOADS
input(defval, title, tooltip, inline, group, display) → input color
input(defval, title, tooltip, inline, group, display) → input string
input(defval, title, tooltip, inline, group, display) → input int
input(defval, title, tooltip, inline, group, display) → input float
input(defval, title, inline, group, tooltip, display) → series float
input(defval, title, tooltip, inline, group, display) → input bool
ARGUMENTS
defval (const int/float/bool/string/color or source-type built-ins) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where script users can change it. Source-type built-ins are built-in series float variables that specify the source of the calculation: close, hlc3, etc.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default depends on the type of the value passed to defval: display.none for bool and color values, display.all for everything else.
EXAMPLE
//@version=6
indicator("input", overlay=true)
i_switch = input(true, "On/Off")
plot(i_switch ? open : na)

i_len = input(7, "Length")
i_src = input(close, "Source")
plot(ta.sma(i_src, i_len))

i_border = input(142.50, "Price Border")
hline(i_border)
bgcolor(close > i_border ? color.green : color.red)

i_col = input(color.red, "Plot Color")
plot(close, color=i_col)

i_text = input("Hello!", "Message")
l = label.new(bar_index, high, text=i_text)
label.delete(l[1])
RETURNS
Value of input variable.
REMARKS
Result of input function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.colorinput.intinput.floatinput.stringinput.symbolinput.timeframeinput.text_areainput.sessioninput.sourceinput.time
input.bool()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a checkmark to the script's inputs.
SYNTAX
input.bool(defval, title, tooltip, inline, group, confirm, display) → input bool
ARGUMENTS
defval (const bool) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.none.
EXAMPLE
//@version=6
indicator("input.bool", overlay=true)
i_switch = input.bool(true, "On/Off")
plot(i_switch ? open : na)
RETURNS
Value of input variable.
REMARKS
Result of input.bool function always should be assigned to a variable, see examples above.
SEE ALSO
input.intinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.color()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a color picker that allows the user to select a color and transparency, either from a palette or a hex value.
SYNTAX
input.color(defval, title, tooltip, inline, group, confirm, display) → input color
ARGUMENTS
defval (const color) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.none.
EXAMPLE
//@version=6
indicator("input.color", overlay=true)
i_col = input.color(color.red, "Plot Color")
plot(close, color=i_col)
RETURNS
Value of input variable.
REMARKS
Result of input.color function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.sourceinput.timeinput
input.enum()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a dropdown with options based on the enum fields passed to its defval and options parameters.
The text for each option in the resulting dropdown corresponds to the titles of the included fields. If a field's title is not specified in the enum declaration, its title is the string representation of its name.
SYNTAX
input.enum(defval, title, options, tooltip, inline, group, confirm, display) → input enum
ARGUMENTS
defval (const enum) Determines the default value of the input, which users can change in the script's "Settings/Inputs" tab. When the options parameter has a specified tuple of enum fields, the tuple must include the defval.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of enum fields: [enumName.field1, enumName.field2, ...]) A list of options to choose from. Optional. By default, the titles of all of the enum's fields are available in the dropdown. Passing a tuple as the options argument limits the list to only the included fields.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("Session highlight", overlay = true)

//@enum        Contains fields with popular timezones as titles.
//@field exch  Has an empty string as the title to represent the chart timezone.
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
RETURNS
Value of input variable.
REMARKS
All fields included in the defval and options arguments must belong to the same enum.
SEE ALSO
input.text_areainput.boolinput.intinput.floatinput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.float()2 overloads
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a field for a float input to the script's inputs.
SYNTAX & OVERLOADS
input.float(defval, title, options, tooltip, inline, group, confirm, display) → input float
input.float(defval, title, minval, maxval, step, tooltip, inline, group, confirm, display) → input float
ARGUMENTS
defval (const int/float) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where script users can change it. When a list of values is used with the options parameter, the value must be one of them.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of const int/float values: [val1, val2, ...]) A list of options to choose from a dropdown menu, separated by commas and enclosed in square brackets: [val1, val2, ...]. When using this parameter, the minval, maxval and step parameters cannot be used.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.float", overlay=true)
i_angle1 = input.float(0.5, "Sin Angle", minval=-3.14, maxval=3.14, step=0.02)
plot(math.sin(i_angle1) > 0 ? close : open, "sin", color=color.green)

i_angle2 = input.float(0, "Cos Angle", options=[-3.14, -1.57, 0, 1.57, 3.14])
plot(math.cos(i_angle2) > 0 ? close : open, "cos", color=color.red)
RETURNS
Value of input variable.
REMARKS
Result of input.float function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.int()2 overloads
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a field for an integer input to the script's inputs.
SYNTAX & OVERLOADS
input.int(defval, title, options, tooltip, inline, group, confirm, display) → input int
input.int(defval, title, minval, maxval, step, tooltip, inline, group, confirm, display) → input int
ARGUMENTS
defval (const int) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where script users can change it. When a list of values is used with the options parameter, the value must be one of them.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of const int values: [val1, val2, ...]) A list of options to choose from a dropdown menu, separated by commas and enclosed in square brackets: [val1, val2, ...]. When using this parameter, the minval, maxval and step parameters cannot be used.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.int", overlay=true)
i_len1 = input.int(10, "Length 1", minval=5, maxval=21, step=1)
plot(ta.sma(close, i_len1))

i_len2 = input.int(10, "Length 2", options=[5, 10, 21])
plot(ta.sma(close, i_len2))
RETURNS
Value of input variable.
REMARKS
Result of input.int function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.price()
Adds a price input to the script's "Settings/Inputs" tab. Using confirm = true activates the interactive input mode where a price is selected by clicking on the chart.
SYNTAX
input.price(defval, title, tooltip, inline, group, confirm, display) → input float
ARGUMENTS
defval (const int/float) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, the interactive input mode is enabled and the selection is done by clicking on the chart when the indicator is added to the chart, or by selecting the indicator and moving the selection after that. Optional. The default is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.price", overlay=true)
price1 = input.price(title="Date", defval=42)
plot(price1)

price2 = input.price(54, title="Date")
plot(price2)
RETURNS
Value of input variable.
REMARKS
When using interactive mode, a time input can be combined with a price input if both function calls use the same argument for their inline parameter.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.resolutioninput.sessioninput.sourceinput.colorinput
input.session()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds two dropdowns that allow the user to specify the beginning and the end of a session using the session selector and returns the result as a string.
SYNTAX
input.session(defval, title, options, tooltip, inline, group, confirm, display) → input string
ARGUMENTS
defval (const string) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it. When a list of values is used with the options parameter, the value must be one of them.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of const string values: [val1, val2, ...]) A list of options to choose from.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.session", overlay=true)
i_sess = input.session("1300-1700", "Session", options=["0930-1600", "1300-1700", "1700-2100"])
t = time(timeframe.period, i_sess)
bgcolor(time == t ? color.green : na)
RETURNS
Value of input variable.
REMARKS
Result of input.session function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sourceinput.colorinput.timeinput
input.source()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a dropdown that allows the user to select a source for the calculation, e.g. close, hl2, etc. The user can also select an output from another indicator on their chart as the source.
SYNTAX
input.source(defval, title, tooltip, inline, group, display, confirm) → series float
ARGUMENTS
defval (open/high/low/close/hl2/hlc3/ohlc4/hlcc4) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
EXAMPLE
//@version=6
indicator("input.source", overlay=true)
i_src = input.source(close, "Source")
plot(i_src)
RETURNS
Value of input variable.
REMARKS
Result of input.source function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.colorinput.timeinput
input.string()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a field for a string input to the script's inputs.
SYNTAX
input.string(defval, title, options, tooltip, inline, group, confirm, display) → input string
ARGUMENTS
defval (const string) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it. When a list of values is used with the options parameter, the value must be one of them.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of const string values: [val1, val2, ...]) A list of options to choose from.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.string", overlay=true)
i_text = input.string("Hello!", "Message")
l = label.new(bar_index, high, i_text)
label.delete(l[1])
RETURNS
Value of input variable.
REMARKS
Result of input.string function always should be assigned to a variable, see examples above.
SEE ALSO
input.text_areainput.boolinput.intinput.floatinput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.symbol()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a field that allows the user to select a specific symbol using the symbol search and returns that symbol, paired with its exchange prefix, as a string.
SYNTAX
input.symbol(defval, title, tooltip, inline, group, confirm, display) → input string
ARGUMENTS
defval (const string) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.symbol", overlay=true)
i_sym = input.symbol("DELL", "Symbol")
s = request.security(i_sym, 'D', close)
plot(s)
RETURNS
Value of input variable.
REMARKS
Result of input.symbol function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.text_area()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a field for a multiline text input.
SYNTAX
input.text_area(defval, title, tooltip, group, confirm, display) → input string
ARGUMENTS
defval (const string) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.none.
EXAMPLE
//@version=6
indicator("input.text_area")
i_text = input.text_area(defval = "Hello \nWorld!", title = "Message")
plot(close)
RETURNS
Value of input variable.
REMARKS
Result of input.text_area function always should be assigned to a variable, see examples above.
SEE ALSO
input.stringinput.boolinput.intinput.floatinput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput.timeinput
input.time()
Adds a time input to the script's "Settings/Inputs" tab. This function adds two input widgets on the same line: one for the date and one for the time. The function returns a date/time value in UNIX format. Using confirm = true activates the interactive input mode where a point in time is selected by clicking on the chart.
SYNTAX
input.time(defval, title, tooltip, inline, group, confirm, display) → input int
ARGUMENTS
defval (const int) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it. The value can be a timestamp function, but only if it uses a date argument in const string format.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, the interactive input mode is enabled and the selection is done by clicking on the chart when the indicator is added to the chart, or by selecting the indicator and moving the selection after that. Optional. The default is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.none.
EXAMPLE
//@version=6
indicator("input.time", overlay=true)
i_date = input.time(timestamp("20 Jul 2021 00:00 +0300"), "Date")
l = label.new(i_date, high, "Date", xloc=xloc.bar_time)
label.delete(l[1])
RETURNS
Value of input variable.
REMARKS
When using interactive mode, a price input can be combined with a time input if both function calls use the same argument for their inline parameter.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.timeframeinput.sessioninput.sourceinput.colorinput
input.timeframe()
Adds an input to the Inputs tab of your script's Settings, which allows you to provide configuration options to script users. This function adds a dropdown that allows the user to select a specific timeframe via the timeframe selector and returns it as a string. The selector includes the custom timeframes a user may have added using the chart's Timeframe dropdown.
SYNTAX
input.timeframe(defval, title, options, tooltip, inline, group, confirm, display) → input string
ARGUMENTS
defval (const string) Determines the default value of the input variable proposed in the script's "Settings/Inputs" tab, from where the user can change it. When a list of values is used with the options parameter, the value must be one of them.
title (const string) Title of the input. If not specified, the variable name is used as the input's title. If the title is specified, but it is empty, the name will be an empty string.
options (tuple of const string values: [val1, val2, ...]) A list of options to choose from.
tooltip (const string) The string that will be shown to the user when hovering over the tooltip icon.
inline (const string) Combines all the input calls using the same argument in one line. The string used as an argument is not displayed. It is only used to identify inputs belonging to the same line.
group (const string) Creates a header above all inputs using the same group argument string. The string is also used as the header's text.
confirm (const bool) If true, then user will be asked to confirm input value before indicator is added to chart. Default value is false.
display (const plot_display) Controls where the script will display the input's information, aside from within the script's settings. This option allows one to remove a specific input from the script's status line or the Data Window to ensure only the most necessary inputs are displayed there. Possible values: display.none, display.data_window, display.status_line, display.all. Optional. The default is display.all.
EXAMPLE
//@version=6
indicator("input.timeframe", overlay=true)
i_res = input.timeframe('D', "Resolution", options=['D', 'W', 'M'])
s = request.security("AAPL", i_res, close)
plot(s)
RETURNS
Value of input variable.
REMARKS
Result of input.timeframe function always should be assigned to a variable, see examples above.
SEE ALSO
input.boolinput.intinput.floatinput.stringinput.text_areainput.symbolinput.sessioninput.sourceinput.colorinput.timeinput
int()4 overloads
Casts na or truncates float value to int
SYNTAX & OVERLOADS
int(x) → const int
int(x) → input int
int(x) → simple int
int(x) → series int
ARGUMENTS
x (const int/float) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to int.
SEE ALSO
floatboolcolorstringlinelabel
label()
Casts na to label
SYNTAX
label(x) → series label
ARGUMENTS
x (series label) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to label.
SEE ALSO
floatintboolcolorstringline
label.copy()
Clones the label object.
SYNTAX
label.copy(id) → series label
ARGUMENTS
id (series label) Label object.
EXAMPLE
//@version=6
indicator('Last 100 bars highest/lowest', overlay = true)
LOOKBACK = 100
highest = ta.highest(LOOKBACK)
highestBars = ta.highestbars(LOOKBACK)
lowest = ta.lowest(LOOKBACK)
lowestBars = ta.lowestbars(LOOKBACK)
if barstate.islastconfirmedhistory
    var labelHigh = label.new(bar_index + highestBars, highest, str.tostring(highest), color = color.green)
    var labelLow = label.copy(labelHigh)
    label.set_xy(labelLow, bar_index + lowestBars, lowest)
    label.set_text(labelLow, str.tostring(lowest))
    label.set_color(labelLow, color.red)
    label.set_style(labelLow, label.style_label_up)
RETURNS
New label ID object which may be passed to label.setXXX and label.getXXX functions.
SEE ALSO
label.newlabel.delete
label.delete()
Deletes the specified label object. If it has already been deleted, does nothing.
SYNTAX
label.delete(id) → void
ARGUMENTS
id (series label) Label object to delete.
SEE ALSO
label.new
label.get_text()
Returns the text of this label object.
SYNTAX
label.get_text(id) → series string
ARGUMENTS
id (series label) Label object.
EXAMPLE
//@version=6
indicator("label.get_text")
my_label = label.new(time, open, text="Open bar text", xloc=xloc.bar_time)
a = label.get_text(my_label)
label.new(time, close, text = a + " new", xloc=xloc.bar_time)
RETURNS
String object containing the text of this label.
SEE ALSO
label.new
label.get_x()
Returns UNIX time or bar index (depending on the last xloc value set) of this label's position.
SYNTAX
label.get_x(id) → series int
ARGUMENTS
id (series label) Label object.
EXAMPLE
//@version=6
indicator("label.get_x")
my_label = label.new(time, open, text="Open bar text", xloc=xloc.bar_time)
a = label.get_x(my_label)
plot(time - label.get_x(my_label)) //draws zero plot
RETURNS
UNIX timestamp (in milliseconds) or bar index.
SEE ALSO
label.new
label.get_y()
Returns price of this label's position.
SYNTAX
label.get_y(id) → series float
ARGUMENTS
id (series label) Label object.
RETURNS
Floating point value representing price.
SEE ALSO
label.new
label.new()2 overloads
Creates new label object.
SYNTAX & OVERLOADS
label.new(point, text, xloc, yloc, color, style, textcolor, size, textalign, tooltip, text_font_family, force_overlay, text_formatting) → series label
label.new(x, y, text, xloc, yloc, color, style, textcolor, size, textalign, tooltip, text_font_family, force_overlay, text_formatting) → series label
ARGUMENTS
point (chart.point) A chart.point object that specifies the label's location.
text (series string) Label text. Default is empty string.
xloc (series string) See description of x argument. Possible values: xloc.bar_index and xloc.bar_time. Default is xloc.bar_index.
yloc (series string) Possible values are yloc.price, yloc.abovebar, yloc.belowbar. If yloc=yloc.price, y argument specifies the price of the label position. If yloc=yloc.abovebar, label is located above bar. If yloc=yloc.belowbar, label is located below bar. Default is yloc.price.
color (series color) Color of the label border and arrow
style (series string) Label style. Possible values: label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond, label.style_text_outline. Default is label.style_label_down.
textcolor (series color) Text color.
size (series int/string) Optional. Size of the label. Accepts a positive int value or one of the built-in size.* constants. The constants and their equivalent numeric sizes are: size.auto (0), size.tiny (~7), size.small (~10), size.normal (12), size.large (18), size.huge (24). The default value is size.normal, which represents the numeric size of 12.
textalign (series string) Label text alignment. Possible values: text.align_left, text.align_center, text.align_right. Default value is text.align_center.
tooltip (series string) Hover to see tooltip label.
text_font_family (series string) The font family of the text. Optional. The default value is font.family_default. Possible values: font.family_default, font.family_monospace.
force_overlay (const bool) If true, the drawing will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
text_formatting (const text_format) The formatting of the displayed text. Formatting options support addition. For example, text.format_bold + text.format_italic will make the text both bold and italicized. Possible values: text.format_none, text.format_bold, text.format_italic. Optional. The default is text.format_none.
EXAMPLE
//@version=6
indicator("label.new")
var label1 = label.new(bar_index, low, text="Hello, world!", style=label.style_circle)
label.set_x(label1, 0)
label.set_xloc(label1, time, xloc.bar_time)
label.set_color(label1, color.red)
label.set_size(label1, size.large)
RETURNS
Label ID object which may be passed to label.setXXX and label.getXXX functions.
SEE ALSO
label.deletelabel.set_xlabel.set_ylabel.set_xylabel.set_xloclabel.set_yloclabel.set_colorlabel.set_textcolorlabel.set_stylelabel.set_sizelabel.set_textalignlabel.set_tooltiplabel.set_textlabel.set_text_formatting
label.set_color()
Sets label border and arrow color.
SYNTAX
label.set_color(id, color) → void
ARGUMENTS
id (series label) Label object.
color (series color) New label border and arrow color.
SEE ALSO
label.new
label.set_point()
Sets the location of the id label to point.
SYNTAX
label.set_point(id, point) → void
ARGUMENTS
id (series label) A label object.
point (chart.point) A chart.point object.
label.set_size()
Sets arrow and text size of the specified label object.
SYNTAX
label.set_size(id, size) → void
ARGUMENTS
id (series label) Label object.
size (series int/string) Size of the label. Accepts a positive int value or one of the built-in size.* constants. The constants and their equivalent numeric sizes are: size.auto (0), size.tiny (~7), size.small (~10), size.normal (12), size.large (18), size.huge (24). The default value is size.normal, which represents the numeric size of 12.
SEE ALSO
size.autosize.tinysize.smallsize.normalsize.largesize.hugelabel.new
label.set_style()
Sets label style.
SYNTAX
label.set_style(id, style) → void
ARGUMENTS
id (series label) Label object.
style (series string) New label style. Possible values: label.style_none, label.style_xcross, label.style_cross, label.style_triangleup, label.style_triangledown, label.style_flag, label.style_circle, label.style_arrowup, label.style_arrowdown, label.style_label_up, label.style_label_down, label.style_label_left, label.style_label_right, label.style_label_lower_left, label.style_label_lower_right, label.style_label_upper_left, label.style_label_upper_right, label.style_label_center, label.style_square, label.style_diamond, label.style_text_outline.
SEE ALSO
label.new
label.set_text()
Sets label text
SYNTAX
label.set_text(id, text) → void
ARGUMENTS
id (series label) Label object.
text (series string) New label text.
SEE ALSO
label.newlabel.set_text_formatting
label.set_text_font_family()
The function sets the font family of the text inside the label.
SYNTAX
label.set_text_font_family(id, text_font_family) → void
ARGUMENTS
id (series label) A label object.
text_font_family (series string) The font family of the text. Possible values: font.family_default, font.family_monospace.
EXAMPLE
//@version=6
indicator("Example of setting the label font")
if barstate.islastconfirmedhistory
    l = label.new(bar_index, 0, "monospace", yloc=yloc.abovebar)
    label.set_text_font_family(l, font.family_monospace)
SEE ALSO
label.newfont.family_defaultfont.family_monospace
label.set_text_formatting()
Sets the formatting attributes the drawing applies to displayed text.
SYNTAX
label.set_text_formatting(id, text_formatting) → void
ARGUMENTS
id (series label) Label object.
text_formatting (const text_format) The formatting of the displayed text. Formatting options support addition. For example, text.format_bold + text.format_italic will make the text both bold and italicized. Possible values: text.format_none, text.format_bold, text.format_italic. Optional. The default is text.format_none.
SEE ALSO
label.newlabel.set_text
label.set_textalign()
Sets the alignment for the label text.
SYNTAX
label.set_textalign(id, textalign) → void
ARGUMENTS
id (series label) Label object.
textalign (series string) Label text alignment. Possible values: text.align_left, text.align_center, text.align_right.
SEE ALSO
text.align_lefttext.align_centertext.align_rightlabel.new
label.set_textcolor()
Sets color of the label text.
SYNTAX
label.set_textcolor(id, textcolor) → void
ARGUMENTS
id (series label) Label object.
textcolor (series color) New text color.
SEE ALSO
label.new
label.set_tooltip()
Sets the tooltip text.
SYNTAX
label.set_tooltip(id, tooltip) → void
ARGUMENTS
id (series label) Label object.
tooltip (series string) Tooltip text.
SEE ALSO
label.new
label.set_x()
Sets bar index or bar time (depending on the xloc) of the label position.
SYNTAX
label.set_x(id, x) → void
ARGUMENTS
id (series label) Label object.
x (series int) New bar index or bar time of the label position. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
SEE ALSO
label.new
label.set_xloc()
Sets x-location and new bar index/time value.
SYNTAX
label.set_xloc(id, x, xloc) → void
ARGUMENTS
id (series label) Label object.
x (series int) New bar index or bar time of the label position.
xloc (series string) New x-location value.
SEE ALSO
xloc.bar_indexxloc.bar_timelabel.new
label.set_xy()
Sets bar index/time and price of the label position.
SYNTAX
label.set_xy(id, x, y) → void
ARGUMENTS
id (series label) Label object.
x (series int) New bar index or bar time of the label position. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
y (series int/float) New price of the label position.
SEE ALSO
label.new
label.set_y()
Sets price of the label position
SYNTAX
label.set_y(id, y) → void
ARGUMENTS
id (series label) Label object.
y (series int/float) New price of the label position.
SEE ALSO
label.new
label.set_yloc()
Sets new y-location calculation algorithm.
SYNTAX
label.set_yloc(id, yloc) → void
ARGUMENTS
id (series label) Label object.
yloc (series string) New y-location value.
SEE ALSO
yloc.priceyloc.abovebaryloc.belowbarlabel.new
library()
Declaration statement identifying a script as a library.
SYNTAX
library(title, overlay, dynamic_requests) → void
ARGUMENTS
title (const string) The title of the library and its identifier. It cannot contain spaces, special characters or begin with a digit. It is used as the publication's default title, and to uniquely identify the library in the import statement, when another script uses it. It is also used as the script's name on the chart.
overlay (const bool) If true, the library will be added over the chart. If false, it will be added in a separate pane. Optional. The default is false.
dynamic_requests (const bool) Specifies whether the script can dynamically call functions from the request.*() namespace. Dynamic request.*() calls are allowed within the local scopes of conditional structures (e.g., if), loops (e.g., for), and exported functions. Additionally, such calls allow "series" arguments for many of their parameters. Optional. The default is true. See the User Manual's Dynamic requests section for more information.
EXAMPLE
//@version=6
// @description Math library
library("num_methods", overlay = true)
// Calculate "sinh()" from the float parameter `x`
export sinh(float x) =>
    (math.exp(x) - math.exp(-x)) / 2.0
plot(sinh(0))
SEE ALSO
indicatorstrategy
line()
Casts na to line
SYNTAX
line(x) → series line
ARGUMENTS
x (series line) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to line.
SEE ALSO
floatintboolcolorstringlabel
line.copy()
Clones the line object.
SYNTAX
line.copy(id) → series line
ARGUMENTS
id (series line) Line object.
EXAMPLE
//@version=6
indicator('Last 100 bars price range', overlay = true)
LOOKBACK = 100
highest = ta.highest(LOOKBACK)
lowest = ta.lowest(LOOKBACK)
if barstate.islastconfirmedhistory
    var lineTop = line.new(bar_index[LOOKBACK], highest, bar_index, highest, color = color.green)
    var lineBottom = line.copy(lineTop)
    line.set_y1(lineBottom, lowest)
    line.set_y2(lineBottom, lowest)
    line.set_color(lineBottom, color.red)
RETURNS
New line ID object which may be passed to line.setXXX and line.getXXX functions.
SEE ALSO
line.newline.delete
line.delete()
Deletes the specified line object. If it has already been deleted, does nothing.
SYNTAX
line.delete(id) → void
ARGUMENTS
id (series line) Line object to delete.
SEE ALSO
line.new
line.get_price()
Returns the price level of a line at a given bar index.
SYNTAX
line.get_price(id, x) → series float
ARGUMENTS
id (series line) Line object.
x (series int) Bar index for which price is required.
EXAMPLE
//@version=6
indicator("GetPrice", overlay=true)
var line l = na
if bar_index == 10
    l := line.new(0, high[5], bar_index, high)
plot(line.get_price(l, bar_index), color=color.green)
RETURNS
Price value of line 'id' at bar index 'x'.
REMARKS
The line is considered to have been created using 'extend=extend.both'.
This function can only be called for lines created using 'xloc.bar_index'. If you try to call it for a line created with 'xloc.bar_time', it will generate an error.
SEE ALSO
line.new
line.get_x1()
Returns UNIX time or bar index (depending on the last xloc value set) of the first point of the line.
SYNTAX
line.get_x1(id) → series int
ARGUMENTS
id (series line) Line object.
EXAMPLE
//@version=6
indicator("line.get_x1")
my_line = line.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time)
a = line.get_x1(my_line)
plot(time - line.get_x1(my_line)) //draws zero plot
RETURNS
UNIX timestamp (in milliseconds) or bar index.
SEE ALSO
line.new
line.get_x2()
Returns UNIX time or bar index (depending on the last xloc value set) of the second point of the line.
SYNTAX
line.get_x2(id) → series int
ARGUMENTS
id (series line) Line object.
RETURNS
UNIX timestamp (in milliseconds) or bar index.
SEE ALSO
line.new
line.get_y1()
Returns price of the first point of the line.
SYNTAX
line.get_y1(id) → series float
ARGUMENTS
id (series line) Line object.
RETURNS
Price value.
SEE ALSO
line.new
line.get_y2()
Returns price of the second point of the line.
SYNTAX
line.get_y2(id) → series float
ARGUMENTS
id (series line) Line object.
RETURNS
Price value.
SEE ALSO
line.new
line.new()2 overloads
Creates new line object.
SYNTAX & OVERLOADS
line.new(first_point, second_point, xloc, extend, color, style, width, force_overlay) → series line
line.new(x1, y1, x2, y2, xloc, extend, color, style, width, force_overlay) → series line
ARGUMENTS
first_point (chart.point) A chart.point object that specifies the line's starting coordinate.
second_point (chart.point) A chart.point object that specifies the line's ending coordinate.
xloc (series string) See description of x1 argument. Possible values: xloc.bar_index and xloc.bar_time. Default is xloc.bar_index.
extend (series string) If extend=extend.none, draws segment starting at point (x1, y1) and ending at point (x2, y2). If extend is equal to extend.right or extend.left, draws a ray starting at point (x1, y1) or (x2, y2), respectively. If extend=extend.both, draws a straight line that goes through these points. Default value is extend.none.
color (series color) Line color.
style (series string) Line style. Possible values: line.style_solid, line.style_dotted, line.style_dashed, line.style_arrow_left, line.style_arrow_right, line.style_arrow_both.
width (series int) Line width in pixels.
force_overlay (const bool) If true, the drawing will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("line.new")
var line1 = line.new(0, low, bar_index, high, extend=extend.right)
var line2 = line.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time, style=line.style_dashed)
line.set_x2(line1, 0)
line.set_xloc(line1, time, time + 60 * 60 * 24, xloc.bar_time)
line.set_color(line2, color.green)
line.set_width(line2, 5)
RETURNS
Line ID object which may be passed to line.setXXX and line.getXXX functions.
SEE ALSO
line.deleteline.set_x1line.set_y1line.set_xy1line.set_x2line.set_y2line.set_xy2line.set_xlocline.set_colorline.set_extendline.set_styleline.set_width
line.set_color()
Sets the line color
SYNTAX
line.set_color(id, color) → void
ARGUMENTS
id (series line) Line object.
color (series color) New line color
SEE ALSO
line.new
line.set_extend()
Sets extending type of this line object. If extend=extend.none, draws segment starting at point (x1, y1) and ending at point (x2, y2). If extend is equal to extend.right or extend.left, draws a ray starting at point (x1, y1) or (x2, y2), respectively. If extend=extend.both, draws a straight line that goes through these points.
SYNTAX
line.set_extend(id, extend) → void
ARGUMENTS
id (series line) Line object.
extend (series string) New extending type.
SEE ALSO
extend.noneextend.rightextend.leftextend.bothline.new
line.set_first_point()
Sets the first point of the id line to point.
SYNTAX
line.set_first_point(id, point) → void
ARGUMENTS
id (series line) A line object.
point (chart.point) A chart.point object.
line.set_second_point()
Sets the second point of the id line to point.
SYNTAX
line.set_second_point(id, point) → void
ARGUMENTS
id (series line) A line object.
point (chart.point) A chart.point object.
line.set_style()
Sets the line style
SYNTAX
line.set_style(id, style) → void
ARGUMENTS
id (series line) Line object.
style (series string) New line style.
SEE ALSO
line.style_solidline.style_dottedline.style_dashedline.style_arrow_leftline.style_arrow_rightline.style_arrow_bothline.new
line.set_width()
Sets the line width.
SYNTAX
line.set_width(id, width) → void
ARGUMENTS
id (series line) Line object.
width (series int) New line width in pixels.
SEE ALSO
line.new
line.set_x1()
Sets bar index or bar time (depending on the xloc) of the first point.
SYNTAX
line.set_x1(id, x) → void
ARGUMENTS
id (series line) Line object.
x (series int) Bar index or bar time. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
SEE ALSO
line.new
line.set_x2()
Sets bar index or bar time (depending on the xloc) of the second point.
SYNTAX
line.set_x2(id, x) → void
ARGUMENTS
id (series line) Line object.
x (series int) Bar index or bar time. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
SEE ALSO
line.new
line.set_xloc()
Sets x-location and new bar index/time values.
SYNTAX
line.set_xloc(id, x1, x2, xloc) → void
ARGUMENTS
id (series line) Line object.
x1 (series int) Bar index or bar time of the first point.
x2 (series int) Bar index or bar time of the second point.
xloc (series string) New x-location value.
SEE ALSO
xloc.bar_indexxloc.bar_timeline.new
line.set_xy1()
Sets bar index/time and price of the first point.
SYNTAX
line.set_xy1(id, x, y) → void
ARGUMENTS
id (series line) Line object.
x (series int) Bar index or bar time. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
y (series int/float) Price.
SEE ALSO
line.new
line.set_xy2()
Sets bar index/time and price of the second point
SYNTAX
line.set_xy2(id, x, y) → void
ARGUMENTS
id (series line) Line object.
x (series int) Bar index or bar time.
y (series int/float) Price.
SEE ALSO
line.new
line.set_y1()
Sets price of the first point
SYNTAX
line.set_y1(id, y) → void
ARGUMENTS
id (series line) Line object.
y (series int/float) Price.
SEE ALSO
line.new
line.set_y2()
Sets price of the second point.
SYNTAX
line.set_y2(id, y) → void
ARGUMENTS
id (series line) Line object.
y (series int/float) Price.
SEE ALSO
line.new
linefill()
Casts na to linefill.
SYNTAX
linefill(x) → series linefill
ARGUMENTS
x (series linefill) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to linefill.
SEE ALSO
floatintboolcolorstringlinelabel
linefill.delete()
Deletes the specified linefill object. If it has already been deleted, does nothing.
SYNTAX
linefill.delete(id) → void
ARGUMENTS
id (series linefill) A linefill object.
linefill.get_line1()
Returns the ID of the first line used in the id linefill.
SYNTAX
linefill.get_line1(id) → series line
ARGUMENTS
id (series linefill) A linefill object.
linefill.get_line2()
Returns the ID of the second line used in the id linefill.
SYNTAX
linefill.get_line2(id) → series line
ARGUMENTS
id (series linefill) A linefill object.
linefill.new()
Creates a new linefill object and displays it on the chart, filling the space between line1 and line2 with the color specified in color.
SYNTAX
linefill.new(line1, line2, color) → series linefill
ARGUMENTS
line1 (series line) First line object.
line2 (series line) Second line object.
color (series color) The color used to fill the space between the lines.
RETURNS
The ID of a linefill object that can be passed to other linefill.*() functions.
REMARKS
If any line of the two is deleted, the linefill object is also deleted. If the lines are moved (e.g. via line.set_xy functions), the linefill object is also moved.
If both lines are extended in the same direction relative to the lines themselves (e.g. both have extend.right as the value of their extend= parameter), the space between line extensions will also be filled.
linefill.set_color()
The function sets the color of the linefill object passed to it.
SYNTAX
linefill.set_color(id, color) → void
ARGUMENTS
id (series linefill) A linefill object.
color (series color) The color of the linefill object.
log.error()2 overloads
Converts the formatting string and value(s) into a formatted string, and sends the result to the "Pine logs" menu tagged with the "error" debug level.
The formatting string can contain literal text and one placeholder in curly braces {} for each value to be formatted. Each placeholder consists of the index of the required argument (beginning at 0) that will replace it, and an optional format specifier. The index represents the position of that argument in the function's argument list.
SYNTAX & OVERLOADS
log.error(message) → void
log.error(formatString, arg0, arg1, ...) → void
ARGUMENTS
message (series string) Log message.
EXAMPLE
//@version=6
strategy("My strategy", overlay = true, process_orders_on_close = true)
bracketTickSizeInput = input.int(1000, "Stoploss/Take-Profit distance (in ticks)")

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    limitLevel = close * 1.01
    log.info("Long limit order has been placed at {0}", limitLevel)
    strategy.order("My Long Entry Id", strategy.long, limit = limitLevel)

    log.info("Exit orders have been placed: Take-profit at {0}, Stop-loss at {1}", close, limitLevel)
    strategy.exit("Exit", "My Long Entry Id", profit = bracketTickSizeInput, loss = bracketTickSizeInput)

if strategy.opentrades > 10
    log.warning("{0} positions opened in the same direction in a row. Try adjusting `bracketTickSizeInput`", strategy.opentrades)

last10Perc = strategy.initial_capital / 10 > strategy.equity
if (last10Perc and not last10Perc[1])
    log.error("The strategy has lost 90% of the initial capital!")
RETURNS
The formatted string.
REMARKS
Any curly braces within an unquoted pattern must be balanced. For example, "ab {0} de" and "ab '}' de" are valid patterns, but "ab {0'}' de", "ab } de" and "''{''" are not.
The function can apply additional formatting to some values inside of the {}. The list of additional formatting options can be found in the EXAMPLE section of the str.format article.
The string used as the formatString argument can contain single quote characters ('). However, one must pair all single quotes in that string to avoid unexpected formatting results.
The "Pine logs..." button is accessible from the "More" dropdown in the Pine Editor and from the "More" dropdown in the status line of any script that uses log.*() functions.
log.info()2 overloads
Converts the formatting string and value(s) into a formatted string, and sends the result to the "Pine logs" menu tagged with the "info" debug level.
The formatting string can contain literal text and one placeholder in curly braces {} for each value to be formatted. Each placeholder consists of the index of the required argument (beginning at 0) that will replace it, and an optional format specifier. The index represents the position of that argument in the function's argument list.
SYNTAX & OVERLOADS
log.info(message) → void
log.info(formatString, arg0, arg1, ...) → void
ARGUMENTS
message (series string) Log message.
EXAMPLE
//@version=6
strategy("My strategy", overlay = true, process_orders_on_close = true)
bracketTickSizeInput = input.int(1000, "Stoploss/Take-Profit distance (in ticks)")

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    limitLevel = close * 1.01
    log.info("Long limit order has been placed at {0}", limitLevel)
    strategy.order("My Long Entry Id", strategy.long, limit = limitLevel)

    log.info("Exit orders have been placed: Take-profit at {0}, Stop-loss at {1}", close, limitLevel)
    strategy.exit("Exit", "My Long Entry Id", profit = bracketTickSizeInput, loss = bracketTickSizeInput)

if strategy.opentrades > 10
    log.warning("{0} positions opened in the same direction in a row. Try adjusting `bracketTickSizeInput`", strategy.opentrades)

last10Perc = strategy.initial_capital / 10 > strategy.equity
if (last10Perc and not last10Perc[1])
    log.error("The strategy has lost 90% of the initial capital!")
RETURNS
The formatted string.
REMARKS
Any curly braces within an unquoted pattern must be balanced. For example, "ab {0} de" and "ab '}' de" are valid patterns, but "ab {0'}' de", "ab } de" and "''{''" are not.
The function can apply additional formatting to some values inside of the {}. The list of additional formatting options can be found in the EXAMPLE section of the str.format article.
The string used as the formatString argument can contain single quote characters ('). However, one must pair all single quotes in that string to avoid unexpected formatting results.
The "Pine logs..." button is accessible from the "More" dropdown in the Pine Editor and from the "More" dropdown in the status line of any script that uses log.*() functions.
log.warning()2 overloads
Converts the formatting string and value(s) into a formatted string, and sends the result to the "Pine logs" menu tagged with the "warning" debug level.
The formatting string can contain literal text and one placeholder in curly braces {} for each value to be formatted. Each placeholder consists of the index of the required argument (beginning at 0) that will replace it, and an optional format specifier. The index represents the position of that argument in the function's argument list.
SYNTAX & OVERLOADS
log.warning(message) → void
log.warning(formatString, arg0, arg1, ...) → void
ARGUMENTS
message (series string) Log message.
EXAMPLE
//@version=6
strategy("My strategy", overlay = true, process_orders_on_close = true)
bracketTickSizeInput = input.int(1000, "Stoploss/Take-Profit distance (in ticks)")

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    limitLevel = close * 1.01
    log.info("Long limit order has been placed at {0}", limitLevel)
    strategy.order("My Long Entry Id", strategy.long, limit = limitLevel)

    log.info("Exit orders have been placed: Take-profit at {0}, Stop-loss at {1}", close, limitLevel)
    strategy.exit("Exit", "My Long Entry Id", profit = bracketTickSizeInput, loss = bracketTickSizeInput)

if strategy.opentrades > 10
    log.warning("{0} positions opened in the same direction in a row. Try adjusting `bracketTickSizeInput`", strategy.opentrades)

last10Perc = strategy.initial_capital / 10 > strategy.equity
if (last10Perc and not last10Perc[1])
    log.error("The strategy has lost 90% of the initial capital!")
RETURNS
The formatted string.
REMARKS
Any curly braces within an unquoted pattern must be balanced. For example, "ab {0} de" and "ab '}' de" are valid patterns, but "ab {0'}' de", "ab } de" and "''{''" are not.
The function can apply additional formatting to some values inside of the {}. The list of additional formatting options can be found in the EXAMPLE section of the str.format article.
The string used as the formatString argument can contain single quote characters ('). However, one must pair all single quotes in that string to avoid unexpected formatting results.
The "Pine logs..." button is accessible from the "More" dropdown in the Pine Editor and from the "More" dropdown in the status line of any script that uses log.*() functions.
map.clear()
Clears the map, removing all key-value pairs from it.
SYNTAX
map.clear(id) → void
ARGUMENTS
id (any map type) A map object.
EXAMPLE
//@version=6
indicator("map.clear example")
oddMap = map.new<int, bool>()
oddMap.put(1, true)
oddMap.put(2, false)
oddMap.put(3, true)
map.clear(oddMap)
plot(oddMap.size())
SEE ALSO
map.new<type,type>map.put_allmap.keysmap.valuesmap.remove
map.contains()
Returns true if the key was found in the id map, false otherwise.
SYNTAX
map.contains(id, key) → series bool
ARGUMENTS
id (any map type) A map object.
key (series <type of the map's elements>) The key to search in the map.
EXAMPLE
//@version=6
indicator("map.includes example")
a = map.new<string, float>()
a.put("open", open)
p = close
if map.contains(a, "open")
    p := a.get("open")
plot(p)
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.size
map.copy()
Creates a copy of an existing map.
SYNTAX
map.copy(id) → map<keyType, valueType>
ARGUMENTS
id (any map type) A map object to copy.
EXAMPLE
//@version=6
indicator("map.copy example")
a = map.new<string, int>()
a.put("example", 1)
b = map.copy(a)
a := map.new<string, int>()
a.put("example", 2)
plot(a.get("example"))
plot(b.get("example"))
RETURNS
A copy of the id map.
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.getmap.size
map.get()
Returns the value associated with the specified key in the id map.
SYNTAX
map.get(id, key) → <value_type>
ARGUMENTS
id (any map type) A map object.
key (series <type of the map's elements>) The key of the value to retrieve.
EXAMPLE
//@version=6
indicator("map.get example")
a = map.new<int, int>()
size = 10
for i = 0 to size
    a.put(i, size-i)
plot(map.get(a, 1))
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.contains
map.keys()
Returns an array of all the keys in the id map. The resulting array is a copy and any changes to it are not reflected in the original map.
SYNTAX
map.keys(id) → array<type>
ARGUMENTS
id (any map type) A map object.
EXAMPLE
//@version=6
indicator("map.keys example")
a = map.new<string, float>()
a.put("open", open)
a.put("high", high)
a.put("low", low)
a.put("close", close)
keys = map.keys(a)
ohlc = 0.0
for key in keys
    ohlc += a.get(key)
plot(ohlc/4)
REMARKS
Maps maintain insertion order. The elements within the array returned by this function will also be in the insertion order.
SEE ALSO
map.new<type,type>map.putmap.getmap.valuesmap.size
map.new<type,type>()
Creates a new map object: a collection that consists of key-value pairs, where all keys are of the keyType, and all values are of the valueType.
keyType can be a primitive type or enum. For example: int, float, bool, string, color.
valueType can be of any type except array<>, matrix<>, and map<>. User-defined types are allowed, even if they have array<>, matrix<>, or map<> as one of their fields.
SYNTAX
map.new<keyType, valueType>() → map<keyType, valueType>
EXAMPLE
//@version=6
indicator("map.new<string, int> example")
a = map.new<string, int>()
a.put("example", 1)
label.new(bar_index, close, str.tostring(a.get("example")))
RETURNS
The ID of a map object which may be used in other map.*() functions.
REMARKS
Each key is unique and can only appear once. When adding a new value with a key that the map already contains, that value replaces the old value associated with the key.
Maps maintain insertion order. Note that the order does not change when inserting a pair with a key that's already in the map. The new pair replaces the existing pair with the key in such cases.
SEE ALSO
map.putmap.keysmap.valuesmap.getarray.new<type>
map.put()
Puts a new key-value pair into the id map.
SYNTAX
map.put(id, key, value) → <value_type>
ARGUMENTS
id (any map type) A map object.
key (series <type of the map's elements>) The key to put into the map.
value (series <type of the map's elements>) The key value to put into the map.
EXAMPLE
//@version=6
indicator("map.put example")
a = map.new<string, float>()
map.put(a, "first", 10)
map.put(a, "second", 15)
prevFirst = map.put(a, "first", 20)
currFirst = a.get("first")
plot(prevFirst)
plot(currFirst)
RETURNS
The previous value associated with key if the key was already present in the map, or na if the key is new.
REMARKS
Maps maintain insertion order. Note that the order does not change when inserting a pair with a key that's already in the map. The new pair replaces the existing pair with the key in such cases.
SEE ALSO
map.new<type,type>map.put_allmap.keysmap.valuesmap.remove
map.put_all()
Puts all key-value pairs from the id2 map into the id map.
SYNTAX
map.put_all(id, id2) → void
ARGUMENTS
id (any map type) A map object to append to.
id2 (any map type) A map object to be appended.
EXAMPLE
//@version=6
indicator("map.put_all example")
a = map.new<string, float>()
b = map.new<string, float>()
a.put("first", 10)
a.put("second", 15)
b.put("third", 20)
map.put_all(a, b)
plot(a.get("third"))
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.remove
map.remove()
Removes a key-value pair from the id map.
SYNTAX
map.remove(id, key) → <value_type>
ARGUMENTS
id (any map type) A map object.
key (series <type of the map's elements>) The key of the pair to remove from the map.
EXAMPLE
//@version=6
indicator("map.remove example")
a = map.new<string, color>()
a.put("firstColor", color.green)
oldColorValue = map.remove(a, "firstColor")
plot(close, color = oldColorValue)
RETURNS
The previous value associated with key if the key was present in the map, or na if there was no such key.
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.clear
map.size()
Returns the number of key-value pairs in the id map.
SYNTAX
map.size(id) → series int
ARGUMENTS
id (any map type) A map object.
EXAMPLE
//@version=6
indicator("map.size example")
a = map.new<int, int>()
size = 10
for i = 0 to size
    a.put(i, size-i)
plot(map.size(a))
SEE ALSO
map.new<type,type>map.putmap.keysmap.valuesmap.get
map.values()
Returns an array of all the values in the id map. The resulting array is a copy and any changes to it are not reflected in the original map.
SYNTAX
map.values(id) → array<type>
ARGUMENTS
id (any map type) A map object.
EXAMPLE
//@version=6
indicator("map.values example")
a = map.new<string, float>()
a.put("open", open)
a.put("high", high)
a.put("low", low)
a.put("close", close)
values = map.values(a)
ohlc = 0.0
for value in values
    ohlc += value
plot(ohlc/4)
REMARKS
Maps maintain insertion order. The elements within the array returned by this function will also be in the insertion order.
SEE ALSO
map.new<type,type>map.putmap.getmap.keysmap.size
