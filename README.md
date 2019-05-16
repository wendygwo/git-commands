# git-commands
A cheat sheet for git commands that I've found useful

## Soft reset
Useful if you forgot to commit something and want a do-over of your last commit
`git reset HEAD~1`

## Workflow for rebasing off of dev branch
While on your feature branch

* Pull down the latest remote so that your origin branches are current

`git fetch`

* Applies all your commits one by one on top of the the remote dev branch

`git rebase origin/dev`

If you run into merge conflicts
* Open the file that's conflicted. Resolve the merge conflict as usual and save file. 
* Confirm that the file you changed is there in the unstaged portion

`git status`

* Add your changes

`git add`

* This commit has been resolved so apply it and move onto the next commit

`git rebase --continue`

* Once all the conflicts are done, run your branch to make sure there were no functional conflicts and everything works as expected.

* Force push to remote

`git push -f origin {feature_branch}`

Note: -f is `force` which will forcibly overwrite what you currently have in the remote version of your branch. Use with caution

* Force push with lease (a kinder, gentler force push)
`git push --force-with-lease`

Read more about it: http://blog.developer.atlassian.com/force-with-lease/
## Workflow for squashing or re-working commits
* Open a file with the list of all your commits

`git rebase -i origin/dev`

* Change `pick` to `s` for the commits that you want to squash. They will be collapsed into the previous commit. Change to `r` to just reword the commit message 

* Force push to origin {feature_branch} when you're done

`git push -f origin {feature_branch}`

## Workflow for rebasing with respect to your own branch
`git rebase -i HEAD~3`

* Edit file that comes up:
* Delete ‘pick’ and type ‘squash’ for the commits you want to sqush

`:wq` in command line

* Edit file that comes up:
* Comment out other commit messages and edit the first one, if you want to modify it

`:wq` in command line

## Steps for merging from d ev branch into your working branch:
`git checkout dev`

`git pull`

`git checkout <branch_name>`

`git merge dev`

Resolve whatever conflicts come up

`git add <whatever files you changed or updated>`

`git commit`

A file will open up with an already filled out commit message (i.e. Merging dev into addQuiz)

Press :q to quit the file

`git push origin <branchname>`

You should be able to merge now


## See evolution of lines in git

`git log -L 15,23:filename.txt`

## Command to run in terminal to clean up all merged branches

`git branch --merged | grep -v "\*" | xargs -n 1 git branch -d `

*References: See http://stevenharman.net/git-clean-delete-already-merged-branches for more details about how this works. http://www.thegeekstuff.com/2013/12/xargs-examples/ has info about xargs*

## Set a new remote

`git remote add origin https://github.com/user/repo.git`

## Verify new remote

`git remote -v`

## To update the local list of remote branches

`git remote update origin --prune`

## Checkout a new branch

`git checkout -b <branchname>`
  
## Global git configuration

`git config --global user.name "wendygwo"`
`git config --global user.email wgwo@hotmail.com`

## View and edit global git configuration

`git config --global --edit`

## To set a new remote url
`git remote set-url origin new_url`
