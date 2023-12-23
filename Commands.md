# Git Commands

Undo commit and keep all files staged:
```
git reset --soft HEAD~
```

Undo commit and unstage all files:
```
git reset HEAD~
```

Undo the commit and completely remove all changes:
```
git reset --hard HEAD~
```

Delete local branch:
```
git branch -d <branch>
```

Delete remote branch:
```
git push origin -d <branch>
```

Generate patch file:
```
git diff > some-changes.patch
```

Apply patch file:
```
git apply /path/to/some-changes.patch
```

Cherry pick just the files:
```
git cherry-pick -n <commit>
```
