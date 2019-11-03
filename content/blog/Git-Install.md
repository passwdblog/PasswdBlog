+++
author = "Root"
categories = ["Git", "Tutorial"]
tags = ["tutorial"]
date = "2019-11-01"
description = "Installing Git for use with Hugo."
featured = "Git-Logo-002.jpg"
featuredalt = "Git Logo"
featuredpath = "date"
linktitle = ""
title = "Git: Installation and Setup for hugo."
type = "post"

+++

# Introduction
This Git installation tutorial is very specific to deploying a ``` hugo ``` website to GitHub Pages using a custom domain. The hugo installation, setup and deployment tutorial can be found [here]({{<relref "/blog/Hugo-Install-Setup-Publish.md">}}).

I will detail both [Windows 10]({{<ref "#windows" >}}) and [Ubuntu-19.10]({{<ref "#ubuntu" >}}) setups. 

___

# windows
## Windows 10 Setup

## Check if git is installed
```
REM run the command from a dos prompt
C:\>git

usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
...
etc
...

```
If you see the text above then Git is installed and working correctly.

## Installing Git
If you don't have hugo installed, download the latest version from https://git-scm.com/download/win. The download of the 64-bit version will start automatically.

Run the executable, I used all the **default** settings except for the Editor setting that I changed from VIM to Notepad++. Choose whatever you are comfortable with.

If you run ```git``` now you should see the output in the section above.

___

# ubuntu
## Ubuntu 19.10 Linux Setup

## Check if git is installed
```
# run the command from a terminal window
$ git

usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]
...
etc
...

```
If you see the text above then Git is installed and working correctly.

## Installing Git
If you don't git hugo installed, enter the command below:

```
# install git via apt
$ sudo apt install git -y

# run git after the installation has completed to check the installation
$ git

```
