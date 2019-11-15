+++
author = "Root"
categories = ["Powershell", "Tutorial"]
tags = ["tutorial"]
date = "2019-11-15"
description = "Notes from (Twitter:@jessitron) Jessica Joy Kerr's Bash to Powershell Twitter Thread."
featured = "powershell.jpg"
featuredalt = "Hugo Logo"
featuredpath = "date"
linktitle = ""
title = "Notes from (Twitter:@jessitron) Jessica Joy Kerr's Bash to Powershell Twitter Thread"
type = "post"
+++

# Introduction
On the 13th of November 2019, someone in my Twitter feel retweeted `@jessitron` Jessica Joy Kerr's Thread titled:

 **"I sat down to learn enough PowerShell to recreate one of my bash functions."**

While I have been using Bash and PowerShell for many years, I learnt quite a few new things and thought I would write it down here for future reference.

# Bash to Powershell

## Long Names
PowerShell prefers long names, and it tries to make them generic. Verb-Noun, do what to what resource.

  `Get-Item, Set-Location`

The PowerShell glossary defines "noun" as "The word that follows the hyphen in a Windows PowerShell cmdlet name."

<a href="https://docs.microsoft.com/en-us/powershell/scripting/learn/windows-powershell-glossary?view=powershell-6" target=_blank> Windows PowerShell Glossary</a>

I like long names for readability of scripts (when trailblazing).

Short names are better for exploring.

## Aliases

PowerShell has aliases, and the standard ones also combine, like "g" for Get- and "l" for Location

`gl=Get-Location`

<a href="https://docs.microsoft.com/en-us/powershell/scripting/learn/using-familiar-command-names?view=powershell-6#interpreting-standard-aliases" target=_blank>Using Familiar Command Names</a>

I love that you get these AND long names for making descriptive scripts.

## STDIN and STDOUT
In bash (and other Unix shells), programs compose on STDIN and STDOUT. The interface between them is strings of text.

In PowerShell, the interface is objects. Programs (cmdlets) pipe objects to each other.

Ah, rich data! Ah, no string parsing!

PowerShell provides each cmdlet with standard

- command-line parsing
- help, triggered by -?
- definitions of some common parameters
- output formatting
- error handling options (coooool)


## WhatIF

The common parameter -WhatIf is a great idea! It's like --dry-run in some Unix utilities like make.

Separate making decisions from implementing them.

You can even turn it on for the whole session with `$WhatIfPreference=$true`

![](/img/2019/11/jessitron-1.jpg)

## -ErrorAction

Then there's the very cool -ErrorAction common parameter.
Set it to "SilentlyContinue" when you don't want errors printed to stderr.

For instance, test whether a directory exists:
if (Get-Location -Path $ofInterest -ErrorAction SilentlyContinue) { … }

## Output Formatting
Output formatting: by default you get some reasonable printout of the object. Or, pipe the output to a formatting cmdlet, like
Format-Table -Property name,value,etc -wrap
Out-Host -paging (like piping to 'less')
Get-Member (like reflection -- see methods & properties)

I got all excited about this and then had a very hard time figuring out how to make a cmdlet at all.

So far:
- make a file with extension .ps1
- create a function in there, and then make it an "advanced function" by adding cmdlet support
- source this file: . ./whatever.ps1

![](/img/2019/11/jessitron-2.png)

but watch out - you need the cmdlet spell and then params(). You'll get an error about CmdletBinding "Unexpected attribute"
until you add params() AFTER it. 
WTFMS

![](/img/2019/11/jessitron-3.jpg)

Here's a weird thing: any command that you call in your function, if it returns something and you don't assign that to a variable or pipe it somewhere, that becomes an object that is output from your script.
Also any value that you put on a line by itself.

![](/img/2019/11/jessitron-4.jpg)
![](/img/2019/11/jessitron-4b.jpg)

PowerShell has a distinction between data output, which continues through the pipeline, and output to the user.

`Write-Host` sends a message to the person running the cmdlet. Something on a line by itself goes down the pipe.

![](/img/2019/11/jessitron-5.jpg)
![](/img/2019/11/jessitron-5b.jpg)

## Exit Code
Checking the exit code of a command is different than in bash. Use $LastExitCode, and test with bash-like comparison operators.

This pops a dialog if "git push" fails:
![](/img/2019/11/jessitron-6.jpg)

## Comparison Operators
Windows is generally case-insensitive. Comparison operators like "-eq" are case-insensitive with strings.

There are case-sensitive versions that add a C.
"Yes" -eq "yes"
but NOT
"Yes -ceq "yes"

I guess this is a benefit of using short names instead of symbols for the operators.


## Tee-object
Like unix tee but even more useful: Tee-Object.
Use it to send output to multiple places. The extra one can be a file or a variable.
![](/img/2019/11/jessitron-7.jpg)

## Newline in strings
Oh, and PowerShell for newline in strings is

`n

(backtick n)
Instead of \n

## Function Parameters
My function (and the alias to it) automatically accept positional parameters in the order I declared them, or named parameters in any order.
Cool! Did not expect!

I love happy surprises like this. It's like Ruby, except easier to install.

## Window Title Change
Now I want to change the title of the terminal tab.

bash:
    echo -ne "\033]0;Changed Title\007"

PowerShell:
   $host.ui.RawUI.WindowTitle = “Changed Title”
💗

## Snippets
ooh VS Code has a snippet for cmdlets --
Type "cmdlet" and ctrl-space. It gives me a whole template for the cmdlet!

![](/img/2019/11/jessitron-8.jpg)
![](/img/2019/11/jessitron-8b.png)

## Map Objects in the Pipe
I finally figured out how to map the objects in the pipe.
It's foreach, then a block in curlies and $_ is the current object.

Get-ChildItem | foreach { $_.name }
![](/img/2019/11/jessitron-9.png)

## Saving Output to a variable
OK, here's something weird. I wanted to get the error message from 'git push' and save it, so that I can display it in my popup dialog.

So, pipe stderr to stdout (like in unix), then tee it to a variable

git push 2>&1 | Tee-Object -Variable PushOutput

![](/img/2019/11/jessitron-10.jpg)
![](/img/2019/11/jessitron-10b.png)

The weird thing is, when git push succeeds, I get a sad error to my console. And the git push output doesn't make it to my screen.

![](/img/2019/11/jessitron-11.png)

Here's the deal: git push writes "Everything up to date" to STDERR.
PowerShell turns everything that came in on STDERR from a string into an ErrorRecord. So I get an ErrorRecord instead.

It's worse when the push does something; the output of the push report is obscured.

![](/img/2019/11/jessitron-12.png)

Why does git send these happy messages to STDERR?
Because it's reserving STDOUT for data that might be piped to another Linux command.
Git writes to STDERR for lack of Write-Host.

PowerShell distinguishes between data output and messages to the user. 💝


So I made a Function to unwrap the error and put it back into a string. It makes sense to pipe through this when I know the command I ran uses STDERR for messages.

<a href="https://gist.github.com/jessitron/c44df7957d2087b49d9fb4bf0b385ef7">fix-stderr.ps1</a>

Piping through my process converts those ErrorRecords in the pipe back into strings, and everything works as expected.

git push 2>&1 | fix-stderr | Tee-Object -Variable PushOutput

![](/img/2019/11/jessitron-13.jpg)
![](/img/2019/11/jessitron-13b.png)
