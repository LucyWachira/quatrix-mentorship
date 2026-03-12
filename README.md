# Git
 - Software developer teams use git to store, share, edit, and manage code in a distributed manner
 -It can be used to create documentation and manage such information.
 - However, one doesn't need to be in a team or Software Development team to utilize git.
 A good example is that the Quatrix mentors will document all their answers to for the mentorship program in a GitHub repo.

 ## Git vs GitHub
 - Git (git) is simply a versioning system that's can also to be used in a distributed fashion. That is, you can install git on PC at home or your office and make it act as a git server to host your own repositories. You can give other users access to your server so that you can all collaborate.

 - GitHub (and GitLab, BitBucket etc.) - are companies that have hosted git servers, and you can choose to use their platform instead of building yours.

Pros - it's less of a headache for you to set up, maintain and upgrade a git server.

Cons - you have to pay for the service and also assume the GitHub/GitLab will do a decent job of protecting your precious data.

## Generating SSH Keys & GitHub Settings

- To be able to clone or push it's recommended to use the ssh protocol as opposed to http protocol. To be able to use the ssh protocol, ensure you have your personal GitHub account with ssh keys. To accomplish that:
1. Create a pair of ssh keys as follows:
- Start a terminal/shell session
-  Invoke the following command:
     `ssh-keygen -t ecdsa`

-  Hit enter to let the ssh-keygen use default locations for the storage of the key pair.
-  Type the following to view the public key:

    `cat ~/.ssh/id_ecdsa.pub`

It should display something similar to:
```
ssh-ecdsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC5U1qjOcLmpjIR1Cq2ib0cOnN9mERr8jjgoJM2dEkQ9cK1dJ0xqS0hpj4TZYatOJVMVwoiY5S4yll2tJQV+G8WYVwMPmODjF+2wGChf2UZF8J9ZeQwpR/xD8MANJl2vg7Ba9jdhbRY5lakq0zQcYInPNw+bccRW1JnMOVSZwsKi7kk9VNBFmV0FhXwQkwjN4JcGlXSV8Jae6njoVBDTqD9LHKPLy+BbSGpDPdHUpaXSL9O8t5L5YLOjRIC46aLGEbWXt6LnU6p4mWAMZx1mhmmePcB9R8YA9B/GVH46lrpdrrTZd2R7vimHvJEE+N2zMqeUjhuHUr944nhbLeR+3fv9SgXcSqeFqmVq5rrzjfxQ531hJqmdSzlMjDeWOH5mtyjdKoWepzaIsH4qXZJcDG1eWAwlXqUPqlsoEY/HS168KQsY3qNy/hHEBIe9Svlnt4+s982TLuY5bSNwKEZThGKxx3eoaQ54fUXRD0NtbZOtCxqRenpzj1uZRox8DffzZE= pomollo@home-pc
```
- Copy the entire key text

2. Navigate to your GitHub personal account's settings and select SSH and GPG keys

- Click on New SSH key
- Paste the copied key into the Key field. Give it an appropriate Title
- Click on Add SSH key.
- Now you can clone using the SSH protocol option as well as do git pushes.
- Remember that if you use several PCs e.g. one in the office and one at home, you will need a 2 different key entries in your personal GitHub account.

## Git Branches
- A git repo always has a default branch referred to either as **main or master** (on older repos)

- Irrespective of whether you use branches or not, it's important to keep track periodically. Once you make small accomplishments, it's necessary to capture the state of your project. This is done by performing a commit. A commit is accompanied by a meaningful message describing what you have just accomplished. These commits allow you to go back to certain states in case you discover for whatever reason that you have gone astray.
## Git Commands
- `help` - provides help on various git commands. Example:
git help clone
- `config` - used to configure git settings eg.
  - `git config` --global core.editor "vim" - This will default to the vim editor for commit/merge comments.
  - `git config --global user.name "Paul Omollo"` - This sets the name to be used for the commit messages.
  - `git config --global user.email paul.omollo@quatrixglobal.com` - This sets the email to be used for the commits.
  - `clone` - used to make a copy of an existing repository from say GitHub, GitLab, BitBucket etc. eg:
  - `git clone git@github.com:quatrix-education/mentor.git` - will clone this repo (mentor repo) on your local computer. NOTE: 
  - GitHub makes it easy for you to get the exact git repo url. Steps to get a repos URL:
