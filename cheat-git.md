# Git et GitHub

### …or create a new repository on the command line

echo "# DEV-FRONT" >> README.md  (
git init <br>
git add README.md<br>
git commit -m "first commit"<br>
git branch -M main<br>
git remote add origin git@github.com:fmarrkiz/DEV-FRONT.git<br>
git push -u origin main

### …or push an existing repository from the command line

git remote add origin git@github.com:fmarrkiz/DEV-FRONT.git
git branch -M main
git push -u origin main


## Tutorial 

[Git Tutorial for Beginners - Mosh](https://www.youtube.com/watch?v=8JJ101D3knE)


Distributed version control systems
**Git**, Mercurial

Git is free, open source, super fast and scalable

#### **Using git**
- command line 
- code editors and IDEs (ex : VS Code through GitLens)
- Graphical user interface *GUI* ex: GitKraken Git, Sourcetree (windows and mac).  
They have limitations though and might not always be available

Use GUI *and* command line (right tool for the right task)

#### Installing git

##### Finding out which version of git I have  
`git --version`

- Set the settings

	- Name

`` git config -- global user.name "Marie KF" ``

We use double quotes because there's a space between the value
	- Email

`` git config --global user.email mariekfruchart@outlook.com ``

No need for double quotes because there's no space

- Default Editor

``git config --global core.editor "code --wait"``  
= wait until we close a new vs code instance

``git config --global -e``  
= `-e` tells Git to open that config file in an editor for manual editing



	- Line Ending
line ending in windows = abc `\r`(carriage return) `\n` (line feed)
in mac = abc `\n`

so we have to `core.autocrlf` (= auto carriage return line feed)

`true` for window users  
`input` for mac users

so `git config --global core.autocrlf input`



##### Different settings level

- System  
All users

- Global
All repositories of the current user

- Local   
The current repository or the repository in the current folder


To get help or get documentation on git 

- look up "git config" on Google
- in terminal : git config --help for the full on version and git config--h for the shorter version


#### Creating a snapshot 

##### Initialising a repository

`mkdir Moon` = make directory (dossier) Moon
`cd Moon` = change directory to 

`git init ` = initialise / add this file to a git repository. It creates a hidden .git in the directory

if we do `ls -a` = list all files

`open .git` = opens the .git file present in the current directory

**Attention** if you corrupt or remove the .git file you'll use the version history

to remove a .git irreversibly unless you have a remote copy or backup : `rm -rf .git`  

`rm` = remove  
`-r` = recursively delete directories and their contents  
`-f` = force deletion without prompting for confirmation

#### Basic Git Workflow

Project directory --- Git repository (hidden in the project dir)

- Check what's in the directory and staging area `git status`
- Staging area ---- `git add`
- From staging area to local git --- `git commit -m ""`
- From local git to github --- `git push origin main` [origin is where we wanna put it; main is the branch we're pushing]

Example

| directory| staging area  <br> `git add` | repo  <br> `git commit -m "initial commit`   |
| ---- | :---: | :---: |
|file 1  | file 1 |
|file 2  | file 2 |


in `git commit -m "commit"` we explain the commit between the parentheses following this norm "typeoffilemodified(nameofthedoc): brief summary of commit"<br> 
ex : "docs(Jour-02): updated finished tasks"

**Attention** when we commit the files, the staging area doesn't become empty

 reminder: <br>
`git add` also works when we want to commit a file removal in the staging area

A commit : <br>
- ID
- Message
- Date/Time
- Author
- Complete snapshot



#### Staging files

***Adding files to a project***

	`echo [option] [string]` is a Unix/Linux command so not specific to *Git* but it allows you to send text, display variables, print special characters to the standard output **and* (what interest us here) to write to a file<br>
`echo "this is a test > file1.txt` will create a file named "test.txt" with the text "This is a text file". If the file already exist, it will be replaced.<br>
`echo "this is a test >> file1.txt` will *append* content to the end of an existing file.<br>
`echo hello > logs/dev.log` will create a new file in a the `'logs` directory




`git status` to check what's the status of the git (duh)

*to add files* <br>
`git add file1.txt` `git add file1.txt file2.txt` `git add *.txt*` <br>
`git add .` = add all the entire directory recursively (be careful though some files you don't need to add)

#### Commiting changes

from staging area to repository

`git commit -m "description"` (`-m` = message)

Common practices : don't make too small or too big commits, use them as checkpoints (save each morceau)

#### Skipping the staging area

do this only if you're 100% sure!

`git commit -a -m` or `git commit -am` (`-a` = all)

#### Removing files

	`rm file1.txt` is a standard unix command, but we'll use it there

`git ls-files` shows files in the staging area. file1.txt is still there after `rm` 

so `git add file1.txt` even to remove<br>
then `git commit -m "txt(file1)removed file`

**OR**

`git rm file1.txt` git removes the file from both staging and repository


***Renaming files***

	`mv file1.txt main.js` is a unix command, it can move and remane files and directories

`git add file1.txt` `gitt add main.js`<br>

**OR**

`git mv file1.txt main.js`

THEN
`git commit -m ""`


***Ignoring files***

	`mkdir` command is a unix command, it creates a new directory


example :
`mkdir logs`<br>
`echo hello > logs/dev.log`

it will appear in `git status`

so to prevent it from going to the staging area, create 
`.gitignore` creates an extension in the root of your project

`echo logs/ > .gitignore`

it won't show on `git status` but `.gitignore` will so 

`git add .gitignore`<br>
`git commit -m ""`

Only works for code never added to the repository

***Remove files from the staging area***

`git ls-files` to see the files in the staging area

THEN

`git rm --cached -r logs/` only remove from the index (=staging area)<br>
`git commmit -m ""`


#### Short status

`git status` --> `git status -s`

| code/shortcut | meaning |
| :--: | :--: |
| M (red) | Modifed file **not** in the staging area |
| M (green) | Modified file in the staging area |
| M(green)M(red) | Some changes to the file have been put<br>in the staging area<br>Some changes haven't been added yet |
| | |
| ?? | Untracked file |
| A | Added file |

#### Viewing the Staged and Unstage Changes

	Best practice : Always review what you have in the staging area before commiting it.

- `git diff --staged`<br>it'll show `diff --git a/file1.js b/file1.js` we're comparing the difference between the copies of file1.js in the staging area vs the repo

- `git diff` compares what we have in the directory with what we have in the staging area


#### Visual diff tools

- KDiff3
- P4Merge
- VSCode


**We config the difftool to VSCode**

`git config --global diff.tool vscode`<br>
`git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"`<br>
`git config --global -e`

open vscode
under [difftool "vscode"]
check that "code --wait --diff $LOCAL $REMOTE" is accuretely written
close VSCode

**THEN**
`git difftool` to compare what's in the directory to what's in the staging area

`git difftool --staged` to compare what's in the staging area to what's in the repo

#### Viewing the history

`git log` to view the commit history and comments from latest to earliest

`git log --oneline` shorter version

`git log --oneline --reverse` shorter version from earliest commit to most recent

### Viewing a Commit

1. To see the file version for a specific commit
`git show [commit number]` **or** `git show HEAD~[number - how many steps backs]`

`git show HEAD~1:[.gitignore]` or `git show HEAD~1.[bin/.gitignore]` if it's in a sub directory

2. To see all files and directories in a commit

`git ls-tree HEAD[~1]`

- `blob` is a file
- `tree` is a directory

#### Unstaging files

- undo the `add` operation

old version `git reset` --- new version `git restore`

example : <br>
`git restore --staged [filename]`or`[.]` for all or`[*.js]` for patterns

File isn't in the staging area anymore 

#### Discarding local changes

`git clean -fd` `-f` = force `-d` remove whole directories <br>
Careful with this command
























