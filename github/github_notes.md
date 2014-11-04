#GitHub Notes
=============

Git allows groups of people to work on the same documents (often code) at the same time, and without stepping on each other's toes. It's a distributed version control system.

**Directory:**
A folder used for storing multiple files.

**Repository:**
A directory where Git has been initialized to start version controlling your files.


1.2 Checking the Status
-----------------------
Good job! As Git just told us, our "octobox" directory now has an empty repository in /.git/. The repository is a hidden directory where Git operates.

**The .git directory**
On the left you'll notice a .git directory. It's usually hidden but we're showing it to you for convenience.
If you click it you'll notice it has all sorts of directories and files inside it. You'll rarely ever need to do anything inside here but it's the guts of Git, where all the magic happens.


**add all:**
You can also type ```git add -A .``` where the dot stands for the current directory, so everything in and beneath it is added. The ```-A``` ensures even file deletions are included.
**git reset:**
You can use ```git reset <filename>``` to remove a file or files from the staging area.


**Staging Area:**
A place where we can group files together before we "commit" them to Git.

**Commit**
A "commit" is a snapshot of our repository. This way if we ever need to look back at the changes we've made (or if someone else does), we will see a nice timeline of all changes.


1.6 Committing
--------------
Notice how Git says changes to be committed? The files listed here are in the Staging Area, and they are not in our repository yet. We could add or remove files from the stage before we store them in the repository.

To store our staged changes we run the commit command with a message describing what we've changed. 


1.7 Adding All Changes
-----------------------
Great! You also can use wildcards if you want to add many files of the same type.

```git add '*.txt'```

**Wildcards:**
We need quotes so that Git will receive the wildcard before our shell can interfere with it. Without quotes our shell will only execute the wildcard search within the current directory. Git will receive the list of files the shell found instead of the wildcard and it will not be able to add the files inside of the octofamily directory.

**Check all the things!**
When using wildcards you want to be extra careful when doing commits. Make sure to check what files and folders are staged by using git status before you do the actual commit. This way you can be sure you're committing only the things you want.


1.9 History
-----------
So we've made a few commits. Now let's browse them to see what we changed.

Fortunately for us, there's git log. Think of Git's log as a journal that remembers all the changes we've committed so far, in the order we committed them.

**More useful logs:**
Use ```git log --summary``` to see more information for each commit. You can see where new files were added for the first time or where files were deleted. It's a good overview of what's going on in the project.


1.10 Remote Repositories
------------------------
We've gone ahead and created a new empty GitHub repository for you to use with Try Git at https://github.com/try-git/try_git.git. To push our local repo to the GitHub server we'll need to add a remote repository.

This command takes a remote name and a repository URL, which in your case is https://github.com/try-git/try_git.git.

**git remote:**
Git doesn't care what you name your remotes, but it's typical to name your main one origin.
It's also a good idea for your main repository to be on a remote server like GitHub in case your machine is lost at sea during a transatlantic boat cruise or crushed by three monkey statues during an earthquake.


1.11 Pushing Remotely
---------------------
The push command tells Git where to put our commits when we're ready, and boy we're ready. So let's push our local changes to our origin repo (on GitHub).

The name of our remote is origin and the default local branch name is master. The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do.

**Cool Stuff:**
When you start to get the hang of git you can do some really cool things with hooks when you push.
For example, you can upload directly to a webserver whenever you push to your master remote instead of having to upload your site with an ftp client. Check out Customizing Git - Git Hooks for more information.


1.12 Pulling Remotely
---------------------
Let's pretend some time has passed. We've invited other people to our github project who have pulled your changes, made their own commits, and pushed them.

We can check for changes on our GitHub repository and pull down any new changes by running:

```git pull origin master```

**git stash:**
Sometimes when you go to pull you may have changes you don't want to commit just yet. One option you have, other than commiting, is to stash the changes.
Use the command 'git stash' to stash your changes, and 'git stash apply' to re-apply your changes after your pull.


