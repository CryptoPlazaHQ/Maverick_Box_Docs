math.abs()8 overloads
Absolute value of number is number if number >= 0, or -number otherwise.
SYNTAX & OVERLOADS
math.abs(number) → const int
math.abs(number) → input int
math.abs(number) → const float
math.abs(number) → simple int
math.abs(number) → input float
math.abs(number) → series int
math.abs(number) → simple float
math.abs(number) → series float
ARGUMENTS
number (const int) The number to use in the calculation.
RETURNS
The absolute value of number.
math.acos()4 overloads
The acos function returns the arccosine (in radians) of number such that cos(acos(y)) = y for y in range [-1, 1].
SYNTAX & OVERLOADS
math.acos(angle) → const float
math.acos(angle) → input float
math.acos(angle) → simple float
math.acos(angle) → series float
ARGUMENTS
angle (const int/float) The value, in radians, to use in the calculation.
RETURNS
The arc cosine of a value; the returned angle is in the range [0, Pi], or na if y is outside of range [-1, 1].
math.asin()4 overloads
The asin function returns the arcsine (in radians) of number such that sin(asin(y)) = y for y in range [-1, 1].
SYNTAX & OVERLOADS
math.asin(angle) → const float
math.asin(angle) → input float
math.asin(angle) → simple float
math.asin(angle) → series float
ARGUMENTS
angle (const int/float) The value, in radians, to use in the calculation.
RETURNS
The arcsine of a value; the returned angle is in the range [-Pi/2, Pi/2], or na if y is outside of range [-1, 1].
math.atan()4 overloads
The atan function returns the arctangent (in radians) of number such that tan(atan(y)) = y for any y.
SYNTAX & OVERLOADS
math.atan(angle) → const float
math.atan(angle) → input float
math.atan(angle) → simple float
math.atan(angle) → series float
ARGUMENTS
angle (const int/float) The value, in radians, to use in the calculation.
RETURNS
The arc tangent of a value; the returned angle is in the range [-Pi/2, Pi/2].
math.avg()2 overloads
Calculates average of all given series (elementwise).
SYNTAX & OVERLOADS
math.avg(number0, number1, ...) → simple float
math.avg(number0, number1, ...) → series float
ARGUMENTS
number0, number1, ... (simple int/float) A sequence of numbers to use in the calculation.
RETURNS
Average.
SEE ALSO
math.sumta.cumta.sma
math.ceil()4 overloads
Rounds the specified number up to the smallest whole number ("int" value) that is greater than or equal to it.
SYNTAX & OVERLOADS
math.ceil(number) → const int
math.ceil(number) → input int
math.ceil(number) → simple int
math.ceil(number) → series int
ARGUMENTS
number (const int/float) The number to round.
RETURNS
The smallest "int" value that is greater than or equal to the number.
SEE ALSO
math.floormath.round
math.cos()4 overloads
The cos function returns the trigonometric cosine of an angle.
SYNTAX & OVERLOADS
math.cos(angle) → const float
math.cos(angle) → input float
math.cos(angle) → simple float
math.cos(angle) → series float
ARGUMENTS
angle (const int/float) Angle, in radians.
RETURNS
The trigonometric cosine of an angle.
math.exp()4 overloads
The exp function of number is e raised to the power of number, where e is Euler's number.
SYNTAX & OVERLOADS
math.exp(number) → const float
math.exp(number) → input float
math.exp(number) → simple float
math.exp(number) → series float
ARGUMENTS
number (const int/float) The number to use in the calculation.
RETURNS
A value representing e raised to the power of number.
SEE ALSO
math.pow
math.floor()4 overloads
Rounds the specified number down to the largest whole number ("int" value) that is less than or equal to it.
SYNTAX & OVERLOADS
math.floor(number) → const int
math.floor(number) → input int
math.floor(number) → simple int
math.floor(number) → series int
ARGUMENTS
number (const int/float) The number to round.
RETURNS
The largest "int" value that is less than or equal to the number.
SEE ALSO
math.ceilmath.round
math.log()4 overloads
Natural logarithm of any number > 0 is the unique y such that e^y = number.
SYNTAX & OVERLOADS
math.log(number) → const float
math.log(number) → input float
math.log(number) → simple float
math.log(number) → series float
ARGUMENTS
number (const int/float) The number to use in the calculation.
RETURNS
The natural logarithm of number.
SEE ALSO
math.log10
math.log10()4 overloads
The common (or base 10) logarithm of number is the power to which 10 must be raised to obtain the number. 10^y = number.
SYNTAX & OVERLOADS
math.log10(number) → const float
math.log10(number) → input float
math.log10(number) → simple float
math.log10(number) → series float
ARGUMENTS
number (const int/float) The number to use in the calculation.
RETURNS
The base 10 logarithm of number.
SEE ALSO
math.log
math.max()8 overloads
Returns the greatest of multiple values.
SYNTAX & OVERLOADS
math.max(number0, number1, ...) → const int
math.max(number0, number1, ...) → const float
math.max(number0, number1, ...) → input int
math.max(number0, number1, ...) → simple int
math.max(number0, number1, ...) → input float
math.max(number0, number1, ...) → series int
math.max(number0, number1, ...) → simple float
math.max(number0, number1, ...) → series float
ARGUMENTS
number0, number1, ... (const int) A sequence of numbers to use in the calculation.
EXAMPLE
//@version=6
indicator("math.max", overlay=true)
plot(math.max(close, open))
plot(math.max(close, math.max(open, 42)))
RETURNS
The greatest of multiple given values.
SEE ALSO
math.min
math.min()8 overloads
Returns the smallest of multiple values.
SYNTAX & OVERLOADS
math.min(number0, number1, ...) → const int
math.min(number0, number1, ...) → const float
math.min(number0, number1, ...) → input int
math.min(number0, number1, ...) → simple int
math.min(number0, number1, ...) → input float
math.min(number0, number1, ...) → series int
math.min(number0, number1, ...) → simple float
math.min(number0, number1, ...) → series float
ARGUMENTS
number0, number1, ... (const int) A sequence of numbers to use in the calculation.
EXAMPLE
//@version=6
indicator("math.min", overlay=true)
plot(math.min(close, open))
plot(math.min(close, math.min(open, 42)))
RETURNS
The smallest of multiple given values.
SEE ALSO
math.max
math.pow()4 overloads
Mathematical power function.
SYNTAX & OVERLOADS
math.pow(base, exponent) → const float
math.pow(base, exponent) → input float
math.pow(base, exponent) → simple float
math.pow(base, exponent) → series float
ARGUMENTS
base (const int/float) Specify the base to use.
exponent (const int/float) Specifies the exponent.
EXAMPLE
//@version=6
indicator("math.pow", overlay=true)
plot(math.pow(close, 2))
RETURNS
base raised to the power of exponent. If base is a series, it is calculated elementwise.
SEE ALSO
math.sqrtmath.exp
math.random()
Returns a pseudo-random value. The function will generate a different sequence of values for each script execution. Using the same value for the optional seed argument will produce a repeatable sequence.
SYNTAX
math.random(min, max, seed) → series float
ARGUMENTS
min (series int/float) The lower bound of the range of random values. The value is not included in the range. The default is 0.
max (series int/float) The upper bound of the range of random values. The value is not included in the range. The default is 1.
seed (series int) Optional argument. When the same seed is used, allows successive calls to the function to produce a repeatable set of values.
RETURNS
A random value.
math.round()8 overloads
Returns the value of number rounded to the nearest integer, with ties rounding up. If the precision parameter is used, returns a float value rounded to that amount of decimal places.
SYNTAX & OVERLOADS
math.round(number) → const int
math.round(number) → input int
math.round(number) → simple int
math.round(number) → series int
math.round(number, precision) → const float
math.round(number, precision) → input float
math.round(number, precision) → simple float
math.round(number, precision) → series float
ARGUMENTS
number (const int/float) The value to be rounded.
RETURNS
The value of number rounded to the nearest integer, or according to precision.
REMARKS
Note that for 'na' values function returns 'na'.
SEE ALSO
math.ceilmath.floor
math.round_to_mintick()2 overloads
Returns the value rounded to the symbol's mintick, i.e. the nearest value that can be divided by syminfo.mintick, without the remainder, with ties rounding up.
SYNTAX & OVERLOADS
math.round_to_mintick(number) → simple float
math.round_to_mintick(number) → series float
ARGUMENTS
number (simple int/float) The value to be rounded.
RETURNS
The number rounded to tick precision.
REMARKS
Note that for 'na' values function returns 'na'.
SEE ALSO
math.ceilmath.floor
math.sign()4 overloads
Sign (signum) of number is zero if number is zero, 1.0 if number is greater than zero, -1.0 if number is less than zero.
SYNTAX & OVERLOADS
math.sign(number) → const float
math.sign(number) → input float
math.sign(number) → simple float
math.sign(number) → series float
ARGUMENTS
number (const int/float) The number to use in the calculation.
RETURNS
The sign of the argument.
math.sin()4 overloads
The sin function returns the trigonometric sine of an angle.
SYNTAX & OVERLOADS
math.sin(angle) → const float
math.sin(angle) → input float
math.sin(angle) → simple float
math.sin(angle) → series float
ARGUMENTS
angle (const int/float) Angle, in radians.
RETURNS
The trigonometric sine of an angle.
math.sqrt()4 overloads
Square root of any number >= 0 is the unique y >= 0 such that y^2 = number.
SYNTAX & OVERLOADS
math.sqrt(number) → const float
math.sqrt(number) → input float
math.sqrt(number) → simple float
math.sqrt(number) → series float
ARGUMENTS
number (const int/float) The number to use in the calculation.
RETURNS
The square root of number.
SEE ALSO
math.pow
math.sum()
The sum function returns the sliding sum of last y values of x.
SYNTAX
math.sum(source, length) → series float
ARGUMENTS
source (series int/float) Series of values to process.
length (series int) Number of bars (length).
RETURNS
Sum of source for length bars back.
REMARKS
na values in the source series are ignored; the function calculates on the length quantity of non-na values.
SEE ALSO
ta.cumfor
math.tan()4 overloads
The tan function returns the trigonometric tangent of an angle.
SYNTAX & OVERLOADS
math.tan(angle) → const float
math.tan(angle) → input float
math.tan(angle) → simple float
math.tan(angle) → series float
ARGUMENTS
angle (const int/float) Angle, in radians.
RETURNS
The trigonometric tangent of an angle.
math.todegrees()
Returns an approximately equivalent angle in degrees from an angle measured in radians.
SYNTAX
math.todegrees(radians) → series float
ARGUMENTS
radians (series int/float) Angle in radians.
RETURNS
The angle value in degrees.
math.toradians()
Returns an approximately equivalent angle in radians from an angle measured in degrees.
SYNTAX
math.toradians(degrees) → series float
ARGUMENTS
degrees (series int/float) Angle in degrees.
RETURNS
The angle value in radians.
matrix.add_col()2 overloads
The function adds a column at the column index of the id matrix. The column can consist of na values, or an array can be used to provide values.
SYNTAX & OVERLOADS
matrix.add_col(id, column) → void
matrix.add_col(id, column, array_id) → void
ARGUMENTS
id (any matrix type) A matrix object.
column (series int) The index of the column after which the new column will be inserted. Optional. The default value is matrix.columns.
Adding a column to the matrix
EXAMPLE
//@version=6
indicator("`matrix.add_col()` Example 1")

