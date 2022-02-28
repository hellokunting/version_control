### Git Intro

- **What's Git?**

  - Git is a version control system
  - Version control is a software that tracks and manages changes to files over time
  - Git can be used in command line or GUI (such as Gitkraken)

- **Configure Git Name & Email**

  ```
  // config globally
  git config --global user.name "Your Name"
  git config --global user.email "Your Email"
  git config user.name // check if you have already had an user name
  git config user.email // check if you have already had an email


  // config locally
  git config credential.username "your_username"
  git config user.email "your_email"
  ```

- **Terminal command line cheat-sheet**
- Navigation

  ```
  ls // list all the files in current directory
  cd file // direct to the file
  open . // open the folder of current directory
  ls app // list all the files within the app
  open  app// open the folder app
  ls Parent/Child // list all files in Child fold whose in the Parent folder
  pwd // print the current path
  cd .. directory back to previous level folder - the parent folder
  ```

- Creating Files & Folders

  ```
  touch newFile.js // create a new file called newFile.js
  mkdir KUKU // create a new folder called KUKU
  ```

- Deleting Files & Folders

  ```
  rm files // permanently delete files
  ls -a // shows all files include hidden Files
  rm -rf Folder // permanently delete folder
  ```

---

### Git Adding & Committing

- Repository:

  - A Git "Repo" is a workspace which tracks and manages files within a folder
  - Anytime we want to use Git with a project, app, etc, we need to create a new git repo.

- To initialize a Repo - **git init**
- For the best practice, only initiate repo for the project folder rather than the whole desktop or system
- **rm -rf .git** // remove the repository
- Adding: uses git add to **add specific files to the staging area**. Separate files with spaces ti add multiple at once.

  - **git add file1 file2**
  - **git add .**

- Git Commit:

  - **commit changes from the staging area**
  - When making a commit, we need to provide a commit message that summarizes the changes and work snapshots in the commit
  - **git commit -m ""message"**
    - the -m flag allows us to pass in an inline commit message, rather than launching a text editor
  - **git log**: a log of your commits
  - **git log --oneline**: a log of your commits with a good one-line style
  - **git commit --amend**: redo to update the previous commit
    - first use git add file you forget
    - then git commit --amend

- **.gitignore file**
  - add files you want git ignored such as **.DS_Store**

---

### Branching

- Think of branches as alternative timelines for a project
- They enable us to create separate contexts where we can try new things or even work on multiple ideas in parallel
- If we make changes on one branch, they do not impact the other branches
- The **Master Branch**: the default branch name
  - it doesn't do anything special or have fancy powers. It's just like any other branch.
- **Feature branching**: a common workflow that creates an experimental branch for new feature and if you like this feature you merge it back with the master

- **(HEAD -> master)**
  - HEAD is simply a pointer that refers to the current "location" in your repo. It points to a particular branch reference.
- **git branch** - show the current branch name
- Creating branches
  - use **git branch BRANCH-NAME** to make a new branch based upon the current HEAD
  - this just creates the branch not switch to the branch you created
- Switching a branch
  - **git switch branchName**
  - **git checkout branchName** - old-school
  - **git switch -c branchName**/ **git checkout -b branchName** - create a branch and switch to that branch
  - **git branch -D branchName** - delete the branch
    - remember: we cannot delete a branch when we are on that branch so we have to switch to other branch
  - **git branch -m newBranchName** - switch the branch you want to rename and use the command

---

### Merging

- git merge helps us incorporate changes from one branch into another
- we merge **branches** not specific commits
- We always merge to the current **HEAD** branch
- To fast-forward merge, there are 2 steps:

1. Switch to or checkout the branch you want to merge the changes into (the receiving branch)
2. Use the git merge command to merge changes from a specific branch into the current branch.

- **git switch master**
- **git merge bugfix**

- Rather than performing a simple fast forward, git performs a "merge commit". We end up with a new commit on the master branch.
- Git will prompt you for a message.

- **Merge Conflicts**

  - Depending on the specific changes you are trying to merge, Git may not be able to automatically merge. This results in merge conflict, which you need to manually resolve.
  - When you open the file:
    - the content from your current HEAD is displayed between the <<<<<<< HEAD and =======
    - The content form the branch you are trying to merge from is displayed between ====== and >>>>>>> symbols

- **Resolve Conflicts**
  - Step 1: Open up the files with merge conflicts
  - Step 2: Edit the files to remove the conflicts. Decide which branch's content you wanna keep in each conflict. Or keep the content from both.
  - Step 3: Remove the conflict markers in the document in VSCode
  - Step 4: Add your changes and then make a commit

---

### Git Diff

