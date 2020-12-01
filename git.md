# GIT

## table of content

- [Vocabulary](#vocabulary)
- [Local configuration](#local-configuration)
- [Initialization](#initialization)
- [Fork](#Fork)
- [Squash][#squash]

## Vocabulary

* `Ahead` commit on local repository but not on remote one
* `Behind` commit on remote repository but not on local one

## Local configuration

```bash
git config --list
git config user.name @oliviergranoux
git config user.email 72553159+oliviergranoux@users.noreply.github.com
```

## Initialization

```bash
# initialize local repository
git init

# add file
echo "# jekyll-gallery" >> README.md
git add README.md
git commit -m "first commit"

# associate local repository to remote repository
git remote add origin https://github.com/oliviergranoux/jekyll-gallery.git
git branch -M master

##on first push
git push -u origin master # -u is short for --set-upstream
```

## Fork

```bash
# listing of remote repositories
git remote -v

# clone the remote repository jekyll-gallery to the local repository olivier-jekyll-gallery (which is not created yet)
git init ##needed?
git clone https://github.com/oliviergranoux/jekyll-gallery.git olivier-jekyll-gallery 

# add needed remote repositories
git remote add origin https://github.com/oliviergranoux/olivier-jekyll-gallery.git
git remote add origin-forked https://github.com/oliviergranoux/jekyll-gallery.git

# disable push commands on the remote repository `origin-forked`
# see http://sushihangover.github.io/git-set-up-a-fetch-only-remote/
git remote set-url --push origin-forked DISABLE

# link remote repositories ... (?!?)
git pull origin-forked master
git branch -M master
git branch --set-upstream-to=origin/master master
git push -u origin master
```

## How to update a forked repository

See https://medium.com/@topspinj/how-to-git-rebase-into-a-forked-repo-c9f05e821c8a

1. Add the remote (original repo that you forked) and call it “upstream”

```bash
git remote add upstream https://github.com/original-repo/goes-here.git
```

2. Fetch all branches of remote upstream

```bash
git fetch upstream
```

3. Rewrite your master with upstream's master using git rebase.

```bash
git rebase upstream/master
```

4. Push your updates to master. You may need to force the push with `--force`.

```bash
git push origin master --force
```

## Squash

> crush or squeeze (something) with force so that it becomes flat, soft, or out of shape. (Google Translate)

See https://www.ekino.com/articles/comment-squasher-efficacement-ses-commits-avec-git

1. Get the identifier of the commit before the group of commit to squash

2. Execute the squash with this identifier,

```bash
git rebase -i a10c90739ab6ea94123ae39e0499af8cddf8b434
```

3. Put `s` ou `squash` in front of lines to consolidate except the first one which is the oldest commit,

4. Confirm by changing the message of the new commit if needed,

5. Change the commits par le new one.

```bash
git push origin master --force
```


## Others

* update git on windows: `git update-git-for-windows`

* modify last commit

```bash
# add staged files and set new message
git commit --ammend -m "new message of last commit"
# and without change the message of the commit
git commit --no-edit
```

```bash
git log origin/master..HEAD HEAD.. origin/master
```
