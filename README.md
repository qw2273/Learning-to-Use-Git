# **How to Use Git**

## What is repository?
* It is a combination of  
   1. the files and directories that you create and edit directly, and 
    2. the extra information that Git records about the project's history. 
    
*  Git stores all of its extra information in a directory called `.git` located in the root directory of the repository. You should **never edit or delete anything** in  `.git`.


# What is staging area ? 
Git has a staging area in which it stores files with changes you want to save that haven't been saved yet. Putting files in the staging area is like putting things in a box, while 
ting those changes is like putting that box in the mail: you can add more things to the box or take things out as often as you want, but once you put it in the mail, you can't make further changes.

![staging-area](/images/staging-area.png)

## Tree-level structure 
1. A **commit** contains metadata such as the author, the commit message, and the time the commit happened. 
2. Each commit also has a **tree**, which tracks the names and locations in the repository when that commit happened. In the oldest (top) commit, there were two files tracked by the repository.
3. For each of the files listed in the tree, there is a **blob**. This contains a compressed snapshot of the contents of the file when the commit happened (blob is short for binary large object, which is a SQL database term for "may contain data of any kind"). In the middle commit, `report.md` and `draft.md` were changed, so the blobs are shown next to that commit. `data/northern.csv` didn't change in that commit, so the tree links to the blob from the previous commit. Reusing blobs between commits help make common operations fast and minimizes storage space.

![tree level structure](/images/gds_2_1_SVG.svg)


# Useful command List 
* `cd repositoryname`: set to specific repository 
* `pwd`: check current path 
* `git status`: shows you which files are in this staging area, and which files have changes that haven't yet been put there. 
* `git add filename`: add a file to the staging area

## View changes
* `git diff filename`: compare the file as it currently is to what you last saved
* `git diff`: show all the changes in your repository
* `git diff directory`: show you the changes to the files in some directory
* `git diff -r HEAD`:  The `-r` flag means "compare to a particular revision", and `HEAD` is a shortcut meaning "the most recent commit"
* The special label `HEAD`, always refers to the most recent commit. The label `HEAD~2` refers to the most recent commit and the one that before it 
* `git diff HEAD~1/hashnumber/branch1..HEAD~3/hashnumber/branch2`: show changes between commits 
* `git annotate file`: shows who made the last change to each line of a file and when
* `cat path/filename`: display the updated content of the file


*Example on how to read git diff output* 
A diff is a formatted display of the differences between two sets of files. Git displays diffs like this:
`diff --git a/data/northern.csv b/data/northern.csvindex 5eb7a96..5a2a259 100644` <br /> 
`--- a/data/northern.csv` <br /> 
`+++ b/data/northern.csv` <br /> 
`@@ -22,3 +22,4 @@ Date,Tooth`<br /> 
`2017-08-13,incisor` <br /> 
`2017-08-13,wisdom` <br /> 
`2017-09-07,molar` <br /> 
`+2017-11-01,bicuspid` 

This shows:
* The command used to produce the output (in this case, `diff --git`). In it, `a` and `b` are placeholders meaning "the first version" and "the second version".
* An index line showing keys into Git's internal database of changes. We will explore these in the next chapter.
* `--- a/report.txt` and `+++ b/report.txt`, wherein lines being removed are prefixed with `-` and lines being added are prefixed with `+`.
* A line starting with `@@` that tells where the changes are being made. The pairs of numbers are `start line` and `number of lines` (in that section of the file where changes occurred). This diff output indicates changes starting at line 22 , with 4 lines where there were once 3.
* A line-by-line listing of the changes with `-` showing deletions and `+` showing additions (we have also configured Git to show deletions in red and additions in green). Lines that haven't changed are sometimes shown before and after the ones that have in order to give context; when they appear, they don't have either `+` or `-` in front of them.

