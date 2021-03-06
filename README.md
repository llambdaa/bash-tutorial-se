# SE-ePortfolio (Bash)
![Bash Logo](https://upload.wikimedia.org/wikipedia/commons/8/82/Gnu-bash-logo.svg)

## Introduction

[Bash](https://de.wikipedia.org/wiki/Bash_(Shell)) is probably the best known shell in the Unix world. It is not only an abstraction </br> of your system (interface) but also a programming/scripting language.

The [presentation](https://docs.google.com/presentation/d/1s_FAR7T6KUhhVNeWfuA77YC00YZyVPudaZfnssebT-w/edit#slide=id.gfbece3e7b9_0_55) shall help you to make your first steps into the Unix/GNU/Linux world and to </br> understand (at least roughly) what is going on behind the scenes and how some things come together.

The talk incorporates a very short theoretical introduction about what shells are and
which types exist, </br> before I jump right into a practical part.
There is simply not much to visualize since bash itself is very </br> system-near.
However, there are many concepts we can explore by working with the system.

Honestly, the syntax is sophisticated and especially for newbies seems cryptic and intimidating. </br>
This is because bash is very nuanced - its short syntax forces extremely high semantic density. </br>
One wrong token in the wrong context can blow up your work, especially when working with arrays </br>
and evaluating expressions. Hence, we only focus on simple behavior and predictable semantics. </br>
But for the ones interested, I provide [cheat sheets](#Cheat-Sheets) and additional information.

So, the overall goal is to show you what is **theoretically** possible. </br>
In the practical part I, I will show you how the shells operates and which
features for every-day-usage it provides. </br> In the practical part II, I want
to show you how you can make your own commands and thus expand the shell - </br>
something I have struggled with when learning bash myself.
  
## Prerequisites
You should have a working Unix system (macOS, GNU/Linux[e.g. Ubuntu]) in order to participate
during the presentation session. If you don't have one, you can set one up for free using a Virtual Machine (VM).

There are many VMs, e.g. [Virtual Box](https://www.virtualbox.org/).
Similarly, there are many good [tutorials](https://www.youtube.com/watch?v=x5MhydijWmc) on how to
set up your system. Most likely, you would want to install a GNU/Linux distribution. For the purpose of the talk,
the exact type doesn't matter - </br> but I would recommend [Ubuntu 21.10](https://releases.ubuntu.com/21.10/), since it is easy to install, and I
can verify that it works.
  
## Cheat Sheets
### Replacements
| Placeholder | Description       |
|-------------|-------------------|
| ~           | Home Directory    |
| .           | Working Directory |
| ..          | Parent Directory  |
| /           | Root Directory    |

### Useful Commands
| Command     | Description             |
|-------------|-------------------------|
| man         | Show Command Help       |
| pwd         | Print Working Directory |
| ls          | Show Folder Content     |
| cd          | Change Directory        |
| cat         | Concatenate to STDOUT   |
| grep        | Search for RegEx        |
| cp          | Copy File               |
| mv          | Move File               |
| rm [-r]     | Delete File/Folder      |
| mkdir       | Make Directory          |
| chmod       | Change File Mode        |
| find        | Search File             |
| where       | Print Command Path      |
| touch       | Modify File Metadata    |
| clear       | Clear Terminal          |
| sudo        | Request Root Previleges |
| source      | Reload Shell Session    |

### More Information
  (1) [Bash General](https://devhints.io/bash) </br>
  (2) [GNU Reference](https://www.gnu.org/savannah-checkouts/gnu/bash/manual/bash.html) </br>
  (3) [Bracket Notation](https://stackoverflow.com/questions/2188199/how-to-use-double-or-single-brackets-parentheses-curly-braces)
  
## Explanation
##### Logic
I have prepared a custom command for the talk - afterwards you should at least know how </br>
to make a global command yourself. Although the syntax is rather strange, the logic is simple:

<pre>
(1) Determine the amount of given arguments.
    Error is thrown if there is not at least one.
(2) The first argument (we don't care about more) must be
    a natural number (proven with RegEx).
(3) Have an accumulator. Iterate n times and multiply the accumulator
    with loop counter variable. This leads to ```1*2*3*...\*n=n!```
(4) Returning result.
</pre>

##### Execution
The script can be using ```bash ./path/to/script/fac```.
However, defining the executing </br> interpreter (```bash```) is cumbersome and repetitive. Including the [shebang](https://de.wikipedia.org/wiki/Shebang) ```#!/bin/bash``` does the trick. </br> The command could now be run with ```./path/to/script/fac```.

##### chmod
However, if not already done, the script must be set to executable mode.
Otherwise, the interpreter won't run it, </br> because the file is seen as a normal text file.
To do so, execute ```chmod +x ./path/to/script/fac```. </br> This will add(*+*) the mode e*X*ecutable to the script file.

##### Globalization
The script is now executable, but not globally visible. You still have to provide a path to the file </br> and
thus it is seen as a simple script, not as a command. </br></br>Either, you move it into a folder found in $PATH - this is
where the system looks for files with the </br> name matching the issued command. Or you include the path to your command
into $PATH. </br></br>One way to do so, is to edit ```~/.bashrc``` using the editor of your least mistrust. </br> In there, you enter ```PATH=$PATH:/path/to/script/```. This script will be issued each time an </br> interactive session is started and so $PATH will always include your custom path. </br> After editing, you have to either source .bashrc or restart the terminal.
