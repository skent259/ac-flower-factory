---
id: git
title: Git and Github
---


## Push

```bash
git push --set-upstream <remote> <local branch> # creates remote branch with same name
```

## Reset/Revert/Checkout

The best reference is [Atlassian Git Reset/Revert/Checkout](https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting)

The 3 trees are:
1. working
2. staging
3. commit history

* `checkout` works on the HEAD pointer only, so switching branches or changing files
* `reset` works on both HEAD and the branch pointer, three flavors `--soft`, `--mixed (default)`, `--hard`.

### Reset file to commit

```bash
git checkout <hash> -- <file1> <file2> # Reset files to a certain hash, defaults to head
```

# Cherry-Pick

`git cherry-pick` is used when you want to selectively apply a commit to your current branch.

`git cherry-pick -x <commit-hash>` - The `-x` option is to add a message saying which commit was applied. The commit hash is the commit you wish to apply to the current branch.

# Stashing

* `git stash` - runs `git stash push` and saves a local snapshot
* `git stash show` - shows the modifications of the most recent stash..
* `git stash list` - shows the stack of stashes of changes made.
* `git stash pop` - defaults to applying the top stash on the stack. Inverse of `git stash push`

# Clean

* `git clean -n` - get rid of untracked, dry run
* `git clean -f` - actually remove them

# Diff

* `git diff` - shows differences of the working tree and HEAD
* `git diff --staged`  - shows differences of the staged files and HEAD

# Tags

* Git tag

# Branches

* `git checkout -b <new-branch-name> <start-point>`
* `git fetch <remote> <branch>` - leaving off the branch gets all branches

# Log

With the zsh aliases.

* `glol` - view all the changes
* `glola` - view all, even included the fetched branches
* `glol master..upstream/master` - see all the commits between master and the upstream/master branch.

# Show

Show a particular git object, tree or commit

```bash
git show # shows most recent commit
git show -5 <filename> # Last 5 commits that changed a particular file
git show --name-only <commit-hash> # see only the files changed in the commit
```

# Merge

`git merge origin/master`

# Pull

`git pull`

# Fetch

## Refspec

[The Internal Refspec](https://git-scm.com/book/en/v2/Git-Internals-The-Refspec)

The refspec looks like this

`fetch = +refs/heads/master:refs/remotes/origin/master`

This says that with fetch, by default will only update the master ref to. The format is `<src>:<dst>`, in which we look on the remote server for `<src>`, and track them locally in `<dst>`. `+` says if it's not a fast forward, do it anyway.

Hence, for an example command (the first is short for the second)

```bash
git fetch origin master:refs/remotes/origin/master
git fetch origin refs/heads/master:refs/remotes/origin/master
```

Looks on the `origin` remote, for a branch called `master`, and writes the hashcode into the file `.git/refs/remotes/origin/master`. That is, it's tracked by `origin/master`.

We can also look on the remote server for checking out a certain pull request. In order to see all the refs on a remote server, we can run,

`git ls-remote <remote>`

##  Common Workflows

### Working on common repository

1. Make a fork on Github and clone it locally
2. Setup the original as a remote repository. origin should be your copy of it
    - `git remote add upstream https:github.com/user/project.git`
* Update the repository occasionally
    - `git fetch upstream`

Other helpful commands

```bash
glola # In Zsh alias to see log with everything in refs
```

### Examining a Pull Request snapshot

Method 1 is probably the easiest

1. Create branch `pr40` locally from pull request refspec on the remote server upstream
    - `git fetch upstream pull/40/head:pr40`
2. Checkout the pr
    - `git checkout pr40`

Other helpful commands

```bash
git ls-remote <remote> # view all refspecs on remote server
```

Method 2 is to pull directly from other person's branch.
The other way to work on the project is to pull changes from the user's copy of the repo.

1. Fork the repo
2. Clone the repo
3. Create some branch to hold the pull request
4. Pull the merge request branch into your local repository on the newly created branch

### Updating a Pull Request

Note that you must have proper permission to push onto someone else's branch. The forks of the original repository will copy the permissions of the original repo. Otherwise you could make a pull request to someone else's forked repo in order for the changes to be tracked on the original pull request.

1. Push the changes onto their forked copy, with the same branch name.

### Making a Pull Request

1. Make a fork of the repository

### Working with Dotfiles

[Dotfile Managment Tutorial](https://www.atlassian.com/git/tutorials/dotfiles)

The setup steps are creating a bare repository with the `$HOME` directory is the working tree.

```bash
git init --bare $HOME/.cfg
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'
config config --local status.showUntrackedFiles no
echo "alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'" >> $HOME/.bashrc
```

The usage of this is as follows:

```bash
config ls-files # See files under git control
config status # everything else works normally
config add path_to_file 
config remote -v
config push
```

### Managing a Web Server on a live server

[Git to Manage Live Web Site](https://gist.github.com/Nilpo/8ed5e44be00d6cf21f22)

Might be worth looking into to set up the SGSA website this way.

## Merge Conflicts

## Undoing previous commit

*  `git commit --ammend` - makes another commit, but modifies the previous commit

