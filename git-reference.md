
## Discard all local commits on branch, update to upstream of branch
`git reset --hard @{u}`

## Determine What Has Been Merged

`git checkout master`

`git branch --merged`

## Prune Remote Branches

`git remote prune origin`

Deletes all stale remote-tracking branches under <name>. These stale branches have already been removed from the remote repository referenced by <name>, but are still locally available in "remotes/<name>".
  
## Branches w/ Deleted Upstream/Remote Counterparts
https://railsware.com/blog/2014/08/11/git-housekeeping-tutorial-clean-up-outdated-branches-in-local-and-remote-repositories/

`git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}'`

## One-liner to Delete Branches w/ Deleted Upstream/Remote Counterparts

`git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -d`

### Powershell + Posh Git

`git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | %{git branch -d $_}`

The command above replaces `xargs` with PowerShell syntax for a Foreach loop. I run posh-git behind PowerShell and was having some issues getting `xargs` to work right. First had to using `-I` flag and wrap the input in quotes to get proper line replacement: `xargs -I% git branch -d '%'`. But then it was still not executing right.

## Select parts of diff to stage for a commit

`git add -p <file>`

https://git-scm.com/docs/git-add#git-add--p

## Selectively stash changes

stash file1.js and file2.js  

`git stash push -m "Description" ./file1.js ./file2.js`

select parts of diff to stage from all files 

`git stash push -p -m "Description"`

select parts of diff to stage from file1.js and file2.js

`git stash push -p -m "Description" ./file1.js ./file2.js`

(q can quit at any point keeping all changes already chosen for stash)

## Update branch w/o switching to it

`git fetch origin <branch>:<branch>`

For example:

`git fetch origin dev:dev`

## Check out branch from another fork/repo

(Stolen from GitHub manual merge of PR instructions)

```
git checkout -b <new branch name> main
git pull git@github.com:<external repo>.git <existing branch>
```
