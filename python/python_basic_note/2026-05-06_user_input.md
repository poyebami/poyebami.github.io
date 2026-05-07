<h1>User Input </h1>
Input() is a function that prompts the user to enter data. Returns the entered data as a string. 
To enter input, we use the input function
 ```console
 input()
 ```
For input function, we need to enter a prompt within quotes.
 ```console
 input("What is your name?: ")
 ```
We can also assign input to a variable.
 ```console
 name = input("What is your name?: ")
 print(f"Hello {name}!")

 Hello Prosper!
 ```
NOTE: THE DATA TYPE OF THE VALUE RETURNED BY THE input() FUNCATION IS ALWAYS A string(str).
 ```console
  name = input("What is your name?: ")
  $ # changing the data type of age to a int variable
  age = int(input("How old are you? : "))
  age = age + 1
  print(f"Your name is {name}")
  print(f"You will be {age} next year")
 ```
<h1>User Input Practice </h1>
Password Code
 ```console
password = input("What is the password: ")
stored_password = ("dragon")
if password == stored_password:
    print("Access Granted")
else:
    print("Wrong Password")
 ```
MINI RPA GAME
 ```console
name = input("What is your name: ")
class_dnd = input("What is your class: ")
print(f"Hello {name}. You are a {class_dnd}")
path  = input("Go Left or Right: " )
enemy = ("There is a dragon! ")

if path == "Right":
    print("You entered a trap. You are dead")
elif path == "Left":
    print(enemy)
     
    action  = input("Run or Fight: ")
    if action == "Run":
        print("You escaped")
    elif action == "Fight": 
        print("Dragon used fireball and burned you alive. Game Over")
 ```
