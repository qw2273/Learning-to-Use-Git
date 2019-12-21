# **How to Use Git**

## What is repository?
* It is a combination of  
   1. the files and directories that you create and edit directly, and 
    2. the extra information that Git records about the project's history. 
    
*  Git stores all of its extra information in a directory called `.git` located in the root directory of the repository. You should **never edit or delete anything** in  `.git`.


# What is staging area ? 
Git has a staging area in which it stores files with changes you want to save that haven't been saved yet. Putting files in the staging area is like putting things in a box, while committing those changes is like putting that box in the mail: you can add more things to the box or take things out as often as you want, but once you put it in the mail, you can't make further changes.

![staging-area](/images/staging-area.png)


## Useful command List 
* `cd repositoryname`: set to specific repository 
* `git status`: shows you which files are in this staging area, and which files have changes that haven't yet been put there. 
* `git add filename`: add a file to the staging area
* `git diff filename`: compare the file as it currently is to what you last saved
* `git diff`: show all the changes in your repository
* `git diff directory`: show you the changes to the files in some directory
* `git diff -r HEAD`:  The `-r` flag means "compare to a particular revision", and `HEAD` is a shortcut meaning "the most recent commit"

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


* `nano filename`: open filename for editing (or create it if it doesn't already exist)<br />
                 1. `Ctrl-K`: delete a line. <br />
                 2. `Ctrl-U`: un-delete a line. <br/>
                 3. `Ctrl-O`: save the file ('O' stands for 'output').<br />
                 4. `Ctrl-X`: exit the editor.

* `git commit -m "add comment messgae here"`: add a single-line message
* `git commit`: add message in a text editor
* `git commit --amend - m "new message"`: revise the message 
* `git log`: view the history , the history is displaced *from latest to the oldest*, push `space` button to continue reading and `q` to exit 
* `git log directroy/filepath`:inspect only the changes to particular files or directories

## Tree-level structure 
1. A **commit** contains metadata such as the author, the commit message, and the time the commit happened. 
2. Each commit also has a **tree**, which tracks the names and locations in the repository when that commit happened. In the oldest (top) commit, there were two files tracked by the repository.
3. For each of the files listed in the tree, there is a **blob**. This contains a compressed snapshot of the contents of the file when the commit happened (blob is short for binary large object, which is a SQL database term for "may contain data of any kind"). In the middle commit, `report.md` and `draft.md` were changed, so the blobs are shown next to that commit. `data/northern.csv` didn't change in that commit, so the tree links to the blob from the previous commit. Reusing blobs between commits help make common operations fast and minimizes storage space.

![tree level structure](/images/gds_2_1_SVG.svg)
