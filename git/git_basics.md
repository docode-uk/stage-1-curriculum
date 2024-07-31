<h1 align="center">Introduction to Git</h1>

## Overview
Git is currently the most popular **version control system** in the world. It records the changes made to files over time in a type of **database** called a **repository**. It's completely free and open source. Git is an extremely powerful tool. It's a good idea to learn how to use Git early on in your coding journey; it allows you to easily share code, collaborate with other people on projects and track the entire version history of the files within a project.

## Git vs GitHub
Git and GitHub are not the same!

### Git
Git is a type of <a href="https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control">distributed version control</a> software which can be installed locally on your computer. It allows you to repeatedly save your code over time as you work on a project into a local Git respository, which is a type of database. Every time you use Git to save the current state of your project, Git takes a "snapshot" of what all your files within that project look like at that moment in time AND stores a reference to that snapshot.

### GitHub
GitHub is a cloud-based website that allows for Git repositories to be hosted online in remote repositories. It includes multiple tools to aid collaboration on projects, including features like issues and pull requests. It is possible to **push** your your Git repositories stored locally on your computer onto the platform so you can share your work with others.

To use <a href= "https://github.com/">GitHub</a>, you need to set up a free account.

<img src="https://user.oc-static.com/upload/2022/01/04/16412576933806_image30.png" alt="GitHub workflow" height="300">

#### A note about GitHub Desktop
GitHub Desktop is GUI which provides an alternative to using the command line, aiming to make it easier for users to interact with Git and GitHub repositories. However, we recommend interacting with Git using the command line; this will allow you to better understand Git concepts and allows access to full functionality of Git. 

## Installing Git
Before using Git you need to make sure it is <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git">installed</a> on your computer.

## Basic Git workflow
The basic Git workflow can be broken down simply into 4 steps, which involve using basic **Git commands** which can be run on the command line:
1. **Initialise** a local Git repository.<br>
    Navigate to your project's directory and then type:<br>
    `$ git init`<br>
    This creates a new subdirectory named .git that contains all of the necessary repository files.

2. **Modify** the files located within the repository and save to your computer.<br>

3. **Stage** the modified files which you want to be committed to the repository.<br>
    To actually start version-controlling existing files you need to first stage the files which you want to commit by typing:<br>
    `$ git add filename`<br>
    Replace filename with the name of the particular file, or if you want to add all files, replace it with ".", e.g.<br>
    `$ git add my_file.c`<br>
    `$ git add .`<br>
4. **Commit** the files, which takes the files in the staging area and stores that "snapshot" in the repository.<br>
    `git commit -m "message"`<br>
    Replace "message" with something which helpfully describes what changes you have made.

Each file in your directory can be either:
1. **"tracked"**, which includes files that have either been staged or committed.
or
2. **"untracked"** which includes all other files.

The above workflow is done repeatedly as you work on your project and make changes such that all changes are tracked.

### Logging
Then `git log` command is used to display the commit history of a Git repository. It will show a list of commits, with the most recent commit appearing first. For example:
```
commit e67b7e8f7c27f1c2d0f2a3f9f06b1b2d6d3e4f7a
Author: Dr Docode <drdocode@example.com>
Date:   Fri Jul 30 10:23:45 2023 +0200
    Initial commit
```
The output shows the commit hash (a unique identifier), the author's name and email, the date the commit was made and the commit message.

### Checking the status of your files
The `git status` command allows you to determine which state the files in your repository are in. It lists which files are staged for the next commit, which files are modified but not yet staged, and which files are untracked. For example:
```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
```

The above code means none of the tracked files are modified, and Git does not detect any untracked files.
```
$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file1.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file2.txt
```
The above code shows `file1.txt` is a tracked file which has new changes that have not been staged for commiting and `file2.txt` is untracked.

Note at the top, it states the current branch is "main" which is the default. We will go over Git branching in another section.

### Checking the detailed changes within files
`git diff`... TODO

### .gitignore 
TODO

## Where does GitHub come in?
<span style="color:red">TODO:</span> paragraph on github/pushing code
`git push`
`git pull`
`git fetch`

### Cloning
In the first of the four steps of the basic Git workflow, rather than setting up your own Git repository, it is possible to get a local copy of an existing remote repository hosted on GitHub.com by the process of **cloning**. For example, this would be useful if you wanted to contribute to a project which has already been started. The code for the first step would be replaced with the following:<br>
`$ git clone url`<br>
Replace "url" with an actual URL of the repository you want. For example if you wanted to clone the "stage-1-curriculum" repository, you would type:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git`<br>
This creates a directory called "stage-1-curriculum" and initialises a .git directory inside it. It pulls down all the data for that repository and checks out a copy of the latest version. If you wanted to clone the repository into a directory named something else, you can specify the new directory name as an additional argument, e.g.:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git mycurriculum`<br>
The above uses the **https:// transfer protocol**. Note that you can also use the <a href="https://graphite.dev/guides/git-clone-ssh-vs-https">SSH transfer protocol</a>.

The <a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository">GitHub Docs</a> provide concise instructions on this process, including how to access the particular URL of the repository you want to clone on GitHub - we would recommend you follow this when cloning for the first time.

## Further resources
### Video demos
TODO
<ul> 
    <li></li>
</ul>

### Articles/guides
<ul> 
    <li><a href="https://git-scm.com/book/en/v2">ProGit</a> --> A great open source reference guide</li>
    <li><a href="https://docs.github.com/en">GitHub Docs</a> --> The official GitHub documentation</li>
    <li><a href="https://git-scm.com/doc">Git Documentation</a> --> The official Git documentation</li>
</ul>

## Exercises
TODO

## NOTES
https://learngitbranching.js.org/ - for git branching, also include git checkout in this, git merge, git reset