<h1>String Indexing</h1>
Indexing allows us to acces elements of a sequence using [] (indexing operator)
Using set of square brackets, following a string, there are up to 3 fields that we can fill in. 
We can access a string point in the string, an ending point, and a step. [ start : end : step]
 ```console
 $ # print the first character within a string
 credit_number = "1234-5678-9012-3456"
 print(credit_number[0])
 $ # Output : 1 

 print(credit_number[1])
 $ # Output : 2

 print(credit_number[4])
 $ # Output : -

 $ # print the first 4 characters within a string
 print(credit_number[0:4]
 $ # output : 1234

 print(credit_number[5:])
 $ # output : 5678-9012-3456

 print(credit_number[-1])
 $ # output : 6
```
With the ending index, this index is exclusive. We did not include the last character (-). The starting index is inclusive. 

We can access the characters in a string by a given step. 
 ```console
 $ # print every second character within our string
 $ print(credit_number[::2])
 $ # output: 13-6891-46
 ```
<h3>Practice</h3>
 ```console
$ # create a program to get the last 4 digits of a credit card number
credit_card = input("Enter your credit card number: ")
last_digit = credit_card[-4:]
print(f"xxxx-xxxx-xxxx-{last_digit}")
$ # output: xxxx-xxxx-xxxx-3456 input : 1234-5678-9012-3456
 ```
 ```console
 $ # print the characters in reverse
credit_card = input("Enter your credit card number: ")
reverse = credit_card[::-1]
print(reverse)
$ # output : 0987654321 input: 1234567890
 ```