// Create a 2x3 "int" matrix containing values `0`.
m = matrix.new<int>(2, 3, 0)

// Add a column with `na` values to the matrix.
matrix.add_col(m)

// Display matrix elements.
if barstate.islastconfirmedhistory
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m))
Adding an array as a column to the matrix
EXAMPLE
//@version=6
indicator("`matrix.add_col()` Example 2")

if barstate.islastconfirmedhistory
    // Create an empty matrix object. 
    var m = matrix.new<int>()
    
    // Create an array with values `1` and `3`.
    var a = array.from(1, 3)
    
    // Add the `a` array as the first column of the empty matrix.
    matrix.add_col(m, 0, a)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m))
REMARKS
Rather than add columns to an empty matrix, it is far more efficient to declare a matrix with explicit dimensions and fill it with values. Adding a column is also much slower than adding a row with the matrix.add_row function.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rowsmatrix.add_row
matrix.add_row()2 overloads
The function adds a row at the row index of the id matrix. The row can consist of na values, or an array can be used to provide values.
SYNTAX & OVERLOADS
matrix.add_row(id, row) → void
matrix.add_row(id, row, array_id) → void
ARGUMENTS
id (any matrix type) A matrix object.
row (series int) The index of the row after which the new row will be inserted. Optional. The default value is matrix.rows.
Adding a row to the matrix
EXAMPLE
//@version=6
indicator("`matrix.add_row()` Example 1")

// Create a 2x3 "int" matrix containing values `0`.
m = matrix.new<int>(2, 3, 0)

// Add a row with `na` values to the matrix.
matrix.add_row(m)

// Display matrix elements.
if barstate.islastconfirmedhistory
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m))
Adding an array as a row to the matrix
EXAMPLE
//@version=6
indicator("`matrix.add_row()` Example 2")

if barstate.islastconfirmedhistory
    // Create an empty matrix object. 
    var m = matrix.new<int>()
    
    // Create an array with values `1` and `2`.
    var a = array.from(1, 2)
    
    // Add the `a` array as the first row of the empty matrix.
    matrix.add_row(m, 0, a)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m))
