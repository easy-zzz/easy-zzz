# Babun - оболочка Windows, которая вам понравится

Хотели бы вы использовать консоль, подобную Linux, на хосте Windows без особых сложностей? Попробуй бабуна!

```
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
// THIS DOCUMENT WAS GENERATED. DO NOT EDIT IT.\n
```

Have a look at a 2 minutes long screencast by https://twitter.com/tombujok[@tombujok]: http://vimeo.com/95045348

video::95045348[vimeo, width=827, height=465, align="center"]

// https://www.youtube.com/watch?v=_h1wJJO0Ukw&vq=hd720

// video::VOHIYhbRIq0[youtube, width=560, height=315, align="center"]

// https://www.youtube.com/watch?v=VOHIYhbRIq0

## Installation

Просто скачайте файл dist с http://babun.github.io , распакуйте его и запустите скрипт install.bat. Через несколько минут babun запускается автоматически.
Приложение будет установлено в каталог `%USER_HOME%\.babun`. Используйте опцию '/target', чтобы установить babun в пользовательский каталог.

NOTE: Нет никаких помех существующей установке Cygwin

NOTE: You may have "whitespace" chars in your username - it is not recommended by Cygwin though http://cygwin.com/faq.html#faq.setup.name-with-space[FAQ]


== Features in 10 seconds

Babun features the following:

* Pre-configured Cygwin with a lot of addons
* Silent command-line installer, no admin rights required
* pact - advanced package manager (like apt-get or yum)
* xTerm-256 compatible console
* HTTP(s) proxying support
* Plugin-oriented architecture
* Pre-configured git and shell
* Integrated oh-my-zsh
* Auto update feature
* "Open Babun Here" context menu entry

Have a look at a sample screenshot!

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_vim.png[babun - a Windows shell you will love!, align="center"]

Do you like it? Follow babun on Twitter https://twitter.com/babunshell[@babunshell] or https://twitter.com/tombujok[@tombujok].

## Features in 3 minutes

### Cygwin

The core of Babun consists of a pre-configured Cygwin. Cygwin is a great tool, but there's a lot of quirks and tricks that makes you lose a lot of time to make it actually 'usable'. Not only does babun solve most of these problems, but also contains a lot of vital packages, so that you can be productive from the very first minute. 

### Package manager

Babun provides a package manager called `pact`. It is similar to 'apt-get' or 'yum'. Pact enables installing/searching/upgrading and deinstalling cygwin packages with no hassle at all. Just invoke `pact --help` to check how to use it.

### Shell

Babun's shell is tweaked in order to provide the best possible user-experience. There are two shell types that are pre-configured and available right away - bash and zsh (zsh is the default one). Babun's shell features:

* syntax highlighting
* UNIX tools
* software development tools
* git-aware prompt 
* custom scripts and aliases
* and much more!

### Console

Mintty is the console used in babun. It features an `xterm-256` mode, nice fonts and simply looks great!

### Proxying

Babun supports HTTP proxying out of the box. Just add the address and the credentials of your HTTP proxy server to the `.babunrc` file located in your home folder and execute `source .babunrc` to enable HTTP proxying. SOCKS proxies are not supported for now.

### Developer tools

Babun provides many packages, convenience tools and scripts that make your life much easier. The long list of features includes:

* programming languages (Python, Perl, etc.)
* git (with a wide variety of aliases and tweaks)
* UNIX tools (grep, wget, curl, etc.)
* vcs (svn, git)
* oh-my-zsh
* custom scripts (pbcopy, pbpaste, babun, etc.)

### Plugin architecture

Babun has a very small microkernel (cygwin, a couple of bash scripts and a bit of a convention) and a plugin architecture on the top of it. It means that almost everything is a plugin in the babun's world! Not only does it structure babun in a clean way, but also enables others to contribute small chunks of code. Currently, babun comprises the following plugins:

* cacert
* core
* git
* oh-my-zsh
* pact
* cygdrive
* dist
* shell

### Auto-update

Self-update is at the very heart of babun! Many Cygwin tools are simple bash scripts - once you install them there is no chance of getting the newer version in a smooth way. You either delete the older version or overwrite it with the newest one losing all the changes you have made in between.

Babun contains an auto-update feature which enables updating both the microkernel, the plugins and even the underlying cygwin. Files located in your home folder will never be deleted nor overwritten which preserves your local config and customizations.

