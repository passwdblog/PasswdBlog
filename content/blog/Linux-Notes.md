+++
author = "Root"
categories = ["Linux", "Notes", "Bash"]
tags = ["tutorial"]
date = "2019-11-15"
description = "Linux Bash Notes - Things I use often, a nice place to keep a reminder..."
featured = "bash.jpg"
featuredalt = "Bash Logo"
featuredpath = "date"
linktitle = ""
title = "Linux Bash Notes - Things I use often, a nice place to keep a reminder..."
type = "post"
+++

# BASH
I use a lot of Bash and Powershell scripts, I will update this page mainly as a aide-memoire for usefull scripts and snippets...

### 1. Time the execution time of your command or script

```
time yourscript.sh

--- or ---

start=`date +%s`
stuff
end=`date +%s`

runtime=$((end-start))

--- or ---

SECONDS=0
myScript.sh
echo $SECONDS
```

### 2. Show the current time in a script

```
echo $(date +"%T")
```

### 3. Output of a command to Bash variable

For example: Store the number of lines in a file in a Bash variable:

```
NUM_LINES=$(wc -l < "$SourceFile")
```
