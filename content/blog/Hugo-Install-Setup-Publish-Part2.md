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
title = "PART 2: Hugo: Installation, Setup and publishing to GitHub pages using a custom domain."
type = "post"

+++

# Introduction
This is Part 2 of my journey installing  ``` hugo ```, setting up Hugo on my authoring **machines** and publishing the site to GitHub pages using a custom domain. 

I will detail both [Windows 10]({{<ref "#windows" >}}) and [Ubuntu-19.10]({{<ref "#ubuntu" >}}) setups. 

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
*(There may be many better ways to do this, but this WORKS for me)*

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
If you don't have git installed, download the latest version from https://git-scm.com/download/win. The download of the 64-bit version will start automatically.

Run the executable, I used all the **default** settings except for the Editor setting that I changed from VIM to Notepad++. Choose whatever you are comfortable with.

If you run ```git``` now you should see the output in the section above.


## GitHub

Register for GitHub if you don't have an account, once you have registered, log in with your GitHub account. On the top right of the main GitHub page click on the small down arrow and select ```Settings```.

Once in the settings menu select ```SSH and GPG keys```, and then click on ```New SSH key```.

### Generating your SSH key.

Click on the Windows start menu and select ```Git Bash```.

In the Git Bash window enter the following command to generate an SSH key:
```
# Change the email address to the one you used to sign up to GitHub!!
# Accept the default path when offered

$ssh-keygen -t rsa -b 4096 -C "your_github_email@domain.com"

Generating public/private ras key pair.

Enter file in which to save the key (/c/Users/user/.ssh/id_rsa)    [Press Enter to accept the default path]

Created directory '/c/Users/user/.ssh'.

Enter passphrase (empty for no passphrase):    [Enter a password if you wish]
Enter same passphrase again: 

Your identification has been saved in /c/Users/user/.ssh/id_rsa.
Your public key has been saved in /c/Users/user/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:AbCdEfG1234567jLbrOkQOYvLXxvs2gojrqvrkuKxnDb7A8 your_github_email@domain.com
The key's randomart image is:
+---[RSA 4029]----+
|          . =.o. |
|           + O   |
|          o = o  |
|         . +     |
|        S   .    |
|. .    +   . .   |
|oo +E  .oo  +    |
|+o. oo. =o+==    |
|*+=*+oo. =++==   |
+----[SHA256]-----+

```

Your private and public RSA key will are stored in /c/Users/user/.ssh  (Accessible via Git Bash).

```
# Change directory to .ssh and do an ls -la to see the files
$ cd .ssh
$ ls -la

total 8
-rw-r--r-- 1 user 197121 3324 Nov  3 13:54 id_rsa
-rw-r--r-- 1 user 197121  730 Nov  3 13:54 id_rsa.pub
```

You now need to copy your Public Key (id_rsa.pub) to GitHub. To see your public key run the following:
```
# show the contents of id_rsa.pub to see your public key
$ cat id_rsa.pub
ssh-rsa BBBB3NzaC1yc2EAAAADAQABAAAB+Bao45bJuM9DljnmwVxRjNK22SXyBIxCmiSPSAMRi/
3tNp9LIULIUtj9Nk98YD1kjxkNcsRjshblrZKXcZIj5D3plIFNL+DvKp3Z6GdfVE7Rho7c3/
+uvdXTvi5Fo4/sMIQNNBoBbuoTVwXZK/OpRjf0nB2lIxWckx9lLikIcfVpk+LLpxqcbQH8fB/
lZDtdVslznxFCpLssEWZlXaBUm/DvATK5aln3W2jTziLLM4hJ/
1A1S9es0hxQjpyq3fJkivAgNYe/bQR6mKmWguGyLVDngjO4BezERhJjBbWQPgH8lZFcFuzLzOs4hgJI/
p0yuK7nr9hqbBHq6jb20l9JzSGoGOXNZyydK6w/rAM+20R+kSPWIsb96K6YGQB/
n3c33+wJJrwLl0z0a+ZN7ms7ADLydcrRGOp2eZCPbHtqRsoXqgKkbQVI+rd8uJB/
3o4dqMtG95UCj8M45Fh7Ms90cIw5UWclNxjKrdVSyEVNzy/oftxSlw== your_github_email@domain.com
```

