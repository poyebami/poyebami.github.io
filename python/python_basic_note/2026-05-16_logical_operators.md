<h1>Logical Operator </h1>
Logical Operator allows us to evaluate multiple conditions. (or, and, not)

<h3>Or</h3>
With `Or` we can check more than one condition. If at least one of those condition is true, then the entire statement is true. 
```console
temp = 25
is_raining = False

$ # since both the condition is false. It prints the else statement
if temp > 35 or temp < 0 or is_raining: 
    print("Outdoor event is canceled")
else: 
    print("The outdoor event is still scheduled")
$ # output: The outdoor event is still scheduled

temp = 40
is_raining = False

$ # with OR and if one of the condition is met
$ # it will print the if statment
if temp > 35 or temp < 0 or is_raining: 
    print("Outdoor event is canceled")
else: 
    print("The outdoor event is still scheduled")
$ # output: Outdoor event is canceled

temp = -5
is_raining = True

$ # it doesn' matter if both condition is true
$ # you just need one of them to be true
if temp > 35 or temp < 0 or is_raining: 
    print("Outdoor event is canceled")
else: 
    print("The outdoor event is still scheduled")
$ # output: Outdoor event is canceled.
 ```
<h3>And</h3>
With `And` we can link two condition together, however unlike Or, both conditions must be True in order for that entire statement to be True. 
 ```console
temp = 30
is_sunny = True

$ # both condition is True
if temp >=28 and is_sunny:
    print("It is HOT outside")
    print("It is SUNNY")
else:
    print("It is not sunny outside")
$ # output: It is HOT outside. It is SUNNY

temp = 30
is_sunny = False

$ # both condition are not met
if temp >=28 and is_sunny:
    print("It is HOT outside")
    print("It is SUNNY")
else:
    print("It is not sunny outside")
$ # output: It is not sunny outside.
 ```
<h3>Not</h3>
Not logical operator inverts the condition. We are checking to see if something is either not False or not True. Not does the opposite you are looking for. 
 ```console
temp = 24
is_sunny = False

 if temp >=28 and is_sunny:
   print("It is HOT outside")
   print("It is SUNNY")
elif temp <= 0 and is_sunny:
   print("This is COLD outisde")
   print("It is SUNNY")
elif 28 > temp > 0 and is_sunny:
   print("It is WARM outside")
   print("It is SUNNY")
elif temp >=28 and not is_sunny:
   print("It is HOT outside")
   print("It is CLOUDY")
elif temp <= 0 and not is_sunny:
   print("This is COLD outisde")
   print("It is CLOUDY")
elif 28 > temp > 0 and not is_sunny:
   print("It is WARM outside")
   print("It is CLOUDY")
$ # output: It is WARM outside. It is CLOUDY
 ```
<h3>NOT IN </h3>
The `Not In` operator evaluates whether an element does not exist inside a given collection (like a list, tuple, or string).
 ```console
banned_user = ["admin", "root", "superuser"]
current_user = "guest"

if current_user not in banned_user:
    print("Access granted.")
 ```
