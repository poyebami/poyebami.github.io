<h1>If Statements</h1>
If statement allows you to execute a block of code only if a specific condition is met or else do something else. With if statement, you can either write a condition or you could use a boolean. 
 ```console
 age = int(input("What is your age? "))

if age >= 18:
    print("You can get a credit card")
else: 
    print("You must be 18+ to get a credit card")
 ```
The `else` statement will be last thing that code does if the other conditions are not met. 

We can check more than one conditon before reaching the else statement. This is called a `else if` statement. 

<h3>Else If Statement</h3>
Else if statement is shorten to `elif`.
 ```console
 age = int(input("What is your age? "))

if age >= 100:
    print("You are too old")
elif age >= 18:
    print("You can sign up")
elif age == 0:
    print("You haven't been born yet ")
else:
    print("You must be 18+ to sign up")
 ```
NOTE: ORDER MATTER FOR BOTH IF AND FOR STATEMENTS BECAUSE THE INTERPRETER EVALUATES CODE SEQUENTIALLY FROM TOP TO BOTTM.

<h3> Boolean Variable and If Statement</h3>
For if statement, you can use the boolean variable in place of a condition. 
 ```console
for_sale = False

if for_sale == True:
    print("This is for sale")
else: 
    print("This is not for sale")
 ```
<h3>If Statement Practice </h3>
Do you want some food
 ```console
 response = input("Would you like food? (Y/N): ")

if response == "Y": 
    print("Have some food")
elif response == "N":
    print("No food for you")
else:
    print("I dont' understand you. ")
 ```
Enter your name
 ```console
# Enter your name

name = input("Enter your name ")

if name == "":
    print("You must enter a name")
elif name == "John":
    print("GET OUT NOW!")
else:
    print(f"Welcome {name}")
 ```
PICK A PATH RPG
 ```console
 # PICK A PATH
path = input("Pick a path: left or right ")
gold = 0
if path == "right":
    print("You found a room at the end of the hall")
    door = input("Do you open the door? Y/N ")
    if door == "Y":
        print("You found a teasure room. +500 GOLD ")
        gold += 500
        print(f"Your total gold is {gold}. ")
    elif door == "N":
        print("You continue to explore the dungeon and got lost. GAME OVER" )
elif path == "left":
    print("You found a chest")
    chest = input("Do you open the chest? Y/N ")
    if chest == "Y":
        print("The chest was a mimic. GAME OVER")
    elif chest == "N":
        print("You looked closely at the chest and noticted it was a mimic.")
        action = input("Do you attack the mimic? Y/N ")
        if action == "Y":
            print("You killed the mimic +20 GOLD")
            gold += 20
            print(f"Your total gold is {gold}.")
        elif action == "N":
            print("You ran away and left the dungeon empty hand. -102 GOLD for not finishing the quest")
            gold -= 102
            print(f"Your total gold is {gold}. You owe the guild 250 gold. ")
else:
    print("You waited too long and a slime killed you. GAME OVER")
 ```
