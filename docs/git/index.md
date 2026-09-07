# Commits
Commits are snapshots of the project.  Lightweight, switching is fast  
it doesnt copy entire directory, it can compress a set of changes or a 'delta', from one version to the next  
```git
git commmit  
```

# Branches
Simply pointers to a specific commit  
A branch to include this commit and all parent commits  
```git
git branch newImage  
```
To make updates to the branch checkout the branch  
Moves pointer to the branch
```git
git checkout <name>  
```
To create a new branch and check it out at the same time
```git
git checkout -b  <name>  
```

# Merging
Merging in git creates a special commit that has 2 unique parents.  I want to include all the work from his parent over here and this one over here.   
Merge branch bugFix and main
```git
git checkout main  
git merge bugFix  
```

# rebase
A second way to combine work between branches is rebasing.  Takes a set of commits, 'copies' them and puts them somewhere else.  Makes a nice linear sequence of commits.  THe log of the repo will be cleaner if only rebasing is allowed.  
If 2 branches, bugFix currently selected, to move our work from bugFix directly into the main, it would look like these 2 features were developed sequentially, rather than in reality in parallel.  
```git
# moves commit to a commit that has main as a parent  
git rebase main

# moves the main branch reference forward in history  
git rebase bugFix
```

# Detached Head

HEAD is the symbolic name for the currently checked out commit, essentially what commit are you working on top of  
HEAD always points to the most recent commit which is reflectedin the working tree.  most git commands which make changes to the working tee will start by changing HEAD.
Normally HEAD points to a branch name (like bugFix) whcn you commit the status is altered and this change is visible through HEAD   
Detaching HEAD is just attaching it to a commit instead of a branch.

```git  
# moves commit to a commit that has main as a parent  
git checkout c1
```

# Relative refs
git log to see commits  
Move upwards one commit at a time with ^  
Move upwards a number with ~<num>  
```git
# moves commit to previous  
git checkout main^  
# moves the main branch back 5  
git checkout HEAD~4
```

# Branch forcing
can erassign a branch to a comit with -f option  
```git  
# moves - by force -  main branch to 3 behind HEAD  
git branch -f main HEAD~3 
git branch -f main c6
git branch -f bugFix HEAD~2
git checkout HEAD^
```  

# Reversing changes in git
2 primary ways git reset and git revert  
```git
# now local repo is in a state as if the last commit didnt happen  
git reset HEAD^1
```
reset doesnt work for remote branches that others are using, to share changes use git revert
```git
# add new commit that is the reverse of the last commit  
git revert HEAD
```

# Moving work around
```git
git cherry-pick c3 c4 c7  
git rebase -i HEAD~4


c0-c1(main)-c2()-c3(printf)-c4(bugFix)  
# make main the HEAD
git checkout main  
# move only the bugfix commit to the main, leave debug code on branch   
git cherry-pick c4
```

# 
```bash
# Compare against a specific commit
git diff abc1234 -- shared/adsl.sas

# Compare between two commits
git diff HEAD~3 HEAD~1 -- shared/adsl.sas

# Compare your working directory (uncommitted changes) against last commit
git diff -- shared/adsl.sas

# Compare between branches
git diff main dema -- shared/adsl.sas
```





