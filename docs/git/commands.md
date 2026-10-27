# Commands

| command | desc |
|--|----|
|git rev-parse --abbrev-ref HEAD |  returns the branch name |
|git diff HEAD~1 -- shared/adsl.sas| compare against previous commit <br> The -- separates the commit reference from the file path, same pattern as the checkout command.|
|git branch -D branch-name  | delete an unmerged branch |
|git branch -d branch-name  | delete a merged branch |
| git fetch    <br>      # See what's changed remotely <br> git status  <br>      # Check the difference<br> git pull    <br>       # Bring remote changes into your branch (if any)<br> git push    <br>       # Send your commits to remote<br> |Most of the time you can skip fetch and just do git pull then git push, but fetch + status lets you inspect before merging.| 
| | |


## git log
- git log --oneline  --all --parents --graph
show previous changes
- git log -p --oneline -1

## branch
- git switch test  
move branch and create
- git switch -c test   
rename
- git branch -m test2 test3
list
- git branch

## merge
git merge test 
If forget to update message
- git commit --amend -m "message"

## fast forward merge
merge onto head which has no commits, moves the pointer to the merge commit, ie no new commit.  IF the tip of th brnahc 
that is merged onto is the merge base then you can fast forward merge
with normal merge a new commit is made from the common base of both branches.  Ths commit has 2 parents


## rebase
moves feature branch onto main, like a fast forward merge
the history is linear rather than having a branch
the new commits for feature are appended to the main, and they are given new sha commits becuase they have a new parent

from the feature branch
- git:(update_dune) git rebase main

warning - never rebase a public branch like main onto anything else.  Other devs have it checked out, if you change its history it will cause problems 
a linear history is usually easier to work with (ieon main) so revert etc is easier.  Branches we can do whatever

## git reset
- git reset --soft COMMITISH
soft useful to go back to previous commit but keep all changes. Committed changes are uncomimtted and staged, uncommitted will remain staged or unstaged as before

HEAD and back 1
- git reset HEAD~1

Go to a previous commit and discard all changes (not unstaged ones) - will undo the index and the workingtree
- git reset --hard COMMITISH


## remote
create remove to uri, can be another folder or url
- git add remote origin ../x

then need to update
- git fetch

can now build from fetched data
- git cat-file -p 7805 

can log the remote branch
- git log remote/branch
- git log origin/main

can merge with a single local repo
- git merge remote/branch
if local is new then it will fast-forward merge

check connection
- git ls-remote 

## push
- git push remote branch
- git push origin main

## pull
want actal changes from remote repo, not just meta data
- git pull remote/branch
without the remote/branch it retrieves the current branch from the remote rep
