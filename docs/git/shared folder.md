# create a shared folder on main to sync with branch


## That's git opening a text editor (usually vim) for you to confirm or edit the merge commit message.  

If it's vim (you'll see the message with lines starting with #):  

Press :wq then Enter  

That saves the message and completes the merge.  

If you just want to exit without merging:  

Press :q! then Enter  


To avoid this in future, you can provide the message upfront:
```bash
git merge main -m "merge main into dema"
```

## how do you compare the current comiit against the previous is there a command like git diff HEAD^1
```bash
git diff HEAD~1
```
other useful variations
```bash
# Compare against 2 commits back
git diff HEAD~2

# See just the file names that changed
git diff HEAD~1 --name-only

# Diff a specific file
git diff HEAD~1 -- shared/utils.js

# See the changes in the last commit as a patch
git show HEAD

```

## how to show what changed
```bash
# What changed in the last commit for the whole shared folder
git diff HEAD~1 -- shared/

# What changed for a specific file
git diff HEAD~1 -- shared/adam/adsl.sas

# Just the file names that changed
git diff HEAD~1 --name-only -- shared/

```
This shows which files changed and where they are. The "1 file changed 38 insertions" might be a file outside shared/ that was sitting uncommitted in your working directory and got swept up by git add ..  
```bash
git show HEAD --stat

```
This tells you which files were in the last commit. 
```bash
# See what the last commit actually changed
git show HEAD --name-only

```
```bash
git log --oneline -5

```
```bash


```

## sheel to check branch and sync main with branch
```bash
#!/bin/bash
CURRENT=$(git branch --show-current)

if [ "$CURRENT" = "main" ]; then
  echo "You're on main, switch to another branch first"
  exit 1
fi

git checkout main -- shared/
git add .
git commit -m "sync shared/ from main into $CURRENT"
echo "shared/ synced to $CURRENT"
```
## how do you compare a file against the previous version 

```bash 
git diff HEAD~1 -- shared/adsl.sas
```
The -- separates the commit reference from the file path, same pattern as the checkout command.  
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



```bash
#!/bin/bash
# Usage: ./sync-shared.sh [branch]
# Defaults to main if no branch specified

SOURCE=${1:-main}
CURRENT=$(git branch --show-current)

if [ "$CURRENT" = "$SOURCE" ]; then
  echo "You're on $SOURCE, switch to target branch first"
  exit 1
fi

# Check source branch exists
if ! git rev-parse --verify "$SOURCE" >/dev/null 2>&1; then
  echo "Branch '$SOURCE' does not exist"
  exit 1
fi

# Get list of top-level folders from source branch
FOLDERS=$(git ls-tree --name-only "$SOURCE" | while read item; do
  if git cat-file -t "$SOURCE:$item" 2>/dev/null | grep -q "tree"; then
    echo "$item"
  fi
done)

if [ -z "$FOLDERS" ]; then
  echo "No folders found on $SOURCE"
  exit 1
fi

# Remove old shared content
rm -rf shared/

# Extract only folders from source branch into shared/
mkdir -p shared
git archive "$SOURCE" -- $FOLDERS | tar -x -C shared/

# Commit
git add shared/
git commit -m "sync folders from $SOURCE into shared/ on $CURRENT"
echo "Synced these folders from $SOURCE into shared/:"
echo "$FOLDERS"
```



## pull request / remote
he typical workflow is:
```bash
# 1. Fetch latest remote state
git fetch

# 2. Check if you're ahead or behind
git status

```
git status will then tell you things like:  
"Your branch is ahead of 'origin/main' by 2 commits" (you have local commits to push)  
"Your branch is behind 'origin/main' by 1 commit" (remote has changes you don't)  
"Your branch is up to date with 'origin/main'" (in sync)  

```bash
git fetch          # See what's changed remotely
git status         # Check the difference
git pull           # Bring remote changes into your branch (if any)
git push           # Send your commits to remote
```
Most of the time you can skip fetch and just do git pull then git push, but fetch + status lets you inspect before merging.