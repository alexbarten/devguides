# How to setup a Python project  

## Setting up VSCode  

* Python extension
* Python specific and MarkDown specific rulers


## Create your project environment and create a Git repository  

1. Create a folder (for instance by using the VSCode terminal (open with 
ctrl ,)  
1. Navigate into the folder from the terminal  
1. Type:  

``` shell
git init <folder name of your project>
```

Git will create the folder, and it will create a .git folder within the main folder, which will hold the Git configs and history.  
  
## Set VSCode as default .gitconfig editor  

Open a VSCode (or other) terminal and type  
``` shell  
git config --global core.editor "code --wait"  
```  
Now the .gitconfig file has been changed, and it will point to VSCode as the default .gitconfig editor.  

To check if this is working as expected, type:  
``` shell  
git config --global -e  
```  
The .gitconfig file will be loaded in a new tab in VSCode.  
Now we add these lines to .gitconfig:  
``` shell
[diff]
    tool = default-difftool
[difftool "default-difftool"]
    cmd = code --wait --diff $LOCAL $REMOTE
```

Now, when you type:
``` shell
git difftool
```
...in the command line, Git will ask if you want to compare versions of a particular changed file. Answering Yes or No, you will traverse through the list of changed files in the current repository. If you answer Yes, VSCode will be started and the current version will be shown next to the last committed version.  
Alternatively, you can right click on the file name in the *Source Control* view of VSCode and select the *Open Changes* context menu choice. This will have the same effect.  


## Configure .gitignore  

The .gitignore file contains files that are not te be considered by Git as project files. Files that comply to this pattern will not be tracked by Git. This should apply to files that are local, like your personal configurations, cache files, scratch files, or local test artefacts.  

1. Create a ".gitignore" file in the main repo folder from VSCode.  
1. Add patterns to the file, for example:  

``` script  
settings.json  
*.code-workspace  
```

* settings.json contains project specific settings in VSCode.  
* the .code-workspace file is the workspace configuration in VSCode.  


## Add source files to the local repository


## Sync local Git repository to Github for the first time  

To move all local source files to a Github repo, you need to 
