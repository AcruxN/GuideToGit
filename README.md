# demoGit

Demo repo for git.

## Git Commands (Local)

1. **Setup and Configuration**

   - `git config --global user.name "Your Name"`: Set your name.
   - `git config --global user.email "your.email@example.com"`: Set your email.

2. **Creating Repositories**

   - `git init`: Initialize a new Git repository.
   - `git clone <repository-url>`: Clone an existing repository.

3. **Basic Commands**

   - `git status`: Check the status of your working directory.
   - `git add <file>`: Stage changes to a file.
   - `git add .`: Stage all changes in the current directory.
   - `git commit -m "Commit message"`: Commit staged changes with a message.
   - `git log`: View the commit history.
   - `git diff`: Show differences between changes in the working directory and the last commit.
   - `git reset <file>`: Unstage a file (keep changes).

4. **Branching and Merging**

   - `git branch`: List branches in the repository.
   - `git branch <branch-name>`: Create a new branch.
   - `git checkout <branch-name>`: Switch to a different branch.
   - `git merge <branch-name>`: Merge a branch into the current branch.

5. **Rebasing and Stashing**

   - `git rebase <branch>`: Reapply commits on top of another base tip.
   - `git stash`: Temporarily save changes without committing.
   - `git stash apply`: Apply stashed changes.

6. **Undoing Changes**
   - `git checkout -- <file>`: Discard changes in a file.
   - `git revert <commit>`: Create a new commit that undoes a previous commit.
   - `git reset --hard`: Reset the working directory to the last commit (WARNING: This will delete uncommitted changes).

## Git Commands (Interacting with GitHub)

1. **Pushing and Pulling**

   - `git push origin <branch-name>`: Push local changes to the remote repository.
   - `git pull origin <branch-name>`: Fetch and merge changes from the remote repository.

2. **Managing Remote Repositories**

   - `git remote -v`: List remote repositories.
   - `git remote add <name> <repository-url>`: Add a new remote repository.
   - `git remote remove <name>`: Remove a remote repository.
   - `git fetch <remote>`: Download changes from the remote repository without merging.

3. **Working with Tags**

   - `git tag <tag-name>`: Create a new tag.
   - `git push origin <tag-name>`: Push a tag to the remote repository.
   - `git tag -d <tag-name>`: Delete a local tag.

4. **Collaboration**

   - `git request-pull <start> <url> <end>`: Generate a request to pull changes from a specific range of commits.
   - `git cherry-pick <commit>`: Apply the changes from a specific commit.

5. **GitHub-Specific Commands (Using GitHub CLI)**
   - `gh repo create`: Create a new GitHub repository.
   - `gh repo clone <repository-name>`: Clone a GitHub repository.
   - `gh pr create`: Create a pull request.
   - `gh pr merge <pr-number>`: Merge a pull request.
