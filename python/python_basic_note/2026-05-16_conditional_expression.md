<h1>Conditional Expression</h1>
A conditional expression is a one-line shortcut for the if-else statement (ternary operator). Using conditioanl expression, we can print or assign one of two values based on a conditional. 

RETURN X if our condition is True, else return Y
 ```console
 num = 5 
 a = 6 
 b = 7
 age = 25
 temperature = 15
 user_role = "admin"
 print("Positive "if num > 0 else "Negative")
 $ # output: Positive

 result = "Even" if num % 2 == 0 else "Odd"
 print(result)
 $ # output: Odd

 max_num = a if a > b else b
 print(max_num)
 $ # output: 7

 min_num = a if a < b else b
 print(min_num)
 $ # output: 6

 status = "Adult" if age >= 18 else "Child"
 print(status)
 $ # output: Adult

 weather = "HOT" if temperature > 20 else "COLD"
 print(weather)
 $ # output: COLD

 access_level = "Full Access" if user_role == "admin" else "Access Denied"
 print(access_level)
 $ # output : Full Access
```
