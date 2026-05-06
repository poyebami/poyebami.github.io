</h1>Typecasting</h1>
Typecasting is the process of converting a variable from one data type to another. str(), int(), float(), bool().
Typecasting is useful with handling user input.:
</h3>How to get the data type of a variable</h3>
Use the type() funcation to get the data type. 
 ```console
 name = "Prosper"
 age = 26
 gpa = 3.2
 is_student = True

 type() -> type(name)
 ```
However if you try to run this code, there is not output. We need to print it.
 ```console
 print(type(name))
 <class 'str'>

 print(type(age))
 <class 'int'>
 
 print(type(gpa))
 <class 'float'>

 print(type(is_student))
 <class 'bool'>
 ```
<h3>Convert from one data type to another</h3>
Reassign variable and use the data type function
 ```console
 gpa = int(gpa)
 print(gpa)
 3

 age = float(age)
 print(age)
 26.0
 ```
When typecasting to a string despite the output of the value, it is going to be a string
 ```console
 age = str(age)
 print(age)
 26
 $ # Even though it is printing a number, the data type is a string. 

 print(type(age)
 <class 'str'>
 ```
When typecasting to a boolean, as long there is a string of characters, the integer and float is not 0, the output will always be `True`. 
 ```console
 name = bool(name)
 print(name)
 True

 age = bool(age)
 print(age)
 True 

 gpa = bool(gpa)
 print(gpa)
 True

 $ # false output
 name = ""
 age = 0
 gpa = 0
 is_student = True

 name = bool(name)
 age = bool(age)
 gpa = bool(gpa)

 False
 False
 False
 ```
