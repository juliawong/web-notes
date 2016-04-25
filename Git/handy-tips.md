http://www.alexkras.com/19-git-tips-for-everyday-use

# Weekly report
`git log --author="Julia" --after="1 week ago" --`

`--oneline` to include hash and commit message

# Log changes in a file
`git log -p filename`

# Log changes for specific lines in a file
`git log -L 1,1:some-file.txt`

# Log changes not merged to parent branch
Ignores merges from parent into current branch

`git log --no-merges master..`

# View version of file on different branch
`git show some-branch:some-file.js`

# Stages
* Not staged for commit
  * Untracked files aren't in this stage
* Staged for commit
* Committed

# Resetting
Return to a particular version in git history

* `git reset --hard {{some-commit-hash}}` changes made after this commit are discarded, ideal for a fresh start
* `git reset {{some-commit-hash}}` changes made after this commit are not staged for commit, ideal for editing and committing in a different order
* `git reset --soft {{some-commit-hash}}` changes made after this commit are moved to staging, ideal for commiting multiple small commits as one large one

# Checkout
Forget local changes for file/s

`git checkout forgetme.txt`

Different version of file
`git checkout some-branch-name file-name.js`

`git checkout {{some-commit-hash}} file-name.js`

# Softly revert
Ideal for experimenting with reverts without needing to commit

`git revert -n`

# Stage different hunks of a file
`git add -p`

# Stash some files
* `git add` files you don't want stashed
* `git stash --keep-index` stash files that haven't been added
* `git reset` unstage added files and continue work

# What broke my feature?
* `git bisect`
* `git bisect reset` restarts the process
* `git bisect log` logs the last successfully completed bisect operation

* `git bisect start`
* `git bisect good {{some-commit-hash}}` known good commit
* `git bisect bad {{some-commit-hash}}` known bad commit
* git checkouts a middle commit between good and bad
* `git bisect bad/good` let git know whether the current commit is working or not
* git will inform you when the first bad commit is found