1.13 Differences
----------------
Uh oh, looks like there have been some additions and changes to the octocat family. Let's take a look at what is different from our last commit by using the git diff command.

In this case we want the diff of our most recent commit, which we can refer to using the HEAD pointer.

```git diff HEAD```

**HEAD**
The HEAD is a pointer that holds your position within all your different commits. By default HEAD points to your most recent commit, so it can be used as a quick way to reference that commit without having to look up the SHA.


1.14 Staged Differences
-----------------------
Another great use for diff is looking at changes within files that have already been staged. Remember, staged files are files we have told git that are ready to be committed.

**Commit Etiquette:**
You want to try to keep related changes together in separate commits. Using 'git diff' gives you a good overview of changes you have made and lets you add files or directories one at a time and commit them separately.

Now go ahead and run git diff with the --staged option to see the changes you just staged. You should see that octodog.txt was created.

```git diff --staged```


1.16 Resetting the Stage
------------------------
You can unstage files by using the git reset command. Go ahead and remove octofamily/octodog.txt.

```git reset octofamily/octodog.txt```


1.17 Undo
----------
git reset did a great job of unstaging octodog.txt, but you'll notice that he's still there. He's just not staged anymore. It would be great if we could go back to how things were before octodog came around and ruined the party.

Files can be changed back to how they were at the last commit by using the command: ```git checkout -- <target>```

**The '--'**
So you may be wondering, why do I have to use this ```'--'``` thing? ```git checkout``` seems to work fine without it. It's simply promising the command line that there are no more options after the ```'--'```. This way if you happen to have a branch named ```octocat.txt```, it will still revert the file, instead of switching to the branch of the same name.


1.18 Branching Out
------------------
When developers are working on a feature or bug they'll often create a copy (aka. branch) of their code they can make separate commits to. Then when they're done they can merge this branch back into their main master branch.

We want to remove all these pesky octocats, so let's create a branch called clean_up, where we'll do all the work:

