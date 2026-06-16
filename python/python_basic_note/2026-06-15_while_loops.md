<h1>While Loops</h1>
While loops will execute some code WHILE some condition remains true. It will continue to execute the code until the conidtion is no longer true. You do need some way to get out of a while loop, otherwise, you'll run into a infinite loop.

```console
$ # while our name variable is empty, print the code forever
name = input("Enter  your name: ")

while name == "":
    print("You did not enter your name")
    name = input("Enter your name: ")
print(f"Hello {name}")
```
You could do something, while something is not true by using the `not` logical operator.
```console
food = input("Enter your favorite food ( q to quit): ")

while not food == "q":
    print(f"You like {food}")
    food = input("Enter another favorite food ( q to quit): ")

print("bye")
```
```console
number = int(input("Enter a number between 1-10: "))

while number < 1 or number > 10:
    print(f"{number} is not vaild")
    number = int(input("Enter a number between 1-10: "))

print(f"The number you picked is {number}")
```
While loops is useful for verifying user input. If a user types in some input that is not vaild, you reprompt them. 
