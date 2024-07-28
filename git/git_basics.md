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
TODO

### Installing Git
Before using Git you need to make sure it is installed on your computer. Follow the instructions on this webpage: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git.

## Repositories
TODO

## Basic Git workflow
The basic Git workflow can be broken down simply into 4 steps:
<ol>
    <li><b>Initialise</b> a local Git repository.</li>
    <li><b>Modify</b> the files located within the repository.</li>
    <li><b>Stage</b> the modified files which you want to be committed to the repository.</li>
    <li><b>Commit</b> the files, which takes the files in the staging area and stores that "snapshot" in the repository.</li>
</ol>

Below are the basic **Git commands** which you will need to get familiar with to complete this basic workflow. All Git commands can be run on the command line.

`git init`

`git log`

`git add filename.`

`git commit -m "Your commit message"`

`git push`

`git log`<br>
A log of all saved changes

Extra stuff:<br>
`git checkout`
Explain how to go back to previous stage using checkout

#### A note about branches
TODO

## Pushing code to GitHub
TODO
Paragraph on github
And mention cloning
`git clone`<br>
Include link

## Further resources
### Video demos
<ul> 
    <li>https://www.youtube.com/watch?v=mJ-qvsxPHpY</li>
</ul>

### Articles/books
<ul> 
    <li>ProGit -> https://git-scm.com/book/en/v2 </li>
A great open source reference guide
</ul>

## Exercises

## NOTES
https://learngitbranching.js.org/ - for git branching