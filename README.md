# Git Crash Course

## Commands reference
```
git clone https://github.com/varbanandreev/git-crash-course.git
git config --local user.name "Git Workshop"
git config --local user.email "git@workshop.com"
git add .gitignore
git commit -m "Add aws_credentials to gitignore"
git add new_file.txt
git add .gitignore
git commit -m "Add new file"
```

```
git revert --no-commit <commit-hash>
git reset HEAD .gitignore
git revert --continue
git checkout -- .gitignore
```

```
git add file.txt
git commit -m "Add empty file"
git add file.txt
git stash save "Update file.txt"
git stash pop
git add file.txt
git commit --amend
git reset --soft <commit-hash>
```

## Challenge 1
- Clone the repository locally.
- Change your **local** user name for this repository to "Git Workshop".
- Change the **local** user email address for this repository to "git@workshop.com".
- Create a new empty text file in the repo and name it "new_file.txt".
- Create another text file and name it "aws_credentials.txt". This file will contain sensitive information - write the text below in this file:
```
[default]
aws_access_key_id=AKIAIOSFODNN7EXAMPLE
aws_secret_access_key=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```
The git status should show the newly created files as untracked files.
- Add "aws_credentials.txt" to the .gitignore.
- Commit the changes made to the .gitignore file only. Name the commit "Add aws_credentials to gitignore". <br />
Now git status should only show the "new_file.txt".
- Create a new empty text file and name it "ignore_file.txt".
- Add "ignore_file.txt" to the .gitignore.
- Open your "new_file.txt" and write something in it. Save and close the file.
- Stage your changes to both files and commit them with the message "Add new file". <br />
Now git status shouldn't show anything. <br />
Your log should have "Git Workshop" as the commit author.

## Challenge 2
- Let's imagine that we've made a mistake in our last commit - we shouldn't have committed the new_file.txt changes and we need to revert them.
- But we need to keep the changes to the .gitignore file.
- This can be done with the ```git revert``` command, using the ```--no-commit``` option and passing the commit hash of the last commit.
- Once you execute the command with this option, git will not directly commit the reverted changes, but will only stage them.
- Now you must un-stage the .gitignore changes and continue with the revert by executing ```git revert --continue```.
- Name your commit "Revert new_file.txt only". <br />
Now your git log should display your new commit as the most recent one.
- As a final step, undo the changes to the .gitignore that you just un-staged. <br />
Now your git status shouldn't show anything.

## Challenge 3
- Create a new empty text file and name it "file.txt". Stage and commit the file with a commit message "Add empty file".
- Now, let's experiment with the stash functionality. Open "file.txt" and write something in it. Save and close the file. Stage your changes and stash them.
- You can include a message for your stashed changes by using ```git stash save "<name>"```. Write "Update file.txt" for your stash message.
- Executing ```git stash list``` should show something like: **stash@{0}: On master: Update file.txt**
- Apply your stashed changes using the ```git stash pop``` command. You can use ```git stash list``` again to confirm that your stash is now empty.
- Now, let's include the unstashed changes by adding them to the last commit, using the amend option. You must first stage your changes before proceeding with the amend.
- Change the commit message to "Add file". <br />
Your log should now show the "Add file" commit at the top, and the "Add empty file" commit should be gone.
- The last thing you will do is to reset your last commit, but keeping the changes staged. This can be done by using ```git reset --soft <commit-hash>```.
- Remember, reset affects all commits from the tip to the passed commit. If you want to reset the last commit, you must pass the hash of the commit before it.
- Your log after resetting the commit should no longer contain the "Add file" commit.
- Your status should show a staged file.txt.

## Bonus Challenge
- Use the reflog to rewind your repo's state to the point right after Challenge 2 and before Challenge 3. From this state, create a new branch named **bonus-challenge**. Verify that the branch history looks something like:
  - (HEAD -> bonus-challenge) Revert new_file.txt only
  - Add new file
  - Add aws_credentials to gitignore
  - Initial commit
