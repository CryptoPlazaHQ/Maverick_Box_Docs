Pine Script® language reference manual
Variables
bar_index
Current bar index. Numbering is zero-based, index of the first bar is 0.
TYPE
series int
EXAMPLE
//@version=6
indicator("bar_index")
plot(bar_index)
plot(bar_index > 5000 ? close : 0)
REMARKS
Note that bar_index has replaced n variable in version 4.
Note that bar indexing starts from 0 on the first historical bar.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
last_bar_indexbarstate.isfirstbarstate.islastbarstate.isrealtime
barstate.isconfirmed
Returns true if the script is calculating the last (closing) update of the current bar. The next script calculation will be on the new bar data.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
It is NOT recommended to use barstate.isconfirmed in request.security expression. Its value requested from request.security is unpredictable.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.islastbarstate.ishistorybarstate.isrealtimebarstate.isnewbarstate.islastconfirmedhistory
barstate.isfirst
Returns true if current bar is first bar in barset, false otherwise.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.islastbarstate.ishistorybarstate.isrealtimebarstate.isnewbarstate.isconfirmedbarstate.islastconfirmedhistory
barstate.ishistory
Returns true if current bar is a historical bar, false otherwise.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.islastbarstate.isrealtimebarstate.isnewbarstate.isconfirmedbarstate.islastconfirmedhistory
barstate.islast
Returns true if current bar is the last bar in barset, false otherwise. This condition is true for all real-time bars in barset.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.ishistorybarstate.isrealtimebarstate.isnewbarstate.isconfirmedbarstate.islastconfirmedhistory
barstate.islastconfirmedhistory
Returns true if script is executing on the dataset's last bar when market is closed, or script is executing on the bar immediately preceding the real-time bar, if market is open. Returns false otherwise.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.islastbarstate.ishistorybarstate.isrealtimebarstate.isnew
barstate.isnew
Returns true if script is currently calculating on new bar, false otherwise. This variable is true when calculating on historical bars or on first update of a newly generated real-time bar.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.islastbarstate.ishistorybarstate.isrealtimebarstate.isconfirmedbarstate.islastconfirmedhistory
barstate.isrealtime
Returns true if current bar is a real-time bar, false otherwise.
TYPE
series bool
REMARKS
Pine Script® code that uses this variable could calculate differently on history and real-time data.
Please note that using this variable/function can cause indicator repainting.
SEE ALSO
barstate.isfirstbarstate.islastbarstate.ishistorybarstate.isnewbarstate.isconfirmedbarstate.islastconfirmedhistory
box.all
Returns an array filled with all the current boxes drawn by the script.
TYPE
array<box>
EXAMPLE
//@version=6
indicator("box.all")
//delete all boxes
box.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time, border_style=line.style_dashed)
a_allBoxes = box.all
if array.size(a_allBoxes) > 0
    for i = 0 to array.size(a_allBoxes) - 1
        box.delete(array.get(a_allBoxes, i))
