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
~~~ 
vim README.md
~~~
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

Using the same gradle init script I restructured the project to actually include the default java app image.
Is pretty easy to understand. There's a new `app` folder, which includes the default maven java project structure.
Meaning a `src` folder on the root, followed by `main` and `test`, inside them, there should be a language specific directory `java` in this case.
And that is the entry point for classes hierarchy, in this case the package is simply `CodeKata` and the main class must include a standard `public static void main(args...)` class.
The `build.gradle` file now is inside the `app` folder at the root. And it includes:
- plugins: Gradle extensible plugins, they provide tasks and config information. In this case only `application` which basically add all java app necessary task
- dependencies and repositories: Maven by default, all package management required info.
- plugin/task specific config: 
  - For the application plugin task, there's the "Where's the main class?" config.
  - There's also instructions to use Junit for the testing task.

The last thing to notice is that `settings.gradle` now has `include('app')`, which let's gradle know that there's such folder that needs to be considered and used as a gradle project.
This comes in handy when there's more than one project. This structure is pretty much the same as a multiproject gradle. Main difference being that multiproject enforces the use of a folder `buildSrc` which is where gradle defines custom plugins.
All is needed, is to append another include for each gradle project folder equivalent to the `app` one in the current.

So, now that the app is properly structured, to run the app both of the following are acceptable:
~~~
./gradlew run
./gradlew app:run
~~~
Also, there's other tasks `check` or `test` will work.

~~There's also a bit of a bug here~~, when trying to run a single test using intellij, wathever is trying to run the tests (most likely local Gradle installation) cannot really find the tests.
But when running `gradlew :test`, test task runs ok. This is easily solved by configuring intellij settings in `Build, Execution, Deployment > Build Tools > gradle` and setting intellij for running tests.
This bug is now fixed, the problem was coming from the fact that gradle was not able to localize the test inside a package starting with uppercase. Changed the case and is working now. This is also java convention.
