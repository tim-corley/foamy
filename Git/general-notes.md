# General Notes

## Git Rebase

```
$ git checkout <feature_branch>
$ git rebase master
$ git checkout master
$ git merge <feature_branch>
```

## Keeping A GitHub Fork Updated

### Track
```
$ git remote add upstream git@github.com:thoughtbot/dotfiles.git
```

### Update (From Local Master)
```
$ git fetch upstream
$ git rebase upstream/master
```