REMARKS
The array is read-only. Index zero of the array is the ID of the oldest object on the chart.
SEE ALSO
box.newline.alllabel.alltable.all
chart.bg_color
Returns the color of the chart's background from the "Chart settings/Appearance/Background" field. When a gradient is selected, the middle point of the gradient is returned.
TYPE
input color
SEE ALSO
chart.fg_color
chart.fg_color
Returns a color providing optimal contrast with chart.bg_color.
TYPE
input color
SEE ALSO
chart.bg_color
chart.is_heikinashi
TYPE
simple bool
RETURNS
Returns true if the chart type is Heikin Ashi, false otherwise.
SEE ALSO
chart.is_renkochart.is_linebreakchart.is_kagichart.is_pnfchart.is_range
chart.is_kagi
TYPE
simple bool
RETURNS
Returns true if the chart type is Kagi, false otherwise.
SEE ALSO
chart.is_renkochart.is_linebreakchart.is_heikinashichart.is_pnfchart.is_range
chart.is_linebreak
TYPE
simple bool
RETURNS
Returns true if the chart type is Line break, false otherwise.
SEE ALSO
chart.is_renkochart.is_heikinashichart.is_kagichart.is_pnfchart.is_range
chart.is_pnf
TYPE
simple bool
RETURNS
Returns true if the chart type is Point & figure, false otherwise.
SEE ALSO
chart.is_renkochart.is_linebreakchart.is_kagichart.is_heikinashichart.is_range
chart.is_range
TYPE
simple bool
RETURNS
Returns true if the chart type is Range, false otherwise.
SEE ALSO
chart.is_renkochart.is_linebreakchart.is_kagichart.is_pnfchart.is_heikinashi
chart.is_renko
TYPE
simple bool
RETURNS
Returns true if the chart type is Renko, false otherwise.
SEE ALSO
chart.is_heikinashichart.is_linebreakchart.is_kagichart.is_pnfchart.is_range
chart.is_standard
TYPE
simple bool
RETURNS
Returns true if the chart type is not one of the following: Renko, Kagi, Line break, Point & figure, Range, Heikin Ashi; false otherwise.
SEE ALSO
chart.is_renkochart.is_linebreakchart.is_kagichart.is_pnfchart.is_rangechart.is_heikinashi
chart.left_visible_bar_time
The time of the leftmost bar currently visible on the chart.
TYPE
input int
REMARKS
Scripts using this variable will automatically re-execute when its value updates to reflect changes in the chart, which can be caused by users scrolling the chart, or new real-time bars.
Alerts created on a script that includes this variable will only use the value assigned to the variable at the moment of the alert's creation, regardless of whether the value changes afterward, which may lead to repainting.
SEE ALSO
chart.right_visible_bar_time
chart.right_visible_bar_time
The time of the rightmost bar currently visible on the chart.
TYPE
input int
REMARKS
Scripts using this variable will automatically re-execute when its value updates to reflect changes in the chart, which can be caused by users scrolling the chart, or new real-time bars.
Alerts created on a script that includes this variable will only use the value assigned to the variable at the moment of the alert's creation, regardless of whether the value changes afterward, which may lead to repainting.
SEE ALSO
chart.left_visible_bar_time
close
Close price of the current bar when it has closed, or last traded price of a yet incomplete, realtime bar.
TYPE
series float
REMARKS
Previous values may be accessed with square brackets operator [], e.g. close[1], close[2].
SEE ALSO
openhighlowvolumetimehl2hlc3hlcc4ohlc4
dayofmonth
Date of current bar time in exchange timezone.
TYPE
series int
REMARKS
Note that this variable returns the day based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the day of the trading day.
SEE ALSO
dayofmonthtimeyearmonthweekofyeardayofweekhourminutesecond
dayofweek
Day of week for current bar time in exchange timezone.
TYPE
series int
REMARKS
Note that this variable returns the day based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00) this value can be lower by 1 than the day of the trading day.
You can use dayofweek.sunday, dayofweek.monday, dayofweek.tuesday, dayofweek.wednesday, dayofweek.thursday, dayofweek.friday and dayofweek.saturday variables for comparisons.
SEE ALSO
dayofweektimeyearmonthweekofyeardayofmonthhourminutesecond
dividends.future_amount
Returns the payment amount of the upcoming dividend in the currency of the current instrument, or na if this data isn't available.
TYPE
series float
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.
dividends.future_ex_date
Returns the Ex-dividend date (Ex-date) of the current instrument's next dividend payment, or na if this data isn't available. Ex-dividend date signifies when investors are no longer entitled to a payout from the most recent dividend. Only those who purchased shares before this day are entitled to the dividend payment.
TYPE
series int
RETURNS
UNIX time, expressed in milliseconds.
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.
dividends.future_pay_date
Returns the Payment date (Pay date) of the current instrument's next dividend payment, or na if this data isn't available. Payment date signifies the day when eligible investors will receive the dividend payment.
TYPE
series int
RETURNS
UNIX time, expressed in milliseconds.
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected Payment date of the next dividend.
earnings.future_eps
Returns the estimated Earnings per Share of the next earnings report in the currency of the instrument, or na if this data isn't available.
TYPE
series float
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.
SEE ALSO
request.earnings
