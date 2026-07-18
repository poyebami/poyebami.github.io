<h1>Test Operators</h1>
In Bash, the `test` command evaluates conditional expressions and returns an exit status of 0 (true) or 1 (false).  We can ask a terminal to show if a string of text is equal to another. 
 ```console
 $ # returns 0 = true
 [ hello = hello]
 echo $?
 $ # output: 0

 $ # returns 1 = false
 [ 1 = 0 ]
 echo $?
 $ # output: 1
 ```
 ```console
 $ # integer operators reference
 -eq: equal to
 [ 1 -eq 1 ]
 $ # output: 1

 -ne: not equal to
 [ 1 -ne 0 ]
 $ # output: 0

 -gt: greater than 
 [ 1 -gt 0 ]
 $ # output: 0

 -ge: greather than or equal to
 [ 1 -ge 0 ] 
 $ # output: 0

 -lt: less than
 [ 1 -lt 0 ]
 $ # output: 1

 -le: less tahn or equal to
 [ 1 -lt 0 ] 
 $ # output: 1
 ```
`echo $?` prints the exit status (or return code) of the last executed command. 
The result of exit status. 
```console
0: the previous command executed successfully with no errors.
Non-zero (1-255): the previous command failed or encountered an unusual condition

Common Exit Code:
1: general catchall for errors
2: misuse of shell built-ins (e.g., missing argument).
126: command invoked cannnot execute (permission denied).
127: command not found
128+N: command terminated by system signal N (e.g., 130 means terminated by Ctrl+c)
```