# Comment on commits and check submitted commits
* `nano filename`: open filename for editing (or create it if it doesn't already exist)<br />
                 1. `Ctrl-K`: delete a line. <br />
                 2. `Ctrl-U`: un-delete a line. <br/>
                 3. `Ctrl-O`: save the file ('O' stands for 'output').<br />
                 4. `Ctrl-X`: exit the editor.
* `git commit filepath -m "add comment messgae here"`:commit with  a single-line message
* `git commit`: add message in a text editor
* `git commit --amend - m "new message"`: revise the message 
* `git log`: view the history , the history is displaced *from latest to the oldest*, push `space` button to continue reading and `q` to exit 
* `git log directroy/filepath`:inspect only the changes to particular files or directories
* `git show first_few_characters_of_hash`: check a specific commit using hash 
* `git log -3 filename`: shows you the last three commits involving in file

## Ignore files 
You can tell it to stop paying attention to files you don't care about by creating a file in the root directory of your repository called `.gitignore` and storing a list of wildcard patterns that specify the files you don't want Git to pay attention to.

## Remove files 
* `git clean -n`: show you a list of files that are in the repository, but whose history Git is not currently tracking. 
* `git clean -f`: delete those files

# Undo changes 
* `git checkout -- filename`: 1.  discard the changes that have not yet been staged. <br />
2. This command can also be used to go back even further into a file's history and restore versions of that file from a commit.  <br />
*Use this command carefully: once you discard changes in this way, they are gone forever.* <br />
For example: `git checkout 2242bd report.txt` would replace the current version of `report.txt` with the version with hash number 2242bd. <br />
* `git reset HEAD path/to/file` + `git checkout -- path/to/file`: discard changes that have been staged. <br />
*you unstaged a change first by `reset` then discard this unstaged change by `checkout`<br />
* `git reset`: unstage any files from the directory
* `git checkout -- .`: revert all files in the current directory.

## Git configuration 
* `git config --list`: show default settings <br /> 
Also available in  one of three additional options:
`--system`: settings for every user on this computer.
`--global`: settings for every one of your projects.
`--local`: settings for one specific project.

* `git config --global setting value`
Using this command, you specify the `setting` you want to change and the `value` you want to set. <br /> 
for eaxmple : `git config --global user.email qw2273@columbia.edu` <br /> 
Change the email address (user.email) configured for the current user for all projects to my personal email.

## Branch
* Each branch is like a parallel universe: changes you make in one branch do not affect other branches (until you merge them back together).
* `git branch`:list all of the branches in a repository. The branch you are currently in will be shown with a * beside its name.
* `git checkout branchname`: switch to other branch 
* `git rm filename`: remove  a file 
* `git merge branch1 branch2`: merge two branches 
* `git checkout -b branch-name`: create a new branch

## Repository
* `git init project-name`: create a new repository, with new root directory name as project-name
* `git init /path/to/project`/`git init`: turn an existing project into a Git repository 
* `git clone /existing/project newprojectname`: create a copy of an existing repository with `newprojectname`, if no projectname provided, it will name it just as `project` 
for example: `git clone /home/thunk/repo dental`

## Remote: 
- A **remote** is like a browser bookmark with a name and a URL.
* `git remote`/`git remote -v`: find the list of remotes 
* `git remote add remote-name URL`:  add more remotes
* `git remote rm remote-name`: remove remotes 

- pull changes from those repositories and push changes to them
* `git pull remote-name branch-name`: gets everything in branch in the remote repository identified by `remote` and merges it into the current `branch` of your local repository.
`git push remote-name branch-name`: push to branch by adding to stage first.


## Pull Request: 
** Once you're satisfied with your work, you can open a pull request to merge the changes in the current branch (the head branch) into another branch (the base branch). For more information, see "About pull requests."
* `git remote`: check the remote server name, <remote-name> 
* `git checkout -b <brach-name>`:  create a new local branch and check it out
* `git push  <remote-name> <brach-name>`: push the local branch to the remote server
**** MAKE CHANGES TO FIELS IN REPO ****
* `git status` or `git diff`: check the changes you've made
* `git add <file>` or `git add --all`: stage the changes
* `git commit  -a -m "add commit message"` : add and commit changes to the repository
* `git push <remote-name>  <branch_name>`: push the change to the specified branch
* Then, go to the GitHub website, Open a Pull request to finish the action;
* Don't forget to Delete a Branch after the PULL Request is Merged

