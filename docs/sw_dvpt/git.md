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



### Remove a submodule

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

### Updating submodule url and branch

The [submodule configuration](https://git-scm.com/docs/git-config#Documentation/git-config.txt-submoduleltnamegturl) can be displayed with `git config`:
```terminal
git config -l
```
A specific config file can be given to `git config` with the `--file` [flag](https://git-scm.com/docs/git-config#Documentation/git-config.txt---fileconfig-file):
```terminal
git config -l --file=.gitmodules
```
Url, branch and [other parameters](https://git-scm.com/docs/git-config#Documentation/git-config.txt-submoduleltnamegturl) can be configured via `git config`
```terminal
git config --file=.gitmodules submodule.<submodule_name>.url <git@github.com:username/repository.git>
git config --file=.gitmodules submodule.<submodule_name>.branch <branch_name>
```
Synchronization adn update of the submodules are done with:
```terminal
git submodule sync
git submodule update --init --recursive --remote
```
## Cherry pick from another repository

First the other repository source must be added to the remote list
```
git remote add other https://other.url/repository.git
git fetch other
```

Then use [`git cherry-pick`](https://git-scm.com/docs/git-cherry-pick)

## Git flow

From [Scott Chacon blog](http://scottchacon.com/2011/08/31/github-flow.html):

> - To work on something new, create a descriptively named branch off of master
> - Commit to that branch locally and regularly push your work to the same named branch on the server
> - When you need feedback or help, or you think the branch is ready for merging, open a pull request
> - After someone else has reviewed and signed off on the feature, you can merge it into master


## Platform specific 

### Github

#### Change the repository language detection

[`.gitattributes`](https://git-scm.com/docs/gitattributes/2.9.5) s used for the files you want to override using the `linguist-documentation`, `linguist-language`, `linguist-vendored`, `linguist-generated` and `linguist-detectable` attributes. 

Installation <badge-doc href='https://github.com/github/linguist#installation', logo='github'></badge-doc> is performed with gem:
```bash
gem install github-linguist
```