REMARKS
Indexing of rows and columns starts at zero. Rather than add rows to an empty matrix, it is far more efficient to declare a matrix with explicit dimensions and fill it with values.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rowsmatrix.add_col
matrix.avg()2 overloads
The function calculates the average of all elements in the matrix.
SYNTAX & OVERLOADS
matrix.avg(id) → series float
matrix.avg(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.avg()` Example")

// Create a 2x2 matrix.
var m = matrix.new<int>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0, 1)
matrix.set(m, 0, 1, 2)
matrix.set(m, 1, 0, 3)
matrix.set(m, 1, 1, 4)

// Get the average value of the matrix.
var x = matrix.avg(m)

plot(x, 'Matrix average value')
RETURNS
The average value from the id matrix.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.col()
The function creates a one-dimensional array from the elements of a matrix column.
SYNTAX
matrix.col(id, column) → array<type>
ARGUMENTS
id (any matrix type) A matrix object.
column (series int) Index of the required column.
EXAMPLE
//@version=6
indicator("`matrix.col()` Example", "", true)

// Create a 2x3 "float" matrix from `hlc3` values.
m = matrix.new<float>(2, 3, hlc3)

// Return an array with the values of the first column of matrix `m`.
a = matrix.col(m, 0)

// Plot the first value from the array `a`.
plot(array.get(a, 0))
RETURNS
An array ID containing the column values of the id matrix.
REMARKS
Indexing of rows starts at 0.
SEE ALSO
matrix.new<type>matrix.getarray.getmatrix.colmatrix.columns
matrix.columns()
The function returns the number of columns in the matrix.
SYNTAX
matrix.columns(id) → series int
ARGUMENTS
id (any matrix type) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.columns()` Example")

// Create a 2x6 matrix with values `0`.
var m = matrix.new<int>(2, 6, 0)

// Get the quantity of columns in matrix `m`.
var x = matrix.columns(m)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, "Columns: " + str.tostring(x) + "\n" + str.tostring(m))
RETURNS
The number of columns in the matrix id.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.colmatrix.rowmatrix.rows
matrix.concat()
The function appends the m2 matrix to the m1 matrix.
SYNTAX
matrix.concat(id1, id2) → matrix<type>
ARGUMENTS
id1 (any matrix type) Matrix object to concatenate into.
id2 (any matrix type) Matrix object whose elements will be appended to id1.
EXAMPLE
//@version=6
indicator("`matrix.concat()` Example")

// Create a 2x4 "int" matrix containing values `0`.
m1 = matrix.new<int>(2, 4, 0)
// Create a 2x4 "int" matrix containing values `1`.
m2 = matrix.new<int>(2, 4, 1)

// Append matrix `m2` to `m1`.
matrix.concat(m1, m2)

// Display matrix elements.
if barstate.islastconfirmedhistory
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix Elements:")
    table.cell(t, 0, 1, str.tostring(m1))
