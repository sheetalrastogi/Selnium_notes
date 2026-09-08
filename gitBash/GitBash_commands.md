**Verify SSH Authentication with GitHub**

- Tests SSH connectivity and authentication with GitHub.
	ssh -T git@github.com

- Clone a Repository Using SSH
	git clone git@github.com:<owner>/<repository>.git
	eg. git clone git@github.com:sheetalrastogi/Selnium_notes.git

**Connect Local Repository to Remote Repository**

```text
# Add remote repository
	git remote add origin <repository_url>

# Example
	git remote add origin https://github.com/user/repo.git
	
	
# View configured remotes
	git remote -v

# View remote names
	git remote
```

**Clone Remote Repository**

```text
# Clone using HTTPS
	git clone <repository_url>

# Clone using SSH
	git clone git@github.com:<owner>/<repository>.git
```


**Push Changes to Remote Repository**

```text
# Push current branch
	git push

# Push specific branch
	git push origin <branch_name>

# Push and set upstream tracking
	git push -u origin <branch_name>

# Push all branches
	git push --all

# Force push
	git push --force

# Dry run
	git push --dry-run

# Atomic push
	git push --atomic origin <branch_name>

# Prune deleted references
	git push --prune
```


**Fetch Changes from Remote Repository**

```text
# Fetch all remote changes
	git fetch

# Fetch specific remote
	git fetch origin
```

**Merge Fetched Changes**

```text
# Merge Fetched changes
	git merge <branch_name>

	Example:  git merge origin/master

```


**Pull Changes**

```text
# Fetch + Merge
	git pull

	Example:  git pull origin master
```


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
