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
Let say that we are working on a new_file and we need to make changes to master branch. However, we didn't want to commit the incomplete new_fiile.
We can use command git stash.
 ```console
 $ # stash all changes in the working area. 
 $ git stash 

 $ # get changes back into the working area
 $ git stash pop
 ```
We can keep on pushing to the stash and the changes will pile up. If multiple stashes are stacked, popping the stash will apply the most recent one first.
 ```console
 $ # list all the stashes 
 $ git stash list
 stash@{0}: WIP on sarah: f4e8304 Added third story
 stash@{1}: WIP on sarah: s53fwe4 Added fourth story
 stash@{2}: WIP on sarah: k4e5432 Added fifth story

 $ # shows the contents of a certain stash
 $ git stash show stash@{1}
 fourth_story.md | 1 +
 1 file changed, 1 addition(+)

 $ # pop a specific stash
 $ git stash pop stash@{1}
 Dropped stash@{1} (2cfe...)
 ```

<h3>Reflog </h3>
Git reflog commands shows us all the actions that have been taken on our repository.
 ```console
 $ git reflog
 a340aae HEAD@{0}: reset: moving to HEAD~1
 8ad5d8c HEAD@{1}: commit: Added third story
 aaba51e HEAD@{2}: commit: Changes to second story
 fb9f13e HEAD@{3}: commit: Added second story
 ```
If we make a mistake and perform a hard reset on a file we later need, we can use the git reflog command to view past actions and reset back to a previous state.
 ```console
 $ # reset the repository to its previous state.
 $ git reset --hard 8ad5d8c
 ```
