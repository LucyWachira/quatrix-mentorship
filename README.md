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
- `merge`
- `squash`
- `log`
- `fetch`
- `reset`
- `rm`
- `mv`
- `branch`
- `remote`
- `stash`
- `rebase`
### Questions
1. What are alternatives to git for source code version control?
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
git status --ignored - shows all files including ignored ones.