# Guide to Git

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
   - `git push -u origin <branch-name>`: Push current branch to remote branch, and set remote branch as upstream (Will be able to git push withuot specifying  `origin <branch-name>`)

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

---
---

## Extra - Miltiple Git User & Multiple Github Account SSH Credential

### 1. **Design Directories**

Set up separate directories for your work and personal profiles to keep configurations organized.

- **Work directory**: `~/projects/work`
- **Personal directory**: `~/projects/personal`

Inside each directory, create a `.gitconfig` file with the profile-specific settings:

#### **Work configuration (`~/projects/work/.gitconfig`)**

```ini
[user]
  name = Your Work Name
  email = your.work.email@example.com
```

#### **Personal configuration (`~/projects/personal/.gitconfig`)**

```ini
[user]
  name = Your Personal Name
  email = your.personal.email@example.com
```

---

### 2. **Modify Global `~/.gitconfig`**

Modify your global `~/.gitconfig` to include profile-specific configurations based on the directory you're working in:

```ini
[includeIf "gitdir:~/projects/work/"]
  path = ~/projects/work/.gitconfig

[includeIf "gitdir:~/projects/personal/"]
  path = ~/projects/personal/.gitconfig
```

This setup ensures that when you are working inside the `work` or `personal` directories, Git uses the correct profile (name and email).

---

### Step 3 Onwards - Multiple GitHub SSH Credentials

---

### 3. **SSH Configuration**

Configure SSH to use different SSH keys for your work and personal Git accounts using aliases in `~/.ssh/config`.

#### 3.1. **Generate SSH Keys for Each Profile**

Generate a unique SSH key for each account:

- **Work**:

  ```bash
  ssh-keygen -t rsa -C "your.work.email@example.com" -f ~/.ssh/id_rsa_work
  ```

- **Personal**:

  ```bash
  ssh-keygen -t rsa -C "your.personal.email@example.com" -f ~/.ssh/id_rsa_personal
  ```

#### 3.2. **Modify `~/.ssh/config`**

Configure the SSH aliases to tell SSH which key to use for each account:

- Open or create `~/.ssh/config` and add the following:
  
  ```ini
  # Work GitHub account
  Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work

  # Personal GitHub account
  Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_personal
  ```

This configuration ensures that SSH uses the correct identity file (SSH key) for each account based on the alias (`github-work` or `github-personal`).

---

### 4. **Verify SSH Connection**

To verify that your SSH keys are correctly configured for each account, use the following commands:

- **For Work**:

  ```bash
  ssh -T git@github-work
  ```

- **For Personal**:

  ```bash
  ssh -T git@github-personal
  ```

If successful, you should receive a message indicating that you've successfully authenticated.

---

### 5. **Using SSH Aliases to Clone Repositories**

When cloning repositories, use the SSH alias corresponding to the account you want to use:

- **For Work**:

  ```bash
  git clone git@github-work:username/work-repo.git
  ```

- **For Personal**:

  ```bash
  git clone git@github-personal:username/personal-repo.git
  ```

This ensures that the correct SSH key is used for each profile when interacting with GitHub.

---
