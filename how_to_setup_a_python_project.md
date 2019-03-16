# How to setup a Python programming project  

## Introduction

This document has been constructed for developers who want to start coding Python in a distributed project (with a Git server). It is aimed at enterprise developers, but anyone can obviously use this documentation.

I wrote this document, because it took me quite some time to gather the information required to have a well functioning set up. Lots of introductions on the internet skip important steps or assume a lot of knowledge on the part of the reader, or are just incomplete or stale. At the same time a lot of developers ask questions about these steps, for instance on StackOverflow.

I tried to address the flaws of other descriptions, for example how to set up a HTTPS-connection to GitHub. Even GitHub's own documentation on this topic is both incomplete and flat out wrong.

*Disclaimer: the current version is work in progress, and as such quite incomplete. This will change over time.*


---
## Setting up Visual Studio Code

Microsoft Visual Studio Code (VSCode) is a free and lean code editor, that supports web programming languages (HTML, (S)CSS, JavaScript, TypeScript) and a number of web frameworks out of the box.  

It is actively maintained for Windows, Linux and MacOS.  

VSCode is very popular, and thousands of extensions have been created to add functionality. This is the architecture of VSCode - it provides very flexible extension APIs, which can use and integrate with nearly any functionality of the editor.  

As a user, you are expected to extend the editor until it fits your needs. That is what we will do in this section.  


### Python configuration

To enable Python in VSCode, you need to install the official (Microsoft) Python extension.  

Press *control shift X* to open the extensions view. Type *python* in the search and filter input field at the top of the view. A lot of options will pop up. Select the Python extension, authored by Microsoft, and install it. It should be at or near the top of the suggestion list. Alternatively, go to the [official Microsoft Python extension web page](https://marketplace.visualstudio.com/items?itemName=ms-python.python) and install the extension from there.  

Note that you need to have Python (the language) installed on your computer to be able to use the extension. If that is not the case, [download and install the latest version](https://www.python.org/).  

After installing the extension, you can start programming right away. To improve the programming experience, you are invited to configure VSCode to suit your needs. One suggestion is to add vertical rulers on position 72 (for Docstrings) and 79 (for Python code). You can add these by configuring a workspace (= project) specific configuration file, or on a global level. This is how it works:  

* Open Settings (*control ,*)  
* Click on the accolade **{ }** icon in the top right of the VSCode window.  
* *settings.json* is opened in a tab. This is your local configuration file.  
* Add this code to settings.json:  

``` json
{
    "[python]": {
        "editor.wordWrap": "wordWrapColumn",
        "editor.rulers": [
            72,
            79
        ]
}
```

When you save the file, vertical rulers will pop up when you edit a Python source file.  


### Other nice extensions

Python is the only extension needed to start coding. But you can improve your workflow significantly by installing additional extensions. For example:  

* File Utils (Steffen Leistner) - Add lots of file operations  
* Git History (Don Jayamanne)   - Compare several versions of the same source  
* gitignore (CodeZombie)        - Language support of .gitignore files  
* List Files (Don Jayamanne)    - List and open files quicker  
* Spell Right (Bartosz Antosik) - Interactive spell checker  



## Create your project environment and create a Git repository  

1. Create a folder (for instance by using the VSCode terminal (open with 
*control ,*)  
1. Navigate into the folder from the terminal  
1. Type:  

``` shell
git init <folder name of your project>
```

Git will create the folder, and it will create a .git folder within the main folder, which will hold the Git configs and history.  

Open VSCode, and type *control k* *control o*, or select 'File/Open Folder...'. A folder selection window will pop up. Navigate to the folder you just created and select this folder. Any file in the folder will now be displayed in the file view column (open that view by pressing *control shift e*).  

To enable VSCode to store Git repository specific settings, it needs to create a *workspace*. By default it will use the current project folder (which you just selected). Select 'File/Save Workspace As...' and save the workspace configuration in the Git repository folder.  



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

The .gitignore file contains files that are not to be considered by Git as project files. Files that comply to this pattern will not be tracked by Git. This should apply to files that are local, like your personal configurations, cache files, scratch files, or local test artefacts.  

1. Create a ".gitignore" file in the main repo folder from VSCode.  
1. Add patterns to the file, for example:  

``` script  
settings.json  
*.code-workspace  
```

* settings.json contains project specific settings in VSCode.  
* the .code-workspace file is the workspace configuration in VSCode.  



## Add source files to the local repository

When you open a new file 



## Sync local Git repository to GitHub for the first time  

To move all local source files to a GitHub repo, you need to 