- use **git diff** to view changes between commits, branches, files, our working directory, and more
- use git diff with git status and git log to get a better picture of a repo and how it has changed over time
- **git diff**: lists all the changes in our working directory that are not Staged for the next commit(any changes before you made git add).
- Reading the result of git diff:
  - **diff --git a/file b/file**: Compared Files
    - For each comparison, git explains which files it is comparing.
    - this is usually just two versions of the same file with changes..
    - Git also declares one file as "a" and the other as "b"
  - then we can skip something like "index 2505c34..1ed8bcc 100644" - it's just hash
  - then we can see two lines of Markers:
    - **--- a/file**: file a has a minus sign
    - **+++ b/file** file b has a plus sign
  - then we will see the chunks: a portions that were modified
    - a chunk also includes some unchanged lines before and after a change to provide some context
    - a chunk header is something like: **@@ -3,4 +3,5 @@**
      - each chunk starts with a chunk header, found between @@
      - the example shows above means:
        - From file a, 4 lines are extracted starting from line 3
        - From file b, 5 lines are extracted starting from line 3
    - every line that changed between the two files is marked with either + or -
      - lines that begin with - come from file a
      - lines that begin with + come from file b
- **git diff --staged/--cached**: list the changes between the staging area and out last commit
  - shows what will be included in my commit if I run git commit rn.
  - shows differences after git add are made (when it is in the staging)
- **git diff HEAD**: lists all changes in the working tree since your last commit including things that are staged (thing after you do git add)
- view the changes within a specific file by providing git diff with a file name
- **git diff HEAD [filename]**
- **git diff --staged [filename]**
- **git diff branch1..branch2**: list the changes between the tips of branch1 and branch2
- **git diff commit1..commit2**: to compare two commits, provide git diff with the **commit hashes** of the commits in question

---

### Stashing

- Sometimes we are working on something but you are not done yet and do not want to make a commit. However, you have to go to other branches.

  - git will make your current changes come with you to the destination branch if there is no conflict
    - if you switch over to previous branch and add it commit; the change you brought to destination branch will disappear
  - or git won't let you switch if it detects potential conflicts

- What should I do? - use **git stash**
  - Git provides an easy way of stashing these uncommitted changes so that we can return to them later, without having to make unnecessary commits.
  - git stash helps you save changes that you are not yet committed. You can stash changes and then come back to them later.
  - Running git stash will take all uncommitted changes (staged and upstaged) and stash them, reverting the changes in your working copy.
- **git stash pop**: remove the most recently stashed changes in your stash and re-apply them to your working copy
- **git stash apply**: apply whatever is stashed away, without removing it from the stash. This can be useful if you want to apply stashed changes to multiple branches.
  - conflicts may occur
- multiple stashes are allowed: you can add multiple stashes onto stack of stashes. They will all be stashed in the order you added them.
  - you can view all the stashes you currently create using **git stash list**
  - **git stash apply stash@{list number}**
- **git stash drop stash@{list number}**: delete a particular stash
- **git stash clear**: delete all stashes

---

### Undoing Changes & Time Traveling

- **git checkout <commit hash>**: jump back a previous commit
  - **Detached HEAD**:
    - Usually, HEAD points to a specific branch reference rather than a particular commit.
    - When we checkout a particular commit, HEAD points at that commit rather than at the branch pointer.
    - Options:
      1. Stay in detached HEAD to examine the contents of the previous commit.
      2. LEAVE and go back to wherever you were before - reattached the header. - git switch
      3. Create a new branch and switch to it. You can now make and save changes, since HEAD is no longer detached.
- **git checkout HEAD~1**: refers to the commit before HEAD
- **git checkout HEAD~2**: refers to 2 commits before HEAD

- **git checkout --/HEAD <filename>**: revert a file back to whatever it looked like when you last committed
- **git restore --staged <filename>**: if you git add files that you don't want, you can use this command to remove it from staging.
- **git restore <filename>**: just like checkout to redo or discard the changes
- **git restore --source HEAD~1 home.html**: restore the contents of home-html to its state from the commit prior to HEAD.
  - HAED~1 can change to commit hash
- **git reset commit-hash**: reset the repo back to a specific commit. The commits are gone but the content still keeps. Useful if we make a commit at the wrong branch. You just switch to the correct branch and make a new commit
- **git reset --hard commit-hash**: undo the commits AND discard changes in the file.
- **git revert**: similar to git reset that they both undo changes. git revert creates a new commit that undoes the changes from a commit.
- **When to use git reset and git revert?**
  - git reset and git revert have a significant difference when it comes to collaboration.
  - If you want to revert some commits that other people already have on their machines, you should use revert.
  - If you want to reverse commits that you haven't shared with others, use reset and no one will ever know.

---

### GitHub

- **git clone URL**: get a local copy of a remote repo hosted on Github or similar repo host websites.
  - We need a URL that we can tell git to clone for use.
  - the repo you cloned to your local machine will all the files and commits.
