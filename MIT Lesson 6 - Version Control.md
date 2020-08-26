<h2>Lecture 6: Version Control (Git)</h2>
**Source:** https://missing.csail.mit.edu/2020/version-control/ <br>
**Quick Fix Recommendation From Teacher:** https://ohshitgit.com/ <br><br>

excercise todos for this: try git add -p filename or somehting (after 1:10:00)<br>
todo: delete your duplicates. Accept the ones from source. Maybe you can conserve yours as detailed explanations.

* All of the commands here have to start with "git".
* Git uses Directed Acyclic Graph to model history.
* Simply put, Git is a version control system that lets you manage and keep track of your source code history.

Basics

    git help <command>: get help for a git command
    git init: creates a new git repo, with data stored in the .git directory
    git status: tells you what’s going on
    git add <filename>: adds files to staging area
    git commit: creates a new commit
        Write good commit messages!
        Even more reasons to write good commit messages!
    git log: shows a flattened log of history
    git log --all --graph --decorate: visualizes history as a DAG
    git diff <filename>: show changes you made relative to the staging area
    git diff <revision> <filename>: shows differences in a file between snapshots
    git checkout <revision>: updates HEAD and current branch

Branching and merging

    git branch: shows branches
    git branch <name>: creates a branch
    git checkout -b <name>: creates a branch and switches to it
        same as git branch <name>; git checkout <name>
    git merge <revision>: merges into current branch
    git mergetool: use a fancy tool to help resolve merge conflicts
    git rebase: rebase set of patches onto a new base

Remotes

    git remote: list remotes
    git remote add <name> <url>: add a remote
    git push <remote> <local branch>:<remote branch>: send objects to remote, and update remote reference
    git branch --set-upstream-to=<remote>/<remote branch>: set up correspondence between local and remote branch
    git fetch: retrieve objects/references from a remote
    git pull: same as git fetch; git merge
    git clone: download repository from remote

Undo

    git commit --amend: edit a commit’s contents/message
    git reset HEAD <file>: unstage a file
    git checkout -- <file>: discard changes

Advanced Git

    git config: Git is highly customizable
    git clone --depth=1: shallow clone, without entire version history
    git add -p: interactive staging
    git rebase -i: interactive rebasing
    git blame: show who last edited which line
    git stash: temporarily remove modifications to working directory
    git bisect: binary search history (e.g. for regressions)
    .gitignore: specify intentionally untracked files to ignore

 

**Staging Area:** This is the place that you tell git what changes should be included in the next snapshot(commit) of the code you take.

help can be used here like this:
``` shell script
git help commandname
```

**HEAD**
    HEAD refers to the last snapshot

**init**<br>
    Turns the current folder into the git repository.
    Creates the hidden .git folder for storing its internal data.
    
**status**<br>
    Prints the current status
    
**add**<br>
    Adds that file(s) to the staging area.
Example:  
``` shell script
git add hello.txt
```

**log**<br>
    Prints out the commit history
    --all
    --graph
    --decorate
    --oneline Shows a more compact list

**checkout**
    You can checkout to previous commits using commit hashes. 
    Or you can use the branch name?
    -f for forcing it.
    
**diff**
    Shows all of the difference at the terminal by default.<br>
    You can use filenames as arguments.<br>
    As far as I understand you can give the beginning of a commit hash too?<br>
Example, it can also be used like this:  
``` shell script
git diff 665d32a6 HEAD hello.txt
```
665d32a6 is the beginning of this commit hash: 665d32a6c8dca1455b4ff4757053a46305ecd284<br>
Apparently, git accepts this.<br>
So this shows the difference of hello.txt between the latest snapshot and that commit.

**branch**
    Can be used to create branches or provide info about new branch.<br>
    -v or --v Provides branch info.  <br>
    --set-upstream-to=origin/master Something like this defines the default action that will be taken when user does "git push"<br>

**merge** 
    Self explanatory. Maybe fill this later.

**mergetool**
    This is for solving conflicts. Use vimdiff.
    
**remote**
    Can list or add git remotes.
    
**push**
    This command can send the changes from your computer to the remote.
``` shell script
git push <remotename(origin for PP)> <localBranch>:<remoteBranch>
```

**clone**<br>
    By default, copies the entire version history.
    --shallow For cloning gigantic repositories, you can use this. 
    Remember, with --shallow you will not get the version history but cloning the repo will be much faster.

**show**<br>
    Shows the commit details
Example:
commit hash can be more easily found after git blame
``` shell script
git show commithash
```

**bisect**<br>
    **This is important. A powerful tool.**<br>
    They are not demonstrating it much because this is complex. 
    This is especially useful for bunch of problems where you need to manually search history.
    For an example scenario, you've been working on a project for a long time, you have like lots of lots 
    snapshots you're a thousand commits in. Then you notice some unit test doesn't pass anymore but you know this was
    passing one year ago. So you are trying to figure out what point did it break. Instead going back to commits one by one,
    "git bisect" automates that process. It actually binary searches your history. Also it can take scripts that it uses to
    try figure out whether a commit looks good or bad. This can be an automated process.


continue after 1:20:00