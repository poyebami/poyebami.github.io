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
