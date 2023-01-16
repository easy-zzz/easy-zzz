---
title: 20 основных команд Linux, которые вам понадобятся ежедневно
tags: Linux, bash 
author: easy-zzz
source: https://likegeeks.com/main-linux-commands-easy-guide/
---
20 основных команд Linux, которые вам понадобятся ежедневно


20 Main Linux commands that you will need daily
========================================

[Mokhtar Ebrahim](https://likegeeks.com/author/admin/) Published: January 31, 2017 Last updated: April 5, 2022  
In the previous post, we discussed [how to install Linux](https://likegeeks.com/how-to-install-linux/); now, we are going to talk about the most powerful features in Linux, which are Linux commands or shell commands.

For the complete documentation of Linux Commands, you can check [Linux Documentation](http://www.tldp.org/).  

The power of Linux is in the power of commands that you can use.

I'm going to talk about the main Linux commands with their main parameters that you might use daily.

Table of Contents
1

* ls command
* cd command
* cp command
* mv command
* rm command
* mkdir command
* rmdir command
* chown command
* chmod command
* locate command
* updatedb command
* date command
* tar command
* cat command
* less command
* grep command
* passwd command
* du command
* reboot command
* halt command

ls command
----------

List files and folders in the current directory.

Parameters

--l

to list the content as a detailed list.

-a

Display all files (hidden + non-hidden).

You can combine parameters like this:

```
ls -la
```

![linux ls command](https://likegeeks.com/wp-content/uploads/2017/01/linux-ls-command.png)

cd command
----------

Change directory from the current directory to another one.

```
cd /home
```

Will go to the home directory

![linux cd command](https://likegeeks.com/wp-content/uploads/2017/01/linux-cd-command.png)

cp command
----------

Copy the source to target.

Parameters

-i

Interactive mode means waiting for the confirmation if there are files on the target, it will be overwritten.

-r

Recursive copy means include subdirectories if they found.

Example  

```
cp –ir sourcedir targetdir
```

![linux cp command](https://likegeeks.com/wp-content/uploads/2017/01/linux-cp-command.png)

mv command
----------

Move the source to target and remove the source.

Parameters

-i

Interactive mode means to wait for the confirmation if there are files on the target, it will be overwritten.

Example

```
mv –i sourceFile targetFile
```

![linux mv command](https://likegeeks.com/wp-content/uploads/2017/01/linux-mv-command.png)

rm command
----------

Delete file or directory, and you must use --r in case you want to delete a directory.

Parameters

-r

Recursive delete means delete all subdirectories if found.  

-i

Interactive means wait till confirmation

![linux rm command](https://likegeeks.com/wp-content/uploads/2017/01/linux-rm-command.png)

mkdir command
-------------

Create a new directory.

```
mkdir newDir
```

![linux mkdir command](https://likegeeks.com/wp-content/uploads/2017/01/linux-mkdir-command.png)

rmdir command
-------------

Delete a directory

![linux rmdir command](https://likegeeks.com/wp-content/uploads/2017/01/linux-rmdir-command.png)

chown command
-------------

Change the owner of a file or directory.

Parameters:

-R

**Capital R**here means to change ownership of all subdirectories if found, and you must use this parameter if you use the command against a directory.

```
chown –R root:root myDir
```

![linux chown command](https://likegeeks.com/wp-content/uploads/2017/01/linux-chown-command.png)  

chmod command
-------------

Change the permission of a file or directory.

Parameters

The mode which consists of 3 parts, **owner** , **group** , and **others** means what will be the permissions for these modes, and you must specify them.

The permission is one of the followings:

**Read** =4

**Write** = 2

**Execute** =1

Every permission represented by a number as shown, and you can combine permissions.

Example

```
chmod 755 myfile
```

That means set permission for the file named myfile as follows:

owner: set it to 7, which means 4+2+1 means read+write+execute.

group: set it to 5, which means 4+1 means read+execute.  

other: set it to 5, which means 4+1 means read+execute.

Note: execute for a folder, means opening it.

![linux chmod command](https://likegeeks.com/wp-content/uploads/2017/01/linux-chmod-command.png)

locate command
--------------

To find a file in your system, the locate command will search the system for the pattern you provide.

```
locate myfile
```

![linux locate command](https://likegeeks.com/wp-content/uploads/2017/01/linux-locate-command.png)

updatedb command
----------------

updates the database used by the locate command.

date command
------------

Simply prints today's date. Just type date on the shell.

tar command
-----------

Combines several files into an archive and compression if you want.

Parameters

-c

Create a new archive.

-z

Compress the archive using gzip package.

-j

Compress the archive using the bzip2 package.

-v

Verbose mode means showing the processed files.

-f

Write the output to a file and not to screen.

-x

Unpack files from an archive.

Example

```
tar –czvf myfiles.tar.gz myfiles
```

![linux tar command create](https://likegeeks.com/wp-content/uploads/2017/01/linux-tar-command-create.png)

This command will pack and compress all files in folder myfiles to a compressed archive named myfiles.tar.gz.

```
tar-xzvf myfiels.tar.gz
```

![linux tar command extract](https://likegeeks.com/wp-content/uploads/2017/01/linux-tar-command-extract.png)

This command will decompress the archive.

cat command
-----------

Display file content to screen without limits.

Example

```
cat myfile.txt
```

![linux cat command](https://likegeeks.com/wp-content/uploads/2017/01/linux-cat-command.png)

less command
------------

Displays file content with a scroll screen so you can navigate between pages using PgUp, PgDn, Home, and End.

```
less myfile
```

grep command
------------

Searches for a string in the specified files and displays which line contains the matched string.

Parameters

-R

Recursive search inside subdirectories if found.

-i

Insensitive search and ignore case.

-l

Displays file name, not the text lines.

Example

```
grep –Ril mystring /home
```

![linux grep command](https://likegeeks.com/wp-content/uploads/2017/01/linux-grep-command.png)

passwd command
--------------

Used to change your user password.

![linux passwd command](https://likegeeks.com/wp-content/uploads/2017/01/linux-passwd-command.png)

du command
----------

Calculates the disk usage of a file or a directory.

Parameters

-h

Display human-readable form.

-s

Summarize the output total size.

Example

```
du –hs /home
```

![linux du command](https://likegeeks.com/wp-content/uploads/2017/01/linux-du-command.png)

reboot command
--------------

Reboot the system immediately. Just type reboot.

halt command
------------

Shuts down the system, but make sure to close all of your files to avoid data loss.

That was just some of the leading Linux commands.

Notice that, if you forget any command parameters, just type the command with -- -help as a parameter, and it will list the used parameters, so you don't have to remember all those parameters at the beginning.

```
cat --help
```

<br />

To be continued.

[Basic Linux commands part2](https://likegeeks.com/basic-linux-commands-part2/)  

* [Share on Facebook](https://www.facebook.com/sharer/sharer.php?u=https://likegeeks.com/main-linux-commands-easy-guide/)
* [Tweet on Twitter](https://twitter.com/intent/tweet?text=20+Main+Linux+commands+that+you+will+need+daily&url=https://likegeeks.com/main-linux-commands-easy-guide/&via=likegeeks)
* [](https://www.linkedin.com/shareArticle?mini=true&url=https://likegeeks.com/main-linux-commands-easy-guide/&title=20 Main Linux commands that you will need daily)
* [](mailto:?subject=20 Main Linux commands that you will need daily&body= https://likegeeks.com/main-linux-commands-easy-guide/ "Share by Email")
* [](https://pinterest.com/pin/create/button/?url=https://likegeeks.com/main-linux-commands-easy-guide/&media=https://likegeeks.com/wp-content/uploads/2017/01/Linux-Commands.png&description=20 Main Linux commands that you will need daily)
* [](https://api.whatsapp.com/send?text=20 Main Linux commands that you will need daily https://likegeeks.com/main-linux-commands-easy-guide/)  
![Mokhtar Ebrahim](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=100&d=mm&r=g)  
[Mokhtar Ebrahim](https://likegeeks.com/author/admin/)  
Mokhtar is the founder of LikeGeeks.com. He works as a Linux system administrator since 2010. He is responsible for maintaining, securing, and troubleshooting Linux servers for multiple clients around the world. He loves writing shell and Python scripts to automate his work.  
[](https://www.linkedin.com/in/mokhtar-ibrahim/)  

##### 6 thoughts on "20 Main Linux commands that you will need daily"

   1. ![](https://secure.gravatar.com/avatar/795ac8d651f15dd52886e9d9790cafaf?s=45&d=mm&r=g) **Gordon** says:  
   [2021-01-08 at 10:03 pm](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27551)  
   nice well explained for a beginer  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2021-01-09 at 8:18 am](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27552)  
      Thanks Gordon!  
      Reply
   2. ![](https://secure.gravatar.com/avatar/9b2734e5cae486fe142d0007e250dff9?s=45&d=mm&r=g) **Manjunath** says:  
   [2021-05-26 at 5:43 am](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27601)  
   Really helpful !  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2021-05-26 at 8:26 am](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27602)  
      Thanks a lot!  
      Reply
   3. ![](https://secure.gravatar.com/avatar/f1941d6de9b67c9ccc5f8d828ddea13f?s=45&d=mm&r=g) **Roman** says:  
   [2022-10-30 at 10:45 pm](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27673)  
   Very helpful. Thanks.  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2022-10-31 at 8:15 am](https://likegeeks.com/main-linux-commands-easy-guide/#comment-27674)  
      You're welcome. Thanks!  
      Reply

###### Leave a Reply Cancel reply

Your email address will not be published. Required fields are marked \*

Comment \*

Name \*

Email \*

Email  

##### My Published Book

[![My Book](https://likegeeks.com/wp-content/uploads/2020/05/My-book.png)](https://www.packtpub.com/virtualization-and-cloud/mastering-linux-shell-scripting-second-edition)

##### Latest Posts

* [Convert Pandas DataFrame to NumPy array](https://likegeeks.com/dataframe-to-numpy-array/)
* [Convert NumPy array to Pandas DataFrame (15+ Scenarios)](https://likegeeks.com/numpy-array-to-pandas-dataframe/)
* [20+ Examples of filtering Pandas DataFrame](https://likegeeks.com/filtering-pandas-dataframe/)
* [Seaborn lineplot (Visualize Data With Lines)](https://likegeeks.com/seaborn-lineplot/)
* [Python string interpolation (Make Dynamic Strings)](https://likegeeks.com/python-string-interpolation/)
* [Seaborn histplot (Visualize data with histograms)](https://likegeeks.com/seaborn-histplot/)
* [Seaborn barplot tutorial (Visualize your data in bars)](https://likegeeks.com/seaborn-barplot/)
* [Python pytest tutorial (Test your scripts with ease)](https://likegeeks.com/python-pytest/)

##### Advertisements

##### Advertisements

Post navigation
---------------

[What is Linux File System? Easy Guide](https://likegeeks.com/linux-file-system/)  
[Basic Linux Commands Made Easy Part2](https://likegeeks.com/basic-linux-commands-part2/)  
* [Disclaimer](https://likegeeks.com/disclaimer/)
* [Privacy Policy](https://likegeeks.com/privacy-policy/)
* [About](https://likegeeks.com/about/)
* [Contact](https://likegeeks.com/contact/)  
* [](https://www.pinterest.com/likegeeks/)
* [](https://www.youtube.com/channel/UC9g6sApRZ3Vib6vROG5YPaA)
* [](https://twitter.com/likegeeks)
* [](https://www.facebook.com/likegeeks)
