<h1>GIT Branches </h1>


<h3>What are GIT Branches </h3>
GIT Branches are pointers to a certain commit. A HEAD is where you are right now in the GIT Repository.
The HEAD points to the last commit in the branch that you're currently on. When switching branches, the HEAD moves with you.

  ```console
  $ # create a new branch
  $ git branch "branch_name" 

  $ # switch to an existing branch
  $ git checkout sarah # switch to branch sarah

  $ # to create a new branch and switch to it 
  $ git checkout -b "branch_name"

  $ # to delete a branch
  $ git branch -d max # delete branch max

  $ # view all braches- both local and remote
  $ git branch -a
  $ # to see the name of all branches
  $ git branch 
  ```

<h3>GIT Merging branches </h3>
To merge branches, we need to checkout to the branch we want to merge with.
For example: we switch to master branch to merge branch feature/signup into master branch
 
 ```console
  $ # checkout to master branch
  $ git checkout master

  $ # merging feature/signup branch to master branch
  $ git merge "feature/signup"
  ```
There are two types of merges. 
  * `Fast-foward` describles what happens when a branch can be moved straight ahead to a new commit without create a merge commit.
  
   ```console
    Before merge 
       A - B - C (main)
                \
                  D - E (feature)

    After merge
        A - B - C - D - E
   ```

  * `No-fast-foward` means GIT is forced to create a merge commit. If we committed changes on the current branch that the branch, we want to merge doesn't have, GIT will perform a no-fast-forward merge.

   ```console
    Before merge
       A - B - C - M (main)
                \
                 D - E (feature)
    After merge
       A - B - C --- M (main)
               \     /
                D - E (feature) 
   ```



