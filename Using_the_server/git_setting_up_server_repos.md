Setting up master git repositories on the server
========================================

## Authorship:
Sam Barnett (February 2018)

## Updated by:

# Description
This file explains how to set up local master git repositories on the
Buckley lab server. This should work on your local machine too, but you'll 
have to change the file paths.

### Creating a new master remote from scratch
This will create a new master remote directory from scratch. This should be done
at the begining of a project, before the project directories have been made.
You must be part of the group "git" in order to do this on the server.

1. Make a bare directory in our server git repo directory (`/home/git/`)
   - `cd /home/git`
   - `mkdir PROJECT_NAME.git`
   - `cd PROJECT_NAME.git`
   - `git --bare init --shared`
2. Clone this repo into your local directory
   - `cd /home/USERNAME/git_repos`
   - `git clone /home/git/PROJECT_NAME.git`
     - *You may get a message saying you just cloned an empty repo*
3. You now have a master and local repo for your project. Before moving on, you should make your first commit and push that to the master.
   - `cd /home/USERNAME/git_repos/PROJECT_NAME`
   - `touch README`
   - `git add README`	
     - *Adds the file `README` to tracking*
   - `git commit -a -m "Inital commit"`
   - `git push origin master`

You are now all set!

### Creating a new master remote repo on the server from started project directory.
This will make a new master remote repo from a directory that you have 
already made in your home directory. This is good if you want to begin keeping
track of changes to a directory of an already started project.

1. Initiate your project directory as a git repo
   - `cd /home/USERNAME/PROJECT_NAME`
   - `git init`	
     - *initiates git repo*
   - `git add .`
     - *adds all current files to tracking*
     - **Note:** *this would be the time to think about which files you want to track and which you dont (`gitignore`).*
   - `git commit -a -m "Initial commit"`
2. Clone and reinitalize this local repo into the master repo directory on the server
   - `cd /home/git`	
   - `git clone --bare /home/USERNAME/PROJECT_NAME /home/git/PROJECT_NAME.git`	
     - *Clones the project into `/home/git/` but bare so no files are actually cloned*
   - `cd PROJECT_NAME.git`
   - `git init --bare --shared`	
     - *Reinitializes the repo*
3. Change the origin path of your local repo to the new master repo
   - `cd /home/USERNAME/PROJECT_NAME`
   - `git remote add origin /home/git/PROJECT_NAME.git` 
     - *Changes the origin path to the new master*
4. Check that it works
   - `git remote show origin`	
     - *Displays the path to the repo origin, should be /home/git/PROJECT_NAME.git*
   - `git push origin master`	
     - *Make sure you can push to the master*

You are now all set!