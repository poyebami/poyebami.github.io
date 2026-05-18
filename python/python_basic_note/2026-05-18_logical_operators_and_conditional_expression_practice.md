<h1>Logical Operator and Conditional Expression Practice </h1>
<h3>Logical Operator</h3>
```console
$ # user input will always print as a string
$ # since im checking for two results 
$ # i have dnd_class check using two separate argument
dnd_class = str(input("What is your class? "))

if dnd_class == "mage" or  dnd_class == "warrior":
    print("Combat class selected")
else:
    print("Support class selected")

```
```console
$ # i can use both and and or logical operators
$ # i put weapon variable in parentheses so it can check for two results using separate argument
$ # and i use and logical operators 
level = int(input("What is you level? : "))
weapon = input("What weapon are you using? : ")

if level >= 10 and (weapon == "sword" or weapon == "staff"):
    print("You can enter")
else:
    print("You cannnot enter")
```
<h3>Conditional Expression</h3>
```console
hp = int(input("What is HP? ")) 

health_bar = "Healthy" if hp > 50 else "Critical"
print(health_bar)
```
```console
dnd_level = int(input("What is your level: "))

rank = "Master" if dnd_level >= 50 else "Novice"
print(f"Your rank is {rank}")
```
```console
dnd_level = int(input("What is your level: "))

rank = "Master" if dnd_level >= 50 else "Novice"
print(f"Your rank is {rank}")
```
<h3>BIGGER CHALLENGER </h3>
```console
name = input("What is your name? :")
dnd_level = int(input("What is your level? :"))
dnd_class = (input("What is your class? : "))
weapon = input("What is your weapon? :")

if dnd_level >= 20 and (dnd_class == "warrior" or dnd_class == "mage" ) and (weapon == "sword" or weapon == "staff"):
    print(f"{name}. You may enter the Dragon Gate")
else: 
    print("Deny entry")

rank = "Elite" if dnd_level >= 50 else "Rookie"
print(f"{name} is a {rank}")
```
