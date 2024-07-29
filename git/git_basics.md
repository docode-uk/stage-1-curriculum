<h1 align="center">Introduction to Git</h1>

## Overview
Git is currently the most popular **version control system** in the world, which records the changes made to files over time in a type of **database** called a **repository**. It is completely free and open source. Git is an extremely powerful tool. It is a good idea to learn how to use Git early on in your coding journey; it allows you to easily share code, collaborate with other people on projects and track the entire version history of the files within a project.

## Git vs GitHub
Git and GitHub are not the same!

### Git
Git is a type of version control software which can be installed locally on your computer. It allows you to repeatedly save your code over time as you work on a project into a local Git respository. Every time you use Git to save the current state of your project, Git takes a "snapshot" of what all your files within that project look like at that moment in time AND stores a reference to that snapshot.

### GitHub
GitHub is a cloud-based website which... TODO

#### A note about GitHub Desktop
<span style="color:red">TODO</span>

## Installing Git
Before using Git you need to make sure it is <a href="https://git-scm.com/book/en/v2/Getting-Started-Installing-Git">installed</a> on your computer.

## Repositories
<span style="color:red">TODO</span>

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

### Logging
<span style="color:red">TODO</span>
`git log` - a log of all saved changes
`git checkout`
Explain how to go back to previous stage using checkout

### A note about branches
<span style="color:red">TODO</span>

## Where does GitHub come in?
<span style="color:red">TODO:</span> paragraph on github/pushing code
`git push`

### Cloning
In the first of the four steps of the basic Git workflow, rather than setting up your own Git repository, it is possible to get a local copy of an existing remote repository hosted on GitHub.com by the process of **cloning**. For example, this would be useful if you wanted to contribute to a project which has already been started. The code for the first step would be replaced with the following:<br>
`$ git clone url`<br>
Replace "url" with an actual url of the repository you want. For example if you wanted to clone the "stage-1-curriculum" repository, you would type:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git`<br>
This creates a directory called "stage-1-curriculum" and initialises a .git directory inside it. It pulls down all the data for that repository and checks out a copy of the latest version. If you wanted to clone the repository into a directory named something else, you can specify the new directory name as an additional argument, e.g.:<br>
`$ git clone https://github.com/docode-uk/stage-1-curriculum.git mycurriculum`<br>
The above uses the **https:// transfer protocol**. Note that you can also use the <a href="https://graphite.dev/guides/git-clone-ssh-vs-https">SSH transfer protocol</a>.

The <a href="https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository">GitHub Docs</a> provide concise instructions on this process, including how to access the particular url of the repository you want to clone on GitHub - we would recommend you follow this when cloning for the first time.

## Further resources
### Video demos
<ul> 
    <li></li>
</ul>

### Articles/guides
<ul> 
    <li><a href="https://git-scm.com/book/en/v2">ProGit</a> --> A great open source reference guide </li>
    <li><a href="https://docs.github.com/en">GitHub Docs</a> --> The official GitHub documentation </li>
</ul>

## Exercises

## NOTES
https://learngitbranching.js.org/ - for git branching