RETURNS
Returns the id1 matrix concatenated with the id2 matrix.
REMARKS
The number of columns in both matrices must be identical.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.copy()
The function creates a new matrix which is a copy of the original.
SYNTAX
matrix.copy(id) → matrix<type>
ARGUMENTS
id (any matrix type) A matrix object to copy.
EXAMPLE
//@version=6
indicator("`matrix.copy()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 "float" matrix with `1` values.
    var m1 = matrix.new<float>(2, 3, 1)
    
    // Copy the matrix to a new one.
    // Note that unlike what `matrix.copy()` does, 
    // the simple assignment operation `m2 = m1`
    // would NOT create a new copy of the `m1` matrix.
    // It would merely create a copy of its ID referencing the same matrix.
    var m2 = matrix.copy(m1)
    
    // Display using a table.
    var t = table.new(position.top_right, 5, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Matrix Copy:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix object of the copied id matrix.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.det()2 overloads
The function returns the determinant of a square matrix.
SYNTAX & OVERLOADS
matrix.det(id) → series float
matrix.det(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.det` Example")

// Create a 2x2 matrix.
var m = matrix.new<float>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0,  3)
matrix.set(m, 0, 1,  7)
matrix.set(m, 1, 0,  1)
matrix.set(m, 1, 1, -4)

// Get the determinant of the matrix. 
var x = matrix.det(m)

plot(x, 'Matrix determinant')
RETURNS
The determinant value of the id matrix.
REMARKS
Function calculation based on the LU decomposition algorithm.
SEE ALSO
matrix.new<type>matrix.setmatrix.is_square
matrix.diff()2 overloads
The function returns a new matrix resulting from the subtraction between matrices id1 and id2, or of matrix id1 and an id2 scalar (a numerical value).
SYNTAX & OVERLOADS
matrix.diff(id1, id2) → matrix<int>
matrix.diff(id1, id2) → matrix<float>
ARGUMENTS
id1 (matrix<int>) Matrix to subtract from.
id2 (series int/float/matrix<int>) Matrix object or a scalar value to be subtracted.
Difference between two matrices
EXAMPLE
//@version=6
indicator("`matrix.diff()` Example 1")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix containing values `5`.
    var m1 = matrix.new<float>(2, 3, 5) 
    // Create a 2x3 matrix containing values `4`.
    var m2 = matrix.new<float>(2, 3, 4) 
    // Create a new matrix containing the difference between matrices `m1` and `m2`.
    var m3 = matrix.diff(m1, m2) 
    
    // Display using a table.
    var t = table.new(position.top_right, 1, 2, color.green)
    table.cell(t, 0, 0, "Difference between two matrices:")
    table.cell(t, 0, 1, str.tostring(m3))
Difference between a matrix and a scalar value
EXAMPLE
//@version=6
indicator("`matrix.diff()` Example 2")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix with values `4`.
    var m1 = matrix.new<float>(2, 3, 4)
    
    // Create a new matrix containing the difference between the `m1` matrix and the "int" value `1`.
    var m2 = matrix.diff(m1, 1)
    
    // Display using a table.
    var t = table.new(position.top_right, 1, 2, color.green)
    table.cell(t, 0, 0, "Difference between a matrix and a scalar:")
    table.cell(t, 0, 1, str.tostring(m2))
RETURNS
A new matrix object containing the difference between id2 and id1.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.eigenvalues()2 overloads
The function returns an array containing the eigenvalues of a square matrix.
SYNTAX & OVERLOADS
matrix.eigenvalues(id) → array<float>
matrix.eigenvalues(id) → array<int>
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.eigenvalues()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 2)
    matrix.set(m1, 0, 1, 4)
    matrix.set(m1, 1, 0, 6)
    matrix.set(m1, 1, 1, 8)
    
    // Get the eigenvalues of the matrix.
    tr = matrix.eigenvalues(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Array of Eigenvalues:")
    table.cell(t, 1, 1, str.tostring(tr))
RETURNS
An array containing the eigenvalues of the id matrix.
REMARKS
The function is calculated using "The Implicit QL Algorithm".
SEE ALSO
matrix.new<type>matrix.setmatrix.eigenvectors
matrix.eigenvectors()2 overloads
Returns a matrix of eigenvectors, in which each column is an eigenvector of the id matrix.
SYNTAX & OVERLOADS
matrix.eigenvectors(id) → matrix<float>
matrix.eigenvectors(id) → matrix<int>
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.eigenvectors()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix 
    var m1 = matrix.new<int>(2, 2, 1)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 2)
    matrix.set(m1, 0, 1, 4)
    matrix.set(m1, 1, 0, 6)
    matrix.set(m1, 1, 1, 8)
    
    // Get the eigenvectors of the matrix.
    m2 = matrix.eigenvectors(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix Elements:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Matrix Eigenvectors:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix containing the eigenvectors of the id matrix.
REMARKS
The function is calculated using "The Implicit QL Algorithm".
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.eigenvalues
matrix.elements_count()
The function returns the total number of all matrix elements.
SYNTAX
matrix.elements_count(id) → series int
ARGUMENTS
id (any matrix type) A matrix object.
SEE ALSO
matrix.new<type>matrix.columnsmatrix.rows
matrix.fill()
The function fills a rectangular area of the id matrix defined by the indices from_column to to_column (not including it) and from_row to to_row(not including it) with the value.
SYNTAX
matrix.fill(id, value, from_row, to_row, from_column, to_column) → void
ARGUMENTS
id (any matrix type) A matrix object.
value (series <type of the matrix's elements>) The value to fill with.
from_row (series int) Row index from which the fill will begin (inclusive). Optional. The default value is 0.
to_row (series int) Row index where the fill will end (not inclusive). Optional. The default value is matrix.rows.
from_column (series int) Column index from which the fill will begin (inclusive). Optional. The default value is 0.
to_column (series int) Column index where the fill will end (non inclusive). Optional. The default value is matrix.columns.
EXAMPLE
//@version=6
indicator("`matrix.fill()` Example")

// Create a 4x5 "int" matrix containing values `0`.
m = matrix.new<float>(4, 5, 0)

// Fill the intersection of rows 1 to 2 and columns 2 to 3 of the matrix with `hl2` values.
matrix.fill(m, hl2, 0, 2, 1, 3)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m))
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.get()
The function returns the element with the specified index of the matrix.
SYNTAX
matrix.get(id, row, column) → <matrix_type>
ARGUMENTS
id (any matrix type) A matrix object.
row (series int) Index of the required row.
column (series int) Index of the required column.
EXAMPLE
//@version=6
indicator("`matrix.get()` Example", "", true)

// Create a 2x3 "float" matrix from the `hl2` values.
m = matrix.new<float>(2, 3, hl2)

// Return the value of the element at index [0, 0] of matrix `m`.
x = matrix.get(m, 0, 0)

plot(x)
RETURNS
The value of the element at the row and column index of the id matrix.
REMARKS
Indexing of the rows and columns starts at zero.
SEE ALSO
matrix.new<type>matrix.setmatrix.columnsmatrix.rows
matrix.inv()2 overloads
The function returns the inverse of a square matrix.
SYNTAX & OVERLOADS
matrix.inv(id) → matrix<float>
matrix.inv(id) → matrix<int>
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.inv()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Inverse of the matrix.
    var m2 = matrix.inv(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Inverse matrix:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix, which is the inverse of the id matrix.
REMARKS
The function is calculated using the LU decomposition algorithm.
SEE ALSO
matrix.new<type>matrix.setmatrix.pinvmatrix.copystr.tostring
matrix.is_antidiagonal()
The function determines if the matrix is anti-diagonal (all elements outside the secondary diagonal are zero).
SYNTAX
matrix.is_antidiagonal(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is anti-diagonal, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.setmatrix.is_squarematrix.is_identitymatrix.is_diagonal
matrix.is_antisymmetric()
The function determines if a matrix is antisymmetric (its transpose equals its negative).
SYNTAX
matrix.is_antisymmetric(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true, if the id matrix is antisymmetric, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.is_square
matrix.is_binary()
The function determines if the matrix is binary (when all elements of the matrix are 0 or 1).
SYNTAX
matrix.is_binary(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is binary, false otherwise.
SEE ALSO
matrix.new<type>matrix.getmatrix.set
matrix.is_diagonal()
The function determines if the matrix is diagonal (all elements outside the main diagonal are zero).
SYNTAX
matrix.is_diagonal(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is diagonal, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.setmatrix.is_squarematrix.is_identitymatrix.is_antidiagonal
matrix.is_identity()
The function determines if a matrix is an identity matrix (elements with ones on the main diagonal and zeros elsewhere).
SYNTAX
matrix.is_identity(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if id is an identity matrix, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.is_squarematrix.is_diagonal
matrix.is_square()
The function determines if the matrix is square (it has the same number of rows and columns).
SYNTAX
matrix.is_square(id) → series bool
ARGUMENTS
id (any matrix type) Matrix object to test.
RETURNS
Returns true if the id matrix is square, false otherwise.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.is_stochastic()
The function determines if the matrix is stochastic.
SYNTAX
matrix.is_stochastic(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is stochastic, false otherwise.
SEE ALSO
matrix.new<type>matrix.set
matrix.is_symmetric()
The function determines if a square matrix is symmetric (elements are symmetric with respect to the main diagonal).
SYNTAX
matrix.is_symmetric(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is symmetric, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.is_square
matrix.is_triangular()
The function determines if the matrix is triangular (if all elements above or below the main diagonal are zero).
SYNTAX
matrix.is_triangular(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to test.
RETURNS
Returns true if the id matrix is triangular, false otherwise.
REMARKS
Returns false with non-square matrices.
SEE ALSO
matrix.new<type>matrix.setmatrix.is_square
matrix.is_zero()
The function determines if all elements of the matrix are zero.
SYNTAX
matrix.is_zero(id) → series bool
ARGUMENTS
id (matrix<int/float>) Matrix object to check.
RETURNS
Returns true if all elements of the id matrix are zero, false otherwise.
SEE ALSO
matrix.new<type>matrix.getmatrix.set
matrix.kron()2 overloads
The function returns the Kronecker product for the id1 and id2 matrices.
SYNTAX & OVERLOADS
matrix.kron(id1, id2) → matrix<float>
matrix.kron(id1, id2) → matrix<int>
ARGUMENTS
id1 (matrix<int/float>) First matrix object.
id2 (matrix<int/float>) Second matrix object.
EXAMPLE
//@version=6
indicator("`matrix.kron()` Example")

// Display using a table.
if barstate.islastconfirmedhistory
    // Create two matrices with default values `1` and `2`. 
    var m1 = matrix.new<float>(2, 2, 1) 
    var m2 = matrix.new<float>(2, 2, 2) 
    
    // Calculate the Kronecker product of the matrices.
    var m3 = matrix.kron(m1, m2) 
    
    // Display matrix elements.
    var t = table.new(position.top_right, 5, 2, color.green)
    table.cell(t, 0, 0, "Matrix 1:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 1, "⊗")
    table.cell(t, 2, 0, "Matrix 2:")
    table.cell(t, 2, 1, str.tostring(m2))
    table.cell(t, 3, 1, "=")
    table.cell(t, 4, 0, "Kronecker product:")
    table.cell(t, 4, 1, str.tostring(m3))
RETURNS
A new matrix containing the Kronecker product of id1 and id2.
SEE ALSO
matrix.new<type>matrix.multstr.tostringtable.new
matrix.max()2 overloads
The function returns the largest value from the matrix elements.
SYNTAX & OVERLOADS
matrix.max(id) → series float
matrix.max(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.max()` Example")

// Create a 2x2 matrix.
var m = matrix.new<int>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0, 1)
matrix.set(m, 0, 1, 2)
matrix.set(m, 1, 0, 3)
matrix.set(m, 1, 1, 4)

// Get the maximum value in the matrix.
var x = matrix.max(m)

plot(x, 'Matrix maximum value')
RETURNS
The maximum value from the id matrix.
SEE ALSO
matrix.new<type>matrix.minmatrix.avgmatrix.sort
matrix.median()2 overloads
The function calculates the median ("the middle" value) of matrix elements.
SYNTAX & OVERLOADS
matrix.median(id) → series float
matrix.median(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.median()` Example")

// Create a 2x2 matrix.
m = matrix.new<int>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0, 1)
matrix.set(m, 0, 1, 2)
matrix.set(m, 1, 0, 3)
matrix.set(m, 1, 1, 4)

// Get the median of the matrix.
x = matrix.median(m)

plot(x, 'Median of the matrix')
REMARKS
Note that na elements of the matrix are not considered when calculating the median.
SEE ALSO
matrix.new<type>matrix.modematrix.sortmatrix.avg
matrix.min()2 overloads
The function returns the smallest value from the matrix elements.
SYNTAX & OVERLOADS
matrix.min(id) → series float
matrix.min(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.min()` Example")

// Create a 2x2 matrix.
var m = matrix.new<int>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0, 1)
matrix.set(m, 0, 1, 2)
matrix.set(m, 1, 0, 3)
matrix.set(m, 1, 1, 4)

// Get the minimum value from the matrix.
var x = matrix.min(m)

plot(x, 'Matrix minimum value')
RETURNS
The smallest value from the id matrix.
SEE ALSO
matrix.new<type>matrix.maxmatrix.avgmatrix.sort
matrix.mode()2 overloads
The function calculates the mode of the matrix, which is the most frequently occurring value from the matrix elements. When there are multiple values occurring equally frequently, the function returns the smallest of those values.
SYNTAX & OVERLOADS
matrix.mode(id) → series float
matrix.mode(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.mode()` Example")

// Create a 2x2 matrix.
var m = matrix.new<int>(2, 2, na)
// Fill the matrix with values.
matrix.set(m, 0, 0, 0)
matrix.set(m, 0, 1, 0)
matrix.set(m, 1, 0, 1)
matrix.set(m, 1, 1, 1)

// Get the mode of the matrix.
var x = matrix.mode(m)

plot(x, 'Mode of the matrix')
RETURNS
The most frequently occurring value from the id matrix. If none exists, returns the smallest value instead.
REMARKS
Note that na elements of the matrix are not considered when calculating the mode.
SEE ALSO
matrix.new<type>matrix.setmatrix.medianmatrix.sortmatrix.avg
matrix.mult()4 overloads
The function returns a new matrix resulting from the product between the matrices id1 and id2, or between an id1 matrix and an id2 scalar (a numerical value), or between an id1 matrix and an id2 vector (an array of values).
SYNTAX & OVERLOADS
matrix.mult(id1, id2) → array<int>
matrix.mult(id1, id2) → array<float>
matrix.mult(id1, id2) → matrix<int>
matrix.mult(id1, id2) → matrix<float>
ARGUMENTS
id1 (matrix<int>) First matrix object.
id2 (array<int>) Second matrix object, value or array.
Product of two matrices
EXAMPLE
//@version=6
indicator("`matrix.mult()` Example 1")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 6x2 matrix containing values `5`.
    var m1 = matrix.new<float>(6, 2, 5) 
    // Create a 2x3 matrix containing values `4`.
    // Note that it must have the same quantity of rows as there are columns in the first matrix.
    var m2 = matrix.new<float>(2, 3, 4) 
    // Create a new matrix from the multiplication of the two matrices.
    var m3 = matrix.mult(m1, m2) 
    
    // Display using a table.
    var t = table.new(position.top_right, 1, 2, color.green)
    table.cell(t, 0, 0, "Product of two matrices:")
    table.cell(t, 0, 1, str.tostring(m3))
Product of a matrix and a scalar
EXAMPLE
//@version=6
indicator("`matrix.mult()` Example 2")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix containing values `4`.
    var m1 = matrix.new<float>(2, 3, 4) 
    
    // Create a new matrix from the product of the two matrices.
    scalar = 5
    var m2 = matrix.mult(m1, scalar) 
    
    // Display using a table.
    var t = table.new(position.top_right, 5, 2, color.green)
    table.cell(t, 0, 0, "Matrix 1:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 1, "x")
    table.cell(t, 2, 0, "Scalar:")
    table.cell(t, 2, 1, str.tostring(scalar))
    table.cell(t, 3, 1, "=")
    table.cell(t, 4, 0, "Matrix 2:")
    table.cell(t, 4, 1, str.tostring(m2))
Product of a matrix and an array vector
EXAMPLE
//@version=6
indicator("`matrix.mult()` Example 3")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix containing values `4`.
    var m1 = matrix.new<int>(2, 3, 4)
    
    // Create an array of three elements.
    var int[] a = array.from(1, 1, 1)
    
    // Create a new matrix containing the product of the `m1` matrix and the `a` array.
    var m3 = matrix.mult(m1, a) 
    
    // Display using a table.
    var t = table.new(position.top_right, 5, 2, color.green)
    table.cell(t, 0, 0, "Matrix 1:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 1, "x")
    table.cell(t, 2, 0, "Value:")
    table.cell(t, 2, 1, str.tostring(a, " "))
    table.cell(t, 3, 1, "=")
    table.cell(t, 4, 0, "Matrix 3:")
    table.cell(t, 4, 1, str.tostring(m3))
RETURNS
A new matrix object containing the product of id2 and id1.
SEE ALSO
matrix.new<type>matrix.summatrix.diff
matrix.new<type>()
The function creates a new matrix object. A matrix is a two-dimensional data structure containing rows and columns. All elements in the matrix must be of the type specified in the type template ("<type>").
SYNTAX
matrix.new<type>(rows, columns, initial_value) → matrix<type>
ARGUMENTS
rows (series int) Initial row count of the matrix. Optional. The default value is 0.
columns (series int) Initial column count of the matrix. Optional. The default value is 0.
initial_value (<matrix_type>) Initial value of all matrix elements. Optional. The default is 'na'.
Create a matrix of elements with the same initial value
EXAMPLE
//@version=6
indicator("`matrix.new<type>()` Example 1")

// Create a 2x3 (2 rows x 3 columns) "int" matrix with values zero.
var m = matrix.new<int>(2, 3, 0)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m))
Create a matrix from array values
EXAMPLE
//@version=6
indicator("`matrix.new<type>()` Example 2")

// Function to create a matrix whose rows are filled with array values.
matrixFromArray(int rows, int columns, array<float> data) =>
    m = matrix.new<float>(rows, columns)
    for i = 0 to rows <= 0 ? na : rows - 1
        for j = 0 to columns <= 0 ? na : columns - 1
            matrix.set(m, i, j, array.get(data, i * columns + j))
    m
    
// Create a 3x3 matrix from an array of values.
var m1 = matrixFromArray(3, 3, array.from(1, 2, 3, 4, 5, 6, 7, 8, 9))
// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m1))
Create a matrix from an input.text_area() field
EXAMPLE
//@version=6
indicator("`matrix.new<type>()` Example 3")

// Function to create a matrix from a text string.
// Values in a row must be separated by a space. Each line is one row.
matrixFromInputArea(stringOfValues) =>
    var rowsArray = str.split(stringOfValues, "\n")
    var rows = array.size(rowsArray)
    var cols = array.size(str.split(array.get(rowsArray, 0), " "))
    var matrix = matrix.new<float>(rows, cols, na) 
    row = 0
    for rowString in rowsArray
        col = 0
        values = str.split(rowString, " ")
        for val in values
            matrix.set(matrix, row, col, str.tonumber(val))
            col += 1
        row += 1
    matrix


stringInput = input.text_area("1 2 3\n4 5 6\n7 8 9")
var m = matrixFromInputArea(stringInput)    

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m))
Create matrix from random values
EXAMPLE
//@version=6
indicator("`matrix.new<type>()` Example 4")

// Function to create a matrix with random values (0.0 to 1.0).
matrixRandom(int rows, int columns)=>
    result = matrix.new<float>(rows, columns)
    for i = 0 to rows - 1
        for j = 0 to columns - 1
            matrix.set(result, i, j, math.random())
    result

// Create a 2x3 matrix with random values.
var m = matrixRandom(2, 3)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m))
RETURNS
The ID of the new matrix object.
SEE ALSO
matrix.setmatrix.fillmatrix.columnsmatrix.rowsarray.new<type>
matrix.pinv()2 overloads
The function returns the pseudoinverse of a matrix.
SYNTAX & OVERLOADS
matrix.pinv(id) → matrix<float>
matrix.pinv(id) → matrix<int>
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.pinv()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Pseudoinverse of the matrix.
    var m2 = matrix.pinv(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Pseudoinverse matrix:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix containing the pseudoinverse of the id matrix.
REMARKS
The function is calculated using a Moore–Penrose inverse formula based on singular-value decomposition of a matrix. For non-singular square matrices this function returns the result of matrix.inv.
SEE ALSO
matrix.new<type>matrix.setmatrix.inv
matrix.pow()2 overloads
The function calculates the product of the matrix by itself power times.
SYNTAX & OVERLOADS
matrix.pow(id, power) → matrix<float>
matrix.pow(id, power) → matrix<int>
ARGUMENTS
id (matrix<int/float>) A matrix object.
power (series int) The number of times the matrix will be multiplied by itself.
EXAMPLE
//@version=6
indicator("`matrix.pow()` Example")

// Display using a table.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, 2)
    // Calculate the power of three of the matrix.
    var m2 = matrix.pow(m1, 3)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Matrix³:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
The product of the id matrix by itself power times.
SEE ALSO
matrix.new<type>matrix.setmatrix.mult
matrix.rank()
The function calculates the rank of the matrix.
SYNTAX
matrix.rank(id) → series int
ARGUMENTS
id (any matrix type) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.rank()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Get the rank of the matrix. 
    r = matrix.rank(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Rank of the matrix:")
    table.cell(t, 1, 1, str.tostring(r))
RETURNS
The rank of the id matrix.
SEE ALSO
matrix.new<type>matrix.setstr.tostring
matrix.remove_col()
The function removes the column at column index of the id matrix and returns an array containing the removed column's values.
SYNTAX
matrix.remove_col(id, column) → array<type>
ARGUMENTS
id (any matrix type) A matrix object.
column (series int) The index of the column to be removed. Optional. The default value is matrix.columns.
EXAMPLE
//@version=6
indicator("matrix_remove_col", overlay = true)

// Create a 2x2 matrix with ones.
var matrixOrig = matrix.new<int>(2, 2, 1)

// Set values to the 'matrixOrig' matrix.
matrix.set(matrixOrig, 0, 1, 2)
matrix.set(matrixOrig, 1, 0, 3)
matrix.set(matrixOrig, 1, 1, 4)


// Create a copy of the 'matrixOrig' matrix.
matrixCopy = matrix.copy(matrixOrig)

// Remove the first column from the `matrixCopy` matrix.
arr = matrix.remove_col(matrixCopy, 0)

// Display matrix elements.
if barstate.islastconfirmedhistory
    var t = table.new(position.top_right, 3, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(matrixOrig))
    table.cell(t, 1, 0, "Removed Elements:")
    table.cell(t, 1, 1, str.tostring(arr))
    table.cell(t, 2, 0, "Result Matrix:")
    table.cell(t, 2, 1, str.tostring(matrixCopy))
RETURNS
An array containing the elements of the column removed from the id matrix.
REMARKS
Indexing of rows and columns starts at zero. It is far more efficient to declare matrices with explicit dimensions than to build them by adding or removing columns. Deleting a column is also much slower than deleting a row with the matrix.remove_row function.
SEE ALSO
matrix.new<type>matrix.setmatrix.copymatrix.remove_row
matrix.remove_row()
The function removes the row at row index of the id matrix and returns an array containing the removed row's values.
SYNTAX
matrix.remove_row(id, row) → array<type>
ARGUMENTS
id (any matrix type) A matrix object.
row (series int) The index of the row to be deleted. Optional. The default value is matrix.rows.
EXAMPLE
//@version=6
indicator("matrix_remove_row", overlay = true)

// Create a 2x2 "int" matrix containing values `1`.
var matrixOrig = matrix.new<int>(2, 2, 1)

// Set values to the 'matrixOrig' matrix.
matrix.set(matrixOrig, 0, 1, 2)
matrix.set(matrixOrig, 1, 0, 3)
matrix.set(matrixOrig, 1, 1, 4)

// Create a copy of the 'matrixOrig' matrix.
matrixCopy = matrix.copy(matrixOrig)

// Remove the first row from the matrix `matrixCopy`.
arr = matrix.remove_row(matrixCopy, 0)

// Display matrix elements.
if barstate.islastconfirmedhistory
    var t = table.new(position.top_right, 3, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(matrixOrig))
    table.cell(t, 1, 0, "Removed Elements:")
    table.cell(t, 1, 1, str.tostring(arr))
    table.cell(t, 2, 0, "Result Matrix:")
    table.cell(t, 2, 1, str.tostring(matrixCopy))
RETURNS
An array containing the elements of the row removed from the id matrix.
REMARKS
Indexing of rows and columns starts at zero. It is far more efficient to declare matrices with explicit dimensions than to build them by adding or removing rows.
SEE ALSO
matrix.new<type>matrix.setmatrix.copymatrix.remove_col
matrix.reshape()
The function rebuilds the id matrix to rows x cols dimensions.
SYNTAX
matrix.reshape(id, rows, columns) → void
ARGUMENTS
id (any matrix type) A matrix object.
rows (series int) The number of rows of the reshaped matrix.
columns (series int) The number of columns of the reshaped matrix.
EXAMPLE
//@version=6
indicator("`matrix.reshape()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix.
    var m1 = matrix.new<float>(2, 3)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 0, 2, 3)
    matrix.set(m1, 1, 0, 4)
    matrix.set(m1, 1, 1, 5)
    matrix.set(m1, 1, 2, 6)
    
    // Copy the matrix to a new one.
    var m2 = matrix.copy(m1)
    
    // Reshape the copy to a 3x2.
    matrix.reshape(m2, 3, 2)
    
    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Reshaped matrix:")
    table.cell(t, 1, 1, str.tostring(m2))
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.add_rowmatrix.add_col
matrix.reverse()
The function reverses the order of rows and columns in the matrix id. The first row and first column become the last, and the last become the first.
SYNTAX
matrix.reverse(id) → void
ARGUMENTS
id (any matrix type) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.reverse()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Copy the matrix to a new one.
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Copy matrix elements to a new matrix.
    var m2 = matrix.copy(m1)
    
    // Reverse the `m2` copy of the original matrix. 
    matrix.reverse(m2)
    
    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Reversed matrix:")
    table.cell(t, 1, 1, str.tostring(m2))
SEE ALSO
matrix.new<type>matrix.setmatrix.columnsmatrix.rowsmatrix.reshape
matrix.row()
The function creates a one-dimensional array from the elements of a matrix row.
SYNTAX
matrix.row(id, row) → array<type>
ARGUMENTS
id (any matrix type) A matrix object.
row (series int) Index of the required row.
EXAMPLE
//@version=6
indicator("`matrix.row()` Example", "", true)

// Create a 2x3 "float" matrix from `hlc3` values.
m = matrix.new<float>(2, 3, hlc3)

// Return an array with the values of the first row of the matrix.
a = matrix.row(m, 0)

// Plot the first value from the array `a`.
plot(array.get(a, 0))
RETURNS
An array ID containing the row values of the id matrix.
REMARKS
Indexing of rows starts at 0.
SEE ALSO
matrix.new<type>matrix.getarray.getmatrix.colmatrix.rows
matrix.rows()
The function returns the number of rows in the matrix.
SYNTAX
matrix.rows(id) → series int
ARGUMENTS
id (any matrix type) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.rows()` Example")

// Create a 2x6 matrix with values `0`.
var m = matrix.new<int>(2, 6, 0)

// Get the quantity of rows in the matrix.
var x = matrix.rows(m)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, "Rows: " + str.tostring(x) + "\n" + str.tostring(m))
RETURNS
The number of rows in the matrix id.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.row
matrix.set()
The function assigns value to the element at the row and column of the id matrix.
SYNTAX
matrix.set(id, row, column, value) → void
ARGUMENTS
id (any matrix type) A matrix object.
row (series int) The row index of the element to be modified.
column (series int) The column index of the element to be modified.
value (series <type of the matrix's elements>) The new value to be set.
EXAMPLE
//@version=6
indicator("`matrix.set()` Example")

// Create a 2x3 "int" matrix containing values `4`.
m = matrix.new<int>(2, 3, 4)

// Replace the value of element at row 1 and column 2 with value `3`.
matrix.set(m, 0, 1, 3)

// Display using a label.
if barstate.islastconfirmedhistory
    label.new(bar_index, high, str.tostring(m))
SEE ALSO
matrix.new<type>matrix.getmatrix.columnsmatrix.rows
matrix.sort()
The function rearranges the rows in the id matrix following the sorted order of the values in the column.
SYNTAX
matrix.sort(id, column, order) → void
ARGUMENTS
id (matrix<int/float/string>) A matrix object to be sorted.
column (series int) Index of the column whose sorted values determine the new order of rows. Optional. The default value is 0.
order (series sort_order) The sort order. Possible values: order.ascending (default), order.descending.
EXAMPLE
//@version=6
indicator("`matrix.sort()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<float>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 3)
    matrix.set(m1, 0, 1, 4)
    matrix.set(m1, 1, 0, 1)
    matrix.set(m1, 1, 1, 2)
    
    // Copy the matrix to a new one.
    var m2 = matrix.copy(m1)
    // Sort the rows of `m2` using the default arguments (first column and ascending order).
    matrix.sort(m2)
    
    // Display using a table.
    if barstate.islastconfirmedhistory
        var t = table.new(position.top_right, 2, 2, color.green)
        table.cell(t, 0, 0, "Original matrix:")
        table.cell(t, 0, 1, str.tostring(m1))
        table.cell(t, 1, 0, "Sorted matrix:")
        table.cell(t, 1, 1, str.tostring(m2))
SEE ALSO
matrix.new<type>matrix.maxmatrix.minmatrix.avg
matrix.submatrix()
The function extracts a submatrix of the id matrix within the specified indices.
SYNTAX
matrix.submatrix(id, from_row, to_row, from_column, to_column) → matrix<type>
ARGUMENTS
id (any matrix type) A matrix object.
from_row (series int) Index of the row from which the extraction will begin (inclusive). Optional. The default value is 0.
to_row (series int) Index of the row where the extraction will end (non inclusive). Optional. The default value is matrix.rows.
from_column (series int) Index of the column from which the extraction will begin (inclusive). Optional. The default value is 0.
to_column (series int) Index of the column where the extraction will end (non inclusive). Optional. The default value is matrix.columns.
EXAMPLE
//@version=6
indicator("`matrix.submatrix()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix matrix with values `0`.
    var m1 = matrix.new<int>(2, 3, 0)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 0, 2, 3)
    matrix.set(m1, 1, 0, 4)
    matrix.set(m1, 1, 1, 5)
    matrix.set(m1, 1, 2, 6)
    
    // Create a 2x2 submatrix of the `m1` matrix.
    var m2 = matrix.submatrix(m1, 0, 2, 1, 3)
    
    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original Matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Submatrix:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix object containing the submatrix of the id matrix defined by the from_row, to_row, from_column and to_column indices.
REMARKS
Indexing of the rows and columns starts at zero.
SEE ALSO
matrix.new<type>matrix.setmatrix.rowmatrix.colmatrix.reshape
matrix.sum()2 overloads
The function returns a new matrix resulting from the sum of two matrices id1 and id2, or of an id1 matrix and an id2 scalar (a numerical value).
SYNTAX & OVERLOADS
matrix.sum(id1, id2) → matrix<int>
matrix.sum(id1, id2) → matrix<float>
ARGUMENTS
id1 (matrix<int>) First matrix object.
id2 (series int/float/matrix<int>) Second matrix object, or scalar value.
Sum of two matrices
EXAMPLE
//@version=6
indicator("`matrix.sum()` Example 1")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix containing values `5`.
    var m1 = matrix.new<float>(2, 3, 5) 
    // Create a 2x3 matrix containing values `4`.
    var m2 = matrix.new<float>(2, 3, 4) 
    // Create a new matrix that sums matrices `m1` and `m2`.
    var m3 = matrix.sum(m1, m2) 
    
    // Display using a table.
    var t = table.new(position.top_right, 1, 2, color.green)
    table.cell(t, 0, 0, "Sum of two matrices:")
    table.cell(t, 0, 1, str.tostring(m3))
Sum of a matrix and scalar
EXAMPLE
//@version=6
indicator("`matrix.sum()` Example 2")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x3 matrix with values `4`.
    var m1 = matrix.new<float>(2, 3, 4)
    
    // Create a new matrix containing the sum of the `m1` matrix with the "int" value `1`.
    var m2 = matrix.sum(m1, 1)
    
    // Display using a table.
    var t = table.new(position.top_right, 1, 2, color.green)
    table.cell(t, 0, 0, "Sum of a matrix and a scalar:")
    table.cell(t, 0, 1, str.tostring(m2))
RETURNS
A new matrix object containing the sum of id2 and id1.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.swap_columns()
The function swaps the columns at the index column1 and column2 in the id matrix.
SYNTAX
matrix.swap_columns(id, column1, column2) → void
ARGUMENTS
id (any matrix type) A matrix object.
column1 (series int) Index of the first column to be swapped.
column2 (series int) Index of the second column to be swapped.
EXAMPLE
//@version=6
indicator("`matrix.swap_columns()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix with ‘na’ values.
    var m1 = matrix.new<int>(2, 2, na)    
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Copy the matrix to a new one.
    var m2 = matrix.copy(m1)
    
    // Swap the first and second columns of the matrix copy.
    matrix.swap_columns(m2, 0, 1)

    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Swapped columns in copy:")
    table.cell(t, 1, 1, str.tostring(m2))
REMARKS
Indexing of the rows and columns starts at zero.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.swap_rows()
The function swaps the rows at the index row1 and row2 in the id matrix.
SYNTAX
matrix.swap_rows(id, row1, row2) → void
ARGUMENTS
id (any matrix type) A matrix object.
row1 (series int) Index of the first row to be swapped.
row2 (series int) Index of the second row to be swapped.
EXAMPLE
//@version=6
indicator("`matrix.swap_rows()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 3x2 matrix with ‘na’ values.
    var m1 = matrix.new<int>(3, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    matrix.set(m1, 2, 0, 5)
    matrix.set(m1, 2, 1, 6)
    
    // Copy the matrix to a new one.
    var m2 = matrix.copy(m1)
    
    // Swap the first and second rows of the matrix copy.
    matrix.swap_rows(m2, 0, 1)
    
    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Swapped rows in copy:")
    table.cell(t, 1, 1, str.tostring(m2))
REMARKS
Indexing of the rows and columns starts at zero.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.swap_columns
matrix.trace()2 overloads
The function calculates the trace of a matrix (the sum of the main diagonal's elements).
SYNTAX & OVERLOADS
matrix.trace(id) → series float
matrix.trace(id) → series int
ARGUMENTS
id (matrix<int/float>) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.trace()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<int>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Get the trace of the matrix.
    tr = matrix.trace(m1)
    
    // Display matrix elements.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Matrix elements:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Trace of the matrix:")
    table.cell(t, 1, 1, str.tostring(tr))
RETURNS
The trace of the id matrix.
SEE ALSO
matrix.new<type>matrix.getmatrix.setmatrix.columnsmatrix.rows
matrix.transpose()
The function creates a new, transposed version of the id. This interchanges the row and column index of each element.
SYNTAX
matrix.transpose(id) → matrix<type>
ARGUMENTS
id (any matrix type) A matrix object.
EXAMPLE
//@version=6
indicator("`matrix.transpose()` Example")

// For efficiency, execute this code only once.
if barstate.islastconfirmedhistory
    // Create a 2x2 matrix. 
    var m1 = matrix.new<float>(2, 2, na)
    // Fill the matrix with values.
    matrix.set(m1, 0, 0, 1)
    matrix.set(m1, 0, 1, 2)
    matrix.set(m1, 1, 0, 3)
    matrix.set(m1, 1, 1, 4)
    
    // Create a transpose of the matrix.
    var m2 = matrix.transpose(m1)
    
    // Display using a table.
    var t = table.new(position.top_right, 2, 2, color.green)
    table.cell(t, 0, 0, "Original matrix:")
    table.cell(t, 0, 1, str.tostring(m1))
    table.cell(t, 1, 0, "Transposed matrix:")
    table.cell(t, 1, 1, str.tostring(m2))
RETURNS
A new matrix containing the transposed version of the id matrix.
SEE ALSO
matrix.new<type>matrix.setmatrix.columnsmatrix.rowsmatrix.reshapematrix.reverse
max_bars_back()
Function sets the maximum number of bars that is available for historical reference of a given built-in or user variable. When operator '[]' is applied to a variable - it is a reference to a historical value of that variable.
If an argument of an operator '[]' is a compile time constant value (e.g. 'v[10]', 'close[500]') then there is no need to use 'max_bars_back' function for that variable. Pine Script® compiler will use that constant value as history buffer size.
If an argument of an operator '[]' is a value, calculated at runtime (e.g. 'v[i]' where 'i' - is a series variable) then Pine Script® attempts to autodetect the history buffer size at runtime. Sometimes it fails and the script crashes at runtime because it eventually refers to historical values that are out of the buffer. In that case you should use 'max_bars_back' to fix that problem manually.
SYNTAX
max_bars_back(var, num) → void
ARGUMENTS
var (series int/float/bool/color/label/line) Series variable identifier for which history buffer should be resized. Possible values are: 'open', 'high', 'low', 'close', 'volume', 'time', or any user defined variable id.
num (const int) History buffer size which is the number of bars that could be referenced for variable 'var'.
EXAMPLE
//@version=6
indicator("max_bars_back")
close_() => close
depth() => 400
d = depth()
v = close_()
max_bars_back(v, 500)
out = if bar_index > 0
    v[d]
else
    v
plot(out)
RETURNS
void
REMARKS
At the moment 'max_bars_back' cannot be applied to built-ins like 'hl2', 'hlc3', 'ohlc4'. Please use multiple 'max_bars_back' calls as workaround here (e.g. instead of a single ‘max_bars_back(hl2, 100)’ call you should call the function twice: ‘max_bars_back(high, 100), max_bars_back(low, 100)’).
If the indicator or strategy 'max_bars_back' parameter is used, all variables in the indicator are affected. This may result in excessive memory usage and cause runtime problems. When possible (i.e. when the cause is a variable rather than a function), please use the max_bars_back function instead.
SEE ALSO
indicator
minute()2 overloads
SYNTAX & OVERLOADS
minute(time) → series int
minute(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Minute (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
SEE ALSO
minutetimeyearmonthdayofmonthdayofweekhoursecond
month()2 overloads
SYNTAX & OVERLOADS
month(time) → series int
month(time, timezone) → series int
ARGUMENTS
time (series int) UNIX time in milliseconds.
RETURNS
Month (in exchange timezone) for provided UNIX time.
REMARKS
UNIX time is the number of milliseconds that have elapsed since 00:00:00 UTC, 1 January 1970.
Note that this function returns the month based on the time of the bar's open. For overnight sessions (e.g. EURUSD, where Monday session starts on Sunday, 17:00 UTC-4) this value can be lower by 1 than the month of the trading day.
SEE ALSO
monthtimeyeardayofmonthdayofweekhourminutesecond
na()2 overloads
Tests if x is na.
SYNTAX & OVERLOADS
na(x) → simple bool
na(x) → series bool
ARGUMENTS
x (simple int/float) Value to be tested.
EXAMPLE
//@version=6
indicator("na")
// Use the `na()` function to test for `na`.
plot(na(close[1]) ? close : close[1])
// ALTERNATIVE
// `nz()` also tests `close[1]` for `na`. It returns `close[1]` if it is not `na`, and `close` if it is.
plot(nz(close[1], close))
RETURNS
Returns true if x is na, false otherwise.
SEE ALSO