### Installer

Babun features an silent command-line installation script that may be executed without admin rights on any Windows hosts.

## Using babun

### Setting up proxy
To setup proxy uncomment following lines in the `.babunrc` file `(%USER_HOME%\.babun\cygwin\home\USER\.babunrc)`
----
# Uncomment this lines to set up your proxy
# export http_proxy=http://user:password@server:port
# export https_proxy=$http_proxy
# export ftp_proxy=$http_proxy
# export no_proxy=localhost
----

=== Setting up git
Babun has a pre-configured git. The only thing you should do after the installation is to add your name and email to the git config:
----
git config --global user.name "your name"
git config --global user.email "your@email.com"
----

There's a lot of great git aliases provided by the git plugin:
----
gitalias['alias.cp']='cherry-pick'
gitalias['alias.st']='status -sb'
gitalias['alias.cl']='clone'
gitalias['alias.ci']='commit'
gitalias['alias.co']='checkout'
gitalias['alias.br']='branch'
gitalias['alias.dc']='diff --cached'
gitalias['alias.lg']="log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %Cblue<%an>%Creset' --abbrev-commit --date=relative --all"
gitalias['alias.last']='log -1 --stat'
gitalias['alias.unstage']='reset HEAD --'
----

=== Installing and removing packages
Babun is shipped with `pact` - a Linux like package manager. It uses the cygwin repository for downloading packages:
----
{ ~ } » pact install arj                                                                     ~ 
Working directory is /setup
Mirror is http://mirrors.kernel.org/sourceware/cygwin/
setup.ini taken from the cache

Installing arj
Found package arj
--2014-03-30 19:34:38--  http://mirrors.kernel.org/sourceware/cygwin//x86/release/arj/arj-3.10.22-1.tar.bz2
Resolving mirrors.kernel.org (mirrors.kernel.org)... 149.20.20.135, 149.20.4.71, 2001:4f8:1:10:0:1994:3:14, ...
Connecting to mirrors.kernel.org (mirrors.kernel.org)|149.20.20.135|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 189944 (185K) [application/x-bzip2]
Saving to: `arj-3.10.22-1.tar.bz2'

100%[=======================================>] 189,944      193K/s   in 1.0s

2014-03-30 19:34:39 (193 KB/s) - `arj-3.10.22-1.tar.bz2' saved [189944/189944]

Unpacking...
Package arj installed
----

Here's the list of all pact's features:
----
{ ~ }  » pact --help                                                                            
pact: Installs and removes Cygwin packages.

Usage:
  "pact install <package names>" to install given packages
  "pact remove <package names>" to remove given packages
  "pact update <package names>" to update given packages
  "pact show" to show installed packages
  "pact find <patterns>" to find packages matching patterns
  "pact describe <patterns>" to describe packages matching patterns
  "pact packageof <commands or files>" to locate parent packages
  "pact invalidate" to invalidate pact caches (setup.ini, etc.)
Options:
  --mirror, -m <url> : set mirror
  --invalidate, -i       : invalidates pact caches (setup.ini, etc.)
  --force, -f : force the execution
  --help
  --version
----

=== Changing the default shell
The zsh (with .oh-my-zsh) is the default babun's shell.

Executing the following command will output your default shell:
----
{ ~ } » babun shell                                                                          ~ 
/bin/zsh
----

In order to change your default shell execute:
----
{ ~ } » babun shell /bin/bash                                                                ~ 
/bin/zsh
/bin/bash
----
The output contains two lines: the previous default shell and the new default shell

=== Checking the configuration

Execute the following command the check the configuration:
----
{ ~ }  » babun check                                                                         ~
Executing babun check
Prompt speed      [OK]
Connection check  [OK]
Update check      [OK]
Cygwin check      [OK]
----

By executing this command you can also check whether there is a newer cygwin version available:
----
{ ~ }  » babun check                                                                            ~
Executing babun check
Prompt speed      [OK]
Connection check  [OK]
Update check      [OK]
Cygwin check      [OUTDATED]
Hint: the underlying Cygwin kernel is outdated. Execute 'babun update' and follow the instructions!
----

It will check if there are problems with the speed of the git prompt, if there's access to the Internet or finally if you are running the newest version of babun.

