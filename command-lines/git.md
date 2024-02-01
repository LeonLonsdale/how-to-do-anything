## How to - Use Git & Github

```shell
git status                                          # check working tree
git add .                                           # add all updated documents to stage
git add <file name> <file name>                     # add specific files
git commit                                          # opens editor for longer commits
git commit -m 'message'                             # commit all staged changes
git commit -a -m 'message'                          # stage all files and commit
git commit --amend                                  # amend a commit (only the last commit - add files before amending if necessary)


git push origin main                                # push commited changes to main branch
git subtree push --prefix dist origin gh-pages      # create and push staged changes to gh-pages branch for live env

git log                                             # view log of all commits
git log	--oneline                                   # show one line of longer commits in log


git branch                                          # list existing branches
git branch -v                                       # list of branches with current commit
git branch <name>                                   # create new branch
git switch <name>                                   # switch to branch
git checkout <name>                                 # switch to branch
git checkout <hash>                                 # checkout an old commit
git switch -c <name>                                # create & switch to a branch
git checkout -b <name>                              # create & switch to a branch
git merge <name of other branch>                    # merge changes in one branch into the current branch

git branch -d <name>                                # delete a branch
git branch -D <name>                                # force delete on unmerged branch

git branch -m <name>                                # rename current branch

git diff                                            # see whats changed in an unstaged file
git diff --staged                                   # staged changes
git diff --cached                                   # staged changes
git diff HEAD                                       # see changes in working tree since last commit

# add a file name to the end of any diff to view changes in a specific file

git diff <branch> <branch>                          # see difference between files in 2 branches
git diff <commitHash> <commitHash>                  # see difference between 2 commits.


# stashing is for storing changes in a branch that are not ready to commit, so you can switch branch.

git stash                                          # stash changes for later
git stash pop                                      # remove from stash to current branch
git stash apply                                    # applies to branch and stays in stash
git stash list                                     # view stash
git stash apply stash@id                           # apply a specific stash
git stash drop stash@id                            # remove a stash

# time travelling

git checkout <hash>                                # view previous commit
git checkout HEAD~x                                # view commit x commits before head
git checkout HEAD <file>                           # undo changes and go back to the HEAD state.
OR
git checkout -- <file> <file>

git restore <file>                                 # undo changes to HEAD
git restore --source HEAD~x <file>                 # restore to a particular commit. HEAD~x can be replaced with a hash.
git restore --staged <file>                        # unstage changes

git reset --hard HEAD                              # reset all files back to last commit state
git reset --hard <hash>                            # reset to a specific commit. get id from log. Changes are lost.
git reset <hash>                                   # reset to a specific commit. Commits are lost, changes are not - they remain in working directory.

git revert <hash>                                  # creates new commit, undoes changes from previous commit.


git remote -v                                      # list remotes assigned to repo
git remote add <name> <url>                        # add remote
git remote remove <name>                           # remove remote
git remote rename <old> <new>                      # rename remote
```
