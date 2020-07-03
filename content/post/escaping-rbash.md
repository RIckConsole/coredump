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
