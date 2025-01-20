earnings.future_period_end_time
Checks the data for the next earnings report and returns the UNIX timestamp of the day when the financial period covered by those earnings ends, or na if this data isn't available.
TYPE
series int
RETURNS
UNIX time, expressed in milliseconds.
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.
SEE ALSO
request.earnings
earnings.future_revenue
Returns the estimated Revenue of the next earnings report in the currency of the instrument, or na if this data isn't available.
TYPE
series float
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.
SEE ALSO
request.earnings
earnings.future_time
Returns a UNIX timestamp indicating the expected time of the next earnings report, or na if this data isn't available.
TYPE
series int
RETURNS
UNIX time, expressed in milliseconds.
REMARKS
This value is only fetched once during the script's initial calculation. The variable will return the same value until the script is recalculated, even after the expected time of the next earnings report.
SEE ALSO
request.earnings
high
Current high price.
TYPE
series float
REMARKS
Previous values may be accessed with square brackets operator [], e.g. high[1], high[2].
SEE ALSO
openlowclosevolumetimehl2hlc3hlcc4ohlc4
hl2
Is a shortcut for (high + low)/2
TYPE
series float
SEE ALSO
openhighlowclosevolumetimehlc3hlcc4ohlc4
hlc3
Is a shortcut for (high + low + close)/3
TYPE
series float
SEE ALSO
openhighlowclosevolumetimehl2hlcc4ohlc4
hlcc4
Is a shortcut for (high + low + close + close)/4
TYPE
series float
SEE ALSO
openhighlowclosevolumetimehl2hlc3ohlc4
hour
Current bar hour in exchange timezone.
TYPE
series int
SEE ALSO
hourtimeyearmonthweekofyeardayofmonthdayofweekminutesecond
label.all
Returns an array filled with all the current labels drawn by the script.
TYPE
array<label>
EXAMPLE
//@version=6
indicator("label.all")
//delete all labels
label.new(bar_index, close)
a_allLabels = label.all
if array.size(a_allLabels) > 0
    for i = 0 to array.size(a_allLabels) - 1
        label.delete(array.get(a_allLabels, i))
REMARKS
The array is read-only. Index zero of the array is the ID of the oldest object on the chart.
SEE ALSO
label.newline.allbox.alltable.all
last_bar_index
Bar index of the last chart bar. Bar indices begin at zero on the first bar.
TYPE
series int
EXAMPLE
//@version=6
strategy("Mark Last X Bars For Backtesting", overlay = true, calc_on_every_tick = true)
lastBarsFilterInput = input.int(100, "Bars Count:")
// Here, we store the 'last_bar_index' value that is known from the beginning of the script's calculation.
// The 'last_bar_index' will change when new real-time bars appear, so we declare 'lastbar' with the 'var' keyword.
var lastbar = last_bar_index
// Check if the current bar_index is 'lastBarsFilterInput' removed from the last bar on the chart, or the chart is traded in real-time.
allowedToTrade = (lastbar - bar_index <= lastBarsFilterInput) or barstate.isrealtime
bgcolor(allowedToTrade ? color.new(color.green, 80) : na)
RETURNS
Last historical bar index for closed markets, or the real-time bar index for open markets.
REMARKS
Please note that using this variable can cause indicator repainting.
SEE ALSO
bar_indexlast_bar_timebarstate.ishistorybarstate.isrealtime
last_bar_time
Time in UNIX format of the last chart bar. It is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
TYPE
series int
REMARKS
Please note that using this variable/function can cause indicator repainting.
Note that this variable returns the timestamp based on the time of the bar's open.
SEE ALSO
timetimenowtimestamplast_bar_index
