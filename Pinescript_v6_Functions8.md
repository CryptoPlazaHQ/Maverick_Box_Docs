array.new_colorarray.new_boolarray.getarray.slicearray.sort
array.new_int()
The function creates a new array object of int type elements.
SYNTAX
array.new_int(size, initial_value) → array<int>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (series int) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("array.new_int example")
length = 5
a = array.new_int(length, int(close))
plot(array.sum(a) / length)
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
SEE ALSO
array.new_floatarray.getarray.slicearray.sort
array.new_label()
The function creates a new array object of label type elements.
SYNTAX
array.new_label(size, initial_value) → array<label>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (series label) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("array.new_label example", overlay = true, max_labels_count = 500)

//@variable The number of labels to show on the chart.
int labelCount = input.int(50, "Labels to show", 1, 500)

//@variable An array of `label` objects.
var array<label> labelArray = array.new_label()

//@variable A `chart.point` for the new label.
labelPoint = chart.point.from_index(bar_index, close)
//@variable The text in the new label.
string labelText = na
//@variable The color of the new label.
color labelColor = na
//@variable The style of the new label.
string labelStyle = na

// Set the label attributes for rising bars.
if close > open
    labelText  := "Rising"
    labelColor := color.green
    labelStyle := label.style_label_down
// Set the label attributes for falling bars.
else if close < open
    labelText  := "Falling"
    labelColor := color.red
    labelStyle := label.style_label_up

// Add a new label to the `labelArray` when the chart bar closed at a new value.
if close != open
    labelArray.push(label.new(labelPoint, labelText, color = labelColor, style = labelStyle))
// Remove the first element and delete its label when the size of the `labelArray` exceeds the `labelCount`.
if labelArray.size() > labelCount
    label.delete(labelArray.shift())
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
SEE ALSO
array.new_floatarray.getarray.slice
array.new_line()
The function creates a new array object of line type elements.
SYNTAX
array.new_line(size, initial_value) → array<line>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (series line) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("array.new_line example")
// draw last 15 lines
var a = array.new_line()
array.push(a, line.new(bar_index - 1, close[1], bar_index, close))
if array.size(a) > 15
    ln = array.shift(a)
    line.delete(ln)
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
SEE ALSO
array.new_floatarray.getarray.slice
array.new_linefill()
The function creates a new array object of linefill type elements.
SYNTAX
array.new_linefill(size, initial_value) → array<linefill>
ARGUMENTS
size (series int) Initial size of an array.
initial_value (series linefill) Initial value of all array elements.
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
array.new_string()
The function creates a new array object of string type elements.
SYNTAX
array.new_string(size, initial_value) → array<string>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (series string) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("array.new_string example")
length = 5
a = array.new_string(length, "text")
label.new(bar_index, close, array.get(a, 0))
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
SEE ALSO
array.new_floatarray.getarray.slice
array.new_table()
The function creates a new array object of table type elements.
SYNTAX
array.new_table(size, initial_value) → array<table>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (series table) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("table array")
tables = array.new_table()
array.push(tables, table.new(position = position.top_left, rows = 1, columns = 2, bgcolor = color.yellow, border_width=1))
plot(1)
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
SEE ALSO
array.new_floatarray.getarray.slice
array.new<type>()
The function creates a new array object of <type> elements.
SYNTAX
array.new<type>(size, initial_value) → array<type>
ARGUMENTS
size (series int) Initial size of an array. Optional. The default is 0.
initial_value (<array_type>) Initial value of all array elements. Optional. The default is 'na'.
EXAMPLE
//@version=6
indicator("array.new<string> example")
a = array.new<string>(1, "Hello, World!")
label.new(bar_index, close, array.get(a, 0))
EXAMPLE
//@version=6
indicator("array.new<color> example")
a = array.new<color>()
array.push(a, color.red)
array.push(a, color.green)
plot(close, color = array.get(a, close > open ? 1 : 0))
EXAMPLE
//@version=6
indicator("array.new<float> example")
length = 5
var a = array.new<float>(length, close)
if array.size(a) == length
    array.remove(a, 0)
    array.push(a, close)
plot(array.sum(a) / length, "SMA")
EXAMPLE
//@version=6
indicator("array.new<line> example")
// draw last 15 lines
var a = array.new<line>()
array.push(a, line.new(bar_index - 1, close[1], bar_index, close))
if array.size(a) > 15
    ln = array.shift(a)
    line.delete(ln)
