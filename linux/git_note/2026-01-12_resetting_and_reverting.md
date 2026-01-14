<h1>Resetting and Reverting </h1>


<h3>Reverting </h3>
Reverting creates a new commit that reverts all the changes that were made on the commit that we specificed. 
Revert command is useful when you want to undo changes and keep those changes in your Git history. 
 ```console
 $ git revert "hashes"

 $ # revert changes on 8ad5d
 $ git revert 8ad5d
 ```

<h3>Reset </h3>
There are two ways to reset the commit in order to undo it. The reset commands also receeive the amount of commits that we wanted to reset.
 ```console
 $ # keep all the changes that were made
 $ git reset --soft HEAD~1
 $ git status
 On branch sarah
 Changes to be committed:
    added:  third_story_md

 $ # lose all the changes that were made on that commit
 $ git reset --hard HEAD~1
 $ git status
 On branch sarah
 Nothing to commit
 ```

 <h3>Stashing </h3>