The command will output hints if problems occur:
----
{ ~ } » babun check                                                                          ~ 
Executing babun check
Prompt speed      [SLOW]
Hint: your prompt is very slow. Check the installed 'BLODA' software.
Connection check  [OK]
Update check      [OK]
Cygwin check      [OK]
----

On each startup, but only every 24 hours, babun will execute this check automatically. You can disable the automatic check in the ~/.babunrc file.

=== Tweaking the configuration

You can tweak some config options in the ~/.babunrc file. Here's the full list of variables that may be modified:
----
# JVM options
export JAVA_OPTS="-Xms128m -Xmx256m"

# Modify these lines to set your locale
export LANG="en_US.UTF-8"
export LC_CTYPE="en_US.UTF-8"
export LC_ALL="en_US.UTF-8"

# Uncomment these lines to the set your machine's default locale (and comment out the UTF-8 ones)
# export LANG=$(locale -uU)
# export LC_CTYPE=$(locale -uU)
# export LC_ALL=$(locale -uU)

# Uncomment this to disable daily auto-update & proxy checks on startup (not recommended!)
# export DISABLE_CHECK_ON_STARTUP="true"

# Uncomment to increase/decrease the check connection timeout
# export CHECK_TIMEOUT_IN_SECS=4

# Uncomment this lines to set up your proxy
# export http_proxy=http://user:password@server:port
# export https_proxy=$http_proxy
# export ftp_proxy=$http_proxy
# export no_proxy=localhost
----

=== Updating babun

To update babun to the newest version execute:
----
babun update
----
Please note that your local configuration files will not be overwritten. 

The 'babun update' command will also update the underlying cygwin version if never version is available. In such case babun will download the new cygwin installer, close itself and start the cygwin installation process. Once cygwin installation is completed babun will restart.

== Screenshots


[big]#Startup screen#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_welcome.png[babun - a Windows shell you will love!, align="center"]

[big]#Pact - package installation#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_pact_install.png[babun - a Windows shell you will love!, align="center"]

[big]#Pact - package installed#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_pact_installed.png[babun - a Windows shell you will love!, align="center"]

[big]#Babun oh-my-zsh - auto-update#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_zsh_update.png[babun - a Windows shell you will love!, align="center"]


[big]#VIM syntax highlighting#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_vim.png[babun - a Windows shell you will love!, align="center"]

[big]#Nano syntax highlighting#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_nano.png[babun - a Windows shell you will love!, align="center"]

[big]#Git aliases - git lg#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_git_lg.png[babun - a Windows shell you will love!, align="center"]

[big]#Git aliases - git st#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_git_st.png[babun - a Windows shell you will love!, align="center"]

[big]#Shell prompt#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_shell.png[babun - a Windows shell you will love!, align="center"]

[big]#Babun update#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_update.png[babun - a Windows shell you will love!, align="center"]

[big]#Open Babun here - Context Menu#

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/screenshots/screen_context_menu.png[babun - a Windows shell you will love!, align="center"]


== Development


== Project structure

The project consists of five modules.

=== babun-packages

The main goal of the `babun-packages` module is to download the cygwin packages listed in the `conf/cygwin.x86.packages` file.
The above mentioned packages will be downloaded together with the whole dependency tree. Repositories which the packages are downloaded from are listed in the `conf/cygwin.repositories` file. At the beginning the first repository is taken, if a package is not available in this repo the second repo is used, etc. The process continues until all packages have been downloaded. 

All downloaded packages are stored in the `target/babun-packages` folder.

=== babun-cygwin

The main goal of the `babun-cygwin` module is to download and invoke the native cygwin.exe installer. The packages downloaded by the babun-packages module are used as the input - all of them will be installed in the offline cygwin installation. 

It is not trivial to install and zip a local instance of Cygwin - there are problems with the symlinks as the symlink-file-flags are lost during the compression process. Babun can work it around though. At first, just after the installation, the `symlinks_find.sh` script is invoked in order to store the list of all cygwin's symlinks. This file is delivered as a part of the the babun's core. Then, after babun is installed from the zip file on the user's host the `symlinks_repair.sh` script is invoked - it will correct all the broken symlinks listed in the above mentioned file.

Preinstalled cygwin is located in the `target/babun-cygwin` folder.

=== babun-core

