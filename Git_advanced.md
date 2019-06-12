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
      
## How to rename branch name in local and remote 
    1. Rename your local branch.
    If you are on the branch you want to rename:
    git branch -m new-name
    
    If you are on a different branch:
    git branch -m old-name new-name
    
    2. Delete the old-name remote branch and push the new-name local branch. 
    git push origin :old-name new-name

    3. Reset the upstream branch for the new-name local branch.
    Switch to the branch and then:
    git push origin -u new-name

## git fetch 
       You can do a git fetch at any time to update your remote-tracking branches under refs/remotes/<remote>/.

      This operation never changes any of your own local branches under refs/heads, and is safe to do without changing your 
      working copy. I have even heard of people running git fetch periodically in a cron job in the background (although I 
      wouldn't recommend doing this).

    A git pull is what you would do to bring a local branch up-to-date with its remote version, while also updating your other 
    remote-tracking branches.
    
## git pull 
- git pull = git fetch + git merge 

 git pull makes sure the files in remote and local are same
 git fetch will get the changes from remote and place it in another branch origin/branch_name, then we need to merge that 
 local branch 

## git clone 
- downloads the remote repository files to local 

        if you want clone repo to particular folder the you need to use below command 
        git clone git@github.com:whatever folder-name

## git diff file_name or git diff commit_id
- it will show you the changes made in particular file or commit 

## git status 
- it give status of which file modified , added or deleted 

## git log 
- it gives commit history of a repo

        if you want only last three commits then you can do git log -3.
        if you want commits in oneline then the command will be git log --oneline
   
## submodules 
   [For mor information](https://www.vogella.com/tutorials/GitSubmodules/article.html#cloning-a-repository-that-contains-submodules)
