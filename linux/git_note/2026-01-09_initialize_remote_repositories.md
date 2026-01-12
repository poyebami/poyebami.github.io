<h1>Initializing a Remote Repositories </h1>


<h3>Remote Repositories </h3>
There are serveral platmores like GitHub on which we can host our remote repository. once we've initializex a repository, we get 
access to a `Connection String`. A Connection String is a URL that we can use in order to let GIT know where the remote repository is located.
 ```console
 $ # add remote repository to our local project
 $ git remote add origin # used origin to know which remote repository we're pushting to withot having to memorize the entire connection string
 $ git remote add origin https://.../.../[name].git 

 $ # list all your remote repositories
 $ git remote -v 

 $  #confique config the GIT remote repository to sarah's story blog
 $ cd /home/sarah/story-blog
 $ git remote add origin http://git.example.com/sarah/story-blog.git
 ```
We can fetch and push the necessary data from our local project to the hosted repository.


<h3>Pushing </h3>
In order to keep our local and remote repository in sync, we need to push the data from our local repository to the remote repository. 
 ```console
 $ # push data to the remote repository
 $ git push origin master # expects two more arguments. The alias of the remote repository, and current branch that we are on.
 ```

<h3>Cloning Remote Repositories </h3>
A new person is hired and they want to get access to all the dataa that's currently hosted on the remote repository. They can colon the 
repository in order to get all the data on their local machines, 
 ```console
 $ git clone [ ssh link ] 
 $ # cloning from GitHub
 $ git clone git@github.com:account/remote-repo.git
 ```

<h3>Pull Request </h3>
 ```console
 $ git push origin sarah # push the latest changes to GitHub
 ```
In order to merge Sarah into Master, we'll have to open a `pull request` and create a pull request on GitHub.
Other teams members can see the changes and comment on them. If everything has been approved, you can merge
your chanages into master by clicking `Merge pull request`.


<h3>Fetching and Pulling </h3>
Since we updated the master branch, our local repository don't automatically have the changes. We have to `fetch` the changes into our local
repository.
 ```console
 $ # update the origin master branch in our local repository
 $ git fetch origin master
 ```
Now that we have fetched the origin master, we can update our local master branch to point to the latest changes made on origin master.
 ```console
 $ # update our local master branch to point to the changes made on origin master by merging
 $ git merge origin/master
 ```
Instead of indivdually fetching and then merging, we can `pull` the origin master branch
 ```console
 $ # two commands in one. (git fetch and git merge)
 $ git pull origin master # two commands in one git fetch and git merge
```

<h3>GIT - Merge Conflicts </h3>
Let say there is a fourth story that Sarah and Max are making. Sarah has updated and merge the fourth story to master first and Max does his next. 
But the master branch contains changes compared to the Max branch in a file that we're currently trying to merge. In the master branch, it says "This is Sarah's version"
while in Max's branch it will say "This is Max's version". Git doesn't know which version you want to keep. This is a `merge conflict`.

During a conflict, Git adds some extra characters to the file that's conflicting.
 ```console
 $ ##  Fourth Story
   <<<<<< HEAD
   This is Sarah's version  # current conext of the conflixting files
   ========
   This is Max's version
   >>>>>> max               # contents that we're trying to merge
   of the fourth story!

   Some extra stuff Sarah 
   added
 ```
 We can remove the lines we don't want to keep and then save the file again.
  ```console
  $ ## Fourth Story

  This is Max's version 
  of the fourth story!

  Some exta stuff Sarah 
  added
  ```
 During the conflict, we made some changes to the fourth story.txt file,, which we'll have to add to Git again.
  ```console
  $ git add fourth_story.txt
  $ git merge
  ```

<h3>Fork </h3>
How do you create a pull request if you're not part of the Git project and therefore not allowed to create brances or push your changes right in? 
One way to contribute to the project is to first `fork` the main project. After `forking` the project, you can add your changes to a branch on the 
forked copy. And then send a pull request to the orignal project to merge your changes right in. When you `fork` a Git repository, you're creating your 
own copy of the original project. 
