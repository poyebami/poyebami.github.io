<h1>C# for Beginners </h1>

<h3>Creating and Running a application </h3>
After creating a folder called code in my D drive, I opened Windows Powershell. To check the content of the folder I used the command line called `DIR`.
 ```console
 $ # DIR lists the contents of a directory
 PS D: \Users\mideo> cd D: \code\
 PS D: \code> dir
 ```
I makde a directory called `helloworld`
 ```console
 PS D: \code> cd .\helloworld\
 PS D: \code\helloworld> dir
 ```
What is dotnet is a command line tool used to create projects, running, testing, and making new applications. 

I'm going to create a console application. 
```console
PS D: \code\helloworld> dotnet new console
```
This created a couples of files. For instance, there is helloworld.csproj which is the project files. It contains the lsit of files in the project. Another file is Program.cs, which is the main program and the entry point. It is where the code runs from. 
To run the program use
```console
 PS D: \code\helloworld> dotnet run
 Hello, World!
 PS D: \code\helloworld> 
```
What dotnet run does is to compile the application, create the output, and then run Hello World. This has also created a extra file called `bin` or `binary`. That is where the application is. 

Different ways to print out the application 
```console
$ # print out the application on notepad
PS D: \code\helloworld> notepad .\Program.c

$ # print out the application on VS Code
PS D: \code\helloworld> code .
$ # . means this folder
```
To run the application in VS Code press `F5 or Ctrl F5`. 
