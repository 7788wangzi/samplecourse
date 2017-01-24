## Git Merge

### Simultaneously Modifying 
there is a case that the exact same file is modified by two different people from two local repositories simultaneously. there should be conflict when they both want to push their local repositories to remote server, it's the solution how git resolve this:  
Remote Repository | (empty) file.txt  -v1  
user1 | file.txt  -v1  
user2 | file.txt  -v1  

1. User1 modified file.txt by adding a new line "User1"
2. User1 committed the changes to local repository. (the file version is v1-v2)
3. User1 pushed the updates to Remote Repository.

**now the file.txt is v2 in both User1 and Remote Repository**  
for the User2

1. User2 modified file.txt by adding a new line "User2". (note that it's still v1)
2. User2 committed the changes to local repository. (the file version is v1-v3)
3. User2 tries to push the updates to remote repository.

however in step3, git identified that the file.txt version in remote repository is v2. the local version v3 is changed directly from v1, so it rejected the push request for User2.  

In order to merge the updates of User2, he first need to pull the v2 from remote repository:
	
	 git pull origin

after the pull action, the file.txt is auto merged by git in User2's local repository.
this is what the file.txt looks like:

><<<<<<< HEAD  
>User2   
>\=======  
>User1  
>\>>>>>>> 119dd0691f2c5e766b5d756e9b3033d75331acf7

now User2 can push the file.txt to the remote repository. and the file.txt would be v3 in remote repository.