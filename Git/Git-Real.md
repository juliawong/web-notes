[Course](https://www.codeschool.com/courses/git-real)

# Git Real
## Useful Stuff
* `git diff --staged` Diff staged
* `git reset HEAD filenames` Unstage
  * `HEAD` refers to the last commit
* `git reset HEAD --hard` remove all changes since HEAD
* `git commit -a -m "modify readme"` skip staging and commit, adds changes from all tracked files
* `git reset --soft HEAD` move commits to staging
* `git commit --ammend` add file to existing commit
* `git reset --hard HEAD^` undo last commmit and all changes
 
## Cloning and Branching
* `git remote -v` list all remotes
* `git merge cat` merge from master
* `git checkout -b catdog_branch` create branch
* `git branch -d cat` remove branch

### Branching
* We have remote branches and tags, we need to link them
* `git push origin branch_name` link local branches to remote (tracking)
* `git branch -r` list all remote branches
* `git remote show origin` find tracked, configure for push and pull
* `git push origin --delete <branchName>` delete remote branch
* `git push origin :<branchName>` delete remote branch
* `git remote show origin` inspect remote branches
* `git remote prune origin` clean up deleted remotes, removes objects that are no longer being referenced

## Tagging
* Reference to a specific commit
* `git tag` list tags
* `git checkout v0.0.1` checkout tag
* `git tag -a v0.0.3 -m "version notes"` add tag
* `git push --tags` push tags

## Rebase
1. Moves all changes to master which aren't in origin/master to a temp area
2. Run all origin/master commits
3. Run all commits from temp area

```
git checkout feature
git rebase master
git checkout master
git merge feature
```

### Interactive Rebase
* Alter commits in the same branch
* Alters commits after specified one
* `git rebase -i HEAD~3` will alter the 4th pervious commit
* `git commit --amend`
* `git rebase -- continue`

## History and config
 `git diff HEAD^` parent of last commit
 `git diff HEAD~5` 5 commits ago
 `git diff HEAD^...HEAD` diff 2nd most recent commit to most recent
 
 Exclude files/folders, add to `.git/info/exclude`
 
## Stashing
* Put away current changes into a temp area
* `git stash save` add
* `git stash apply` apply
* `git stash apply stash@{2}` apply specific
* `git stash drop` remove from list
* `git stash pop` apply and remove (doesn't always drop when there's a conflict)
* `git stash save --keep-index` don't stash files in staging
* `git stash save --include-untracked` stash untracked files
* `git stash clear` remove all stashed
* `git stash branch branch_name` create branch and apply

## Pruning History
* Tree filter (real file tree) and Index filter (git index)
* `git filter-branch --tree-filter <cmd> ...`
* `--all` filter all commits in branches
* `HEAD` fulter only current branch
* `--index-filter git rm --cached --ignore-unmatched` operate on staging
* `git filter-branch -f prune-empty -- --all` drops commits not editing files

## Collaboration
* `git config --global` change settings with parameters and values
* Charrypicks move commits from a branch to the other
* `git cherry-pick <hash>` moves commit to current branch
* `git cherry-pick --edit <hash>` change commit message
* `--signoff` show who cherrypicked
* `--no-commit` don't create new commit
* `-x` where is the commit coming from

## Reflog
* 2nd log in local repo
* `git reset --hard hash HEAD@{1}`
* `git log --walk-reflogs` recover branches, walk reflog entries from the most recent one to older ones