The main goal of the `babun-core` module is to install babun's core along with all the plugins and tools. `install.sh` script is invoked during the creation of the distribution package in order to preinstall the plugins. Whenever babun is installed on the user's host the `install_home.sh` script is invoke in order to install the babun-related files to the cygwin-user's home folder.

Preinstalled cygwin with installed babun is located in the `target/babun-cygwin` folder.

=== babun-dist

The main goal of the `babun-dist` module is to zip the ready-made instance of babun, copy some installation scripts and zip the distribution.

Distribution package is located in the `target/babun-dist` folder.

=== babun-doc

This module contains documentation written in ASCIIDOC.


== Building from source

The project is regularly build on Jenkins, on a slave node featuring the Windows Server OS. The Windows OS is required to fully build the distribution package as one of the goals invokes the native `cygwin.exe` installer. The artifacts created by each module are cached/stored in the target folder after a successful build of each step. This mechanism is not intelligent enough to calculate the diffs so if you would like to fully rebuild the whole dist package make sure to invoke the `clean` goal before the `package` goal. For now it's not possible to invoke a build of a selective modules only. 

In order to build the dist package invoke:
----
groovy build.groovy package 
----

In order to clean the project target folder invoke:
----
groovy build.groovy clean 
----

In order to publish the release version to bintray invoke:
----
groovy build.groovy release
----
The release goal expects the following environment variables: `bintray_user` and `bintray_secret`

== Developing a plugin

Every plugin has to consist of three main files:

* install.sh - a file that will be executed during the creation of the babun's distribution
* install_home.sh - a file that will be executed during the installation of babun to the user's home folder 
* plugin.desc - a plugin description that contains the plugin_name and plugin_version variables
* start.sh (optional) - a file that will be executed on babun startup
* exec.sh (optional) - a file that allows adding commands to babun script

Have a look at the pact plugin - it's a perfect example of a relatively small plugin using all the features.

=== install.sh

Its main responsibility is to install the plugin - for example to copy the plugin files to, e.g. `/usr/local/etc` or `/usr/local/bin` directories. install.sh script is also responsible for preparing the user's home folder template. The template files have to be copied to the `/usr/local/babun/home/<plugin_name>` folder.

install.sh will be invoked many times - on every plugin update if the plugin version is higher than the version of the installed plugin - thus it's logic has to work in an incremental way. This mechanism is invoked automatically though. The plugin does not have to contain the version check.

The script has to begin with the following statement:
----
#!/bin/bash
set -e -f -o pipefail
source "/usr/local/etc/babun/source/babun-core/tools/script.sh"
----

=== install_home.sh

Its main responsibility is to configure the user's home folder with the plugin related stuff, if necessary. For example, it may copy the files from the `/usr/local/babun/home/<plugin_name>` folder to the user's home folder.
It is also responsible for any other things that may be necessary during the user's home configuration process.

install_home.sh will be invoked many times - on every plugin update if the plugin version is higher than the version of the installed plugin - thus it's logic has to work in an incremental way.

Both scripts (install.sh and install_home.sh) scripts have to begin with the following statement:
----
#!/bin/bash
set -e -f -o pipefail
source "/usr/local/etc/babun/source/babun-core/tools/script.sh"
----

=== uninstall.sh (optional)

Its responsibility is to cleanup all entries that a plugin may leave for example on the filesystem or in the windows registry.

=== plugin.desc

A plugin descriptor looks like this:
----
# plugin descriptor
plugin_name=pact
plugin_version=1
----

Every time the plugin is changed the version has to be incremented. Otherwise the newest version will not be installed.

=== start.sh (optional)

The start.sh is an optional script for plugins that require triggering certain actions on every babun start (for example update check).

=== exec.sh (optional)

If the plugin folder contains an exec.sh script, 
whenever `babun <plugin_name> xxx yyy` command is invoked, the execution is passed to `<plugin_name>/exec.sh` script with params `xxx yyy`. 
In this way a plugin may add some additional shell commands without implementing its own `/usr/local/bin/xxx` script.

== Branches

The babun's repository contains three main branches:

* master - development branch
* candidate - release candidate branch, no direct commits, only fast forwards from the master/other branch
* release - release, no direct commits, only fast forwards from the candidate branch

In order to check babun update against other branch (for example during a development of a plugin), set the babun_branch variable to (master or candidate). External repo's are not supporter (this mechanism has to be extended to include user's repos).

