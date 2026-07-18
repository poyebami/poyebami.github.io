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

<h3>Key Components</h3>
 ```console
 if : initiates the conditional statement and evaluates the first test.
 then: signals the start of the code execuation block if the preceding conditional is met
 elif: It specifies a new condition to test if the previous ones fail.
 else: outlines a fallback block of code that runs only if none of the if or elif test evaluates to true.
 ```
<h3>Grade script</h3>
 ```console
 #!/bin/bash

 if [ $1 -ge 90 ]; then
    echo "Your grade is a A"
 elif [ $1 -ge 80 ]; then
    echo "Your grade is a B"
 elif [ $1 -ge 70 ]; then
    echo "Your grade is a C"
 elif [ $1 -ge 60 ]; then
    echo "Your grade is a D"
 else
    echo "Your grade is a F"
 fi
 ```
