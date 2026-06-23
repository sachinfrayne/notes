# github

## worktrees

Work on a separate branch without disturbing your current working directory.

### create a worktree from a remote branch

```bash
git worktree add ../my-repo-branch -b new-branch-name origin/main
```

### copy a file into the worktree, commit, and push

```bash
cp path/to/file ../my-repo-branch/path/to/file
cd ../my-repo-branch
git add path/to/file
git commit -m "my commit message"
git push -u origin new-branch-name
```

### remove the worktree when done

```bash
git worktree remove ../my-repo-branch
```