- **Configuring SSH Keys**:
  - We need to be authenticated on GitHub to do certain operations, like pushing up code from local machine.
  - Your terminal will prompt you every single time for your GitHub email and password
  - However, if you generate and configure an SSH key, you can connect to GitHub without having to supply your username and password every time.
  - Step 1: check if you've already had a SSH keys by entering command:
    ```
    ls -al ~/.ssh
    ```
  - Step 2: if not, generate a new SSH key by following the instruction on
    - [Generate SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
  - Step3: Make sure your config the correct git username and email that are matched to the one you are working on in GitHub.
- **git remote**:

  - Before we can push anything up to GitHub we need to tell git about our remote repository on Github.
  - We need to set up a destination to push up to.
  - In git, we refer to these "destinations" as remotes. Each remote is simply a URL where a hosted repo lives.
  - We use **git remote** to check if there is any remote already exists
  - We use **git remote -v** lists urls for remote repo
  - **git remote add name url**: a remote has 2 things: a name and a url. To add a new remote, we need to provide both to git
    - the remote name is usually called origin but you can change it to other names
    - the URL is the repo url on the GitHub repo
  - **git push origin master/other branch names**: push up the master branch to origin remote
  - While we often want to push a local branch up to a remote branch of the same name, we don't have to. To push our local pancake branch up to a remote waffle branch we can just do:
    ```
    git push origin pancake:waffler
    ```

- How to add collaborators in GitHub?

  - Settings -> Manage access -> Invite a collaborator -> collaborator's GitHub username

- Some Features of GitHub:

  - README includes:

    - What the project does
    - How to run the project
    - What noteworthy
    - Who maintains the project

  - GitHub Gists:
    - a simple way to share code snippets and useful fragments with others. Gists are much easier to create but offer far fewer features than a typical GitHub repo.
    - Your profile icon -> your gists
  - gh pages:
    - GitHub Pages are public webpages that are hosted and published via GitHub.
    - They allow you to create a website simply by pushing your code to GitHub.

---

### Fetching & Pulling

- **Remote tracking Branches**:

  - It follows the pattern **remote name/branch name**
  - origin/master: this is called remote tracking branch. It's a reference to the state of the master branch on the remote. I can't move this myself. It's pointing to the last commit on the master branch on origin remote.
  - upstream/logoRedesign: references the state of the logoRedesign branch on the remote named upstream.
  - **git branch -r**: view all the remote branches our local repo knows about

  - **Your branch is ahead of 'origin/main' by 1 commit**: means you made1 commit after you clone the origin repo on your local machine.
  - **git checkout origin/master**: switch branch to the origin/master.
  - Every time you clone a repo, by default, your current local branch master is already tracking origin/master. If you want to connect to other remote branches, you can just use **git switch remote-branch-name** to create a new local branch from the remote branch of the **same** name.

- **Fetching**:

  - allows us to download changes from a remote repo, BUT those changes will not
    automatically integrated into our working files.
  - It lets you see what others have been working on, without having to merge those changes into your local repo.
  - Think of it as "please fo and get the latest information from GitHub, but don't screw up my working directory".
  - It updates the origin/master, not the local master branch, so your current working directory does not change.
  - **git fetch origin/remote-name**: fetches branches and history from a specific remote repo. It only updates remote tracking branches.
  - **git fetch remote-name branch-name**: fetches a specific branch from a remote.

- **Pulling**:
  - Unlike fetching, pulling will update our working directory or our current HEAD branch with whatever changes are retrieved from the remote.
  - **git pull origin master**: fetch the latest information from the origin's master branch and merge those changes into our current local branch.
  - Running **git pull** without specifying a particular remote or branch to pull from, git assumes the following:
    - remote will default to origin
    - branch will default to whatever tracking connection is configured for your current branch (the same name matched to the remote repo branch name).
- fetch & pull conflicts sometimes happen and need to be fixed.

---

### Git Collaboration Workflows

- **Centralized Workflow**:

  - AKA 'Everyone Works On Master/Main'
  - AKA 'The Most Basic Workflow Possible'
  - shortcomings: - lost of time spent resolving merging conflicts - no one can work on anything without distributing the main codebase.

- **Feature Branches Workflow**
  - Rather than working directly on master/main, all new development should be done on separate branches.
  - Treat master/main branch as the official project history
  - Allows multiple teammates to collaborate on a single feature and share code back and forth without polluting the master/main
  - **Merging in Feature Branches**:
    - At some points, some feature branches need to be merged to the master branch
      - You can send an email or char message to your team to discuss if the changes should be merged in.
      - Or you can use **Pull Requests**

<!-- ### Rebasing

- Why we are using rebase command?
  - as an alternative to merging to help combine changes from two branches
  - as a cleanup tool -->

<!--

### Interactive Rebase - History Cleanup



### Git Tags



### Hashing & Objects




### Reflogs



### Custom Git Aliases -->