```git branch clean_up````

**Branching**
Branches are what naturally happens when you want to work on multiple features at the same time. You wouldn't want to end up with a master branch which has Feature A half done and Feature B half done.

Rather you'd separate the code base into two "snapshots" (branches) and work on and commit to them separately. As soon as one was ready, you might merge this branch back into the master branch and push it to the remote server.


1.19 Switching Branches
-----------------------
Great! Now if you type ```git branch``` you'll see two local branches: a main branch named **master** and your new branch named **clean_up**.

You can switch branches using the ```git checkout <branch>``` command. Try it now to switch to the clean_up branch:

```git checkout clean_up```

**All at Once**
You can use:
```git checkout -b new_branch```
to checkout and create a branch at the same time. This is the same thing as doing:

```git branch new_branch```
```git checkout new_branch```


1.20 Removing All The Things
----------------------------
Ok, so you're in the **clean_up** branch. You can finally remove all those pesky octocats by using the ```git rm``` command which will not only remove the actual files from disk, but will also stage the removal of the files for us.

You're going to want to use a wildcard again to get all the octocats in one sweep, go ahead and run:

```git rm '*.txt'```

**Remove all the things!**
Removing one file is great and all, but what if you want to remove an entire folder? You can use the recursive option on git rm:

```git rm -r folder_of_cats```

This will recursively remove all folders and files from the given directory.


1.21 Commiting Branch Changes
-----------------------------
Now that you've removed all the cats you'll need to commit your changes.

Feel free to run ```git status``` to check the changes you're about to commit.

```git commit -m "Remove all the cats"```

**The '-a' option**
If you happen to delete a file without using ```'git rm'``` you'll find that you still have to ```'git rm'``` the deleted files from the working tree. You can save this step by using the ```'-a'``` option on ```'git commit'```, which auto removes deleted files with the commit.

```git commit -am "Delete stuff"```


1.22 Switching Back to master
-----------------------------
Great, you're almost finished. You just need to switch back to the **master** branch so you can copy (or **merge**) your changes from the **clean_up** branch back into the **master** branch.

Go ahead and checkout the master branch:

```git checkout master```

**Pull Requests**
If you're hosting your repo on GitHub, you can do something called a pull request.

A pull request allows the boss of the project to look through your changes and make comments before deciding to merge in the change. It's a really great feature that is used all the time for remote workers and open-source projects.


1.23 Preparing to Merge
-----------------------
Alrighty, the moment has come when you have to merge your changes from the **clean_up** branch into the **master** branch. 

We're already on the **master** branch, so we just need to tell Git to merge the **clean_up** branch into it:

```git merge clean_up```

**Merge Conflicts**
Merge Conflicts can occur when changes are made to a file at the same time. A lot of people get really scared when a conflict happens, but fear not! They aren't that scary, you just need to decide which code to keep.


1.24 Keeping Things Clean
-------------------------
Congratulations! You just accomplished your first successful bugfix and merge. All that's left to do is clean up after yourself. Since you're done with the **clean_up** branch you don't need it anymore.

You can use ```git branch -d <branch name>``` to delete a branch. Go ahead and delete the clean_up branch now:

```git branch -d clean_up```

**Force delete**
What if you have been working on a feature branch and you decide you really don't want this feature anymore? You might decide to delete the branch since you're scrapping the idea. You'll notice that ```git branch -d bad_feature``` doesn't work. This is because ```-d``` won't let you delete something that hasn't been merged.

You can either add the ```--force (-f)``` option or use ```-D``` which combines ```-d -f``` together into one command.

**Learning more about Git**
We only scratched the surface of Git in this course. There is so much more you can do with it. Check out the **Git documentation** for a full list of functions.

**The Pro Git book**, by Scott Chacon, is an excellent resource to teach you the inner workings of Git.

**help.github** and GitHub Training are also great for anything related to Git in general and using Git with GitHub.


GIT REAL LEVEL 1
================

Level 1 - GIT BASICS
--------------------
###Commands
Access documentation on github commands:

```$ git help```

Narrow ```git help``` search results:

```$ git help config```

To set up who gets credit for changes:

```$ git config --global user.name "Bobby Joe Smith III"```

What email you use:

```$ git config --global user.email "me@email.com"```

Command line colors:

```$ git config --global color.ui true```

**You can add multiple files to the staging area using a few different methods.**

List all of the files you want to add to the staging area with:

```$ git add file1.txt file2.txt```

Check for and add all new or modified files with: 

```$ git add --all```

You can use a wildcard to add all of the files of a certain type (.txt files in example) using:

```$ git add *.txt```

Add all files of a certain type (ex. .txt) in a specific directory (ex. docs):

```$ git add docs/*.txt```

Add all files in a specific directory (ex. docs):

```$ git add docs/```

Add all files of a specific type (ex. txt) in the entire project:

```git add "*.txt"```

Review the git timeline history:

```$ git log```



###Concepts
#####Background
Github is a "Distributed Version Control System" (DVCS) created to help teams merge changes to a project, as well as create a timeline of changes to said project. Previously, teams used to transfer computer files using a File Transfer Protocol (FTP) to a central repository. This would cause programmers working on the same files to accidentally overwrite each others' code. Also, since all of the code was stored on a central repository, coders ran the risk of losing all of their work if the repository crashed or was deleted. In a DVSC setup, everyone gets a copy of the master repository on their own server, reducing the risk of losing everything in the repository if something were to happen to one of the repositories.

#####Git Help
You can access documentation on github commands right in the command line by typing:
```$ git help```

You can pass in any git command with ```git help``` and narrow the search results. For example, if you want a quick view of the configuration commands type:
```$ git help config``` 

#####Setting Up Git
To set up who gets credit for changes:
```$ git config --global user.name "Bobby Joe Smith III"```

What email you use:
```$ git config --global user.email "me@email.com"```

Command line colors:
```$ git config --global color.ui true```

#####Starting A Repository
1. Navigate to the directory where you want to store your empty git repository
2. Initialize the git repository by typing ```git init``` into the command line. A hidden .git directory containing git metadata will be stored in the directory in which you initialized git.

#####Git Work Flow
1. Create or modify files
2. Add new or modified files to the staging area. This will tell the repository to start tracking any files that weren't previously being tracked for changes. Adding files to the staging area are also a way to group together changes made to the repository that you want logged on the project timeline together. 
3. Commit changes. This creates a snapshot of the current state of all of the changes to the files added on the stage. These snapshots will be logged on the project timeline. Always write your commit message in the past tense so people can understand what merging that commit will do to their code.

#####Additional Commands
You can add multiple files to the staging area using a few different methods.

List all of the files you want to add to the staging area with:
```$ git add file1.txt file2.txt```

Check for and add all new or modified files with: 
```$ git add --all```

You can use a wildcard to add all of the files of a certain type (.txt files in example) using:
```$ git add *.txt```

Add all files of a certain type (ex. .txt) in a specific directory (ex. docs):
```$ git add docs/*.txt```

Add all files in a specific directory (ex. docs):
```$ git add docs/```

Add all files of a specific type (ex. txt) in the entire project:
```git add "*.txt"```

Review the git timeline history:
```$ git log```


Level 2 - Staging and Remotes
-----------------------------
###Commands
#####Staging
Show unstaged differences since last commit:

```$ git diff ```

Show staged differences since last commit:

```$ git diff --staged```

Unstage a file:

```$ git reset HEAD <filename>```

```HEAD``` refers to the last command on the timeline we are on.

Reset an unstaged file that has been modified to the last state it was in before it was modified:

```$ git checkout -- <filename>```

Add AND commit any modified tracked files:

```$ git commit -a -m "commit message"```

This will not add any files that are not already being tracked.

Undo last commit and move everything from the last commit back into staging:

```$ git reset --soft HEAD^```

Add files to last commit:

```$ git add <file>``` add the file you want to add to the last commmit and,
```$ git commit --amend -m "Modify readme and add file.txt."```

If we specify a new commit message it will overwrite our previous commit message.

Completely undo last commit and all changes:

```$ git reset --hard HEAD^```

Undo last two commits and all changes:

```$ git reset --hard HEAD^^```

keep adding a ```^``` for each commit you want to blow away.

#####Remote Repositories
Link our local repository to a remote repository:

```$ git remote add origin <repo url>```

Get a list of all of the remote repositories our local repository has access to:

```$ git remote -v```

Push files from local repository to remote repository and have the computer remember the path:

```$ git push -u <remote name> <branch>```

To remove remotes:
```$ got remote rm <name>```


###Concepts
When we are editing our files, staging, and committing them, we are making the changes on our own local repository. To get these changes up to a repository that anyone else can access, we need to push and pull changes to a remote repository. When dealing with remote repositories, it is all about the ```git remote``` command.

Git doesn't take care of access control for you, meaning, it doesn't allow you to specify who has access to the remote repository. In order to implement access control, some additional software is needed. If you want to use a hosted access control software, you can use Github or Bitbucket. If you want a self managed solution, you can use Gitosis or Gitorious. 

If we wanted to store our remote repository on github, we would create a github account, and then create a new repository on github. Once we create a repository on github, github will give us a url that refers to that repository.

To push to github, we are first going to have to run ```git remote add origin <repository url>```. ```add``` creates a new remote repository, ```origin``` is the name of the remote, and the url is the address of the remote repository. We can give the remote any name, but usually we refer to our "canonical repository" as "origin". Then, we are going to push the files from the local repository to the remote with ```$ git push -u origin master```. ```-u``` tells the computer to remember push settings so next time you don't have to specify the name and the branch. ```origin``` is the name of the remote repository. ```master``` is the local branch to push. Github will ask for your username and password. If you want to cache your username and password so that you don't haave to enter it everytime you push, got to https://help.github.com/articles/set-up-git .

To pull changes down from a remote repository and sync up your local repository, use ```$ git pull```. You will want to use this when changes have been made to the remote repository and you want your local repository to be up to date.

We have github as our canonical remote called "origin", but it is not uncommon to have multiple remotes with a project. We might have a test server that runs our tests for us that we will occassionally push our repo over there. Or we might have a hosting provider that has our production code in it. To add new remotes follow the steps above and use the name that corrisponds to appropriate remote server.

```$ git remote add <name> <address>```

An example of removing remote repositories would be:

```$ git remote rm origin```

An example of pushing to a remote would be:

```$ git push -u origin master```

Don't use any of the commands the roll back commits after you have pushed. You only want to do those before you've pushed, because if do so and then make the changes locally it's kind of like changing history, which is dangerous to do when working on a project.


Level 3 - Cloning and Branching
--------------------------------
###Commands

Clone a remote repository:

```$ git clone <url of remote repository>```

Cone a remote repository and rename the local file it will be cloned into:

```$ git clone <url of remote repository> <folder name>```

Create new branch:

```$ git branch <name of branch>```

Check which branch you are currently on:

```$ git branch```

Switch HEAD to new branch:

```$ git checkout <name of branch>```

Create a text file and write something in it:

```$ echo "<message>" > <name of file>.txt```

Merge branch:

```$ git merge <name of branch>```

Delete branch:

```$ git branch -d <name of branch>```

Create new feature branch and switch HEAD to that branch:

```$ git checkout -b <branch name>```

#####Vi Commands

```j``` down

```k``` up

```h``` left

```l``` right

```ESC``` leave mode

```i``` insert mode

```:wq``` save and quit

```:q!``` cancel and quit


###Concepts
To start collaborating, generally we will need to bring a copy of a remote repository onto our local server. To do this, we will clone the remote repository and download the entire repository into a local directory/repository.

When we need to work on a feature that will take some time, it's best to create a branch off of the master branch. Any changes, adds, and commits that occur on the new branch will not effect or show up on the master branch until we merge both branches. If changes were only made to the new branch and not the master branch, it is possible to do a "fast-forward" merge. However, when changes occur to the master branch and the new branch, git can't fast forward since changes were made in both branches. Instead, git will have to perform a recursive merge to merge both branches.


Level 4 - Collaboration Basics

###Concepts
#####Situation 1:
You want to push a commit to a remote repository but someone has made changes to the same remote repository you are working on, causing your local repository to no longer be up-to-date.

#####Solution: 
```git pull``` the changes from the remote repository, then ```git push``` your changes.

When you pull from a remote repository to "Fetch" (or Sync) our local repository with the remote one, Fetch doesn't actually update any of our local code. Instead a branch called "origin/master" get's created off of the local master branch, and git merges origin/master with the remote master. After ```git pull``` fetches the remote repo and syncs it with the origin/master branch, ```git pull``` then does a recurssive merge of the origin/master branch with the local master branch. Since git is trying to do a merge with branches that have two difference commits, it will pop us straight into an editor (Vi) where we will have to create a merge commit. Once we save from the editor, we are going to get an output from the pull command that tells us that it did a recursive merge.

At this point, the origin/master branch doesn't know about the local change we made to master, or the merge commit that was just performed. Origin/master will not know about it until we do a ```git push```. At that point, origin/master points to the same master (the remote master on github) branch and everything's been updated.

Some people don't like using merge commits in this way because it pollutes the repo history, and would prefer to do "rebase".


#####Situation 2:
You want to push a commit to a remote repository but someone has pushed changes to the same file you are working on to the remote repository.

#####Solution:
```git pull``` the changes. Type in ```git status``` to see which files have both been modified. Go into file and you will see notation from github that looks like:

```<<<<<<<<<<<<<< HEAD
the cake is a lie.
===================
the cake is telling the truth!
>>>>>>>>>>>>>>>>
7e45847f8939dkkf9929388'''

The portion above the line are your changes. The portion below the line are the other person's changes that were pushed to the remote repository. Choose which changes you want to go with and clean up the git notation. Then just commit the changes with ```$ git commit -a``` no need to leave a commit message since git will already provide pretty good commentary on what transpired. Then push to the remote repository.