Navigate to git repository's landing page.
  - Click on the green button "<> Code" and switch to the SSH tab.
  - Copy the URL.
  - Proceed to paste and run git clone theURLCopiedfromGitHub/Gitlab.
- `checkout` - used to switch from one branch to another. It can also be used to create a branch off of the currently checked out branch. Examples:
  - `git checkout feature/add-bash-details` - will switch to the branch named feature/add-bash-details. The assumption is that the branch already exists.
  - `git checkout -b hotfix/correct-vi-details`- will create a new branch called hotfix/correct-vi-details. CAUTION - this branch will be created based off the currently checked out branch. It will also switch to the new branch created.
- `status` - shows the working tree status i.e.:
  - Changes to be committed - files that would end up in the commit, if and when it happens. We can also refer to these files as having been staged.
  - Changes not staged - files that will be omitted in the commit unless they are staged or added to the list of files to be commited.
- `diff` - The git status command is helpful as it shows the files that have been updated or created that need to be staged and committed. However, you might want to confirm the actual changes made in the files list. The `git diff `command helps show the difference between the immediate previous state and the current state of the files that have been affect. To see the difference, run:
```
git diff
```
NB: git diff only works on files that are not staged for commit. If by chance you have already staged the files, you can still see the difference by using:
```
git diff --staged
```
OR
```
git diff --cached
```
- `add` - this is used to add files that have not been staged, so that they can then be committed. Examples:
  - `git add bash/README.md` adds the README file in the bash folder.
  - CAUTION: git add .  adds/stages all files in the current directory. This is usually not ideal as you might end up committing files that should never be in the repository.
- `commit` - records the changes staged. Examples:
  - `git commit -am "Updated the git README.md to show an example of a commit"`. In this case, we have combined two(2) options for the commit command namely -a that automatically stages previously commit files therefore negating the need to doing the `git add <file(s)>` for them and then the `-m` option to indicate that the commit will capture a message to describe the commit.
- `git commit -m`"Updated the landing README.md"". This scenario assumes that the `git add` ... has already been done therefore only a commit message option and the message are indicated.
- `push` - uploads the local copy of the repository to a remote one e.g. one residing on GitHub, GitLab or BitBucket. Examples and scenarios:
  - git push - will upload your local branch to the remote copy of the repository.
  - If the branch being pushed is new, e.g. lets call the branch - feature/supplemental-module and you do a simple push as shown above, it will not work, and you will be presented with a message as follows:

  ```
  fatal: The current branch feature/supplemental-module has no upstream branch.To push the current branch and set the remote as upstream, use
        git push --set-upstream origin feature/supplemental-moduleTo have this happen automatically for branches without a tracking upstream, see 'push.autoSetupRemote' in 'git help config'.```

- The reason for the error message is that git requires that you match the local branch with the remote branch. For consistency, most people keep the same branch name on the remote branch. As the message indicates you can just run this and you commits will be pushed.:
```git push --set-upstream origin feature/supplemental-module```
  - For future pushes for this branch, all you need to do is git push
- `pull` - this fetches the most current state of a git repository. If working in a repository where others as also pushing their changes, doing frequent git pulls is important to avoid conflicts. To get the last updates from a repo, run:
```
git pull
```
- `merge` - Merging in Git means combining the changes from one branch into another.

- `squash` - process of combining multiple commits into a single, more concise commit.
git merge --squash feature-branch

- `log` - The git log command displays the history of commits in a Git repository

- `fetch` - used to download commits, files, and refs from a remote repository into your local repository. It updates your local repository with the latest changes from the remote, but it does not merge those changes into your current working branch.

- `reset` -  is a powerful Git command used to undo changes in your local repository.

- `rm` - used to remove files from a Git repository. It performs two key actions: 
Removes the file from the working directory - This deletes the file from your local filesystem.
Stages the deletion - It marks the removal of the file in the Git index (staging area), preparing this change to be included in the next commit.

- `mv` - used to move or rename files, directories, or symlinks within a Git repository while preserving their history.

- `branch` - used for managing branches within a repository

- `remote` - used to manage connections to other repositories, known as "remotes." Remotes are essentially bookmarks or aliases for the URLs of other Git repositories, typically hosted on platforms like GitHub, GitLab, or a private server. These remotes facilitate collaboration by allowing developers to push and pull changes between their local repository and the shared remote repository.