RETURNS
The ID of an array object which may be used in other array.*() functions.
REMARKS
An array index starts from 0.
If you want to initialize an array and specify all its elements at the same time, then use the function array.from.
SEE ALSO
array.fromarray.pusharray.getarray.sizearray.removearray.shiftarray.sum
array.percentile_linear_interpolation()2 overloads
Returns the value for which the specified percentage of array values (percentile) are less than or equal to it, using linear interpolation.
SYNTAX & OVERLOADS
array.percentile_linear_interpolation(id, percentage) → series float
array.percentile_linear_interpolation(id, percentage) → series int
ARGUMENTS
id (array<int/float>) An array object.
percentage (series int/float) The percentage of values that must be equal or less than the returned value.
REMARKS
In statistics, the percentile is the percent of ranking items that appear at or below a certain score. This measurement shows the percentage of scores within a standard frequency distribution that is lower than the percentile rank you're measuring. Linear interpolation estimates the value between two ranks.
SEE ALSO
array.new_floatarray.insertarray.slicearray.reverseorder.ascendingorder.descending
array.percentile_nearest_rank()2 overloads
Returns the value for which the specified percentage of array values (percentile) are less than or equal to it, using the nearest-rank method.
SYNTAX & OVERLOADS
array.percentile_nearest_rank(id, percentage) → series float
array.percentile_nearest_rank(id, percentage) → series int
ARGUMENTS
id (array<int/float>) An array object.
percentage (series int/float) The percentage of values that must be equal or less than the returned value.
REMARKS
In statistics, the percentile is the percent of ranking items that appear at or below a certain score. This measurement shows the percentage of scores within a standard frequency distribution that is lower than the percentile rank you're measuring.
SEE ALSO
array.new_floatarray.insertarray.slicearray.reverseorder.ascendingorder.descending
array.percentrank()2 overloads
Returns the percentile rank of the element at the specified index.
SYNTAX & OVERLOADS
array.percentrank(id, index) → series float
array.percentrank(id, index) → series int
ARGUMENTS
id (array<int/float>) An array object.
index (series int) The index of the element for which the percentile rank should be calculated.
REMARKS
Percentile rank is the percentage of how many elements in the array are less than or equal to the reference value.
SEE ALSO
array.new_floatarray.insertarray.slicearray.reverseorder.ascendingorder.descending
array.pop()
The function removes the last element from an array and returns its value.
SYNTAX
array.pop(id) → series <type>
ARGUMENTS
id (any array type) An array object.
EXAMPLE
//@version=6
indicator("array.pop example")
a = array.new_float(5,high)
removedEl = array.pop(a)
plot(array.size(a))
plot(removedEl)
RETURNS
The value of the removed element.
SEE ALSO
array.new_floatarray.setarray.pusharray.removearray.insertarray.shift
array.push()
The function appends a value to an array.
SYNTAX
array.push(id, value) → void
ARGUMENTS
id (any array type) An array object.
value (series <type of the array's elements>) The value of the element added to the end of the array.
EXAMPLE
//@version=6
indicator("array.push example")
a = array.new_float(5, 0)
array.push(a, open)
plot(array.get(a, 5))
SEE ALSO
array.new_floatarray.setarray.insertarray.removearray.poparray.unshift
array.range()2 overloads
The function returns the difference between the min and max values from a given array.
SYNTAX & OVERLOADS
array.range(id) → series float
array.range(id) → series int
ARGUMENTS
id (array<int/float>) An array object.
EXAMPLE
//@version=6
indicator("array.range example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
plot(array.range(a))
RETURNS
The difference between the min and max values in the array.
SEE ALSO
array.new_floatarray.minarray.maxarray.sum
array.remove()
The function changes the contents of an array by removing the element with the specified index.
SYNTAX
array.remove(id, index) → series <type>
ARGUMENTS
id (any array type) An array object.
index (series int) The index of the element to remove.
EXAMPLE
//@version=6
indicator("array.remove example")
a = array.new_float(5,high)
removedEl = array.remove(a, 0)
plot(array.size(a))
plot(removedEl)
RETURNS
The value of the removed element.
REMARKS
If the index is positive, the function counts forwards from the beginning of the array to the end. The index of the first element is 0, and the index of the last element is array.size() - 1. If the index is negative, the function counts backwards from the end of the array to the beginning. In this case, the index of the last element is -1, and the index of the first element is negative array.size(). For example, for an array that contains three elements, all of the following are valid arguments for the index parameter: 0, 1, 2, -1, -2, -3.
SEE ALSO
array.new_floatarray.setarray.pusharray.insertarray.poparray.shift
array.reverse()
The function reverses an array. The first array element becomes the last, and the last array element becomes the first.
SYNTAX
array.reverse(id) → void
ARGUMENTS
id (any array type) An array object.
EXAMPLE
//@version=6
indicator("array.reverse example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
plot(array.get(a, 0))
array.reverse(a)
plot(array.get(a, 0))
SEE ALSO
array.new_floatarray.sortarray.pusharray.setarray.avg
array.set()
The function sets the value of the element at the specified index.
SYNTAX
array.set(id, index, value) → void
ARGUMENTS
id (any array type) An array object.
index (series int) The index of the element to be modified.
value (series <type of the array's elements>) The new value to be set.
EXAMPLE
//@version=6
indicator("array.set example")
a = array.new_float(10)
for i = 0 to 9
    array.set(a, i, close[i])
plot(array.sum(a) / 10)
REMARKS
If the index is positive, the function counts forwards from the beginning of the array to the end. The index of the first element is 0, and the index of the last element is array.size() - 1. If the index is negative, the function counts backwards from the end of the array to the beginning. In this case, the index of the last element is -1, and the index of the first element is negative array.size(). For example, for an array that contains three elements, all of the following are valid arguments for the index parameter: 0, 1, 2, -1, -2, -3.
SEE ALSO
array.new_floatarray.getarray.slice
array.shift()
The function removes an array's first element and returns its value.
SYNTAX
array.shift(id) → series <type>
ARGUMENTS
id (any array type) An array object.
EXAMPLE
//@version=6
indicator("array.shift example")
a = array.new_float(5,high)
removedEl = array.shift(a)
plot(array.size(a))
plot(removedEl)
RETURNS
The value of the removed element.
SEE ALSO
array.unshiftarray.setarray.pusharray.removearray.includes
array.size()
The function returns the number of elements in an array.
SYNTAX
array.size(id) → series int
ARGUMENTS
id (any array type) An array object.
EXAMPLE
//@version=6
indicator("array.size example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
// note that changes in slice also modify original array
slice = array.slice(a, 0, 5)
array.push(slice, open)
// size was changed in slice and in original array
plot(array.size(a))
plot(array.size(slice))
RETURNS
The number of elements in the array.
SEE ALSO
array.new_floatarray.sumarray.slicearray.sort
array.slice()
The function creates a slice from an existing array. If an object from the slice changes, the changes are applied to both the new and the original arrays.
SYNTAX
array.slice(id, index_from, index_to) → array<type>
ARGUMENTS
id (any array type) An array object.
index_from (series int) Zero-based index at which to begin extraction.
index_to (series int) Zero-based index before which to end extraction. The function extracts up to but not including the element with this index.
EXAMPLE
//@version=6
indicator("array.slice example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
// take elements from 0 to 4
// *note that changes in slice also modify original array 
slice = array.slice(a, 0, 5)
plot(array.sum(a) / 10)
plot(array.sum(slice) / 5)
RETURNS
A shallow copy of an array's slice.
SEE ALSO
array.new_floatarray.getarray.slicearray.sort
array.some()
Returns true if at least one element of the id array is true, false otherwise.
SYNTAX
array.some(id) → series bool
ARGUMENTS
id (array<bool>) An array object.
REMARKS
This function also works with arrays of int and float types, in which case zero values are considered false, and all others true.
SEE ALSO
array.everyarray.get
array.sort()
The function sorts the elements of an array.
SYNTAX
array.sort(id, order) → void
ARGUMENTS
id (array<int/float/string>) An array object.
order (series sort_order) The sort order: order.ascending (default) or order.descending.
EXAMPLE
//@version=6
indicator("array.sort example")
a = array.new_float(0,0)
for i = 0 to 5
    array.push(a, high[i])
array.sort(a, order.descending)
if barstate.islast
    label.new(bar_index, close, str.tostring(a))
SEE ALSO
array.new_floatarray.insertarray.slicearray.reverseorder.ascendingorder.descending
array.sort_indices()
Returns an array of indices which, when used to index the original array, will access its elements in their sorted order. It does not modify the original array.
SYNTAX
array.sort_indices(id, order) → array<int>
ARGUMENTS
id (array<int/float/string>) An array object.
order (series sort_order) The sort order: order.ascending or order.descending. Optional. The default is order.ascending.
EXAMPLE
//@version=6
indicator("array.sort_indices")
a = array.from(5, -2, 0, 9, 1)
sortedIndices = array.sort_indices(a) // [1, 2, 4, 0, 3]
indexOfSmallestValue = array.get(sortedIndices, 0) // 1
smallestValue = array.get(a, indexOfSmallestValue) // -2
plot(smallestValue)
SEE ALSO
array.new_floatarray.insertarray.slicearray.reverseorder.ascendingorder.descending
array.standardize()2 overloads
The function returns the array of standardized elements.
SYNTAX & OVERLOADS
array.standardize(id) → array<float>
array.standardize(id) → array<int>
ARGUMENTS
id (array<int/float>) An array object.
EXAMPLE
//@version=6
indicator("array.standardize example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
b = array.standardize(a)
plot(array.min(b))
plot(array.max(b))
RETURNS
The array of standardized elements.
SEE ALSO
array.maxarray.minarray.modearray.avgarray.variancearray.stdev
array.stdev()2 overloads
The function returns the standard deviation of an array's elements.
SYNTAX & OVERLOADS
array.stdev(id, biased) → series float
array.stdev(id, biased) → series int
ARGUMENTS
id (array<int/float>) An array object.
biased (series bool) Determines which estimate should be used. Optional. The default is true.
EXAMPLE
//@version=6
indicator("array.stdev example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
plot(array.stdev(a))
RETURNS
The standard deviation of the array's elements.
REMARKS
If biased is true, function will calculate using a biased estimate of the entire population, if false - unbiased estimate of a sample.
SEE ALSO
array.new_floatarray.maxarray.minarray.avg
array.sum()2 overloads
The function returns the sum of an array's elements.
SYNTAX & OVERLOADS
array.sum(id) → series float
array.sum(id) → series int
ARGUMENTS
id (array<int/float>) An array object.
EXAMPLE
//@version=6
indicator("array.sum example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
plot(array.sum(a))
RETURNS
The sum of the array's elements.
SEE ALSO
array.new_floatarray.maxarray.min
array.unshift()
The function inserts the value at the beginning of the array.
SYNTAX
array.unshift(id, value) → void
ARGUMENTS
id (any array type) An array object.
value (series <type of the array's elements>) The value to add to the start of the array.
EXAMPLE
//@version=6
indicator("array.unshift example")
a = array.new_float(5, 0)
array.unshift(a, open)
plot(array.get(a, 0))
SEE ALSO
array.shiftarray.setarray.insertarray.removearray.indexof
array.variance()2 overloads
The function returns the variance of an array's elements.
SYNTAX & OVERLOADS
array.variance(id, biased) → series float
array.variance(id, biased) → series int
ARGUMENTS
id (array<int/float>) An array object.
biased (series bool) Determines which estimate should be used. Optional. The default is true.
EXAMPLE
//@version=6
indicator("array.variance example")
a = array.new_float(0)
for i = 0 to 9
    array.push(a, close[i])
plot(array.variance(a))
RETURNS
The variance of the array's elements.
REMARKS
If biased is true, function will calculate using a biased estimate of the entire population, if false - unbiased estimate of a sample.
SEE ALSO
array.new_floatarray.stdevarray.minarray.avgarray.covariance
barcolor()
Set color of bars.
SYNTAX
barcolor(color, offset, editable, show_last, title, display) → void
ARGUMENTS
color (series color) Color of bars. You can use constants like 'red' or '#ff001a' as well as complex expressions like 'close >= open ? color.green : color.red'. Required argument.
offset (simple int) Shifts the color series to the left or to the right on the given number of bars. Default is 0.
editable (const bool) If true then barcolor style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
title (const string) Title of the barcolor. Optional argument.
display (input plot_simple_display) Controls where the barcolor is displayed. Possible values are: display.none, display.all. Default is display.all.
EXAMPLE
//@version=6
indicator("barcolor example", overlay=true)
barcolor(close < open ? color.black : color.white)
SEE ALSO
bgcolorplotfill
bgcolor()
Fill background of bars with specified color.
SYNTAX
bgcolor(color, offset, editable, show_last, title, display, force_overlay) → void
ARGUMENTS
color (series color) Color of the filled background. You can use constants like 'red' or '#ff001a' as well as complex expressions like 'close >= open ? color.green : color.red'. Required argument.
offset (simple int) Shifts the color series to the left or to the right on the given number of bars. Default is 0.
editable (const bool) If true then bgcolor style will be editable in Format dialog. Default is true.
show_last (input int) Optional. The number of bars, counting backwards from the most recent bar, on which the function can draw.
title (const string) Title of the bgcolor. Optional argument.
display (input plot_simple_display) Controls where the bgcolor is displayed. Possible values are: display.none, display.all. Default is display.all.
force_overlay (const bool) If true, the plotted results will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
EXAMPLE
//@version=6
indicator("bgcolor example", overlay=true)
bgcolor(close < open ? color.new(color.red,70) : color.new(color.green, 70))
SEE ALSO
barcolorplotfill
bool()4 overloads
Converts the x value to a bool value. Returns false if x is na, false, or an int/float value equal to 0. Returns true for all other possible values.
SYNTAX & OVERLOADS
bool(x) → const bool
bool(x) → input bool
bool(x) → simple bool
bool(x) → series bool
ARGUMENTS
x (simple int/float/bool) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to bool.
SEE ALSO
floatintcolorstringlinelabel
box()
Casts na to box.
SYNTAX
box(x) → series box
ARGUMENTS
x (series box) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to box.
SEE ALSO
floatintboolcolorstringlinelabel
box.copy()
Clones the box object.
SYNTAX
box.copy(id) → series box
ARGUMENTS
id (series box) Box object.
EXAMPLE
//@version=6
indicator('Last 50 bars price ranges', overlay = true)
LOOKBACK = 50
highest = ta.highest(LOOKBACK)
lowest = ta.lowest(LOOKBACK)
if barstate.islastconfirmedhistory
    var BoxLast = box.new(bar_index[LOOKBACK], highest, bar_index, lowest, bgcolor = color.new(color.green, 80))
    var BoxPrev = box.copy(BoxLast)
    box.set_lefttop(BoxPrev, bar_index[LOOKBACK * 2], highest[50])
    box.set_rightbottom(BoxPrev, bar_index[LOOKBACK], lowest[50])
    box.set_bgcolor(BoxPrev, color.new(color.red, 80))
SEE ALSO
box.newbox.delete
box.delete()
Deletes the specified box object. If it has already been deleted, does nothing.
SYNTAX
box.delete(id) → void
ARGUMENTS
id (series box) A box object to delete.
SEE ALSO
box.new
box.get_bottom()
Returns the price value of the bottom border of the box.
SYNTAX
box.get_bottom(id) → series float
ARGUMENTS
id (series box) A box object.
RETURNS
The price value.
SEE ALSO
box.newbox.set_bottom
box.get_left()
Returns the bar index or the UNIX time (depending on the last value used for 'xloc') of the left border of the box.
SYNTAX
box.get_left(id) → series int
ARGUMENTS
id (series box) A box object.
RETURNS
A bar index or a UNIX timestamp (in milliseconds).
SEE ALSO
box.newbox.set_left
box.get_right()
Returns the bar index or the UNIX time (depending on the last value used for 'xloc') of the right border of the box.
SYNTAX
box.get_right(id) → series int
ARGUMENTS
id (series box) A box object.
RETURNS
A bar index or a UNIX timestamp (in milliseconds).
SEE ALSO
box.newbox.set_right
box.get_top()
Returns the price value of the top border of the box.
SYNTAX
box.get_top(id) → series float
ARGUMENTS
id (series box) A box object.
RETURNS
The price value.
SEE ALSO
box.newbox.set_top
box.new()2 overloads
Creates a new box object.
SYNTAX & OVERLOADS
box.new(top_left, bottom_right, border_color, border_width, border_style, extend, xloc, bgcolor, text, text_size, text_color, text_halign, text_valign, text_wrap, text_font_family, force_overlay, text_formatting) → series box
box.new(left, top, right, bottom, border_color, border_width, border_style, extend, xloc, bgcolor, text, text_size, text_color, text_halign, text_valign, text_wrap, text_font_family, force_overlay, text_formatting) → series box
ARGUMENTS
top_left (chart.point) A chart.point object that specifies the top-left corner location of the box.
bottom_right (chart.point) A chart.point object that specifies the bottom-right corner location of the box.
border_color (series color) Color of the four borders. Optional. The default is color.blue.
border_width (series int) Width of the four borders, in pixels. Optional. The default is 1 pixel.
border_style (series string) Style of the four borders. Possible values: line.style_solid, line.style_dotted, line.style_dashed. Optional. The default value is line.style_solid.
extend (series string) When extend.none is used, the horizontal borders start at the left border and end at the right border. With extend.left or extend.right, the horizontal borders are extended indefinitely to the left or right of the box, respectively. With extend.both, the horizontal borders are extended on both sides. Optional. The default value is extend.none.
xloc (series string) Determines whether the arguments to 'left' and 'right' are a bar index or a time value. If xloc = xloc.bar_index, the arguments must be a bar index. If xloc = xloc.bar_time, the arguments must be a UNIX time. Possible values: xloc.bar_index and xloc.bar_time. Optional. The default is xloc.bar_index.
bgcolor (series color) Background color of the box. Optional. The default is color.blue.
text (series string) The text to be displayed inside the box. Optional. The default is empty string.
text_size (series int/string) Optional. Size of the box's text. The size can be any positive integer, or one of the size.* built-in constant strings. The constant strings and their equivalent integer values are: size.auto (0), size.tiny (8), size.small (10), size.normal (14), size.large (20), size.huge (36). The default value is size.auto or 0.
text_color (series color) The color of the text. Optional. The default is color.black.
text_halign (series string) The horizontal alignment of the box's text. Optional. The default value is text.align_center. Possible values: text.align_left, text.align_center, text.align_right.
text_valign (series string) The vertical alignment of the box's text. Optional. The default value is text.align_center. Possible values: text.align_top, text.align_center, text.align_bottom.
text_wrap (series string) Optional. Whether to wrap text. Wrapped text starts a new line when it reaches the side of the box. Wrapped text lower than the bottom of the box is not displayed. Unwrapped text stays on a single line and is displayed past the width of the box if it is too long. If the text_size is 0 or text.wrap_auto, this setting has no effect. The default value is text.wrap_none. Possible values: text.wrap_none, text.wrap_auto.
text_font_family (series string) The font family of the text. Optional. The default value is font.family_default. Possible values: font.family_default, font.family_monospace.
force_overlay (const bool) If true, the drawing will display on the main chart pane, even when the script occupies a separate pane. Optional. The default is false.
text_formatting (const text_format) The formatting of the displayed text. Formatting options support addition. For example, text.format_bold + text.format_italic will make the text both bold and italicized. Possible values: text.format_none, text.format_bold, text.format_italic. Optional. The default is text.format_none.
EXAMPLE
//@version=6
indicator("box.new")
var b = box.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time, border_style=line.style_dashed)
box.set_lefttop(b, time, 100)
box.set_rightbottom(b, time + 60 * 60 * 24, 500)
box.set_bgcolor(b, color.green)
RETURNS
The ID of a box object which may be used in box.set_*() and box.get_*() functions.
SEE ALSO
box.deletebox.get_leftbox.get_topbox.get_rightbox.get_bottombox.set_top_left_pointbox.set_leftbox.set_topbox.set_bottom_right_pointbox.set_rightbox.set_bottombox.set_border_colorbox.set_bgcolorbox.set_border_widthbox.set_border_stylebox.set_extendbox.set_textbox.set_text_formatting
box.set_bgcolor()
Sets the background color of the box.
SYNTAX
box.set_bgcolor(id, color) → void
ARGUMENTS
id (series box) A box object.
color (series color) New background color.
SEE ALSO
box.new
box.set_border_color()
Sets the border color of the box.
SYNTAX
box.set_border_color(id, color) → void
ARGUMENTS
id (series box) A box object.
color (series color) New border color.
SEE ALSO
box.new
box.set_border_style()
Sets the border style of the box.
SYNTAX
box.set_border_style(id, style) → void
ARGUMENTS
id (series box) A box object.
style (series string) New border style.
SEE ALSO
box.newline.style_solid
box.set_border_width()
Sets the border width of the box.
SYNTAX
box.set_border_width(id, width) → void
ARGUMENTS
id (series box) A box object.
width (series int) Width of the four borders, in pixels.
SEE ALSO
box.new
box.set_bottom()
Sets the bottom coordinate of the box.
SYNTAX
box.set_bottom(id, bottom) → void
ARGUMENTS
id (series box) A box object.
bottom (series int/float) Price value of the bottom border.
SEE ALSO
box.newbox.get_bottom
box.set_bottom_right_point()
Sets the bottom-right corner location of the id box to point.
SYNTAX
box.set_bottom_right_point(id, point) → void
ARGUMENTS
id (series box) A box object.
point (chart.point) A chart.point object.
box.set_extend()
Sets extending type of the border of this box object. When extend.none is used, the horizontal borders start at the left border and end at the right border. With extend.left or extend.right, the horizontal borders are extended indefinitely to the left or right of the box, respectively. With extend.both, the horizontal borders are extended on both sides.
SYNTAX
box.set_extend(id, extend) → void
ARGUMENTS
id (series box) A box object.
extend (series string) New extending type.
SEE ALSO
box.newextend.none
box.set_left()
Sets the left coordinate of the box.
SYNTAX
box.set_left(id, left) → void
ARGUMENTS
id (series box) A box object.
left (series int) Bar index or bar time of the left border. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
SEE ALSO
box.newbox.get_left
box.set_lefttop()
Sets the left and top coordinates of the box.
SYNTAX
box.set_lefttop(id, left, top) → void
ARGUMENTS
id (series box) A box object.
left (series int) Bar index or bar time of the left border.
top (series int/float) Price value of the top border.
SEE ALSO
box.newbox.get_leftbox.get_top
box.set_right()
Sets the right coordinate of the box.
SYNTAX
box.set_right(id, right) → void
ARGUMENTS
id (series box) A box object.
right (series int) Bar index or bar time of the right border. Note that objects positioned using xloc.bar_index cannot be drawn further than 500 bars into the future.
SEE ALSO
box.newbox.get_right
box.set_rightbottom()
Sets the right and bottom coordinates of the box.
SYNTAX
box.set_rightbottom(id, right, bottom) → void
ARGUMENTS
id (series box) A box object.
right (series int) Bar index or bar time of the right border.
bottom (series int/float) Price value of the bottom border.
SEE ALSO
box.newbox.get_rightbox.get_bottom
box.set_text()
The function sets the text in the box.
SYNTAX
box.set_text(id, text) → void
ARGUMENTS
id (series box) A box object.
text (series string) The text to be displayed inside the box.
SEE ALSO
box.set_text_colorbox.set_text_sizebox.set_text_valignbox.set_text_halignbox.set_text_formatting
box.set_text_color()
The function sets the color of the text inside the box.
SYNTAX
box.set_text_color(id, text_color) → void
ARGUMENTS
id (series box) A box object.
text_color (series color) The color of the text.
SEE ALSO
box.set_textbox.set_text_sizebox.set_text_valignbox.set_text_halign
box.set_text_font_family()
The function sets the font family of the text inside the box.
SYNTAX
box.set_text_font_family(id, text_font_family) → void
ARGUMENTS
id (series box) A box object.
text_font_family (series string) The font family of the text. Possible values: font.family_default, font.family_monospace.
EXAMPLE
//@version=6
indicator("Example of setting the box font")
if barstate.islastconfirmedhistory
    b = box.new(bar_index, open-ta.tr, bar_index-50, open-ta.tr*5, text="monospace")
    box.set_text_font_family(b, font.family_monospace)
SEE ALSO
box.newfont.family_defaultfont.family_monospace
box.set_text_formatting()
Sets the formatting attributes the drawing applies to displayed text.
SYNTAX
box.set_text_formatting(id, text_formatting) → void
ARGUMENTS
id (series box) A box object.
text_formatting (const text_format) The formatting of the displayed text. Formatting options support addition. For example, text.format_bold + text.format_italic will make the text both bold and italicized. Possible values: text.format_none, text.format_bold, text.format_italic.
SEE ALSO
box.set_text_colorbox.set_text_sizebox.set_text_valignbox.set_text_halignbox.set_text
box.set_text_halign()
The function sets the horizontal alignment of the box's text.
SYNTAX
box.set_text_halign(id, text_halign) → void
ARGUMENTS
id (series box) A box object.
text_halign (series string) The horizontal alignment of a box's text. Possible values: text.align_left, text.align_center, text.align_right.
SEE ALSO
box.set_textbox.set_text_sizebox.set_text_valignbox.set_text_color
box.set_text_size()
The function sets the size of the box's text.
SYNTAX
box.set_text_size(id, text_size) → void
ARGUMENTS
id (series box) A box object.
text_size (series int/string) Size of the box's text. The size can be any positive integer, or one of the size.* built-in constant strings. The constant strings and their equivalent integer values are: size.auto (0), size.tiny (8), size.small (10), size.normal (14), size.large (20), size.huge (36).
SEE ALSO
box.set_textbox.set_text_colorbox.set_text_valignbox.set_text_halign
box.set_text_valign()
The function sets the vertical alignment of a box's text.
SYNTAX
box.set_text_valign(id, text_valign) → void
ARGUMENTS
id (series box) A box object.
text_valign (series string) The vertical alignment of the box's text. Possible values: text.align_top, text.align_center, text.align_bottom.
SEE ALSO
box.set_textbox.set_text_sizebox.set_text_colorbox.set_text_halign
box.set_text_wrap()
The function sets the mode of wrapping of the text inside the box.
SYNTAX
box.set_text_wrap(id, text_wrap) → void
ARGUMENTS
id (series box) A box object.
text_wrap (series string) Whether to wrap text. Wrapped text starts a new line when it reaches the side of the box. Wrapped text lower than the bottom of the box is not displayed. Unwrapped text stays on a single line and is displayed past the width of the box if it is too long. If the text_size is 0 or text.wrap_auto, this setting has no effect. Possible values: text.wrap_none, text.wrap_auto.
SEE ALSO
box.set_textbox.set_text_sizebox.set_text_valignbox.set_text_halignbox.set_text_color
box.set_top()
Sets the top coordinate of the box.
SYNTAX
box.set_top(id, top) → void
ARGUMENTS
id (series box) A box object.
top (series int/float) Price value of the top border.
SEE ALSO
box.newbox.get_top
box.set_top_left_point()
Sets the top-left corner location of the id box to point.
SYNTAX
box.set_top_left_point(id, point) → void
ARGUMENTS
id (series box) A box object.
point (chart.point) A chart.point object.
chart.point.copy()
Creates a copy of a chart.point object with the specified id.
SYNTAX
chart.point.copy(id) → chart.point
ARGUMENTS
id (chart.point) A chart.point object.
chart.point.from_index()
Returns a chart.point object with index as its x-coordinate and price as its y-coordinate.
SYNTAX
chart.point.from_index(index, price) → chart.point
ARGUMENTS
index (series int) The x-coordinate of the point, expressed as a bar index value.
price (series int/float) The y-coordinate of the point.
REMARKS
The time field values of chart.point instances returned from this function will be na, meaning drawing objects with xloc values set to xloc.bar_time will not work with them.
chart.point.from_time()
Returns a chart.point object with time as its x-coordinate and price as its y-coordinate.
SYNTAX
chart.point.from_time(time, price) → chart.point
ARGUMENTS
time (series int) The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
price (series int/float) The y-coordinate of the point.
REMARKS
The index field values of chart.point instances returned from this function will be na, meaning drawing objects with xloc values set to xloc.bar_index will not work with them.
chart.point.new()
Creates a new chart.point object with the specified time, index, and price.
SYNTAX
chart.point.new(time, index, price) → chart.point
ARGUMENTS
time (series int) The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
index (series int) The x-coordinate of the point, expressed as a bar index value.
price (series int/float) The y-coordinate of the point.
REMARKS
Whether a drawing object uses a point's time or index field as an x-coordinate depends on the xloc type used in the function call that returned the drawing.
It's important to note that this function does not verify that the time and index values refer to the same bar.
SEE ALSO
polyline.new
chart.point.now()
Returns a chart.point object with price as the y-coordinate
SYNTAX
chart.point.now(price) → chart.point
ARGUMENTS
price (series int/float) The y-coordinate of the point. Optional. The default is close.
REMARKS
The chart.point instance returned from this function records values for its index and time fields on the bar it executed on, making it suitable for use with drawing objects of any xloc type.
color()4 overloads
Casts na to color
SYNTAX & OVERLOADS
color(x) → const color
color(x) → input color
color(x) → simple color
color(x) → series color
ARGUMENTS
x (const color) The value to convert to the specified type, usually na.
RETURNS
The value of the argument after casting to color.
