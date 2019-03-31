# How to setup a Python programming project  

## Contents

1. [Introduction](#Introduction)  
1. [Setting up Visual Studio Code](#Setting-up-Visual-Studio-Code)  
   * [Python configuration](#Python-configuration)  
   * [Adding a linter](#Adding-a-linter)
   * [Other nice extensions](#Other-nice-extensions)  
1. [Create your project environment and create a Git repository](#Create-your-project-environment-and-create-a-Git-repository)  
1. [Set VSCode as default .gitconfig editor](#Set-VSCode-as-default-.gitconfig-editor)  
1. [Configure .gitignore](#Configure-.gitignore)  
1. [Add source files to the local Git repository](#Add-source-files-to-the-local-Git-repository)  
1. [Sync local Git repository to GitHub for the first time](#Sync-local-Git-repository-to-GitHub-for-the-first-time)  


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

Press *control shift X* to open the Extensions pane. Type *python* in the search and filter input field at the top of the pane. A lot of options will pop up. Select the Python extension, authored by Microsoft, and install it. It should be at or near the top of the suggestion list. Alternatively, go to the [official Microsoft Python extension web page](https://marketplace.visualstudio.com/items?itemName=ms-python.python) and install the extension from there.  

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
}
```

When you save the file, vertical rulers will pop up when you edit a Python source file.  


### Adding a linter  

When you code Python using the official VSCode Python extension, you have the ability to have your code checked at all times by a so called *linter*. A *linter* is a utility that checks if your code is standards-compliant. In the case of Python, the standards are listed in the [Python PEP-rules](https://www.python.org/dev/peps/). PEP means Python Enhancement Proposal. Any enhancement to the language is described here.  

Most languages are supported by one or more linters. Some of these may be part of the language distribution itself, and others are provided by third party developers. Python is supported by a large number of linters. Each one of these has different strengths, and you are advised to study the documentation of each of the linters to choose your favorite, or the linter that supports a particular use case.  

A good multi-purpose linter is Flake8. It applies the [Python PEP8-rules](https://www.python.org/dev/peps/pep-0008/) like most linters do, but this one does it in a better way.  

To set up a linter in VSCode, you press the *control shift p* shortcut to bring up the VSCode command line. Type *python: select linter* and press ENTER to choose from a number of linters known by VSCode (actually: known by the Python extension). Flake8 is amongst the choices. Navigate and select this option and press ENTER again. Probably a window will popup in the downright corner to warn that this Python library has not yet been installed. The window offers buttons to start the installation process. Select the option to start the installation. A Windows command line will show the progress.  

When you have installed the linter, you press *control shift p* and type *python: run linting* to run the linter in your current tab (which should be loaded with a Python source file). If the linter encounters a problem (some code that does not comply to the rules), it will show these in the problem tab of the terminal window in VSCode. When you click on the problem(s) with the left mouse button, the offensive part of your code will be displayed in the editor window.  

By the way: when you save your Python file, your code will be checked automatically. And in the latest versions of VSCode, online real-time checking is also enabled. This means that explicit commands to run a linter are mostly interesting, when you temporarily select an alternative linter (by repeating the command in the previous paragraphs). One of the most interesting alternatives to Flake8 is [Bandit](https://github.com/PyCQA/bandit). Bandit scans your code for security vulnerabilities. After the scan you repeat *python: select linter* once again to switch back to Flake8. Another interesting linter is Pylint. Pylint can give a lot of feedback. It is advised to not use Pylint as your primary linter, but as an extra, because it sometimes is too harsh/strict on your code.  


### Other nice extensions

Python is the only extension needed to start coding. But you can improve your workflow significantly by installing additional extensions. For example:  

* File Utils (Steffen Leistner) - Add lots of file operations  
* Git History (Don Jayamanne)   - Compare several versions of the same source  
* gitignore (CodeZombie)        - Language support of .gitignore files  
* List Files (Don Jayamanne)    - List and open files quicker  
* Spell Right (Bartosz Antosik) - Interactive spell checker  



## Create your project environment and create a Git repository  

Why would you create a Git repository? Git does several things for you.  
1. It adds discipline. You create or change code, you stage the changes, you commit the changes and think about the consequences while you do it. 
1. It creates an unbreakable trail of changes. You can see through the history of your developed solutions, and fall back to an older state, or analyze when you introduced an error.
1. As you add files to the repository, you think about its size, about its functionality and about the current state of things. What to release? What to postpone? Because you add these formal steps of committing changes, you are more aware of each step you take.  

So, how to create a Git repository?
1. Create a folder by using the VSCode terminal (open with 
*control shift `*)  
1. Navigate into the folder from the terminal  
1. Type (replace <...> with your project name):  

``` shell
git init <folder name of your project>
```

Git will now create the project folder, and it will create a .git folder within the main folder, which will hold the Git configs and history. You never have to navigate into that folder manually, it is Git's work folder.  

Congratulations, you just created your first local Git project. From now on, when you create a file within this folder or update code in an existing code file, Git will (if you let it) track the changes (*stage* the change) and set status checkpoints (*commit* the change). Moreover, VSCode will now understand that you are connected to Git as a Source Control Provider (which it does not know before you create a Git repo or before you open a source file in an existing Git repo).  

Type *control k* *control o* in VSCode, or select 'File/Open Folder...'. A folder selection window will pop up. Navigate to the folder you just created and select this folder. Any file in the folder will now be displayed in the Explorer pane (open this pane by pressing *control shift e*).  

To enable VSCode to store project specific settings, it needs to create a *workspace*. By default it will use the current project folder (which you just selected). Select 'File/Save Workspace As...' and save the workspace configuration in the Git repository folder.  



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
Alternatively, you can right click on the file name in the *Source Control* pane of VSCode and select the *Open Changes* context menu choice. This will have the same effect.  



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



## Add source files to the local Git repository

As stated before in section [Create your project environment and create a Git repository](#Create-your-project-environment-and-create-a-Git-repository): when you create a new file in VSCode within the active workspace, the file will be visible in the Explorer pane on the left side of the screen. As you might remember, you open this pane by pressing *control shift e*. Note that any ignored file (filtered by the rules in the .gitignore file) will be displayed in a slightly washed out grey color, to show that it is not controlled by Git.  

When you add code (or text) to the new file, and save it while progressing (by pressing *control s*), you will notice that the file is tagged with a 'U' sitting behind it, meaning that it is *untracked*.  

To add the new file to Git's version tracking, you must select the file in the Source Control pane, and when you hover over its filename with the mouse in the Source Control pane, a few icons will be displayed. Click the plus (+) icon. The file is now added to the local Git project: its changes have been staged (this is Git-speak for preparing a checkpoint).  

After some time you want to make the staged changes irreversible. You do this by committing the change. At the top of the Source Control panel you type a text in the text box to summarize the change in one line. Then you press *control alt enter*. The changed file (or files if you changed more than one) will now be saved into Git as the new base version, but only all changes that have been staged before.   


## Sync local Git repository to GitHub for the first time  

You could work forever with local Git repositories. 

GitHub is a Git server. There are several others, like GitLab and Microsoft TFS/Azure. A Git server has the ability to store multiple Git repositories. You can synchronize your local repository once, if you started locally (as described before), and from then on regard the version on the server as the master.

To move all local source files to a GitHub repo, you need to create a repository in GitHub first.
