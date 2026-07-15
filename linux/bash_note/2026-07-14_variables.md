<h1>Variable</h1>
When creating variables make sure that is not space before or after the equals sign.
 ```console
 $ # incorrectly variable with spacing

 #!/bin/bash
 FIRST_NAME = John
 LAST_NAME=Smith
 echo hello $FIRST_NAME $LAST_NAME

 $ ./hellothere.sh
 $ # error: ./hellothere.sh: line 3: John: command not found. 
 $ # output: hello Smith

 $ # correct variable with no spacing
 #!/bin/bash
 First_NAME=John
 LAST_NAME=Smith
 echo hello $FIRST_NAME $LAST_NAME

 $ ./hellothere.sh
 $ # output: hello John Smith
 ```
<h3>Asking for Input</h3>
When asking for user input, use the read command
 ```console
 $ # asking for user input
 #!/bin/bash

 echo What is your first name?
 read FIRST_NAME
 echo What is your last name?
 read LAST_NAME
 
 echo Hello $FIRST_NAME $LAST_NAME

 $ ./input.sh
 $ # output: Hello John Smith
 ```
To make it easier, you don't have to use `echo` command to ask for user input. Instead use -p flag. The -p flag let you show a prompt message on the same line, right before the user types their answer. Make sure to put the variable name at the end of the line
 ```console
 $ # ask for input with -p flag
 #!/bin/bash
 read -p "What is your first name: " FIRST_NAME
 read -p "What is your last name: " LAST_NAME
 echo "Hello, $FIRST_NAME $LAST_NAME"
 ```
<h3>Flag</h3>
There are lot of different flags you can use to modify the behavior of the read command.
 ```console
 $ # -s hides the characters as the user types, used for sensitive data
 read -sp "Enter your password: " password
 ```
 ```console
 $ # -t automatically stops waiting after a specified number of seconds
 $ # timeout after 5 seconds
 read -t 5 -p "Enter answer in 5 seconds: " response
 ```
 ```console
 $ # -n automatically terminates that input after a specific number of characters are typed
 $ # limit to 1 character
 read -n 1 -p "Press Y or N to continue: " confirmation
 ```
