 var x = close
    b := x
    green_bars_count := green_bars_count + 1
    if green_bars_count >= 10
        var y = close
        c := y
plot(a)
plot(b)
plot(c)
The variable 'a' keeps the closing price of the first bar for each bar in the series.
The variable 'b' keeps the closing price of the first "green" bar in the series.
The variable 'c' keeps the closing price of the tenth "green" bar in the series.
varip
varip (var intrabar persist) is the keyword used for the assignment and one-time initialization of a variable or a field of a user-defined type. It’s similar to the var keyword, but variables and fields declared with varip retain their values between executions of the script on the same bar.
SYNTAX
varip [<variable_type> ]<variable_name> = <expression>

[export ]type <UDT_identifier>
    varip <field_type> <field_name> [= <value>]
where:
variable_type - An optional fundamental type (int, float, bool, color, string) or a user-defined type, or an array or matrix of one of those types. Special types are not compatible with this keyword.
variable_name - A valid identifier. The variable can also be an object created from a UDT.
expression - Any arithmetic expression, just as when defining a regular variable. The expression will be calculated and assigned to the variable only once, on the first bar.
UDT_identifier, field_type, field_name, value - Constructs related to user-defined types as described in the type section.
EXAMPLE
//@version=6
indicator("varip")
varip int v = -1
v := v + 1
plot(v)
With var, v would equal the value of the bar_index. On historical bars, where the script calculates only once per chart bar, the value of v is the same as with var. However, on realtime bars, the script will evaluate the expression on each new chart update, producing a different result.
EXAMPLE
//@version=6
indicator("varip with types")
type barData
    int index = -1
    varip int ticks = -1

var currBar = barData.new()
currBar.index += 1
currBar.ticks += 1

// Will be equal to bar_index on all bars
plot(currBar.index)
// In real time, will increment per every tick on the chart
plot(currBar.ticks)
The same += operation applied to both the index and ticks fields results in different real-time values because ticks increases on every chart update, while index only does so once per bar. Note how the currBar object does not use the varip keyword. The ticks field of the object can increment on every tick, but the reference itself is defined once and then stays unchanged. If we were to declare currBar using varip, the behavior of index would remain unchanged because while the reference to the type instance would persist between chart updates, the index field of the object would not.
REMARKS
When using varip to declare variables in strategies that may execute more than once per historical chart bar, the values of such variables are preserved across successive iterations of the script on the same bar.
The effect of varip eliminates the rollback of variables before each successive execution of a script on the same bar.
while
The while statement allows the conditional iteration of a local code block.
SYNTAX
variable_declaration = while condition
    …
    continue
    …
    break
    …
    return_expression
where:
variable_declaration - An optional variable declaration. The return expression can provide the initialization value for this variable.
condition - when true, the local block of the while statement is executed. When false, execution of the script resumes after the while statement.
continue - The continue keyword causes the loop to branch to its next iteration.
break - The break keyword causes the loop to terminate. The script's execution resumes after the while statement.
return_expression - An optional line providing the while statement's returning value.
EXAMPLE
//@version=6
indicator("while")
// This is a simple example of calculating a factorial using a while loop.
int i_n = input.int(10, "Factorial Size", minval=0)
int counter   = i_n
int factorial = 1
while counter > 0
    factorial := factorial * counter
    counter   := counter - 1

