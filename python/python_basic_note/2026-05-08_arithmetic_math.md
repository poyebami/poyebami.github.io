<h1>Arithmetic and Math in Python</h1>

<h3>Addition Operator</h3>
 ```console
 friends = friends + 1
 ```
<h3>Subtraction Operator</h3>
 ```console
 friends = friends - 2
 ```
<h3>Multiplication Operator</h3>
 ```console
 friends = friends * 3
 ```
<h3>Divison Operator</h3>
 ```console
 friends = friends / 2
 ```
<h3>Exponents Operator</h3>
 ```console
 friends = friends ** 2
 ```
<h3>Modulus Operator</h3> 
Gives you the remainder of any division. The `%` is known as the modulus operator. 
 ```console
 friends = 10
 remainder = friends % 3 
 print(reminder)
 1
 ```
Modulus Operator is useful to find if a number is even or odd.
<h3>Augmented Assignment</h3>
Augmented Assignment is useful because it uses less text and easier to read. 
 ```console
 $ # Augmented Addition
 friends += 1
 1

 $ # Augmented Subtraction
 friends -= 2
 -2

 $ # Augmented Multiplication 
 friends *= 3
 18

 $ # Augmented Division
 friends /= 2
 3

 $ # Augmented Exponments
 friends ** = 2
 25
 ```
<h3>Built-in Math Related Funcation</h3>
The Python `round`() is a built-in function used to round a numeric value to a specified number of decimal places. 
 ```console
 x = 3.14
 y = -4
 z = 5
 
 result = round(x)
 print(result)
 3
 ```
The `abs`() is the distance away from zero as a whole number.
 ```console
 result = abs(y)
 print(result)
 4
 ```
The `Pow`() function is used for exponentiation, calculating a base raised to a specific power.
 ```console
 # simple power: 4^3 = 64
 print(pow(4,3))
 64
 ```
The `max`() function is used to find the maximum value of various values. 
 ```console
 $ # prints maximum value between x, y, and z
 result = max(x, y, z)
 5
 ```
The `min`() function is used to find the minimum value of various values.
 ```console
 $ # prints the minimum value between x, y, and z
 result = min(x, y, and z)
 -4
 ```
There is also `log` function that computes the natural logarithm (base e)
 ```console
 math.log(x)

 $ # base 10 (log_10x)
 math.log10(x)
 
 $ # base 2 (10_2x)
 math.log2(x)
 ```
<h3>Useful Constants and Functions</h3>
To use mathematical functions beyond basic arithemtic (like addition or multiplication) in Python, you need to import the built-in `math module`.

The most common ways to import it is with the `import` statement at the top of your file.
 ```console
 import math

 print(math.pi)
 3.141592653

 print(math.e)
 2.178281828459045

 x = 9 
 result = math.sqrt(x)
 print(result)
 3.0

 $ # ceil will always round a floating point number up
 x = 9.1
 result = math.ceil(x)
 print(result)
 10

 $ # floor will always round a floating point down
 x = 6.2
 result = math.floor(x)
 6
 ```
<h3>Arithmetic and Math Practice</h3>
Calculate the circumference of a circle
 ```console
 radius = float(input("What is the radius of the circle: "))
 circumference = 2 * (math.pi) * radius
 print(f"The circumference of the circle is {circumference:.2f}.")

 # another ways to round
 print(f"The circumference of the circle is {round(circumference, 2)}.")
 ```
Calculate the are of a cicle
 ```console
 radius = float(input("What is the radius?: "))
 area = math.pi * pow(radius, 2)

 print(f"The are of the circle is {round(area, 2)}."

 ```