Go back to GitHub, enter a description in the ```Title``` field, and paste all the text into the ```Key``` field. The key should contain everything in id_rsa.key, including ssh-rsa at the beginning and your email address at the end.

Click ```Add SSH Key``` to save your key.

Test your SSH Keys with GitHub by running the following:
```
# From Git Bash run the following command to test your SSH keys with GitHub
$ ssh -T git@github.com

Hi your_github_username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Creating your GitHub Repository
Click on + (Plus) sign at the top right of the GitHub page and select ```New Repository```.

In the Repository name filed enter the name of your site, for example ```PasswdTest.Blog```. 
Ensure you have set the repository to ```public``` and click on Create repository.


## Setting up Git to work with Hugo
Now we can start to configure git to work with your site.

```
REM Change directory to where your site is located
C:\>cd \Hugo\Sites\PasswdTest.Blog

C:\Hugo\Sites\PasswdTest.Blog> git init
Initialized empty Git repository in C:/Hugo/Sites/PasswdTest.blog/.git/

REM I am using the hugo-future-imperfect theme
REM get the theme from github as a submodule 
C:\Hugo\Sites\PasswdTest.Blog> git submodule add https://github.com/jpescador/hugo-future-imperfect.git themes\hugo-future-imperfect

Cloning into 'C:/Hugo/Sites/PasswdTest.Blog/themes\hugo-future-imperfect'...
remote: Enumerating objects: 1386, done.
Receiving objects: 100% (1386/1386), 4.38 MiB | 2.65 MiB/s, done.
Resolving deltas: 100% (792/792), done.
warning: LF will be replaced by CRLF in .gitmodules.
The file will have its original line endings in your working directory
```

You should now see a ```hugo-future-imperfect``` directory under C:\Hugo\Sites\PasswdTest.blog\themes.

*I had issues commiting files to GitHub without the following two lines YMMMV*
```
git config user.name "your_github_username"
git config user.email "your_github_email@domain.com"
```

If you have content for your site already you can skip this step, if you want some sample content the run the following:
```
REM Copy the hugo-future-imperfect sample data to your site
C:\Hugo\Sites\PasswdTest.Blog> xcopy C:\Hugo\Sites\PasswdTest.Blog\themes\hugo-future-imperfect\exampleSite\*.* C:\Hugo\Sites\PasswdTest.Blog /s /e
```

We are now ready to test the site. 
```
REM start the hugo server to view the sample site
REM NOTE: you have to be in your site's directory
C:\Hugo\Sites\PasswdTest.Blog>hugo server

Building sites …
                   | EN
+------------------+----+
  Pages            | 32
  Paginator pages  |  2
  Non-page files   |  0
  Static files     | 17
  Processed images |  0
  Aliases          |  6
  Sitemaps         |  1
  Cleaned          |  0

Total in 120 ms
Watching for changes in C:\Hugo\Sites\PasswdTest.Blog\{archetypes,content,data,layouts,static,themes}
Watching for config changes in C:\Hugo\Sites\PasswdTest.Blog\config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at //localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Browse to ```localhost:1313``` to view the site.

### Doing the first commmit to GitHub
```
REM Do the initial commit to GitHub
C:\Hugo\Sites\PasswdTest.Blog>git commit -m "initial commit"
[master (root-commit) fd968e8] initial commit
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 themes/hugo-future-imperfect


C:\Hugo\Sites\PasswdTest.Blog>git add *

C:\Hugo\Sites\PasswdTest.Blog>git remote add origin git@github.com:your_github_username/your_github_repository.Blog.git

C:\Hugo\Sites\PasswdTest.Blog>git push -u origin master

Warning: Permanently added the RSA host key for IP address '123.123.123.123' to the list of known hosts.
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 20 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 397 bytes | 397.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
remote: This repository moved. Please use the new location:
remote:   git@github.com:your_github_username/your_github_repository.git
To github.com:your_github_username/your_github_repository.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```

