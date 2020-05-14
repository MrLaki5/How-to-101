## Some usefull git commands:


* Git squash branch to one commit:
``` bash
git checkout feature_branch
git reset --soft <commit where branch is going from mother branch> # This will move local branch pointer also
git add -A && git commit -m "commit message goes here"
```

* Add git tree in git configuration:
``` bash
[alias]
lg1 = log --graph --abbrev-commit --decorate --date=relative --format=format:'%C(bold blue)%h%C(reset) - %C(bold green)(%ar)%C(reset) %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)' --all
tree = !"git lg1"
```