# Reproducing this repo

These are instructions mostly to myself and possibly to anyone interested. 
I try to do most things using the terminal and the commands in here are mostly curated after usage. (Feels a bit like cheating, but the main goal is to have a record or reference of what I know how to do).  
Will try to add **TODO** items for the steps I still need to do in a graphic interface. 
The idea is to be able to reproduce the skeleton of the project using these instructions.

So, first create the root directory and switch to it:
~~~
mkdir CodeKata
cd CodeKata
~~~
Create README.md 
 
    vim README.md
Use `a` (for append) to enter _INSERT_MODE_ and type away.  
Press ESC to exit _INSERT_MODE_.  
Type command `:wq` to save changes and exit.

Created a repository on my GitHub profile. //TODO: There might be a CLI GitGub API
For now just followed instructions on screen to create a new Public repository. Once created:
~~~
git init
git remote add origin https://github.com/CodeKata
git add .
git commit -m "Initial commit"
git push -u origin master
~~~
`commit -m` is a shortcut to prevent the editor screen for the commit message.  
`push -u` is equivalent to `push --set-upstream` where I'm indicating the remote and local branch to be tracked.

Now for the second file, same process:
~~~
vim REPRODUCE.md
//edit and save the file
git add .
git commit -m "Including REPRODUCE.md"
git push
~~~
