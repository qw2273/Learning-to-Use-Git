# **How to Use Git**

## What is repository?
- The combination of  1. the files and directories that you create and edit directly, and 2. the extra information that Git records about the project's history. 
- Git stores all of its extra information in a directory called `.git`located in the root directory of the repository. You should **never edit or delete anything** in  `.git`.


# What is staging area ? 
Git has a staging area in which it stores files with changes you want to save that haven't been saved yet. Putting files in the staging area is like putting things in a box, while committing those changes is like putting that box in the mail: you can add more things to the box or take things out as often as you want, but once you put it in the mail, you can't make further changes.

<img src="https://s3.amazonaws.com/assets.datacamp.com/production/course_5355/datasets/staging-area.png")

git status shows you which files are in this staging area, and which files have changes that haven't yet been put there. In order to compare the file as it currently is to what you last saved, you can use git diff filename. git diff without any filenames will show you all the changes in your repository, while git diff directory will show you the changes to the files in some directory

## Useful command List 
* Go  to specific repository: `cd "repository name"` 
* Check status of a repository: `git status`
* Check what has been changed: `git diff`
                              * 

