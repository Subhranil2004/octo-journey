### Stage
`git add <path>` : path can be a file or folder. Ex: `git add notes/`, `git add media.html`, `git add .`

### Commit
`git commit -m "Title" -m "Description..."`, or 
`git commit` then in editor:
```plaintext
commit message

detailed desc...
```

- `git commit --amend -m "new commit msg"` : amends prev commit

### Restore

- `git restore --staged <path>` 
- `git restore .` : to restore contents of all ***unstaged and tracked*** files to prev commit state. 
  - If staged, first run the prev cmd, then this.
  - If untracked, do manually

### .gitignore 

For ignoring globally `git ignore --global core.excludesfile <file>`
> If your notes directory is being tracked even though it's listed in your .gitignore, it's likely because Git started tracking it before you added it to .gitignore. Git does not ignore files that are already being tracked. To stop tracking the notes directory:

1. Remove the directory from the index (but keep the files locally):
```bash
git rm -r --cached notes/
```
2. Commit the change


### Delete
- `git rm <path>` : deletes and stages dir/file

### Rename
- `git mv <file>` : renames (del prev file create new file) and stages

### Log
- `git log` : `--oneline` shows logs in one line

### Reset
`git reset --hard <hash>` : resets the working directory and index to the specified commit, but keeps changes in the working directory as modified.  
The `--hard` flag discards all changes as well.

### Rebase
play around with the commits in the history.
- `git rebase -i root` : interactive rebase
- `git rebase -i HEAD~n` : interactive rebase for the last n commits
in editor:
```plaintext
pick <hash> <msg>
pick <hash> <msg>   
pick <hash> <msg>
```
- `pick` : keep the commit
- `edit` : edit the commit
- `squash` : combine the commit with the previous one keeping the commit message
example:
```plaintext
pick    commit1 Add feature
squash  commit2 Fix typo in feature
pick    commit3 Add tests for feature
```
> **WARNING**  
> if commit1 and commit2 are not related, it may cause conflicts.

commit2 will be squashed into commit1 (changes and message are merged).
commit3 will remain separate — not combined with commit1 or commit2.

- `fixup` : same as `squash`, but discard the commit message of the commit being squashed

### Branch
- `git branch` : list branches and shows the current branch
- `git switch -c <name>` : create and switch to a new branch
- `git switch <name>` : switch to a branch, if it exists, if not, it will throw an error
- `git merge <branch>` : merge the specified branch into the current branch

- `git branch -d <name>` : delete a branch

### Stash
- `git stash push -u -m "custom-name"` : save the current changes in a custom-named stash. 
  - `-u` : include untracked files
  - `-a` : include all files (tracked, untracked and ignored)
  - `-m` : custom name for the stash
- `git stash list` : list all stashes
- `git stash apply <stash-name>` : apply a specific stash
- `git stash pop <stash-name>` : apply a specific stash and delete it
- `git stash branch <branch-name> <stash-name>` : create a new branch from a specific stash and apply it
- `git stash drop <stash-name>` : delete a specific stash
- `git stash clear` : delete all stashes

> any command without a stash name will apply the most recent stash

### Remote
- `git remote add <name> <url>` : add a remote repository
```shell
git remote add origin <url.git>
``` 
- `git remote -v` : list all remotes

- `git remote rename <old-name> <new-name>` : rename a remote repository
- `git remote remove <name>` : remove a remote repository
- `git remote set-url <name> <url>` : change the URL of a remote repository

- `git fetch <remote_url>` : fetch changes from a remote repository

### Push
- `
- `git push -u <remote> <branch>` : push changes to a remote repository
  - `-u` or `--set-upstream` : set the upstream branch for the current branch if pushing for the first time
```shell
git push -u origin main
```

- `git push --all` : push all branches to the remote repository
> WARN: if remote isnt setup for all branches, it will throw an error

### Pull
- `git pull <remote> <branch>` : fetch and merge changes from a remote repository

*******

## Make changes to a new branch (other than main) in the forked repo:

> [!TIP]  
> Useful for open-src contributions
- `git clone -b <branch_name> <fork_url>`

  Ex: `git clone -b ethnicity-classification https://github.com/Subhranil2004/DL-Simplified.git`

- Add original repo as upstream
  Ex: `git remote add upstream https://github.com/abhisheks008/DL-Simplified.git`

- Verify the branch u are updating
  `git branch` if not then, `git checkout -b <branch-name>` 
- Do local changes
  `git add .` and `git commit -m "..."`
- Pull the changes from the original repo
  `git pull upstream main` when `main` is the main branch of action in orig repo

- Push
  `git push origin <branch-name>`

  If errors come at this stage:
```sh
PS E:\GSSoC24\DL-Simplified\Ethnicity Classification of Asian People> git push origin ethnicity-classification
To https://github.com/Subhranil2004/DL-Simplified.git
 ! [rejected]        ethnicity-classification -> ethnicity-classification (fetch first)
error: failed to push some refs to 'https://github.com/Subhranil2004/DL-Simplified.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```
Do `git pull` then repeat the last cmd.
Like:
```sh
PS E:\GSSoC24\DL-Simplified\Ethnicity Classification of Asian People> git pull
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), 974 bytes | 21.00 KiB/s, done.
From https://github.com/Subhranil2004/DL-Simplified
   9ba92a4..fa686c1  ethnicity-classification -> origin/ethnicity-classification
Merge made by the 'ort' strategy.
```


******


# Markdown 
> GitHub flavoured

> [!NOTE]
> Useful information that users should know, even when skimming content.

> [!TIP]
> Helpful advice for doing things better or more easily.

> [!IMPORTANT]
> Key information users need to know to achieve their goal.

> [!WARNING]
> Urgent info that needs immediate user attention to avoid problems.

> [!CAUTION]
> Advises about risks or negative outcomes of certain actions.

A reference text [^1] for more info.

[^1]: 1st footnote. https://www.markdownguide.org/basic-syntax/

Another reference [^2] for more info.

[^2]: 2nd footnote. https://www.markdownguide.org/extended-syntax/

[![Image](photo-1747901718331-0e5d361cf5f4.avif)](https://github.com/Subhranil2004/octo-journey) <!-- image link -->

# Special files
- [README.md](README.md) : this file
- [LICENSE](LICENSE) : license file. ***Needs to be at the root of the repo.***
- CODE_OF_CONDUCT.md : code of conduct file. 
- SECURITY.md : security policy file.
- CONTRIBUTING.md : contributing guidelines file.
- SUPPORT.md : support file.
- CODEOWNERS : file to specify who owns the code in the repository.
> Those people will be automatically requested for review when a pull request is made.
> syntax similar to `.gitignore` file.
```plaintext
# CODEOWNERS file example
**/*.js @subhranil2004 
# Subhranil2004 owns all JS files and will be requested for review when a PR is made
docs/ @subhranil2004 @another-user 
# Subhranil2004 and another-user own the docs directory and will be requested for review when a PR is made
```