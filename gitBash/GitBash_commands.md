# View commit history (short format)
git log --oneline

# Create a tag on the latest commit of branch 'dev'
git tag ongoing dev

# Create an annotated tag on a specific commit
git tag -a <tag_name> -m "<message_for_commit>" <commit_hash>

# List all tags
git tag

# Push all tags to remote repository
git push --tags

# Delete a local tag
git tag -d ongoing

# Delete a remote tag
git push origin :<tag_name>

# Move/update an existing tag to another commit
git tag -f <tag_name_to_update> <hash_code_new_commit>

# Push updated tag
git push origin v2.0

# Force update tag on remote
git push --force origin v2.0
