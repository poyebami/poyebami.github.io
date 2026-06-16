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

<h3>Countdown</h3>
```console
$ # initialize the starting number 
count = 1 

$ # loop as long as count is less than or equal to 5
while count <= 5:
    print(count)
$ # increment the number so the loop eventually stops
    count += 1
```
```console
$ # Count down from 10 to 1 then print "Blast off!"
count = 10

while count <= 10 and count >= 1:
    print(count)
    count -= 1
    
print("Blast Off")
```
<h3>While Loop Practice </h3>
```console
$ # starting total number is 0
total =0
user_input = input("Enter a number: type done to stop ")
$ # checks to see if user_input is not 'done'
while not user_input == "done":
    $ # turns user input into int datatype and also add the total to new total
    total = total + int(user_input)
    user_input = input("Enter a number: type done to stop ")

print(total)
```
