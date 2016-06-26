* http://www.alexkras.com/19-git-tips-for-everyday-use
* http://devblog.nestoria.com/post/98892582763/maintaining-a-consistent-linear-history-for-git
* http://www.metaltoad.com/blog/beginners-guide-git-bisect-process-elimination
* http://vanwilson.info/2016/05/wrangling-wandering-whitespace-git/
* http://learngitbranching.js.org/

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

## Operators
* ^ parent of commit
 * `git checkout master^` first parent of master
 * Number indicates parent reference from merge
* ~<num>
 * `git checkout HEAD~3` move upwards 3 times

# Branch Forcing

Move, by force, master branch to 3 commits behind HEAD
`git branch -f master HEAD~3`


# Revert

Creates a new commit that introduces changes to reverse the commit

`git revert HEAD`

Soft revert is ideal for experimenting with reverts without needing to commit

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


# git log first-parent
* Merge = commit with 2+ parents, parents are ordered
* After merging branch into master, first parent is tip commit of master, second parent is tip commit of other branch
* `git log --first-parent`
 * Follows each commit's parents
 * Commits from branch aren't displayed
 * Merge commits are displayed
 * Similar to folds in a text editor

# Whitespace

* Git shows trailing whitespace in diffs
* Highlight tabs for indentation `git config --global core.whitespace "tab-in-indent"`
 * `blank-at-eol` - show space at end of lines
 * `blank-at-eof` - show space at end of files
 * `indent-with-non-tab` - show spaces in indentation 
* Show what git considers whitespace errors `git diff --check`
* Fix whitespace errors in last commit with rebase if not yet pushed
 * Check previous commit `git diff HEAD~1 HEAD`
 * `git rebase HEAD~1 --whitespace=fix`

# Cherry-pick

Copy a series of commits to below HEAD

`git cherry-pick <Commit1> <Commit2> <...>`


Copy commits C2 and C4 to after master (current branch)

`git cherry-pick C2 C4`

# Tags

Permanently mark commits as milestones that can be easily referenced

Can't commit afterwards, checked out as detached head state

Create a tag named `v1` and reference commit `C1` (if commit not given, `HEAD` is used)

`git tag v1 C1`

## Describe

Describe where you are relative to closest tag

If no ref given, use `HEAD`

`git describe <ref>`

Outputs

`<tag>_<numCommits>_g<hash>`

* tag - closest ancestor tag in history
* numCommits - how many commits away that tag is
* hash - hash of commit described

# Remotes

## Clone
* Creates a remote branch for every branch on the remote, e.g. `origin/master`
  * Tracks changes on the remote
  * Checking out to this results in detached state
* Creates local branch to track each active branch on the remote e.g. `master`

## Tracking

Checkout new branch and specify remote branch for push and pull

`git checkout -b foo o/master`

`git branch -u o/master foo`

## Push

`git push <remote> <place>`

e.g. `git push origin master`

Goes to branch named `master`, grabs all commits then goes to `origin/master` and places missing commits on there

## Refspec

* Location that git can figure out

`git push origin <source>:<destination>`

Use to specify source and destination of place

`git push origin foo^:master`

* Git resolves `foo^` into a location
* Upload commits that aren't present on remote
* Update destination

If destination you want to push to doesn't exist then git will create one on the remote for you

`git push origin master:newBranchName`

## Fetch

Doesn't update your local non-remote branches

`git fetch origin foo`

* Go to `foo` branch on remote
* Grab all commits that aren't in the local `foo` branch
* Put on `origin/foo` branch locally

Fetch commits directly to a local branch, not checkout out branch

`git fetch origin <source>:<destination>`

* Source is the remote
* Destination is the local branch to place commits
