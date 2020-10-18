# Why are we learning this
- The goal is to learn git through PC so we could learn how to upload the Obsidian notes to the server

### Reference:
- I saw this to learn the basics (https://www.youtube.com/watch?v=J_Clau1bYco)
- I am going to explain the same here, so you don't have to read it

### How to get started
- Download GIT from https://git-scm.com/download/win
- While installing the package select "Use git and optional UNIX tools" and other options can just be left at the default
- Create a repo in the Github page https://github.com/
---
### What is GIT?
Git is a version controlling software that helps you maintian a software in it's different versions

### What is Github ?
Helps us maintain an online repository of our version controlled database of our code

## Let's start:-
### Step 1:
- Open/Create a folder where you'd like to have your local git repository 
- Right click over that folder and you should see `Git Bash Here` option, select it and a new terminal like window will open
- This is more like a terminal and you can use `cd` command to move to a particular location and `ls` command to look at all the files in that particular directory.

### Step 2:
Login into your github account using wither of the following commands
- git config --global user.name "Your Name"
-  git config --global user.email "youremail@domain.com"

### Step 3:
- Now try to clone the project into your desired folder, you can find your cloning like in the github page of the project you'd like to clone, It'd look something like this `https://github.com/gamersuji/Grid-System-.git`
 	- `git clone (url)`
 -  Now you'll see the project in your directory, now navigate the git bash command prompt to the folder where you've downloaded the git, using a `cd` command
 -  You can now try adding a file in directory, like say a  `.txt` file. Now use the git add command to add the to the local github project
	 -  `git add (file names)` 
 -  Now you've just added the project but int order for you to upload this to the github repo you need to commit the files that you've added now. Use the git commit command to commit the changes, you have to give a commit message (which is a detail about that commit).
	 - `git commit -m "(committed message)`
 - Once commited you can now push to the repo using the git push command.
	 - `git push -u origin master` 	
	