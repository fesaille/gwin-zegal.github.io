# GIT

## Configuration

The configuration is made out of [four files](https://git-scm.com/docs/git-config#FILES):

- `$(prefix)/etc/gitconfig`
- `$XDG_CONFIG_HOME/git/config`
- `~/.gitconfig`
- `$GIT_DIR/config`

## Pull request

### Write a pull request

https://github.blog/2015-01-21-how-to-write-the-perfect-pull-request/


https://stackoverflow.com/questions/14680711

https://stackoverflow.com/questions/29049650


Switch branches or restore working tree files


```terminal
git checkout master
git checkout -b mybranch
```

`git remote` manage the set of repositories ("remotes") whose branches you track.
```terminal
git remote -v
# If upstream is not configured, add the upstream route
git remote add upstream /url/original/repo

git fetch upstream

# reset master to upstream/master
git checkout master
git reset --hard upstream/master
git push --force

  y--y--y (mybranch)
 /
z--z--z   (master, upstream/master, origin/master)

# replay the patches (even they are rejected for now) on top of master
git checkout mybranch
git rebase master
git push -u origin mybranch

        y'--y'--y' (mybranch, origin/mybranch)
       /
z--z--z   (master, upstream/master, origin/master)
```

## Submodules

### Commands

`status` prints the SHA1 status of checked submodules. Prefixed with:

- **-** if the submodule is not initialized
- **+** in case of conflicts between current subdmodule and the index of the containing directory
- **U** in case of merge conflicts 



#### Remove a submodule

A submodule can be deleted by running `git rm <submodule path> && git commit`. `$GIT_DIR/modules/<name>` delete the submodule completly. Util then, deletion can be undone using `git revert`.

Alternative method:

Remove the submodule entry from .git/config
```
git submodule deinit -f path/to/submodule
```

Remove the submodule directory from the superproject's .git/modules directory
```
rm -rf .git/modules/path/to/submodule
```

Commit the changes
```
 git commit-m "Removed submodule "
```



Remove the entry in .gitmodules and remove the submodule directory located at path/to/submodule
```
git rm -f path/to/submodule
```

## Cherry pick from another repository

First the other repository source must be added to the remote list
```
git remote add other https://other.url/repository.git
git fetch other
```

Then use [`git cherry-pick`](https://git-scm.com/docs/git-cherry-pick)
