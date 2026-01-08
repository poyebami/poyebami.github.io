<h1>Starting GIT</h1>

<h3>Initializing a GIT Repository </h3>

  ```console
  $ git init # initialized empty GIT repository
  $ touch story1.txt # create a new txt file
  $ echo "This is a beautiful story" >> story1.txt # edit text into file without using vi commands
  $ git status # to see the satus of git
  ```

<h3>What does each GIT Status represents </h3>

  ```console
  $ git status
    On branch master # branches are multiple states of the codebase. Different versions of the code to test new feature, bux fixes, or experiments without affecting the original project. Master branch is the default
        no commits yet # commits are changes made on the  repository
         untracked files: # untracked files are files GIT knows of but we had not yet told GIT what to do with them
            Story1.txt
    # nothing added to commit but untracked files present
   ```

<h3> Commiting Files in GIT </h3>

  Each commit is used to solve a singple probelm or to implement a specific feature or improvement
  ```console
  $ git add # to put files into the staging area
  $ git commit -m "message" # adds the files into the committed files. Put useful message to summarize what changees have been made
  # -m is to pass in the commit message without going into the files and typing in a message
  ```

 * Before committing, GIT need to know who you are. Use config command to set the name and email of the user
 
  ```console
  $ git config user.name "name"
  $ git config user.email "name@example.com"
  ``` 

  ```console
  $ git add . # stage both modified file and untracked file
  ```

  ```console
  # commiting modified file and untracked files separately
  $ git add <file_name_1>
  $ git commit -m "updated file_name_1"
  $ git add <file_name_2>
  $ git commit -m "adding second file"
  ```

  ```console
  $ git restore <file_name> # this restore the file from the previous commit
  ```

  ```console
  # staged <file_name_1> and updated <file_name_2> but you want to commit <file_name_2> first
  $ git restore -staged <file_name_1> # to remove file_name_1 from the staging area
  $ git add <file_name_2> # put file_name_2 to the staging area and then commit
  ```
  
  ```console
  # commit a file without adding personal_notes
  $ git rm <personal_notes> # you must specify with options. Cached or Force

  Specifying the cached option will retain the file in our directory and the force option will delete  the file permanently 
  $ git rm --cashed <personal notes> # move file from staging area to untracked working area. However we need GIT to ignore the file
  $ echo "personal_notes" >> .gitignore
  $ cat .gitignore # view gitignore files
  ```

<h3>Showing all information from commits </h3>
 
  ```console
  $ git log # shows information about all commits made including commit hash, author name, date, and commit message

  $ git log --oneline # only shwos condensed views of commit history
  $ git log --name-only # will show the list of changed files names
  $ git log -1 # shows the latest commit in the repository
  ```