Refresh your GitHub page, all the directories and files in your site's directory should now be in GitHub.

Continue to [Part 3]({{<relref "/blog/Hugo-Install-Setup-Publish-Part3.md">}}).

















___

# ubuntu
*(There may be many better ways to do this, but this WORKS for me)*

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
If you don't have git installed, enter the command below:

```
# install git via apt
$ sudo apt install git -y

# run git after the installation has completed to check the installation
$ git

```




Register for GitHub if you don't have an account, once you have registered, log in with your GitHub account. On the top right of the main GitHub page click on the small down arrow and select ```Settings```.

Once in the settings menu select ```SSH and GPG keys```, and then click on ```New SSH key```.

### Generating your SSH key.

Enter the following command to generate an SSH key:
```
# Change the email address to the one you used to sign up to GitHub!!
# Accept the default path when offered

$ssh-keygen -t rsa -b 4096 -C "your_github_email@domain.com"

Generating public/private ras key pair.

Enter file in which to save the key (/home/user/.ssh/id_rsa)    [Press Enter to accept the default path]

Created directory '/home/user/.ssh'.

Enter passphrase (empty for no passphrase):    [Enter a password if you wish]
Enter same passphrase again: 

Your identification has been saved in /c/Users/user/.ssh/id_rsa.
Your public key has been saved in /c/Users/user/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:AbCdEfG1234567jLbrOkQOYvLXxvs2gojrqvrkuKxnDb7A8 your_github_email@domain.com
The key's randomart image is:
+---[RSA 4029]----+
|          . =.o. |
|           + O   |
|          o = o  |
|         . +     |
|        S   .    |
|. .    +   . .   |
|oo +E  .oo  +    |
|+o. oo. =o+==    |
|*+=*+oo. =++==   |
+----[SHA256]-----+

```

Your private and public RSA key will are stored in /home/user/.ssh

```
# Change directory to .ssh and do an ls-la to see the files
$ cd .ssh
$ ls -la

total 8
-rw-r--r-- 1 user 197121 3324 Nov  3 13:54 id_rsa
-rw-r--r-- 1 user 197121  730 Nov  3 13:54 id_rsa.pub
```

You now need to copy your Public Key (id_rsa.pub) to GitHub. To see your public key run the following:
```
# show the contents of id_rsa.pub to see your public key
$ cat id_rsa.pub
ssh-rsa BBBB3NzaC1yc2EAAAADAQABAAAB+Bao45bJuM9DljnmwVxRjNK22SXyBIxCmiSPSAMRi/
3tNp9LIULIUtj9Nk98YD1kjxkNcsRjshblrZKXcZIj5D3plIFNL+DvKp3Z6GdfVE7Rho7c3/
+uvdXTvi5Fo4/sMIQNNBoBbuoTVwXZK/OpRjf0nB2lIxWckx9lLikIcfVpk+LLpxqcbQH8fB/
lZDtdVslznxFCpLssEWZlXaBUm/DvATK5aln3W2jTziLLM4hJ/
1A1S9es0hxQjpyq3fJkivAgNYe/bQR6mKmWguGyLVDngjO4BezERhJjBbWQPgH8lZFcFuzLzOs4hgJI/
p0yuK7nr9hqbBHq6jb20l9JzSGoGOXNZyydK6w/rAM+20R+kSPWIsb96K6YGQB/
n3c33+wJJrwLl0z0a+ZN7ms7ADLydcrRGOp2eZCPbHtqRsoXqgKkbQVI+rd8uJB/
3o4dqMtG95UCj8M45Fh7Ms90cIw5UWclNxjKrdVSyEVNzy/oftxSlw== your_github_email@domain.com
```

