## Git Commands

## Git Reset

- **git reset --soft HEAD~1** : This command will reset the Commit history to the previous commit and the changes will be in the staging area.
- **git reset --mixed HEAD~1** : This command will reset the Commit history to the previous commit and the changes will be in the working directory.
- **git reset --hard HEAD~1** : This command will reset the Commit history to the previous commit and the changes will be lost.
- In soft and mixed reset, the changes will be in the staging area and working directory respectively. So, we can add the changes to the staging area and commit them again.
- In hard reset, the changes will be lost. So, we can't get the changes back.
- In soft and mixed reset, If we have the old commit id, we can get the commit history. But in hard reset, we can't get the commit history.

## Git Revert

- **git revert <commit-id> : It will preserve the commit history and the changes will be deleted.

## Git Stash

- **git stash** : It will save the changes in the stash and the working directory will be clean.
- **git stash list** : It will list all the stashes.
- **git stash save "message"** : It will save the changes in the stash with the message.
- **git stash show stash@{0}** : It will show the changes in the stash with the stash id=0.
- **git stash pop stash@{0}** : It will add the changes from the stash to the working directory and the stash will be deleted.
- **git stash apply stash@{0}** : It will add the changes from the stash to the working directory and the stash will be preserved.
- **git stash drop stash@{0}** : It will delete the stash with the stash id=0.

## .gitignore file

.gitignore file is used to ignore the files and folders in the git repository. We can add the files and folders in the .gitignore file and commit it. Then, the files and folders will be ignored in the git repository.
