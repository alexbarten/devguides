# Pipenv

## Contents

1. [Introduction](#Introduction)
1. [What problem does Pipenv solve?](#What-problem-does-Pipenv-solve?)

## TODO

## Introduction

Pipenv is a third party tool to manage module dependencies in projects. It combines functionality of the existing tools Pip and Venv.  

Its main functions are:

* Install modules for a project.
* Create and maintain a project environment that is separated from other projects.
* Manage dependencies between module versions within a project.
* Create and freeze installation files for a project, to help releases to other platforms and to other environments (stages).

## What problem does Pipenv solve?

Pipenv actually solves more than one problem. As stated in the introduction, it has four main functions.  

Just like Pip, it installs modules. Unlike Pip, it has advanced dependency management, for instance to solve conflicts of dependencies of dependencies between top level modules.  

Next to this, it will by default create project-specific module installations. Pip does not do this, and you would need to use Pip and Venv together to replicate this behavior.  

When you are done developing your project, you can freeze the module versions that you used, send the frozen module versions list to the environment where you want to deploy your project, run Pipenv over there and rest assured that the correct versions will be installed over there. As the frozen versions list is created independently from the installed versions in your development environment, you can keep updating versions over there, and send the latest 'frozen' list with each deployment. This way of working supports continuous deployment perfectly, and is easy to automate.  

Pipenv is promoted by the Python organization for these tasks, as a replacement for Pip and Venv.  

## Install Pipenv

Pipenv is installed through the `pip` command. You install it like this:  

```console
pip install pipenv
```

## How to use Pipenv

Pipenv is to be used from the command line. Just like `git`, you have to navigate to your project root folder, usually the same folder that is your local git project path.  

Assuming you have now navigated successfully to the project root folder, you start the pipenv shell. Type:

```console
pipenv shell
```

The command line will be prepended with a string identifying your project. Suppose that your project (and, hence, your root folder) is named `baldursgate`, your terminal line will be identified like this:

```console
(baldursgate-7IUbXOit) C:\Users\you\Documents\development\baldursgate>
```

Pipenv has now created a _virtual environment_ for your current project. This means that any module installation will be valid for the currently active project only. Its configuration is stored in a file named `Pipfile`, and this file is located in the project root folder.

> **_Note:_** Do not edit the `Pipfile` by hand. You must rely on using the `Pipenv` command instead, to prevent errors in the dependency management.

The `Pipfile` holds all module dependencies of the project. You should keep it as part of your Git project on the Git server (in other words, do not enter it in the .gitignore file), because anyone who clones the project can now easily replicate the exact same module installation on their machine.

Now, instead of using `Pip`, you must install modules with `Pipenv`, for example:

```console
pipenv install pytest
```

This will install the latest version of `pytest`.

```console
pipenv install pytest==3.2.0
```

... will install this version 3.2.0 of `pytest`.

```console
pipenv install pytest --dev
```

... will install pytest in your development environment. This means you can use it right here and now, but when you move the project to a different stage (more on that later), pytest will not be part of the deployment configuration. In other words, this argument helps you to make an important distinction between modules that you need to _develop_ software, as opposed to modules that you need to _run_ software. With `Pip` you would have to maintain two different `requirements.txt` files by hand. `Pipenv` saves you that trouble.

## Promote software to the next stage

When you are done developing your project, you want to deploy the software in a different environment, typically Test, Acceptance or Production.

In order to make sure that you deploy with the module versions that you used during the test, you must freeze the module version configuration directly after finishing your test:

```console
pipenv lock
```

This makes sure that all currently used modules (except the ones that have been installed using the --dev argument) are listed in the `Pipfile.lock` file.
