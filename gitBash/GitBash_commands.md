## Git Tags

Git Tags are named references that point to a specific commit in a Git repository. They are commonly used to mark important milestones such as releases, versions, hotfixes, or production deployments.

Unlike branches, tags are typically static and do not move automatically when new commits are added.

| Category | Action | Command |
|----------|----------|----------|
| Create & View Tags | View commit history (short format) | `git log --oneline` |
| Create & View Tags | Create a tag on the latest commit of branch `dev` | `git tag ongoing dev` |
| Create & View Tags | Create an annotated tag on a specific commit | `git tag -a <tag_name> -m "<message_for_commit>" <commit_hash>` |
| Create & View Tags | List all tags | `git tag` |
| Push | Push all local tags to remote | `git push --tags` |
| Delete Tags | Delete a local tag | `git tag -d ongoing` |
| Delete Tags | Delete a remote tag | `git push origin :<tag_name>` |
| Update Tags | Move/update an existing tag to another commit | `git tag -f <tag_name_to_update> <hash_code_new_commit>` |
| Update Tags | Push updated tag (may be rejected if tag already exists remotely) | `git push origin v2.0` |
| Update Tags | Force update tag on remote | `git push --force origin v2.0` |


## Git Branch

A Git Branch is an independent line of development within a Git repository. It allows developers to work on new features, bug fixes, experiments, or releases without affecting the main codebase.

| Category | Action | Command |
|----------|----------|----------|
| View Branches | View local branches | `git branch` |
| View Branches | View local and remote branches | `git branch -a` |
| Create Branches | Create a new branch | `git branch <branch_name>` |
| Create Branches | Create branch `prod` | `git branch prod` |
| Push Local Branch to Remote | Push local branch to remote repository | `git push -u origin <branch_name>` |
| Push Local Branch to Remote | Push branch `prod` to remote | `git push -u origin prod` |
| Switch (Checkout) Branches | Switch to an existing branch | `git checkout <branch_name>` |
| Switch (Checkout) Branches | Switch to branch `prod` | `git checkout prod` |
| Create and Switch Branch | Create and switch to a new branch | `git checkout -b <branch_name>` |
| Create and Switch Branch | Create and switch to `feature-login` | `git checkout -b feature-login` |
| Delete Branches | Delete a local branch | `git branch -d <branch_name>` |
| Delete Branches | Delete local branch `prod` | `git branch -d prod` |
| Delete Branches | Force delete a local branch | `git branch -D <branch_name>` |
| Delete Branches | Force delete local branch `prod` | `git branch -D prod` |
| Delete Remote Branch | Delete a remote branch | `git push <remote_repo_name> --delete <branch_name>` |
| Delete Remote Branch | Delete remote branch `prod` | `git push origin --delete prod` |
| Merge Branches | Merge a branch into the current branch | `git merge <branch_name>` |
| Merge Branches | Merge branch `dev` into current branch | `git merge dev` |
| Rename Branch | Rename a branch | `git branch -m <old_name> <new_name>` |
| Rename Branch | Rename `prod` to `production` | `git branch -m prod production` |
| Recover Deleted Branch | View reflog history to recover deleted branch | `git reflog` |

### Branch Commands Cheat Sheet

| Command | Purpose |
|----------|----------|
| `git branch` | View local branches |
| `git branch -a` | View local and remote branches |
| `git branch <branch_name>` | Create a new branch |
| `git push -u origin <branch_name>` | Push local branch to remote |
| `git checkout <branch_name>` | Switch to an existing branch |
| `git checkout -b <branch_name>` | Create and switch to a new branch |
| `git branch -d <branch_name>` | Delete local branch |
| `git branch -D <branch_name>` | Force delete local branch |
| `git push origin --delete <branch_name>` | Delete remote branch |
| `git merge <branch_name>` | Merge branch into current branch |
| `git branch -m <old_name> <new_name>` | Rename branch |
| `git reflog` | View reflog and recover deleted branches |
