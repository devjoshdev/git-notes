# Git Notes

# MIT Missing Semester Lecture 6 

[Source](https://www.youtube.com/watch?v=2sjqTHE0zok)

## Why use version control systems (VCS)? 
+ Keep track of changes in a software project
+ Know who authored a change to the code and when that happened
+ Work simultaenously on bug fixes and new features independently using branches
+ Allows code to be shared easily

## What is the best way to learn Git?
+ Understand the underlying <ins>data model</ins> first to gain an understanding behind the common commands

## What is the data model?
+ Folders are called **trees**
+ Files are called **blobs**
+ Snapshots are called **commits**
+ Commits have metadata such as parent, author, and timestamp

## How does Git track history?
+ Uses commits which are all the trees and blobs at some point in time, but does not maintain them linearly
+ Uses an **acyclic directed graph (ADG)** where each snapshot points to the previous snapshot
+ The reason for using an ADG is to allow for branching and merging
+ These commits are maintained in memory as objects, referenced by a hash of the data inside it (hexadecimal strings)
+ Use commit messages to have human readable identifiers for them

## How to create a Git repository
+ `git init`
+ This will make the current folder the root to a git repository
+ A folder called `.git` will be created to store the objects and references
+ This will also create the master branch

## How to get information about various commands
+ `git help [command]`
+ Using this command will display the man page for a given git command

## How to get status of current branch you're on
+ `git status`

## What is the staging area?
+ The staging area is an intermediate area where you can prepare and review changes before making a commit (from ChatGPT)

## Why use the staging area? 
+ One use case could be that you've implemented two features in two separate blobs and want them in separate commits, can stage both changes and commit them one at a time instead of all at once 

## How to add file to staging area? 
+ `git add [filename]`

## How to commit changes? 
+ `git commit -m [message]`

## How to view the ADG?
+ `git log`
+ Can use `git log --all --graph --decorate`
+ TODO: look more into this ^^

## The HEAD reference
+ This is a special reference to the latest commit of the branch that is currently checked out
+ Can check out a specific commit in the branch to be in the detached HEAD state
+ Use cases include
    + Inspecting previous commits
    + Creating new branch from previous state
    + Amending previous commit

## How to go to a different commit in the ADG?
+ `git checkout [previous commit's hash]`

## How to view changes made in a file? 
+ `git diff [commit hash] [filename]`
+ If the commit hash is not supplied then it will be compared to the content of filename of the commit where the HEAD is

## Using branches
+ The `git branch` command will list all branches for the project
+ `git branch -vv` will be extra verbose

## How to create a new branch? 
+ `git branch [branch name]`
+ This will create a new branch wherever HEAD is, but won't switch the current branch

## How to switch branches? 
+ `git checkout [branch name]`

## How to combine these two commands? 
+ `git checkout -b [branch name]`
+ This is equivalent to doing
    + `git branch [branch name]`
    + `git checkout [branch name]`

## How to merge different branches? 
+ `git merge [branch name]`
+ This will merge the branch in the command into the current branch

## What happens when there are merge conflicts? 
+ The merge command can return an error if it doesn't know how to automatically merge
+ Can use a configured tool to resolve those conflicts (need to have one installed)
    + `git mergetool` This will take you through all the changes that need to be made
    + Then `git add [all files required]`
    + Then `git merge --continue`
+ Can also manually resolve those conflicts in the necessary files
    + Then `git add [all files required]`
    + Then `git merge --continue`

## What are remotes? 
+ A repository can be hosted on a server or some other location on a network/computer
+ `git remote` shows the names of the remotes associated with the current repository
+ `git remote add [name] [URL]` will make local repo aware of the remote
+ `git push [remote name] [local branch]:[remote branch]` sends changes from your computer to the remote
+ `git clone [URL] [where to clone]` will grab code from the specified remote for you to use locally
+ `git fetch [remote]` will grab the latest code from a remote repo but won't integrate the updated code into your local repo, will need to do a `git merge` to integrate the changes
+ `git pull [remote]` will grab the latest code from a remote repo and integrate the changes into your local repo, effectively acting as a `git fetch` followed by a `git merge`