# Commands

| command | desc |
|--|----|
|git rev-parse --abbrev-ref HEAD |  returns the branch name |
|git diff HEAD~1 -- shared/adsl.sas| compare against previous commit <br> The -- separates the commit reference from the file path, same pattern as the checkout command.|
|git branch -D branch-name  | delete an unmerged branch |
|git branch -d branch-name  | delete a merged branch |
| git fetch    <br>      # See what's changed remotely <br> git status  <br>      # Check the difference<br> git pull    <br>       # Bring remote changes into your branch (if any)<br> git push    <br>       # Send your commits to remote<br> |Most of the time you can skip fetch and just do git pull then git push, but fetch + status lets you inspect before merging.| 
| | |
