## git clone -b branch_name --single-branch --depth 1 clone_link
- -b is for after cloning repo in local Directory which should be the default branch to point 
- --single-branch it will clone only specified branch in -b 
- --depth number of commits to clone 

## git branch or git branch -a 
- -a is for all branches 

## git remote -v 
- to get clone link and push link and below is the output 
    
       origin	ssh://git@storegit.apple.com:4443/project/repo.git (fetch)
       origin	ssh://git@storegit.apple.com:4443/project/repo.git (push)
       
## git checkout -b branch_name 
- To create branch from files which are there in present branch 

## git checkout branch_name 
- To change the branch we will use above command 

## git checkout file_name
- To igonre the changes of modified files in local

## git status 
- To know any changes made in a directory 

## git rm --cached file_name 
- to remove file from staging area

## git pull origin branch_name 
- if are there in other branch but you need to pull updates of other branch 

## git mergetool --tool=opendiff
- To resolve the confilcts 

## Stashing
    Often, when you’ve been working on part of your project, things are in a messy state and you want to switch branches for a 
    bit to work on something else. The problem is, you don’t want to do a commit of half-done work just so you can get back to 
    this point later. The answer to this issue is the git stash command. 
   [for more reference](https://git-scm.com/book/en/v1/Git-Tools-Stashing)
    
  ### git stash
       where you have the changes 
       
 ### git stash list 
       to list all stash 
       
 ### git stash apply 
      to get back the most recent stashed changes 
    
 ### git stash apply stash@{2}
      to get particular stash to local directory , by default most recent 
    
