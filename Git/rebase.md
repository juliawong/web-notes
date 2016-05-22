# Rebase

* Merge another branch into the branch where you are currently working
* Move all of the local commits that are ahead of the rebased branch to the top of the history on that branch

e.g. you work on the *master* branch and other people have pushed to *origin/master* while you've worked.
We could `git pull` (which does a `git fetch origin` and then a `git origin/master`) but we don't want merges and want a nice linear history.

From the `master` branch we can do a `git rebase origin/master` to bring in those commits and then apply our local commits on top.

`git pull --rebase`
does this

e.g. you commit to a branch and other people have committed. You attempt to push but git tells you to pull changes.
* pull changes
* reapply (rebase) your un-pushed commits on top of latest version of remote branch

```
git fetch origin
git rebase --onto origin/foo e foo
```

## Remove a commit from the wrong branch
e.g. you have some previous commits but some are on the wrong branch

`git rebase -i HEAD~2`
Delete the commit

## Squashing many commits into one
e.g. you commit some code and then the test

`git rebase -i HEAD~n`
`n` is the number of commits you need access to
Change *pick* to *squash*

## Change the message on many commits
`git rebase -i`
Change *pick* to *edit*

`git commit --amend -s` and `git rebase --continue` for each commit

`git push -f` may be necessary. Don't use this on public branches without explicit permission.

# Topic branch off another topic branch
e.g. a branch (client) of a branch (server) off master

## Merge client into master without affecting server
* Takes changes on client that aren't on server
* Replay them on master
* master now contains commits from client that aren't on server

```
 git rebase --onto master server client
 ```
 
 * Check out the client branch
 * Figure out the patches from the common ancestor of the client and server branches
 * Replay them onto master
 
```
git checkout master
git merge client
```

Fast-forward master branch to include client branch changes.

## Merge server into master
* Rebase with

```
git rebase [basebranch] [topicbranch]
```

* Checks out topicbranch
* Replays on top of basebranch

Then fast-forward master branch to include server branch changes



