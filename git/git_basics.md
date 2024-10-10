<h1 align="center">Introduction to Git and GitHub</h1>

## Overview
Git is currently the most popular **version control system** in the world. It records the changes made to files over time in a type of **database** called a **repository**. It's completely free and open source. Git is an extremely powerful tool. It's a good idea to learn how to use Git early on in your coding journey; it allows you to easily share code, collaborate with other people on projects and track the entire version history of the files within a project. Below is a summary of the main concepts and commands you need to know to get started with Git.

## Git vs GitHub
Git and GitHub are not the same!

### Git
Git is a type of <a href="https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control">distributed version control</a> software which can be installed locally on your computer. It allows you to repeatedly save your code over time as you work on a project into a **local Git respository**, which is a type of database stored locally on your computer. Every time you use Git to save the current state of your project, Git takes a "snapshot" of what all your files within that project look like at that moment in time AND stores a reference to that snapshot.

Before using Git you need to make sure it is <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git">installed</a> on your computer.

### GitHub
GitHub is a cloud-based website that allows for Git repositories to be hosted online in **remote repositories** so that they can be easily shared with others. It includes multiple tools to aid collaboration on projects, including features like issues and pull requests. It is possible to **push** your your Git repositories stored locally on your computer onto the platform so you can share your work with others.

To use <a href= "https://github.com/">GitHub</a>, you need to set up a free account.

#### A note about GitHub Desktop
GitHub Desktop is GUI which provides an alternative to using the command line, aiming to make it easier for users to interact with Git and GitHub repositories. However, we recommend interacting with Git using the command line; this will allow you to better understand Git concepts and allows access to full functionality of Git. 

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

Note at the top, it states the current branch is "main" which is the default. Don't worry about this now - we will go over Git branching in another section.

## Where does GitHub come in?
GitHub allows you to host the work stored in your local Git repository in a remote repository online, enabling collaboration with others and remote access to your projects.

The main steps in this process are as follows:
1. Log into GitHub.com and <a href  ="https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository">make a new remote repository</a> using the web interface.

2. Once you click "Create repository" as per the instructions on the above link,

 "Link your local repository to it and **push** your code to the remote repository.
Ensure you are within your project directory. Use the following commands :
```
git remote add origin URL
```
Replace URL with the URL of your newly created GitHub repository. 

```

git branch -M main
git push -u origin main
```

### Cloning
In the first of the four steps of the basic Git workflow, rather than setting up your own Git repository, it is possible to get a local copy of an existing remote repository hosted on GitHub.com by the process of **cloning**. For example, this would be useful if you wanted to contribute to a project which has already been started. A cloned repository is linked to the original remote repository, allowing you to push code to the project. The code for the first step of the basic Git workflow above would be replaced with the following:<br><br>
`$ git clone url`<br>
Replace "url" with an actual URL of the repository you want. For example if you wanted to clone the "stage-1-curriculum" repository, you would type:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git`<br><br>
This creates a directory called "stage-1-curriculum" and initialises a .git directory inside it. It pulls down all the data for that repository and checks out a copy of the latest version. If you wanted to clone the repository into a directory named something else, you can specify the new directory name as an additional argument, e.g.:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git mycurriculum`<br><br>
The above uses the **https:// transfer protocol**. Note that you can also use the **SSH transfer protocol**.

The <a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository">GitHub Docs</a> provide concise instructions on this process, including how to access the particular URL of the repository you want to clone on GitHub - we would recommend you follow this when cloning for the first time.

 We will discuss how Git/GitHub can be used to collaborate on projects with others in more depth in subsequent chapters, including using cloning and branching.

## .gitignore
<a href= "https://git-scm.com/docs/gitignore">.gitignore</a> specifies files that you intentionally want to remain untracked and therefore ignored. This is useful for keeping sensitive information such as passwords and configuration files private, especially when pushing code to a public remote repository.

To do this, you need to create a `.gitignore` file in the **root directory** of your project:
1. Navigate to root directory of project
```
cd /path_to_root_directory
```
2. Create and open .gitignore file in text editor (e.g. nano)
```
nano .gitignore
```
3. Add files and directories you want to ignore, e.g.
```
secrets.txt
.env
.DS_Store
```
4. Save and close the .gitignore file
In nano, press CTRL+X, then Y, and then ENTER to save and exit.
5. Check the status of your files using `git status` to ensure the specified files are being ignored.

Here are some useful <a href = "https://github.com/github/gitignore">gitignore templates</a>.

## Summary
We have covered the core topics required to get started with making your own local Git repository and pushing this to a remote repository on GitHub. 

## Further resources
<ul> 
    <li><a href ="https://youtu.be/hwP7WQkmECE?si=l65hOA6M2rc-53-V">Git explained in 100 seconds</a></li>
    <li><a href="https://git-scm.com/book/en/v2">ProGit</a> --> A great open source reference guide</li>
    <li><a href="https://docs.github.com/en">GitHub Docs</a> --> The official GitHub documentation</li>
    <li><a href="https://git-scm.com/doc">Git Documentation</a> --> The official Git documentation</li>
    <li><a href="https://training.github.com/downloads/github-git-cheat-sheet.pdf">Git cheat sheet</a> --> A useful cheat sheet with the most common Git commands</li>
</ul>

## Exercise
Work through the above steps to set up your own local repository with a project you have completed, and push this to a remote repository on GitHub.