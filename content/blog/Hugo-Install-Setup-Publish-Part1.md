+++
author = "Root"
categories = ["Hugo", "Tutorial"]
tags = ["tutorial"]
date = "2019-11-01"
description = "Learn how to install and set-up Hugo, and publish to GitHub pages using a custom domain."
featured = "Hugo-Logo-004.png"
featuredalt = "Hugo Logo"
featuredpath = "date"
linktitle = ""
title = "PART 1: Hugo: Installation, Setup and publishing to GitHub pages using a custom domain."
type = "post"

+++

# Introduction
This post is somewhat meta, it describes my journey installing  ``` hugo ```, setting up Hugo on my authoring **machines** and publishing the site to GitHub pages using a custom domain. 

I will detail both [Windows 10]({{<ref "#windows" >}}) and [Ubuntu-19.10]({{<ref "#ubuntu" >}}) setups. 

I found a lot of very good information on the web, but found it a bit fragmented and made a lot of assumptions, especially as far as ```git``` knowledge is concerned.  

Click [here]({{<relref "/blog/Hugo-Install-Setup-Publish-Part1.md">}}) for Part 1.
### In Part 1
1. Installing Hugo
2. Configuring Hugo
3. Creating a Hugo Site

Click [here]({{<relref "/blog/Hugo-Install-Setup-Publish-Part2.md">}}) for Part 2.
### In Part 2
1. Installing Git
2. Setting up GitHub
3. Setting up Git to work with Hugo
4. Installing a Theme
5. Running the site for the first time
6. Pushing all the code to GitHub

Click [here]({{<relref "/blog/Hugo-Install-Setup-Publish-Part3.md">}}) for Part 3.
### In Part 3
1. Build the site for the first time
2. Adding the published site to GitHub
3. Ongoing editing and publishing



___

# windows
## Windows 10 Setup
In this tutorial, commands that you enter will start with the ">" prompt. For example: ```C:\Hugo\Sites>``` The output will follow. Lines that start with "REM" are comments that I've added to explain a point. When I show updates to a file, the ```[SAVE&EXIT]``` on the last line means to save the file and exit from the editor.

Here's an example:

```
REM this is a comment
C:\Hugo> echo this is a command
this is a command

REM edit the file
C:\Hugo>notepad foo.md
+++
date = "2019-11-01"
title = "creating a post"
+++

Text in the post goes here....
[SAVE&EXIT]

REM show it
$ type foo.md
+++
date = "2019-11-01"
title = "creating a post"
+++

Text in the post goes here....
C:\Hugo>
```

## Assumptions
1. You will use ```C:\Hugo\Sites``` as the starting point for your new project.
2. You will use ```C:\Hugo\bin``` to store executable files
3. I am using ```PasswdTest.Blog``` as the name of my site, directories, etc. Substitute your site wherever you see PasswdTest.Blog.
4. You will be publishing your site to GitHub Pages using a custom domain name.
5. You have an account on GitHub.

## Check if hugo is installed
```
REM run the command from a dos prompt
C:\Hugo>hugo --help

hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.

...
etc
...

```
If you see the text above then Hugo is installed and working correctly.

## Installing Hugo
If you don't have hugo installed, download the latest version from https://github.com/gohugoio/hugo/releases

On Windows 10 the file is called ```hugo_extended_0.59.1_Windows-64bit.zip```

Create the following directories:
```
REM create C:\Hugo and C:\Hugo\bin directories
C:\>md Hugo
C:\Hugo>md bin
```

Unzip the downloaded file into the ```C:\Hugo\bin\``` folder. You should now have three files in the folder:
```
C:\Hugo\bin>dir
 Volume in drive C has no label.
 Volume Serial Number is A4A4-A8FE

 Directory of C:\Hugo\bin

02/11/2019  11:14 PM    <DIR>          .
02/11/2019  11:14 PM    <DIR>          ..
21/10/2019  08:41 PM        38,937,088 hugo.exe
21/10/2019  08:33 PM            11,357 LICENSE
21/10/2019  08:33 PM            11,235 README.md
               3 File(s)     38,959,680 bytes
               4 Dir(s)  83,648,753,664 bytes free
```

If you run ```hugo --help``` now you should see the output in the section above. The command will only work from the ```C:\Hugo\Bin\``` directory since Windows will not be able to find from anywhere else in your system. 

To fix this we will add the path to hugo to Windows' ```%PATH%``` variable.

## Adding hugo.exe to the Windows %PATH% variable

1. Right click on the ```This PC``` icon.
2. Click on Advanced System Settings on the left.
3. Click on the Environment Variables… button on the bottom.
4. In the User variables section, find the row that starts with PATH.
5. Double-click on PATH.
6. Click the ```New``` button.
7. Type ```C:\Hugo\bin``` and click OK.
8. Click OK at every window to exit.
9. Open a new Command Prompt window and type ```hugo --help``` to make sure the path works.


# Creating your hugo site
Now we can start to create your site. To keep things neat we will store all our sites in the ```C:\Hugo\Sites``` directory.

```
C:\Hugo>md Sites