- `stash` - used to temporarily save changes in your working directory and index that are not yet ready to be committed. This allows you to revert your working directory to a clean state, typically matching the HEAD commit, so you can switch branches, pull updates, or perform other tasks without losing your current work in progress.

- `rebase` - used to integrate changes from one branch into another by reapplying commits from the current branch on top of a target branch. Unlike git merge, which creates a new merge commit, git rebase rewrites the project history by creating new commits for each commit in the original branch, resulting in a cleaner, linear commit history. 

### Questions
1. What are alternatives to git for source code version control?
Centralized VCS (CVCS) — single central server (e.g. SVN, Perforce).

Distributed VCS (DVCS) — each user has a full copy of the repository (e.g. Git, Mercurial).

2. What is the difference between git and GitHub/gitlab?
- Git is a free and open source version control system. It is a version control system you install and use on your computer.
  - Helps you to track changes of your code.
  - Lets you to commit,branch and merge.
  - stores your code and its full history locally.

 - GitHub/GitLab/Bitbucket - these are hosting platforms for Git repositories. They run on the web.
   - Stores your Git repositories online.
   - Lets you collaborate with others : share code
3. What does it mean to initialize a git repo? How does one initialize a repo on the command line and upload it to GitHub or GitLab? How does one initialize a repo on GitHub / GitLab? How does one then make changes to such a repo on their local PC?

- To initialize a git repo- means transforming a regular directory on your local machine into a Git-managed project. To start tracking changes in your folder using git.
- How to initialize a repo and upload it to GitHub:
  - git init - initializes git
  - git add . - adds files to track
  - git commit -am "message" - commit the files
- To upload it to Github:
  - create the repo on Github
  - Fill in the repository name
  - Choose public or private
  - Run those commands in your local terminal 
  ```git remote add origin https://github.com/your-username/my-project.git
   git branch -M main
    git push -u origin main
    ```
  Now the local repo is linked to the remote Github repo.

- To make changes on local pc:
  - Make edits to the file
  - git status - to check what has changed.
  - git add . - to stage the changes.
  - git commit -am "message" - to commit your changes.
  - git push - pushes the changes to GitHub.

 4. What is a .gitignore file used for in a git repo? What do you recall about the characteristics of files that start with a dot(.) in bash? 

 - .gitignore file -tells Git which files or folders it should ignore — meaning, don’t track or commit them.It only affects untracked files.
If a file was already committed before you added it to .gitignore, Git will keep tracking it unless you remove it explicitly

- In bash files that start with (.) are hidden files. They dont show up when you run ls, you have to use ls -a
git status --ignored - shows all files including ignored ones


5. What is a conflict regarding version control systems? What are practices that help minimize conflicts? How can one resolve conflicts in a git repo?

- A conflict occurs when two or more changes to the same file or lines in a file cannot be automatically merged by the VCS.Conflicts typically happen when multiple people edit the same part of a file concurrently.

- To minimize conflicts:
  Pull and update frequently
  Work on separate branches
  Break changes into small, manageable commits
  Communicate with your team

6. What are some basic Git and GitHub naming and documentation conventions? Does your quatrix-mentorship git repo adhere to these conventions?

  -  Repo Naming- Lowercase letters, hyphens instead of spaces
  - README - Every repo should have a README.md that explains:Project name and purpose.
  - gitignore- Exclude files that shouldn’t be tracked (e.g., node_modules/, temporary files, logs).
  - Commit messages — are they clear and follow a standard format,

  **REVISION**
 1. `git clone git@github.com:<user_name>/the-repo-you-are-cloning.git` - Clones your remote origin repo locally

 2. `git fetch upstream` - Pulls in the remote changes not present in your local repo. Downloads objects and references from another repository.
 3. `git merge upstream/master` - Merges any changes fetched into your working files
 4. `git add <file>` -Start tracking new files and also stage changes to already tracked files
 5. `git status & git diff` - Tells us what files and assets have been modified and staged git status -s This will display what files have been removed, changed or modified.
(M) - modified
(A) - added
(AM) - file has not been altered since it was last added

