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