Go back to GitHub, enter a description in the ```Title``` field, and paste all the text into the ```Key``` field. The key should contain everything in id_rsa.key, including ssh-rsa at the beginning and your email address at the end.

Click ```Add SSH Key``` to save your key.

Test your SSH Keys with GitHub by running the following:
```
# Run the following command to test your SSH keys with GitHub
$ ssh -T git@github.com

Hi your_github_username! You've successfully authenticated, but GitHub does not provide shell access.
```

### Creating your GitHub Repository
Click on + (Plus) sign at the top right of the GitHub page and select ```New Repository```.

In the Repository name filed enter the name of your site, for example ```PasswdTest.Blog```. 
Ensure you have set the repository to ```public``` and click on Create repository.


## Setting up Git to work with Hugo
Now we can start to configure git to work with your site.

```
# Change directory to where your site is located
$ cd ~/Sites/PasswdTest.Blog

~/Sites/PasswdTest.Blog$ git init
Initialized empty Git repository in /home/user/PasswdTest.blog/.git/

# I am using the hugo-future-imperfect theme
# get the theme from github as a submodule 
~/Sites/PasswdTest.Blog$ git submodule add https://github.com/jpescador/hugo-future-imperfect.git themes/hugo-future-imperfect

Cloning into '/home/user/Sites/PasswdTest.Blog/themes/hugo-future-imperfect'...
remote: Enumerating objects: 1386, done.
Receiving objects: 100% (1386/1386), 4.38 MiB | 2.65 MiB/s, done.
Resolving deltas: 100% (792/792), done.
```

You should now see a ```hugo-future-imperfect``` directory under /home/user/Sites/PasswdTest.blog/themes.

*I had issues commiting files to GitHub without the following two lines YMMMV*
```
git config user.name "your_github_username"
git config user.email "your_github_email@domain.com"
```

If you have content for your site already you can skip this step, if you want some sample content the run the following:
```
# Copy the hugo-future-imperfect sample data to your site
~/Sites/PasswdTest.Blog$ cp -r ~/Sites/PasswdTest.Blog/themes/hugo-future-imperfect/exampleSite/* ~/Sites/PasswdTest.Blog
```

We are now ready to test the site. 
```
# start the hugo server to view the sample site
# NOTE: you have to be in your site's directory
~/Sites/PasswdTest.Blog$ hugo server

Building sites …
                   | EN
+------------------+----+
  Pages            | 32
  Paginator pages  |  2
  Non-page files   |  0
  Static files     | 17
  Processed images |  0
  Aliases          |  6
  Sitemaps         |  1
  Cleaned          |  0

Total in 120 ms
Watching for changes in /home/user/Sites/PasswdTest.Blog/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /home/user/Sites/PasswdTest.Blog/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at //localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```

Browse to ```localhost:1313``` to view the site.

### Doing the first commmit to GitHub
```
# Do the initial commit to GitHub
~/Sites/PasswdTest.Blog$ git commit -m "initial commit"
[master (root-commit) fd968e8] initial commit
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 themes/hugo-future-imperfect


~/Sites/PasswdTest.Blog$ git add *

~/Sites/PasswdTest.Blog$ git remote add origin git@github.com:your_github_username/your_github_repository.Blog.git

~/Sites/PasswdTest.Blog$ git push -u origin master

Warning: Permanently added the RSA host key for IP address '123.123.123.123' to the list of known hosts.
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 20 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 397 bytes | 397.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
remote: This repository moved. Please use the new location:
remote:   git@github.com:your_github_username/your_github_repository.git
To github.com:your_github_username/your_github_repository.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```

Refresh your GitHub page, all the directories and files in your site's directory should now be in GitHub.

Continue to [Part 3]({{<relref "/blog/Hugo-Install-Setup-Publish-Part3.md">}}).