plot(factorial)
REMARKS
The local code block after the initial while line must be indented with four spaces or a tab. For the while loop to terminate, the boolean expression following while must eventually become false, or a break must be executed.
Types
array
Keyword used to explicitly declare the "array" type of a variable or a parameter. Array objects (or IDs) can be created with the array.new<type>, array.from function.
EXAMPLE
//@version=6
indicator("array", overlay=true)
array<float> a = na
a := array.new<float>(1, close)
plot(array.get(a, 0))
REMARKS
Array objects are always of "series" form.
SEE ALSO
varlinelabeltableboxarray.new<type>array.from
bool
Keyword used to explicitly declare the "bool" (boolean) type of a variable or a parameter. "Bool" variables can have values true or false.
EXAMPLE
//@version=6
indicator("bool")
bool b = true    // Same as `b = true`
plot(b ? open : close)
REMARKS
Explicitly mentioning the type in a variable declaration is optional. Learn more about Pine Script® types in the User Manual page on the Type System.
SEE ALSO
varvaripintfloatcolorstringtruefalse
box
Keyword used to explicitly declare the "box" type of a variable or a parameter. Box objects (or IDs) can be created with the box.new function.
EXAMPLE
//@version=6
indicator("box")
// Empty `box1` box ID.
var box box1 = na
// `box` type is unnecessary because `box.new()` returns a "box" type.
var box2 = box.new(na, na, na, na)
box3 = box.new(time, open, time + 60 * 60 * 24, close, xloc=xloc.bar_time)
REMARKS
Box objects are always of "series" form.
SEE ALSO
varlinelabeltablebox.new
chart.point
Keyword to explicitly declare the type of a variable or parameter as chart.point. Scripts can produce chart.point instances using the chart.point.from_time, chart.point.from_index, chart.point.now, and chart.point.new functions.
FIELDS
index (series int) The x-coordinate of the point, expressed as a bar index value.
time (series int) The x-coordinate of the point, expressed as a UNIX time value, in milliseconds.
price (series float) The y-coordinate of the point.
SEE ALSO
polyline
color
Keyword used to explicitly declare the "color" type of a variable or a parameter.
EXAMPLE
//@version=6
indicator("color", overlay = true)

color textColor = color.green
color labelColor = #FF000080 // Red color (FF0000) with 50% transparency (80 which is half of FF).
if barstate.islastconfirmedhistory
    label.new(bar_index, high, text = "Label", color = labelColor, textcolor = textColor)

