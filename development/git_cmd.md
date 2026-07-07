# Most important💡 Git commands

## Basic Git commands
```bash
git log			# show the history of the commits (example: `git log -2` shows only the last two)
git push		# push files to GitHub (example: `git push -u origin master`)
git pull		# pull files from GitHub (example: `git pull origin master`)
git remote		# `git remote -v` (shows the remote url)
git status		# show the status of the git repo (if it exists)
git commit		# commit files to the staging area (example: `git commit -a` adds all files to the
				# staging area, `git commit -a -m` adds them with a message)
git add			# add specific files to the staging area (example: `git add .` adds all files)
git remote		# add the remote place. This is needed if we have not created the git repo online,
				# but worked localy with `git init` (example: `git remote add origin <url of git repo>`)
```

## First steps
**1️⃣ Install Git** 
```bash
apt-get install git
```

**2️⃣ Set up user data**
```bash
git config --global user.name "Username of github or bitbucket"
git config --global user.email "Email of github or bitbucket"
git config --list
# Note: The above data is contained in .gitconfig which is located in the home directory. Those, can be displayed in the terminal:
```

**3️⃣ Clone the remote git repo**
Example: git clone https://user@github.com/repo_name/repodata.git
**NOTE:** If a project exists initialize the folder
```bash
git init
```

**4️⃣ Show the status of the repository**
```bash
git status  
# This should output:
# On branch master
# Your branch is up to date with 'origin/master'.
# <and a list of files to commit>
```

**5️⃣ Add files to the local repository**
```bash
git add <file> <file> ... or git add . 
```

**6️⃣ Commit the local files to the remote repository** 
```bash
git commit -m "<commit message>"
```

```bash
# **Note:** The local files are still not on the remote repo. To achieve this push the files first:
git push -u origin master
```

## Git operations

**1️⃣ Pull a specific commit from the repo**
```bash
git log 
git log-remote <path to url> # list the last commit
git fetch origin <SHA-1> # copy the desired hash SHA-1 string from the list
git checkout FETCH_HEAD
```

**2️⃣ Pull a specific commit from a local remote branch**
```bash
git clone <remote url> -b <branch name>
cd <repo name>
git checkout <COMMIT HASH e.g. f7255cf2cc6b5116e50840816d70d21e7cc039bb>
**Note:** avoid using reset
```

**3️⃣ Drops a commit**
```bash
git stash save --keep-index
git stash drop # if the files are not needed anymore
git stash pop OR by index git stash apply --index # get the stashed files
```

**4️⃣ Another way to stash (IMPORTANT: Carry over from branch to branch)**
```bash
git stash save "message"
git stash list 	# list all stashed contents
git stash pop 	# pop the first position (stack)
git stash drop stash@{1} # drop the stash of the index 1
git stash clear # remove all stashes (BE CAREFUL)
```

**5️⃣ Untrack added files to .gitignore which are still shown**
```bash
# Commit any outstanding code changes
git rm -r --cached .
git add .
git commit -am ".gitignore is now working"
```

**6️⃣ Revert changes to modified file**
```bash
git reset --hard
```

**7️⃣ Remove all untracked files and directories**
```bash
git clean -fd # `-f` is `force`, `-d` is `remove directories`
```

**8️⃣ Push an existing local repo to the remote repo**
```bash
git remote add origin <url-repository.git>
git push -u origin master
# Example:
git remote add origin <url-repository.git>
git push -u origin master
```

**9️⃣ Update a remote url: git remote set-url origin <new remote url>**
```bash
git remote set-url origin <url-repository.git>
```

**1️⃣0️⃣ Get help: git help operation**
```bash
git help ignore
```

**1️⃣1️⃣ Undo added file**
```bash
git reset # or for specific files
git reset <file_name>
```

**1️⃣2️⃣ Fixes a detached head**
```bash
git branch <branch-name> 		# create a branch of <name> by typing: 
git checkout <branch-name>		# switch over to your new branch
git branch -f master <name>		# point the master pointer to the <name> branch pointer (the-f means force)
git checkout master				# switch to the master branch
git branch -d <name>			# now delete the old branch
git push origin master			# push the new changes to the remote repository
```

**1️⃣3️⃣ How to untrack specific files or folders**
```bash
git rm --cached .idea/workspace.xml # untracks a file
# or
git rm --cached .idea/ 				# untracks a folder
```

**1️⃣4️⃣ Switch remotely to another branch**
```bash
git checkout master # master is the new branch
```

