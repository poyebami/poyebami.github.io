<h1>If/Elif/else</h1>
 ```console
 #!/bin/bash

$ # ,, parameter expansion allows us to ignore
$ # upper and lower cases when comparing to values.
$ # ; is used to end the test operator 

if [ ${1,,} = prosper ]; then
        echo "Welcome!"
elif
        [ ${1,,} = help ]; then
        echo "Enter your username"
else
        echo "I don't know who you are"
 ```
`fi` is the keyword used to close an if conditional statement.
