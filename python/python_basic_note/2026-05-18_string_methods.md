<h1>String Methods</h1>
A string is a series of characters. 

<h3>Len()</h3>
The len() length function will give us the length of a string. How many characters is it? 
 ```console
 name = input("Enter your full name: ")

 result = len(name)
 print(result)
 $ # output: input is kris main and the result is 9
 ```
NOTE: len() includes SPACES

<h3>Find</h3>
The find method will return the first occurrence of a given character, the position. When working with indexes, we always begin with zero. The first character would have an index of zero.
```console
name = input("Enter your full name: ")
result = name.find(" ")
print(result)
$ # output: input is kris main and result is 4
```
```console
$ # if it can't find the character; it will return -1
name = input("Enter your full name: ")
result = name.find("q")
print(result)
$ # output: input is kris main and result is -1
```
```console
$ # to find the last occurrence
name = input("Enter your name: ")
result = name.rfind("p")
print(result)
$ # output: input is prosper and result is 4
```
<h3>Capitalize</h3>
Capitalize () command will capitalize the first character in the string. 
 ```console
 name = input("Enter your full name: ")
 name = name.capitalize()
 print(name)
 $ # output: input is prosper and result is Prosper
 ```
<h3>Upper</h3>
The upper () command will capitalize every characters in the strig.
 ```console
 name = input("Enter your full name: ")
 name = name.upper()
 print(name)
 $ # output: input is prosper and result is PROSPER
 ```
<h3>Lower</h3>
The lower () command will make every character in the string lowercase.
 ```console
 name = input("Enter your full name: ")
 name = name.lower()
 print(name)
 $ # output: input is PROSPER and result is prosper
 ```
<h3>IsDigit</h3>
The isdigit() will return either true or false. It only returns true if the string contain only digits. The result is a boolean. If there is a space, it will print False
 ```console
 name = input("Enter your name: ")
 result = name.isdigit()
 print(result)
 $ # output: input is prosper and result is False
 $ # output: input is prosper123 and result is False
 $ # output: input is 12345 and result is True
 $ # output: input is 123 456 and result is False
 ```
<h3>isalpha()</h3>
isalpha() command will return either true or false. It only returns true if the string contain only alphabetical characters. The result is a boolean. If there is a space, it will print False
 ```console
 name = input("Enter your name: ")
 result = name.isalpha()
 print(result)
 $ # output: input is prosper and result is True
 $ # output: input is PROSPER and result is True
 $ # output: input is prosper123 and result is False
 $ # output: input is 123 and result is False
 $ # output: input is bro code and result is False
 ```
<h3>Count()</h3>
count() command will result and integer and returns the number of times a specific value appears within a sequence. 
 ```console
 phone_number = input("Enter your phone number: ")
 
 result = phone_number.count("-")
 print(result)
 $ # output: input is 123-456-7890 and result is 2
 ```
<h3>Replace</h3>
The replace() command is the most used command in python. It will replace any occurrence with one character with another. 
 ```console
 phone_number = input("Enter your phone number: ")
 
 result = phone_number.replace("-", " ")
 print(result)
 $ # output: input is 123-456-7890 and result is 123 456 7890
 ```
We can remove the characters completely by replacing them with an empty string
 ```console
 phone_number = input("Enter your phone number: ")

 result = phone_number.replace("-", "")
 print(result)
 $ # output: input is 123-456-7890 and result is 1234567890
 ```
<h3>Help</h3>
Print a comprehensive list of all of the string method.
 ```console
 print(help(str))
 ```
