Git squash branch to one commit:
git checkout feature_branch
git reset --soft <commit where branch is going from mother branch>
git add -A && git commit -m "commit message goes here"