6. `git commit -m 'the message goes here for the commit'`- Records a snapshot of the project into your history at the time of your commit.
7. `git add '*.<file_extension>'`- This command adds all file types with the same extension, especially from different directories. Without quotes the command will only execute within the same directory it's been called from.
8. `git rm --cached <file>`- Unstages a file from the working tree (i.e. stops tracking the file).
9. `git log`- Remembers all the changes we've committed so far, in the order we committed them.
10. `git log --summary`- See where new files were added for the first time or where files were deleted.
11. `git remote add origin git@github.com:<user_name>/<repo_name>.git` - Creates a brand new remote repository.
12. `git remote -v`- Show a list of the current remote repositories
13. `git reset <file>`- Removes the desired file from staging area.
14. `git branch -r`- List all the remote branches currently tracked
15. `git remote prune origin`- Deletes branch locally if it has been removed remotely. Helps to remove stale references.
16. `git checkout -- <target>`- Changes the desired target back to the state of the last commit. A target can be a file or a directory (for example).
git rebase
Rebase allows you to easily change a series of commits, reordering, editing, or squashing commits together into a single commit.

### Adding
1. git add <list of files> git add --all - Add all the new files since last
2. `git add *.txt `-Add all txt files in directory

### Staging
1. `git diff` - Show unstaged differences since last commit
2. `git diff --staged` - Gets the staged differences and displays what has changed since our last commit

### Reverting
1. `git reset HEAD <file>`- Head is the last commit on the current branch we are on. What if you stage something you didn't need to be staged? This is the key.

git checkout -- <file>
Reset all changes to a file since last commit

git reset --soft HEAD^
What if you regret a commit? This will undo your last commit. (^ means move commit before HEAD and puts changes into staging).

git reset --hard HEAD^
Traverse through commits and revert back one by one.

git reset --hard HEAD
Undo Last commit and all changes

git commit --amend -m "added another file to the commit'
New commit message will override previous commit message

### Remotes
1. `git remote -v`- Show the current remote repos
2. `git remote add <name> <address>`- Add a new remote repo

3. `git remote rm <name>` - Remove remote repo

### Cloning, Branching, Fetching & Merging
1. `git fetch` -Pulls down any changes but doesn't merge them
2. `git branch <branch name>` - Makes a new branch
3. `git checkout <branch name>` - Switching branch and on a different timeline
4. `git merge <branch>`- Merges branch into master
5. `git branch -d <branch name>`- Deletes branch
6. `git checkout -b <branch name>`- Creates a new branch and then switches to it

### Pushing & Pulling
1. `git push -u origin master (remote repo name[origin], local branch name[master])`- Lets you just run git push later on without specifying name and branch
2. `git pull` -Pull changes in and syncs up your repo. Doesn't update local code
3. `git branch -r`- List all remote branches
4. `git remote show origin` - Show all the remote branches
5. `git branch -D <branch name>` -Delete the local repo branch and if you don't want the commits any longer on it then delete them too.
6. `git remote prune origin` - Deletes the branch locally if it has been removed remotely. Helps to remove stale references.
7. `git rebase` -Move all changes to master local which are not in origin/master remote to a temporary area
8. `git log`- Viewing the commits history
9. `git config --global color.ui true`- Color codes the commit SHA
10. `git log --pretty=oneline` OR `git log --pretty=oneline` Commit and history is one line
11. git log --pretty=format:"%h
Exactly how you want the output using placeholders (use git help log)

git log --until <value>
Date Ranges. For example you could grab everything from the year 2013 using git log --until 2013
12. `git rm <filename>` - Removes file completely
13. `git rm --cached <file names>`- Won't be deleted from your file system, but keeps the local changes still.
14. `git help` `git help <command>` - for help



- The valid merge strategies from your list are 1. Fast-forward and 2. Recursive. 
Fast-forward: This occurs when there is a linear path from the current branch tip to the target branch. Git simply moves the branch pointer forward instead of creating a new merge commit.
Recursive: This is the default strategy when merging one branch that has diverged from your current branch. It uses a 3-way merge algorithm to combine changes and creates a new merge commit. 
GeeksforGeeks
GeeksforGeeks
 +4
- Other Official Git Strategies:
If you are diving deeper into Git, you might also encounter these official strategies:
ORT: The modern replacement for the recursive strategy (stands for "Ostensibly Recursive's Twin").
Octopus: Used when merging more than two branches at once.
Ours: Merges any number of heads but ignores all changes from the other branches, keeping only the current branch's code.
Subtree: Used for merging a project into a subdirectory of another project.