
- [Git Configuration](#git-configuration)
- [Git Areas](#git-areas)


## Git Configuration

git config is a command used to configure Git settings—such as name, email, editor, and behavior preferences—either globally (across all repositories for a user) or locally (specific to a single repository).

Git uses configuration files to determine how it should behave for a given user or repository. The git config command is the interface for reading and writing those settings.

configuration files at different levels:

- System-level: Affects all users on the system

- Global-level: Affects all repositories for a single user

- Local-level: Specific to a single repository

Configuration Files

1. System-level Configuration
Location: /etc/gitconfig on Unix-like systems
Applies to: All users on the system
How to set: ```git config --system <key> <value>```

2. Global-level Configuration
Location: ~/.gitconfig or ~/.config/git/config on Unix-like systems
Applies to: All repositories for the current user
How to set: ```git config --global <key> <value>```

3. Local-level Configuration
Location: .git/config in the repository directory
Applies to: Only the current repository
How to set: ` git config --local <key> <value> (or just git config <key> <value>)`

**Viewing Configuration**

To view all configurations and where they're set:

`git config --list --show-origin`

To view a specific configuration value:

`git config <key>`

Common Configuration Settings

**User Information**

Essential for commits:

```
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```


Editor

Set your preferred text editor:
```
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"         # Vim
git config --global core.editor "nano"        # Nano
```
Merge and Diff Tools

Configure merge/diff tools:
```
git config --global merge.tool vimdiff
git config --global diff.tool vimdiff
```
Aliases

Create shortcuts for common commands:
```
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
```
Line Endings

Important for cross-platform work:

#Windows
`git config --global core.autocrlf true`

#Linux/Mac
`git config --global core.autocrlf input`

**Default Branch Name**

Set the default branch name for new repositories:

`git config --global init.defaultBranch main`

Credential Storage

Configure how Git stores credentials:
``` bash
git config --global credential.helper cache  # Temporarily stores in memory
git config --global credential.helper store  # Stores in plaintext file (less secure)
```

**Git Hooks**

Configure hooks directory:

> git config core.hooksPath /path/to/custom/hooks


**SSH Command**

Specify custom SSH command:

>git config --global core.sshCommand "ssh -i ~/.ssh/custom_id"


**Editing Configuration Files Directly**

You can edit configuration files directly:

> git config --global --edit

This opens your global configuration in your default editor.

---

## Git Areas

In Git, there are three main areas that track the state of the files and control the flow of versioning:

1. **Working Directory (Working Tree)**
   - This is actual project folder on disk.Where we make actual changes to code
   - Also called the "untracked" or "modified" area
   - Contains all files in project folder (both tracked and untracked)

    **Files can be in one of three states:**
    - Untracked: New files Git doesn't know about yet
    - Modified: Tracked files that have been changed but not staged
    - Unmodified: Tracked files that haven't changed since last commit

    **Commands that affect this area:**

    Any file modification (editing, creating, deleting)

    `git status` shows changes here

    `git checkout -- <file>` discards changes here

    `git clean` removes untracked files

**2. Staging Area (Index)**

   - An intermediate area between working directory and repository, Also called the "index"
   - A snapshot of what will go into the next commit, Acts as a preview of next commit
   - Allows partial commits. You can commit only part of your changes.
   - Keeps your commit history clean and focused.
   - Changes must be staged before they can be committed
   
**Commands that affect this area:**

`git add` moves changes from working directory to staging

`git reset` (with options) can unstage changes

`git diff --cached` shows changes that are staged

`git rm --cached` removes files from staging (but keeps in working dir)

`git restore --staged <file>` removes file from staging area but keeps changes in working directory.

**3. Git Repository (Git Directory)**

- The .git folder in project root, The actual Git database.
- Contains snapshots of project from past commits.
- HEAD points to the latest commit in current branch.
- Contains all commits, branches, tags, and Git's configuration
- Stores compressed, immutable snapshots of your project
- Commits here are permanent (though can be amended or rebased)

**Contains several sub-areas:**

**Object database:** Stores all commit objects, trees, blobs

**Refs:** Stores pointers to branches and tags

**HEAD:** Pointer to current branch/commit

***Commands that affect this area:***

`git commit` moves changes from staging to repository

`git log` shows repository history

`git branch/git tag` modify references in repository

`git push/git fetch` synchronize with remote repositories

**The Git Workflow**

A typical workflow moves changes through these areas:

- Modify files in Working Directory

- Stage changes with git add (to Staging Area)

- Commit changes with git commit (to Repository)


**Stashing** (Fourth Area?)

- Git's stash acts like a temporary holding area for uncommitted changes

- git stash saves working directory and staging changes

- git stash pop restores them

**Remote Repository**

While not a local area, the remote repository is where you push your commits to share with others.

How Areas Interact

git add: Working Directory → Staging Area

git commit: Staging Area → Repository

git checkout: Repository → Working Directory

git reset: Can move changes between all areas depending on flags

---


