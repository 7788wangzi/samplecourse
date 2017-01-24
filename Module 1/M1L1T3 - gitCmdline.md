## Introduction to Git Commands
### Two Types of VCS
- centralized version control  
- distributed version control 

git is a distributed version control system.  
each computer store a full database, you don't need to connect to server to get a file or update a file.

server - reprository  
====|====  
====|====|computer1 - repository  
database=|computer2 - repository  
======== |computer3 - repository  

git three main states: ***committed, modified, staged***

**committed** means that the data is safely stored in your local database.  
**modified** means that you have changed the file but have not committed it to your database yet.  
**staged** means that you have marked a modified file in its current version to go into your next commit snapshot.  

### Git Command lines

#### 1. For create a local repository first

First, you create a folder in your disk, then use `git init` to make this folder a repository.  

    mkdir createdlocal
    cd createdlocal
    git init


you can see the empty repository with commandline `ls -ah`.


get the commit status  

	git status

>Note: git status only check the diff of his local version with the last push version of his own, it doesn't identify the changes pushed by other people.

staging and commit 
   
	git add <file>  
	git commit -m "comment goes here"  

skip staging, directly commit

	git commit -a -m "comment goes here"

get differences

	git diff --staged
	git diff --cached

delete a local file

	git rm <file>

untrack a file

	git rm --cached <file> -f

rename a file

	git mv <fileA> <fileB>
	git commit -m "comment goes here"

view committed version
	
	git log  
	git log -p -2  
	git log --stat  
	git log --pretty-oneline  
	git log --pretty:format:"%h  %an, %ar  : %s"  
	git log --since=1.weeks  
	

unstage a staged file

	git reset head <file>

unmodifying a modified file

	git checkout --<file>

rollback to a previous version  commit number "e77ab46b2800c8c758a05985dfa428a12773ed14"  

    git reset --hard e77ab46b2800c8c758a05985dfa428a12773ed14

then you will get a message "HEAD is no at 10c4dde XXX"



#### 2. Work with Remote repository
clone a remote repository, cd to the expected path in local, then run:

	git clone https://github.com/7788wangzi/git_ws10.git

or add local repository to a remote location

	git remote add [name] [url]
	E.G. git remote add origin https://github.com/7788wangzi/git_2.git

check remote version

	git remote -v

push local update to remote

	git push [remoteName] [localBranchName]

pull remote repository to local

	git pull [remoteName] [localBranchName]

stop mapping local and server

	git remote rm origin

create local branch

	git branch [branchName]
	E.G. git branch 117

switch to branch 117

	git checkout 117

sync branch to remote

	git push origin 117

delete remote branch

	git push origin :heads/117

delete local brach

	git branch -d 117

get a specific branch from server (for clone project only)

	git branch -b 1118 origin/1118

merge a branch to current branch

	git merge 1118



#### 3. Issues

if you runinto following issues

> Another git process seems to be running in this repository, e.g.
an editor opened by 'git commit'. Please make sure all processes
are terminated then try again. If it still fails, a git process
may have crashed in this repository earlier:
remove the file manually to continue.

You can use following command to resolve it  

    rm .git/index.lock

Note: Not git `rm .git/index.lock`