== Folder structure in Cygwin

An instance of babun installed in Cygwin is located in the `/usr/local/etc/babun` folder.
The folder structure looks like this:
----
├── babun
│   ├── external
│   │   └── oh-my-zsh
│   ├── home
│   │   ├── core
│   │   ├── oh-my-zsh
│   │   ├── pact
│   │   └── shell
│   ├── installed
│   │   ├── babun
│   │   ├── cacert
│   │   ├── core
│   │   ├── git
│   │   ├── oh-my-zsh
│   │   ├── pact
│   │   └── shell
│   ├── source
│   │   ├── babun.version
│   │   ├── babun-core
│   │   ├── babun-cygwin
│   │   ├── babun-dist
│   │   ├── babun-doc
│   │   ├── babun-packages
│   │   ├── build.groovy
│   │   └── README.adoc
│   └── stamps
│       ├── check
│       └── welcome
├── babun.bash
├── babun.instance
├── babun.rc
├── babun.start
└── babun.zsh

16 directories, 17 files
----

=== source

The folder contains the sources of babun checkout from github.

=== stamps

The folder contains files which modification time indicates certain things to babun. For example `babun check` is executed automatically on babun's start up every 24 hours. Whenever it's invoked a file named `checked` is being modified (the content of the modification does not matter).Whenever the mod_time of this file is not within 24 hours and babun is being started a `babun check` will be invoked and the file `check` located in the `stamps` folder will be modified again.

=== installed

The folder contains files that indicated which versions of babun's plugins and babun itself are installed. Each file contains a number - for example: a file named `core` contains has one line with number `2` in its content. It means that the plugin `core` is installed and has version `2`

=== external

The folder contains external resources, like cloned repos of other projects (for example oh-my-zsh).

=== home

The folder contains folders named like plugins. If a plugin needs to install something to user's folder this content has to be copied to `home/<plugin_name>` folder. It's just a store of the user's home files, so that whenever a new user's account is created babun can install user's home related content to the user's home folder (it's the plugin install_home.sh script's responsibility, however, to copy this content to the actual user's home folder). 


== Licence

The source code located in the babun's repository is published under the Apache License, Version 2.0, January 2004 if not stated otherwise. 

Since the distribution (zip) package contains the Cygwin's DLLs the distribution package is licensed under the GPLv3+ licence to satisfy the Cygwin's licensing terms (http://cygwin.com/licensing.html).

== Supporters

Special thanks go to companies who provided free hosting! 

=== XCLOUD

http://xcloud.me/[XCLOUD.ME] provided a free hosted OS X instance (a free Xcloud Mini Server subscription). It works like a charm! Thank you!

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/xcloud_logo.png["XCLOUD", link="http://xcloud.me/", window="_blank"]
"Run, manage and scale your virtual dedicated OS X Server in the Cloud."

_XCLOUD is a trademark of AG from Switzerland._

=== Windows Azure

http://www.azure.microsoft.com[Windows Azure] provided a free Windows Hosting (a free, renewable MSDN subscription). Everything was organised by @bureado. Thank you!

image::https://raw.githubusercontent.com/babun/babun.github.io/master/images/ms_azure_logo.png["Windows Azure", link="http://www.azure.microsoft.com", window="_blank"]

_Microsoft and Windows are registered trademarks of Microsoft Corporation in the United States of America and other countries. Windows Azure is a trademark of Microsoft Corporation._


== Contribute

Babun is open source and driven by the community. There are many ways to contribute:

* Use it and tell us what you think
* Recommend it to your friends
* Submit a https://github.com/babun/babun/issues[feature request] or a https://github.com/babun/babun/issues[bug report]
* Fork it on https://github.com/babun/babun[github] and submit pull request
* Motivate the community, tweet about the project and star it on github :)

We are looking for new contributors, so if you fancy bash programming and if you would like to contribute a patch or a code up a new plugin give us a shout!

Visit the http://babun.github.io/development/[development] section to find out how to create plugins and extensions.

== Meet the team

https://twitter.com/tombujok[@tombujok]

https://twitter.com/lukaszpielak[@lukaszpielak]

image::https://d2weczhvl823v0.cloudfront.net/reficio/babun/trend.png["Bitdeli Badge", link="https://bitdeli.com/free"]
