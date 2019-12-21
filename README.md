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
* `git diff filename`: compare the file as it currently is to what you last saved
* `git diff without any filenames`: show all the changes in your repository
* `git diff directory`: show you the changes to the files in some directory

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
* The command used to produce the output (in this case, diff --git). In it, `a` and `b` are placeholders meaning "the first version" and "the second version".
* An index line showing keys into Git's internal database of changes. We will explore these in the next chapter.
* `--- a/report.txt` and `+++ b/report.txt`, wherein lines being removed are prefixed with `-` and lines being added are prefixed with `+`.
* A line starting with `@@` that tells where the changes are being made. The pairs of numbers are `start line` and `number of lines` (in that section of the file where changes occurred). This diff output indicates changes starting at line 22 , with 4 lines where there were once 3.
* A line-by-line listing of the changes with `-` showing deletions and `+` showing additions (we have also configured Git to show deletions in red and additions in green). Lines that haven't changed are sometimes shown before and after the ones that have in order to give context; when they appear, they don't have either `+` or `-` in front of them.
