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
