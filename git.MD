## Some usefull git commands:


* Git squash branch to one commit:
``` bash
git checkout feature_branch
git reset --soft <commit where branch is going from mother branch> # This will move local branch pointer also
git add -A && git commit -m "commit message goes here"
```