**1️⃣5️⃣ Duplicate a remote repository**
```bash
git clone --bare <old-url-repository.git>
cd old-repository.git
git push --mirror <new-url-repository.git>
cd ..
rm -rf <old-url-repository.git>
```

**1️⃣6️⃣ Show information about a remote repository**
```bash
git remote show origin
```

**1️⃣7️⃣ Rename a branch name**
```bash
git branch -m master default # from master to default
```

**1️⃣8️⃣ Delete a branch (not set to default)**
```bash
git push origin --delete master (deletes the remote master branch)
```

**1️⃣9️⃣ Delete a local branch **
```bash
git branch --delete <branchname> or git branch -D <branchname> # if not merged before
```

**2️⃣0️⃣ Clone from a specific branch**
```bash
git clone -b <branch-name> <url-repository.git>
```

**2️⃣1️⃣ Fix the “modified content, untracked content”**
```bash
git rm -rf --cached <untracked-folder> # this tells git to forget about it since it was being tracked formally
git add <untracked-folder> 
```

**2️⃣2️⃣ Add an embedded folder to the staging area and then push it to the repo**
1. Go into the embedded folder where changes have been made
2. Do a normal add/commit
3. Return to the toplevel and add the folder as via git add <folder-name>
4. Do normal git commit and push to the repo
Based on [this](https://stackoverflow.com/questions/24167676/cant-stage-folder-for-commit-with-git-add-or-git-add-u) issue.

**2️⃣3️⃣ Change a branch name locally and remotely**
[video](https://www.youtube.com/watch?v=znaLboom6BA)
```bash
# Switch to the master branch
git branch master/main
git branch -m <old_name> <new_name>
git branch -a 	# show the new local branch name
# Note: Change the remote name also:
git push origin <old_name> <new_name>
# Now do a refresh on the remote site. The new branch name should appear.
```

**2️⃣4️⃣ Clone a specific file or folder**
There are two ways to achieve this, one is by using [svn](https://stackoverflow.com/questions/7106012/download-a-single-folder-or-directory-from-a-github-repo) (easier way) and the other via [git](https://stackoverflow.com/questions/18900774/equivalent-of-svn-checkout-for-git):

**2️⃣5️⃣ Delete the [whole commit history](https://stackoverflow.com/questions/13716658/how-to-delete-all-commit-history-in-github) - tested on GitHub**
**Note💡:**Deleting the .git folder may cause problems in your git repository. If you want to delete all your commit history but keep the code in its current state, it is safer to do it as in the following:

```bash
git checkout --orphan latest_branch
git add -A
git commit -am "commit message"
git branch -D main 		# delete the branch
git branch -m main		# rename the current branch to main or master
git push -f origin main	# force updating the repository:

**Note💡:** This will not keep your old commit history around
```

**2️⃣6️⃣ Copy the content of a branch to another one**
```bash
git checkout -b <branch_to> <branch_from>
```

**2️⃣7️⃣ Fixing GitHub folders that have a [white arrow](https://stackoverflow.com/questions/62056294/github-folders-have-a-white-arrow-on-them) on them**

In order to restore that folder content:

**Submodule**
A git clone --recurse-submodules would restore the content of that submodule in your local repository (as opposed to a nested Git repo, where its URL is not recorded, and the content of the folder would remain empty).

The white arrow would remain on the remote repository, with folder @ version displaying what SHA1 of the submodule repository is referenced by your project.

**Nested Git repository**
Alternatively, you could, if you don't care about the history of that folder, delete locally its .git subfolder (assuming it is not a submodule, meaning it is not referenced in a .gitmodules file in your main repository), add, commit and push.
The white arrow would then disappear, and you would be able to access that folder content on GitHub.

Then you would need to delete the gitlink entry:

```bash
git rm --cache client_folder 	# without a trailing slash, example: not client_folder/ but client_folder
```
Finally, you can add, commit and push that folder content.


**2️⃣8️⃣ Check the file sizes using [Git-Status-Size](https://github.com/jtloong/git-status-size?tab=readme-ov-file) before git add**
```bash
git clone https://github.com/jtloong/git-status-size
cd git-status-size
```
To invoke it anywhere you'll need to export the file into your environment variable PATH. Do do this write in your script file: 
```bash
export PATH="/path/to/your-script/directory:$PATH
sudo chmod +x git-status-size	# Make it into an executable
```

**Note💡:** If you don't know your git PATH you can check with `type git`.

Now it should work! Go to the terminal in any repo, call git status-size, and you should recieve an output like the one in the gif above. If you have any files over Github's 100 mb limit, you will be prompted if you want to add these files to your .gitignore.