cd Sites

C:\Hugo\Sites>
```

Run the command to generate a new site. I am using ```PasswdTest.Blog``` as the name of the site.
```

C:\Hugo\Sites> hugo new site PasswdTest.Blog


Congratulations! Your new Hugo site is created in C:\Hugo\Sites\PasswdTest.Blog.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.

```

You should now have a directory at ```C:\Hugo\Sites\PasswdTest.Blog```. Change into that directory and list the contents. Your output should look similar to the following:
```
C:\Hugo\Sites> cd PasswdTest.Blog

C:\Hugo\Sites\PasswdTest.Blog> dir

 Volume in drive C has no label.
 Volume Serial Number is A4A4-A8FE

 Directory of C:\Hugo\Sites\PasswdTest.Blog

03/11/2019  08:26 AM    <DIR>          .
03/11/2019  08:26 AM    <DIR>          ..
03/11/2019  08:26 AM    <DIR>          archetypes
03/11/2019  08:26 AM                82 config.toml
03/11/2019  08:26 AM    <DIR>          content
03/11/2019  08:26 AM    <DIR>          data
03/11/2019  08:26 AM    <DIR>          layouts
03/11/2019  08:26 AM    <DIR>          static
03/11/2019  08:26 AM    <DIR>          themes
               1 File(s)             82 bytes
               8 Dir(s)  83,632,214,016 bytes free

```
Continue to [Part 2]({{<relref "/blog/Hugo-Install-Setup-Publish-Part2.md">}}).
___

# ubuntu
## Ubuntu 19.10 Linux Setup
In this tutorial, commands that you enter will start with the "$" prompt. The output will follow. Lines that start with "#" are comments that I've added to explain a point. When I show updates to a file, the ":wq" on the last line means to save the file.


Here's an example:

```
## this is a comment
$ echo this is a command
this is a command

## edit the file
$vi foo.md
+++
date = "2019-11-01"
title = "creating a post"
+++

Text in the post goes here....
:wq

## show it
$ cat foo.md
+++
date = "2014-09-28"
title = "creating a post"
+++

Text in the post goes here....
$
```

## Assumptions
1. You will use your "home" directory ```/home/user``` as the starting point for your new project.
2. I am using ```PasswdTest.Blog``` as the name of my site, directories, etc. Substitute your site wherever you see PasswdTest.Blog.
3. You will be publishing your site to GitHub Pages using a custom domain name.
4. You have an account on GitHub.

## Check if hugo is installed
```
# run the command from a terminal window
$ hugo --help

hugo is the main command, used to build your Hugo site.

Hugo is a Fast and Flexible Static Site Generator
built with love by spf13 and friends in Go.

Complete documentation is available at http://gohugo.io/.

...
etc
...

```
If you see the text above then Hugo is installed and working correctly.

## Installing Hugo
If you don't have hugo installed, enter the command below:

```
# install hugo via snap
$ sudo snap install hugo
hugo 0.59.1 from Hugo Authers installed
```

There are various other ways to install hugo, flex your <a href="https://en.wiktionary.org/wiki/Google-fu" target="_blank">Google-Fu</a>.

You can now try to run ```hugo --help``` again from a terminal and you should see the output above if the installation was successful.

# Creating your hugo site
Now we can start to create your site. To keep things simple we will store all our sites in the "home" directory ```/home/user``` or ```~/```. Wherever we use ```~``` in the tutorial we mean ```/home/user```, everything will be relative to that path.

```
~$ mkdir Sites

cd Sites

~/Sites$
```

Run the command to generate a new site. I am using ```PasswdTest.Blog``` as the name of the site.
```

~/Sites$ hugo new site PasswdTest.Blog


Congratulations! Your new Hugo site is created in C:\Hugo\Sites\PasswdTest.Blog.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>\<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.

```

You should now have a directory at ```~/Sites/PasswdTest.Blog```. Change into that directory and list the contents. Your output should look similar to the following:
```
~/Sites$cd PasswdTest.Blog

~/Sites/PasswdTest.Blog$ ls -la

total 4
drwxr-xr-x 8 ubuntu ubuntu 180 Nov  2 21:33 .
drwxr-xr-x 3 ubuntu ubuntu  60 Nov  2 21:33 ..
drwxr-xr-x 2 ubuntu ubuntu  60 Nov  2 21:33 archetypes
-rw-r--r-- 1 ubuntu ubuntu  82 Nov  2 21:33 config.toml
drwxr-xr-x 2 ubuntu ubuntu  40 Nov  2 21:33 content
drwxr-xr-x 2 ubuntu ubuntu  40 Nov  2 21:33 data
drwxr-xr-x 2 ubuntu ubuntu  40 Nov  2 21:33 layouts
drwxr-xr-x 2 ubuntu ubuntu  40 Nov  2 21:33 static
drwxr-xr-x 2 ubuntu ubuntu  40 Nov  2 21:33 themes

~/Sites/PasswdTest.Blog$

```

Continue to [Part 2]({{<relref "/blog/Hugo-Install-Setup-Publish-Part2.md">}}).
