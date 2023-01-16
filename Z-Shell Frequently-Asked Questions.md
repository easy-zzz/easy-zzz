---
title: 
tags: 
author: easy-zzz
source: https://zsh.sourceforge.io/FAQ/
---
Z-Shell Frequently-Asked Questions

Z-Shell Frequently-Asked Questions
==================================

Peter Stephenson
----------------

2010/02/15
----------

Table of Contents
=================


Chapter 1: Introducing zsh and how to install it
------------------------------------------------


:


    ### 1.1: Sources of information


    ### 1.2: What is it?


    ### 1.3: What is it good at?


    ### 1.4: On what machines will it run?


    ### 1.5: What's the latest version?


    ### 1.6: Where do I get it?


    ### 1.7: I don't have root access: how do I make zsh my login shell?


Chapter 2: How does zsh differ from...?
---------------------------------------


:


    ### 2.1: Differences from sh and ksh


    ### 2.2: Similarities with csh


    ### 2.3: Why do my csh aliases not work? (Plus other alias pitfalls.)


    ### 2.4: Similarities with tcsh


    ### 2.5: Similarities with bash


    ### 2.6: Shouldn't zsh be more/less like ksh/(t)csh?


    ### 2.7: What is zsh's support for Unicode/UTF-8?


    ### 2.8: Why does my bash script report an error when I run it under zsh?


Chapter 3: How to get various things to work
--------------------------------------------


:


    ### 3.1: Why does `$var` where `var="foo bar"` not do what I expect?


    ### 3.2: In which startup file do I put...?


    ### 3.3: What is the difference between \`export' and the `ALL_EXPORT` option?


    ### 3.4: How do I turn off spelling correction/globbing for a single command?


    ### 3.5: How do I get the Meta key to work on my xterm?


    ### 3.6: How do I automatically display the directory in my xterm title bar?


    ### 3.7: How do I make the completion list use eight bit characters?


    ### 3.8: Why do the cursor (arrow) keys not work? (And other terminal oddities.)


    ### 3.9: Why does my terminal act funny in some way?


    ### 3.10: Why does zsh not work in an Emacs shell mode any more?


    ### 3.11: Why do my autoloaded functions not autoload \[the first time\]?


    ### 3.12: How does base arithmetic work?


    ### 3.13: How do I get a newline in my prompt?


    ### 3.14: Why does `bindkey ^a command-name` or `stty intr ^-` do something funny?


    ### 3.15: Why can't I bind `\C-s` and `\C-q` any more?


    ### 3.16: How do I execute command `foo` within function `foo`?


    ### 3.17: Why do history substitutions with single bangs do something funny?


    ### 3.18: Why does zsh kill off all my background jobs when I logout?


    ### 3.19: How do I list all my history entries?


    ### 3.20: How does the alternative loop syntax, e.g. `while {...} {...}` work?


    ### 3.21: Why is my history not being saved?


    ### 3.22: How do I get a variable's value to be evaluated as another variable?


    ### 3.23: How do I prevent the prompt overwriting output when there is no newline?


    ### 3.24: What's wrong with cut and paste on my xterm?


    ### 3.25: How do I get coloured prompts on my colour xterm?


    ### 3.26: Why is my output duplicated with \``foo 2>&1 >foo.out | bar`'?


    ### 3.27: What are these \`\^' and \`\~' pattern characters, anyway?


    ### 3.28: How do I edit the input buffer in $EDITOR?


    ### 3.29: Why does \`which' output for missing commands go to stdout?


    ### 3.30: Why doesn't the expansion `*.{tex,aux,pdf}` do what I expect?


Chapter 4: The mysteries of completion
--------------------------------------


:


    ### 4.1: What is completion?


    ### 4.2: What sorts of things can be completed?


    ### 4.3: How does zsh deal with ambiguous completions?


    ### 4.4: How do I complete in the middle of words / just what's before the cursor?


    ### 4.5: How do I get started with programmable completion?


    ### 4.6: Suppose I want to complete all files during a special completion?


Chapter 5: Multibyte input and output
-------------------------------------


:


    ### 5.1: What is multibyte input?


    ### 5.2: How does zsh handle multibyte input and output?


    ### 5.3: How do I ensure multibyte input and output work on my system?


    ### 5.4: How can I input characters that aren't on my keyboard?


Chapter 6: The future of zsh
----------------------------


:


    ### 6.1: What bugs are currently known and unfixed? (Plus recent important changes)


    ### 6.2: Where do I report bugs, get more info / who's working on zsh?


    ### 6.3: What's on the wish-list?


    ### 6.4: Did zsh have problems in the year 2000?


    ### 6.5: When reporting a bug, how do I reduce my `.zshrc` into a minimal reproduction recipe?


<br />


**Archive-Name:**

**Last-Modified:**

**Submitted-By:**

**Posting-Frequency:**

**Copyright:**

This document contains a list of frequently-asked (or otherwise significant) questions concerning the Z-shell, a command interpreter for many UNIX systems which is freely available to anyone with FTP access. Zsh is among the most powerful freely available Bourne-like shells for interactive use.

If you have never heard of `sh`, `csh` or `ksh`, then you are probably better off to start by reading a general introduction to UNIX rather than this document.

If you just want to know how to get your hands on the latest version, skip to question 1.6; if you want to know what to do with insoluble problems, go to 6.2.

