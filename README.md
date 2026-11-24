# Git Branching and Merging Demo

Concepts: `git branch`, `git checkout` / `git switch`, `git merge`, merge conflict.

## Part 1 - Feature branch and merge
```bash
git init -b main
git add . && git commit -m "Initial commit"
git switch -c feature-header          # create + switch (old way: git checkout -b feature-header)
# edit index.html + style.css to add a header
git add . && git commit -m "Add header to the page"
git switch main                       # old way: git checkout main
git merge feature-header --no-ff -m "Merge branch 'feature-header' into main"
```

## Part 2 - Merge conflict (same line changed in two branches)
```bash
git switch -c feature-footer-a        # change footer line -> "Branch A"
git commit -am "Change footer text in feature-footer-a"
git switch main
git switch -c feature-footer-b        # change SAME footer line -> "Branch B"
git commit -am "Change footer text in feature-footer-b"
git switch main
git merge feature-footer-a            # fast-forward, no problem
git merge feature-footer-b            # CONFLICT in index.html
```
Conflict markers shown in the file:
```
<<<<<<< HEAD
    <p>Footer: Copyright 2026 - Branch A</p>
=======
    <p>Footer: Made with love - Branch B</p>
>>>>>>> feature-footer-b
```

## Resolving the conflict
1. Open `index.html`, keep the final text you want, delete the `<<<<<<<`, `=======`, `>>>>>>>` lines.
2. `git add index.html`
3. `git commit` (completes the merge)

Final footer: `Footer: Copyright 2026 - Made with love`

## Useful commands
```bash
git branch            # list branches
git log --oneline --graph --all
git branch -d feature-header   # delete merged branch
```