// When declaring variables with color literals, built-in constants(color.green) or functions (color.new(), color.rgb()), the "color" keyword for the type can be omitted.
c = color.rgb(0,255,0,0)
plot(close, color = c)
REMARKS
Color literals have the following format: #RRGGBB or #RRGGBBAA. The letter pairs represent 00 to FF hexadecimal values (0 to 255 in decimal) where RR, GG and BB pairs are the values for the color's red, green and blue components. AA is an optional value for the color's transparency (or alpha component) where 00 is invisible and FF opaque. When no AA pair is supplied, FF is used. The hexadecimal letters can be upper or lower case.
Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.
SEE ALSO
varvaripintfloatstringcolor.rgbcolor.new
const
The const keyword explicitly assigns the "const" type qualifier to variables and the parameters of non-exported functions. Variables and parameters with the "const" qualifier reference values established at compile time that never change in the script's execution.
In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "const" is the weakest.
Explicitly declaring a variable with the const keyword restricts the type qualifier to "const", meaning the variable cannot accept a value with a stronger qualifier (e.g., "input"), nor can the value assigned to the variable change at any point in the script's execution.
When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.
SYNTAX
[method ]<functionName>([const <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]const <variableType> <variableName> = <variableValue>
EXAMPLE
//@version=6
indicator("custom plot title")

//@function Concatenates two "const string" values.
concatStrings(const string x, const string y) =>
    const string result = x + y

//@variable The title of the plot.
const string myTitle = concatStrings("My ", "Plot")

plot(close, myTitle)
EXAMPLE
//@version=6
indicator("can't assign input to const")

//@variable A variable declared as "const float" that attempts to assign the result of `input.float()` as its value.
//          This declaration causes an error. The "input float" qualified type is stronger than "const float".
const float myVar = input.float(2.0)

plot(myVar)
REMARKS
To learn more, see our User Manual's section on type qualifiers.
SEE ALSO
simpleseries
float
Keyword used to explicitly declare the "float" (floating point) type of a variable or a parameter.
EXAMPLE
//@version=6
indicator("float")
float f = 3.14    // Same as `f = 3.14`
f := na
plot(f)
REMARKS
Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.
SEE ALSO
varvaripintboolcolorstring
int
Keyword used to explicitly declare the "int" (integer) type of a variable or a parameter.
EXAMPLE
//@version=6
indicator("int")
int i = 14    // Same as `i = 14`
i := na
plot(i)
REMARKS
Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.
SEE ALSO
varvaripfloatboolcolorstring
label
Keyword used to explicitly declare the "label" type of a variable or a parameter. Label objects (or IDs) can be created with the label.new function.
EXAMPLE
//@version=6
indicator("label")
// Empty `label1` label ID.
var label label1 = na
// `label` type is unnecessary because `label.new()` returns "label" type.
var label2 = label.new(na, na, na)
if barstate.islastconfirmedhistory
    label3 = label.new(bar_index, high, text = "label3 text")
REMARKS
Label objects are always of "series" form.
SEE ALSO
varlineboxlabel.new
line
Keyword used to explicitly declare the "line" type of a variable or a parameter. Line objects (or IDs) can be created with the line.new function.
EXAMPLE
//@version=6
indicator("line")
// Empty `line1` line ID.
var line line1 = na
// `line` type is unnecessary because `line.new()` returns "line" type.
var line2 = line.new(na, na, na, na)
line3 = line.new(bar_index - 1, high, bar_index, high, extend = extend.right)
REMARKS
Line objects are always of "series" form.
SEE ALSO
varlabelboxline.new
linefill
Keyword used to explicitly declare the "linefill" type of a variable or a parameter. Linefill objects (or IDs) can be created with the linefill.new function.
EXAMPLE
//@version=6
indicator("linefill", overlay=true)
// Empty `linefill1` line ID.
var linefill linefill1 = na
// `linefill` type is unnecessary because `linefill.new()` returns "linefill" type.
var linefill2 = linefill.new(na, na, na)

if barstate.islastconfirmedhistory
    line1 = line.new(bar_index - 10, high+1, bar_index, high+1, extend = extend.right)
    line2 = line.new(bar_index - 10, low+1, bar_index, low+1, extend = extend.right)
    linefill3 = linefill.new(line1, line2, color = color.new(color.green, 80))
REMARKS
Linefill objects are always of "series" form.
SEE ALSO
varlinelabeltableboxlinefill.new
map
Keyword used to explicitly declare the "map" type of a variable or a parameter. Map objects (or IDs) can be created with the map.new<type,type> function.
EXAMPLE
//@version=6
indicator("map", overlay=true)
map<int, float> a = na
a := map.new<int, float>()
a.put(bar_index, close)
label.new(bar_index, a.get(bar_index), "Current close")
REMARKS
Map objects are always of series form.
SEE ALSO
map.new<type,type>
matrix
Keyword used to explicitly declare the "matrix" type of a variable or a parameter. Matrix objects (or IDs) can be created with the matrix.new<type> function.
EXAMPLE
//@version=6
indicator("matrix example")

// Create `m1` matrix of `int` type.
matrix<int> m1 = matrix.new<int>(2, 3, 0)

// `matrix<int>` is unnecessary because the `matrix.new<int>()` function returns an `int` type matrix object.
m2 = matrix.new<int>(2, 3, 0)

// Display matrix using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m2))
REMARKS
Matrix objects are always of "series" form.
SEE ALSO
varmatrix.new<type>array
polyline
Keyword to explicitly declare the type of a variable or parameter as polyline. Scripts can produce polyline instances using the polyline.new function.
SEE ALSO
chart.point
series
The series keyword explicitly assigns the "series" type qualifier to variables and function parameters. Variables and parameters that use the "series" qualifier can reference values that change throughout a script's execution.
Explicit use of the series keyword when declaring the parameters of a library's exported functions is typically unnecessary, as the compiler can usually automatically detect whether a parameter is compatible with "series" or "simple" qualified values. By default, all exported function parameters are qualified as "series" wherever possible.
In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "series" is the strongest.
Explicitly declaring a variable with the series keyword restricts the type qualifier to "series", meaning the script cannot pass its value to any variable or function parameter that requires a value with a weaker qualifier ("const", "input", or "simple").
When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.
SYNTAX
export [method ]<functionName>([[series ]<paramType>] <paramName>[ = <defaultValue>])

[method ]<functionName>([series <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]series <variableType> <variableName> = <variableValue>
EXAMPLE
//@version=6
//@description A library with custom functions.
library("CustomFunctions", overlay = true)

//@function Finds the highest `source` value over `length` bars, filtered by the `cond` condition.
export conditionalHighest(series float source, series bool cond, series int length) =>
    //@variable The highest `source` value from when the `cond` was `true` over `length` bars.
    series float result = na
    // Loop to find the highest value.
    for i = 0 to length - 1
        if cond[i]
            value   = source[i]
            result := math.max(nz(result, value), value)
    // Return the `result`.
    result

//@variable Is `true` once every five bars.
series bool condition = bar_index % 5 == 0

//@variable The highest `close` value from every fifth bar over the last 100 bars.
series float hiValue = conditionalHighest(close, condition, 100)

plot(hiValue)
bgcolor(condition ? color.new(color.teal, 80) : na)
EXAMPLE
//@version=6
indicator("series variable not allowed")

//@variable A variable declared as "series int" with a value of 5.
series int myVar = 5

// This call causes an error.
// The `histbase` accepts "input int/float". It can't accept the stronger "series int" qualified type.
plot(close, style = plot.style_histogram, histbase = myVar)
REMARKS
To learn more, see our User Manual's section on type qualifiers.
SEE ALSO
simpleconst
simple
The simple keyword explicitly assigns the "simple" type qualifier to variables and function parameters. Variables and parameters that use the "simple" qualifier can reference values established at the beginning of a script's execution that do not change later.
To restrict the parameters in a library's exported functions to only allow values with a "simple" or weaker type qualifier, using the simple keyword when declaring parameters is often necessary, as libraries automatically qualify all parameters as "series" wherever possible by default. Explicitly restricting functions to accept "simple" arguments also allows them to return "simple" values in some cases, depending on the operations they execute, making them usable with the parameters of built-in functions that do not allow "series" arguments.
In variable declarations, the compiler can usually infer the qualified type automatically based on the values assigned to a variable, and it can automatically change a variable's qualifier to a stronger one when necessary. The type qualifier hierarchy is "const" < "input" < "simple" < "series", where "simple" is stronger than "input" and "const".
Explicitly declaring a variable with the simple keyword restricts the type qualifier to "simple", meaning the script cannot pass its value to any variable or function parameter that requires a value with a weaker qualifier ("const" or "input"). Additionally, one cannot assign a "series" value to a variable explicitly declared with the simple keyword.
When using this keyword to specify the type qualifier, one must also use a type keyword to declare the allowed type.
SYNTAX
export [method ]<functionName>([[simple ]<paramType>] <paramName>[ = <defaultValue>])

[method ]<functionName>([simple <paramType> ]<paramName>[ = <defaultValue>])

[var/varip ]simple <variableType> <variableName> = <variableValue></variableValue>
EXAMPLE
//@version=6
//@description A library with custom functions.
library("CustomFunctions", overlay = true)

//@function         Calculates the length values for a ribbon of four EMAs by multiplying the `baseLength`.
//@param baseLength The initial EMA length. Requires "simple int" because you can't use "series int" in `ta.ema()`.
//@returns          A tuple of length values.
export ribbonLengths(simple int baseLength) =>
    simple int length1 = baseLength
    simple int length2 = baseLength * 2
    simple int length3 = baseLength * 3
    simple int length4 = baseLength * 4
    [length1, length2, length3, length4]

// Get a tuple of "simple int" length values.
[len1, len2, len3, len4] = ribbonLengths(14)

// Plot four EMAs using the values from the tuple.
plot(ta.ema(close, len1), "EMA 1", color = color.red)
plot(ta.ema(close, len2), "EMA 1", color = color.orange)
plot(ta.ema(close, len3), "EMA 1", color = color.green)
plot(ta.ema(close, len4), "EMA 1", color = color.blue)
EXAMPLE
//@version=6
indicator("can't change simple to series")

//@variable A variable declared as "simple float" with a value of 5.0.
simple float myVar = 5.0

// This reassignment causes an error.
// The `close` variable returns a "series float" value. Since `myVar` is restricted to "simple" values, it cannot
// change its qualifier to "series".
myVar := close

plot(myVar)
REMARKS
To learn more, see our User Manual's section on type qualifiers.
SEE ALSO
seriesconst
string
Keyword used to explicitly declare the "string" type of a variable or a parameter.
EXAMPLE
//@version=6
indicator("string")
string s = "Hello World!"    // Same as `s = "Hello world!"`
// string s = na // same as "" 
plot(na, title=s)
REMARKS
Explicitly mentioning the type in a variable declaration is optional, except when it is initialized with na. Learn more about Pine Script® types in the User Manual page on the Type System.
SEE ALSO
varvaripintfloatboolstr.tostringstr.format
table
Keyword used to explicitly declare the "table" type of a variable or a parameter. Table objects (or IDs) can be created with the table.new function.
EXAMPLE
//@version=6
indicator("table")
// Empty `table1` table ID.
var table table1 = na
// `table` type is unnecessary because `table.new()` returns "table" type.
var table2 = table.new(position.top_left, na, na)

if barstate.islastconfirmedhistory
    var table3 = table.new(position = position.top_right, columns = 1, rows = 1, bgcolor = color.yellow, border_width = 1)
    table.cell(table_id = table3, column = 0, row = 0, text = "table3 text")
REMARKS
Table objects are always of "series" form.
SEE ALSO
varlinelabelboxtable.new
Operators
-
Subtraction or unary minus. Applicable to numerical expressions.
SYNTAX
expr1 - expr2
RETURNS
Returns integer or float value, or series of values:
Binary - returns expr1 minus expr2.
Unary - returns the negation of expr.
REMARKS
You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.
-=
Subtraction assignment. Applicable to numerical expressions.
SYNTAX
expr1 -= expr2
EXAMPLE
//@version=6
indicator("-=")
// Equals to expr1 = expr1 - expr2.
a = 2
b = 3
a -= b
// Result: a = -1.
plot(a)
RETURNS
Integer or float value, or series of values.
:=
Reassignment operator. It is used to assign a new value to a previously declared variable.
SYNTAX
<var_name> := <new_value>
EXAMPLE
//@version=6
indicator("My script")

myVar = 10

if close > open
    // Modifies the existing global scope `myVar` variable by changing its value from 10 to 20.
    myVar := 20
    // Creates a new `myVar` variable local to the `if` condition and unreachable from the global scope.
    // Does not affect the `myVar` declared in global scope.
    myVar = 30

plot(myVar)
!=
Not equal to. Applicable to expressions of any type.
SYNTAX
expr1 != expr2
RETURNS
Boolean value, or series of boolean values.
?:
Ternary conditional operator.
SYNTAX
expr1 ? expr2 : expr3
EXAMPLE
//@version=6
indicator("?:")
// Draw circles at the bars where open crosses close
s2 = ta.cross(open, close) ? math.avg(open,close) : na
plot(s2, style=plot.style_circles, linewidth=2, color=color.red)

// Combination of ?: operators for 'switch'-like logic
c = timeframe.isintraday ? color.red : timeframe.isdaily ? color.green : timeframe.isweekly ? color.blue : color.gray
plot(hl2, color=c)
RETURNS
expr2 if expr1 is evaluated to true, expr3 otherwise. Zero value (0 and also NaN, +Infinity, -Infinity) is considered to be false, any other value is true.
REMARKS
Use na for 'else' branch if you do not need it.
You can combine two or more ?: operators to achieve the equivalent of a 'switch'-like statement (see examples above).
You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.
SEE ALSO
na
[]
Series subscript. Provides access to previous values of series expr1. expr2 is the number of bars back, and must be numerical. Floats will be rounded down.
SYNTAX
expr1[expr2]
EXAMPLE
//@version=6
indicator("[]")
// [] can be used to "save" variable value between bars
a = 0.0 // declare `a`
a := a[1] // immediately set current value to the same as previous. `na` in the beginning of history
if high == low // if some condition - change `a` value to another
    a := low
plot(a)
RETURNS
A series of values.
SEE ALSO
math.floor
*
Multiplication. Applicable to numerical expressions.
SYNTAX
expr1 * expr2
RETURNS
Integer or float value, or series of values.
*=
Multiplication assignment. Applicable to numerical expressions.
SYNTAX
expr1 *= expr2
EXAMPLE
//@version=6
indicator("*=")
// Equals to expr1 = expr1 * expr2.
a = 2
b = 3
a *= b
// Result: a = 6.
plot(a)
RETURNS
Integer or float value, or series of values.
/
Division. Applicable to numerical expressions.
SYNTAX
expr1 / expr2
RETURNS
Integer or float value, or series of values.
/=
Division assignment. Applicable to numerical expressions.
SYNTAX
expr1 /= expr2
EXAMPLE
//@version=6
indicator("/=")
// Equals to expr1 = expr1 / expr2.
float a = 3.0
b = 3
a /= b
// Result: a = 1.
plot(a)
RETURNS
Integer or float value, or series of values.
%
Modulo (integer remainder). Applicable to numerical expressions.
SYNTAX
expr1 % expr2
RETURNS
Integer or float value, or series of values.
REMARKS
In Pine Script®, when the integer remainder is calculated, the quotient is truncated, i.e. rounded towards the lowest absolute value. The resulting value will have the same sign as the dividend.
Example: -1 % 9 = -1 - 9 * int(-1/9) = -1 - 9 * int(-0.111) = -1 - 9 * 0 = -1.
%=
Modulo assignment. Applicable to numerical expressions.
SYNTAX
expr1 %= expr2
EXAMPLE
//@version=6
indicator("%=")
// Equals to expr1 = expr1 % expr2.
a = 3
b = 3
a %= b
// Result: a = 0.
plot(a)
RETURNS
Integer or float value, or series of values.
+
Addition or unary plus. Applicable to numerical expressions or strings.
SYNTAX
expr1 + expr2
RETURNS
Binary + for strings returns concatenation of expr1 and expr2
For numbers returns integer or float value, or series of values:
Binary + returns expr1 plus expr2.
Unary + returns expr (does nothing added just for the symmetry with the unary - operator).
REMARKS
You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.
+=
Addition assignment. Applicable to numerical expressions or strings.
SYNTAX
expr1 += expr2
EXAMPLE
//@version=6
indicator("+=")
// Equals to expr1 = expr1 + expr2.
a = 2
b = 3
a += b
// Result: a = 5.
plot(a)
RETURNS
For strings returns concatenation of expr1 and expr2. For numbers returns integer or float value, or series of values.
REMARKS
You may use arithmetic operators with numbers as well as with series variables. In case of usage with series the operators are applied elementwise.
<
Less than. Applicable to numerical expressions.
SYNTAX
expr1 < expr2
RETURNS
Boolean value, or series of boolean values.
<=
Less than or equal to. Applicable to numerical expressions.
SYNTAX
expr1 <= expr2
RETURNS
Boolean value, or series of boolean values.
==
Equal to. Applicable to expressions of any type.
SYNTAX
expr1 == expr2
RETURNS
Boolean value, or series of boolean values.
=>
The '=>' operator is used in user-defined function declarations and in switch statements.
The function declaration syntax is:
SYNTAX
<identifier>([<parameter_name>[=<default_value>]], ...) =>
    <local_block>
    <function_result>
A <local_block> is zero or more Pine Script® statements.
The <function_result> is a variable, an expression, or a tuple.
EXAMPLE
//@version=6
indicator("=>")
// single-line function
f1(x, y) => x + y
// multi-line function
f2(x, y) => 
    sum = x + y
    sumChange = ta.change(sum, 10)
    // Function automatically returns the last expression used in it
plot(f1(30, 8) + f2(1, 3))
REMARKS
You can learn more about user-defined functions in the User Manual's pages on Declaring functions and Libraries.
>
Greater than. Applicable to numerical expressions.
SYNTAX
expr1 > expr2
RETURNS
Boolean value, or series of boolean values.
>=
Greater than or equal to. Applicable to numerical expressions.
SYNTAX
expr1 >= expr2
RETURNS
Boolean value, or series of boolean values.
Annotations
@description
Sets a custom description for scripts that use the library declaration statement. The text provided with this annotation will be used to pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
// @description Provides a tool to quickly output a label on the chart.
library("MyLibrary")

// @function Outputs a label with `labelText` on the bar's high.
// @param labelText (series string) The text to display on the label.
// @returns Drawn label.
export drawLabel(string labelText) =>
    label.new(bar_index, high, text = labelText)
@enum
If placed above an enum declaration, it adds a custom description for the enum. The Pine Editor's autosuggest uses this description and displays it when a user hovers over the enum name. When used in library scripts, the descriptions of all enums using the export keyword will pre-fill the "Description" field in the publication dialogue.
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
@field
If placed above a type or enum declaration, it adds a custom description for a field of the type/enum. After the annotation, users should specify the field name, followed by its description.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the type/enum or field name. When used in library scripts, the descriptions of all types/enums using the export keyword will pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
indicator("New high over the last 20 bars", overlay = true)

//@type A point on a chart.
//@field index The index of the bar where the point is located, i.e., its `x` coordinate.
//@field price The price where the point is located, i.e., its `y` coordinate.
type Point
    int index
    float price

//@variable If the current `high` is the highest over the last 20 bars, returns a new `Point` instance, `na` otherwise.
Point highest = na

if ta.highestbars(high, 20) == 0
    highest := Point.new(bar_index, high)
    label.new(highest.index, highest.price, str.tostring(highest.price))
@function
If placed above a function declaration, it adds a custom description for the function.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the function name. When used in library scripts, the descriptions of all functions using the export keyword will pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
// @description Provides a tool to quickly output a label on the chart.
library("MyLibrary")

// @function Outputs a label with `labelText` on the bar's high.
// @param labelText (series string) The text to display on the label.
// @returns Drawn label.
export drawLabel(string labelText) =>
    label.new(bar_index, high, text = labelText)
@param
If placed above a function declaration, it adds a custom description for a function parameter. After the annotation, users should specify the parameter name, then its description.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the function name. When used in library scripts, the descriptions of all functions using the export keyword will pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
// @description Provides a tool to quickly output a label on the chart.
library("MyLibrary")

// @function Outputs a label with `labelText` on the bar's high.
// @param labelText (series string) The text to display on the label.
// @returns Drawn label.
export drawLabel(string labelText) =>
    label.new(bar_index, high, text = labelText)
@returns
If placed above a function declaration, it adds a custom description for what that function returns.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the function name. When used in library scripts, the descriptions of all functions using the export keyword will pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
// @description Provides a tool to quickly output a label on the chart.
library("MyLibrary")

// @function Outputs a label with `labelText` on the bar's high.
// @param labelText (series string) The text to display on the label.
// @returns Drawn label.
export drawLabel(string labelText) =>
    label.new(bar_index, high, text = labelText)
@strategy_alert_message
If used within a strategy script, it provides a default message to pre-fill the "Message" field in the alert creation dialogue.
EXAMPLE
//@version=6
strategy("My strategy", overlay=true, margin_long=100, margin_short=100)
//@strategy_alert_message Strategy alert on symbol {{ticker}}

longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)
strategy.exit("Exit", "My Long Entry Id", profit = 10 / syminfo.mintick, loss = 10 / syminfo.mintick)
@type
If placed above a type declaration, it adds a custom description for the type.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the type name. When used in library scripts, the descriptions of all types using the export keyword will pre-fill the "Description" field in the publication dialogue.
EXAMPLE
//@version=6
indicator("New high over the last 20 bars", overlay = true)

//@type A point on a chart.
//@field index The index of the bar where the point is located, i.e., its `x` coordinate.
//@field price The price where the point is located, i.e., its `y` coordinate.
type Point
    int index
    float price

//@variable If the current `high` is the highest over the last 20 bars, returns a new `Point` instance, `na` otherwise.
Point highest = na

if ta.highestbars(high, 20) == 0
    highest := Point.new(bar_index, high)
    label.new(highest.index, highest.price, str.tostring(highest.price))
@variable
If placed above a variable declaration, it adds a custom description for the variable.
The Pine Editor's autosuggest uses this description and displays it when a user hovers over the variable name.
EXAMPLE
//@version=6
indicator("New high over the last 20 bars", overlay = true)

//@type A point on a chart.
//@field index The index of the bar where the point is located, i.e., its `x` coordinate.
//@field price The price where the point is located, i.e., its `y` coordinate.
type Point
    int index
    float price

//@variable If the current `high` is the highest over the last 20 bars, returns a new `Point` instance, `na` otherwise.
Point highest = na

if ta.highestbars(high, 20) == 0
    highest := Point.new(bar_index, high)
    label.new(highest.index, highest.price, str.tostring(highest.price))
@version=
Specifies the Pine Script® version that the script will use. The number in this annotation should not be confused with the script's version number, which updates on every saved change to the code.
EXAMPLE
//@version=6
indicator("Pine v6 Indicator")
plot(close)
EXAMPLE
//This indicator has no version annotation, so it will try to use v1.
//Pine Script® v1 has no function named `indicator()`, so the script will not compile.
indicator("Pine v1 Indicator")
plot(close)
REMARKS
The version should always be specified. Otherwise, for compatibility reasons, the script will be compiled using Pine Script® v1, which lacks most of the newer features and is bound to confuse. This annotation can be anywhere within a script, but we recommend placing it at the top of the code for readability.


