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

After that, a bit of editing in README.md, editing in vim is a bit tricky and I required some practice.
But basically you use `h` `j` `k` `l` as arrows and move into different modes to edit and navigate.  
_COMMAND_MODE_ is where you use commands preceded by `:`to do stuff, for example `:wq` stands for write and quit and `:q!` is force quit (Quit!)

Now for Gradle initialization:
~~~
gradle init
// accept all defaults
echo .idea >> .gitignore
git add .
git commit -m "gradle basic project initialised"
~~~
`.gitignore` file was automatically added by gradle to ignore `.gradle` and build files.
I just appended `.idea` because I will use the editor at some point and don't want to generate extra files in the repo.
The project now has an empty gradle project, which basically includes a jar executable `gradle/gradle-wrapper.jar` which runs through `gradlew` or `gradlew.bat` (depends on the system) is the program in charge of reading `settings.gradle` and `build.gradle`.
Gradle files inculde instructions on how to use "plugins", which are basically set of instructions for gradle to handle source files and its tasks.
I really like using gradle, specially for managing multiple projects in the same repo.
For now however, I will only use it for a single Java application, but will refactor it later to include multiple projects, maybe some React projects as well.
