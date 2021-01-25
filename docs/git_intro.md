

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Installing Git:](#installing-git)
- [Creating or Cloning a Git Repository:](#creating-or-cloning-a-git-repository)
- [Useful Git Commands:](#useful-git-commands)
- [Connecting to Gihub:](#connecting-to-gihub)
  - [Connecting via SSH:](#connecting-via-ssh)
    - [1. Generate SSH key:](#1-generate-ssh-key)
    - [2. Start the ssh-agent in the background:](#2-start-the-ssh-agent-in-the-background)
    - [3. Add your SSH private key to ssh-agent:](#3-add-your-ssh-private-key-to-ssh-agent)
    - [4. Add your public SSH key to your github account.](#4-add-your-public-ssh-key-to-your-github-account)
  - [Connecting via HTTPS:](#connecting-via-https)

# Installing Git:
Git would typically already be installed on any large server. If you would like to install git on your own computer there are instructions here:

<https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>

If you do all of your work on the servers, it is not essential that you install git on your own computer.

# Creating or Cloning a Git Repository:
To create git repository out of an existing folder. Open a terminal for the folder and use the command below:

```
$ git init
```

To Clone a repository from github to your machine use the following command. 
```
$ git clone https:// <github.com> / <your username> / <your repository name>
```


For more information check out this [basic guide for getting a git repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository).


# Useful Git Commands:
Also check out the git cheat-sheet for commands. 
Git should already be installed on your server. To add changes to your local git repository and push them to the remote repository follow these steps:
 
To get a status message that shows tracked files and folders
```
$ git status
```
To add all files in repository for next commit.
```
$ git add .
```
To commit files to git with the provided commit message.
```
$ git commit -m "YOUR COMMIIT MESSAGE"
```
To push the commits to remote repository. 
```
$ git push
```
To pull changes from remote repository.
```
$ git pull
```
To create a new branch from the branch you are on
```
$ git checkout -b <branch_name>
```
To change to an existing branch
```
$ git checkout <branch_name>
```

# Connecting to Gihub:
To push and pull to and from the remote repository on github it used to be possible to simply authenticate the connection using your github email and password.
It looks like that option will be depreciated for security reasons soon. 
Alternatives are below:
 
## Connecting via SSH:
(Tested on cook)
Below are the steps for setting up SSH, check out [this github guide](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) for more details.
 
### 1. Generate SSH key:
*Note that the github guide recommends ed25519 rather than rsa, but it does not seem to be available on cook.*
```
$ ssh-keygen -t rsa -b 4096 -C  "your github email address" 
```
This should ask you to enter a location to save the ssh key pairs, defaulting to your home directory and generate the following files:  
private key:*/home/xic/your_username/.ssh/id_rsa*  
public key: */home/xic/your_username/.ssh/id_rsa.pub*  
 
You are then asked if you want to add a passphrase. This should not be necessary.
 
### 2. Start the ssh-agent in the background:
```
$ eval "$(ssh-agent -s)"
```

### 3. Add your SSH private key to ssh-agent:
```
$ ssh-add ~/.ssh/id_rsa
```
### 4. Add your public SSH key to your github account.
*note: your public key is in the "id_rsa.pub" file if you used rsa for key generation.* 

See [this guide](https://docs.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account) for more details.
 
Please note that for previously cloned repositories you need to change the local git settings to point to an SSH link for your remote.
To check your remote address or to change it see below.

Prints remotes
```
$ git remote -v
```
Changes remote
```
$ git remote set-url origin git@github.com:<Username>/<Project>.git
```
## Connecting via HTTPS:
See the [github guide](https://docs.github.com/en/github/getting-started-with-github/set-up-git#next-steps-authenticating-with-github-from-git) for further help: 

