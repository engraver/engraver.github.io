---
layout: post
title:  "Midnight commander does not percept mouse clicks"
tags: linux
math: false
---

After the last update on our HPC I noticed that Midnight commander run in SSH Bash session (Konsole from KDE) cannot interpret mouse clicks correctly and produces texts like `9:12M9;12m9:12M9:12m`. After consultation with Claude two ways of fix have been found.

## Disable mouse completely

```bash
mc --nomouse
```

and set the alias 

```bash
alias mc='mc --nomouse'
```

in `~/.bashrc`. 

## Get mouse working again

There were different suggestions, the working one is provided below. One dumps the terminal info

```bash
infocmp xterm-256color > ~/terminfo
```

The following text should be removed from `~/terminfo` if present:

```
XM=\E[?1006;1000%?%p1%{1}%=%th%el%;,
kmous=\E[M,
```

In my case, the first line has been absent, but the second one was the source of issues. The modified file then is moved into its own folder:

```bash
mkdir -p ~/.terminfo
tic -o ~/.terminfo ~/terminfo
```

and the following lines are added to `~/.bashrc`:

```bash
export TERMINFO=~/.terminfo
export TERM=xterm-256color
```

Now Midnight commander can be run with the proper interaction with mouse in the terminal.
