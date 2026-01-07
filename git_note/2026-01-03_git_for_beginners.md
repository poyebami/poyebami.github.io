<h1>GIT Introduction </h1>

<h3>What is GIT</h3>

* `GIT` is an open sourse distributed version contrl system. It is a content tracker that stores all our code changes

   * The `version control system` means that we can go back in time and work with a different version of our codecase, since GIT stores it all and works with `branches`.

   * `Distributed` means that there is a `remote repository` that is stored in a server and a `local repository` is stored on the computer of every developed working on the project.

   * GIT in short can make me go back in time without losing a new changes.  Can have access to the entire project's history, and the changes made, who made those changes, and when it was made.

* Installing GIT

  * To install GIT, you can download it directly from the offical website or install it using Homebre with command 

   ```console
   $ brew install git
   ```
   The installation process may very dependubg on your operating system, so be sure to look up the appropriate instructions for your system.

 * Identify GIT Version
    
    * To identify the version of GIT use
    
    ```console
    $ git version
    $ git help $ view git commands
    $ git help <command>  # to view a detailed help for any git command
    ```
<h3>Local Repositories</h3>

* Local Repositories are on my own machine and I have direct access to it.

  * Local Repository has 3 stages

  * The `Working Area` are all my active changes

  * The `Staging Area` contains new changes that will soon be commited

  * The `Commit Files` is where people could add their changes and save new states of the project each time. 
      1. People can commit their changes in order to add version control to the project.

      2. Files that should be included in the commit are first added to the staging area.

      3. A commit get created when a developer actually commit those files.
         
<h3>Remove Repositories</h3>

* Remote Repositories is usually a centralized server and is entire optional. We can save the changes that we made locally on this remove server. 

   * It is useful when I want to have a backup of my data incase my comptuer breaks or when working with a team.

   * Teammates can initialize their own local repositories on their own computer and pull the data from the remote repository in order to start working on my project.

   * When one of the teamamtes has made some changes, they can push these changes to the remote repository.

   * To keep my local and remote repository in sync, I can pull these changes from the remote preository into my own local repository. 




