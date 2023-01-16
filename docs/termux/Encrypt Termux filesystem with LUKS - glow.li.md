---
title: 
tags: termux,cli,android,tutorial,snippet
author: easy-zzz
source: https://glow.li/posts/encrypt-termux-fs/
---
Encrypt Termux filesystem with LUKS - glow.li  

```
  ▁            ▁
▗▛▀▜▄ ▃▃▃,,. ~°°°┐
▐▌▗███████%#X0,  #
 ▀███▛▜███@K°%M#%°
 ▟███ o▟██▙o #5M%
 ██#██▛▗▄▄▖▜██#0K
▕██M%█▏▝▜▛▘▕█████▏
 ▜████▙━▘▝━▟████▛
  ▝▀▀▜██████▛▀▀▘
```

[glow.li](https://glow.li/)
===========================



[Encrypt Termux filesystem with LUKS](https://glow.li/posts/encrypt-termux-fs/)
-------------------------------------------------------------------------------

[![Screenshot of Termux running the script in this tutorial](https://glow.li/media/images/small/encrypt-termux-fs-screenshot.webp?chash=875a1 "Screenshot of Termux running the script in this tutorial")](https://glow.li/media/images/big/encrypt-termux-fs-screenshot.webp?chash=cd440) People sometimes store sensitive information within [Termux](https://termux.com), like SSH Keys or PGP Keys. Within Android, this is fairly secure. No other app can access the Termux storage without explicit user consent. But our phones aren't secure devices for most people. Most people have a really short pin or password (or even none at all). So if our devices get stolen or seized, this data can easily be extracted. This short tutorial will show you a way to encrypt the whole Termux filesystem, so this data cannot be extracted once the phone has turned off or the filesystem is unmounted and closed again.  
* [Procedure](https://glow.li/#Procedure)
* [Requirements](https://glow.li/#Requirements)
  * [Rooted phone](https://glow.li/#Rooted+phone)
  * [Blank Termux](https://glow.li/#Blank+Termux)
  * [Packages](https://glow.li/#Packages)
* [Create filesystem](https://glow.li/#Create+filesystem)
  * [Step 1: Create a blank image file](https://glow.li/#Step+1%3A+Create+a+blank+image+file)
  * [Step 2: Encrypt image file using LUKS](https://glow.li/#Step+2%3A+Encrypt+image+file+using+LUKS)
  * [Step 3: Temporarily open image file](https://glow.li/#Step+3%3A+Temporarily+open+image+file)
  * [Step 4: Format the image file](https://glow.li/#Step+4%3A+Format+the+image+file)
  * [Step 5: Close the image file again](https://glow.li/#Step+5%3A+Close+the+image+file+again)
* [Entering the encrypted Termux](https://glow.li/#Entering+the+encrypted+Termux)
  * [Find your su binary](https://glow.li/#Find+your+su+binary)
* [Restore your existing installation](https://glow.li/#Restore+your+existing+installation)
* [Unmounting your filesystem](https://glow.li/#Unmounting+your+filesystem)
* [Accessing your unencrypted Termux while in the encrypted environment](https://glow.li/#Accessing+your+unencrypted+Termux+while+in+the+encrypted+environment)
* [Caveats](https://glow.li/#Caveats)
  * [Termux:Tasker](https://glow.li/#Termux%3ATasker)
  * [SELinux](https://glow.li/#SELinux)

### Procedure

We're creating a separate filesystem in an encrypted image file, which we're then mounting at `/data/data/com.termux/files`, which contains all of Termux' data.

### Requirements

#### Rooted phone

Unfortunately, this only works with a rooted device, as you need access to cryptsetup and mount

#### Blank Termux

It is recommended to start out with a freshly installed Termux. This is the host Termux, that will only be used to mount the encrypted Termux. You can do it on an existing Termux installation, but be aware that all data that is already in your Termux installation, will not be encrypted. If you want encrypt an existing installation you need to make a backup of it now and then reset your Termux.

    rsync -a /data/data/com.termux/files /data/data/com.termux/files-backup

Make sure to delete this backup at the end.

After that you can delete `/data/data/com.termux/files` to reset your Termux (restart after doing so). Beware that this will delete all your files. Make sure you've backed them up.

#### Packages

Install the root repo:

    pkg install root-repo

Install required packages:

    pkg install util-linux cryptsetup tsu e2fsprogs rsync

### Create filesystem

#### Step 1: Create a blank image file

To create an encrypted filesystem you need to first create a blank '.img' file. Adjust the size to your preference. Beware that it will use up this space on your device instantly.

    fallocate -l 16G /data/data/com.termux/termux-fs.img

#### Step 2: Encrypt image file using LUKS

Next we are encrypting this '.img' using [LUKS](https://en.wikipedia.org/wiki/Linux_Unified_Key_Setup).

    sudo cryptsetup luksFormat /data/data/com.termux/termux-fs.img

Answer the first prompt with `YES` and then enter a passphrase twice:


    WARNING!
    ========
    This will overwrite data on /data/data/com.termux/termux-fs.img irrevocably.

    Are you sure? (Type 'yes' in capital letters): YES
    Enter passphrase for /data/data/com.termux/termux-fs.img:
    Verify passphrase:
#### Step 3: Temporarily open image file

To format the image file we need to temporarily open it.

    sudo cryptsetup open /data/data/com.termux/termux-fs.img termux-fs-tmp

You will be prompted to enter your passphrase

#### Step 4: Format the image file

Create a ext4 filesystem inside the encrypted volume.

    sudo mkfs.ext4 /dev/mapper/termux-fs-tmp

#### Step 5: Close the image file again

    sudo cryptsetup close termux-fs-tmp

### Entering the encrypted Termux

Now that we created the encrypted disk we simply need to mount it. Since we need to do this every time we boot our device, it's best we create a script for that. Use [this script](https://glow.li/media/files/termuxmount.sh) to enter your new filesystem:

    #!/usr/bin/env bash
    u=$(whoami)
    export LD_PRELOAD=
    /sbin/su -c "cryptsetup luksOpen /data/data/com.termux/termux-fs.img termux-fs"
    /sbin/su -c "mount /dev/mapper/termux-fs /data/data/com.termux/files"
    /sbin/su -c "/system/bin/chown $u.$u /data/data/com.termux/files"
You will be prompted your passphrase. This will mount your filesystem to `/data/data/com.termux/files`. After you've run this script, exit your Termux App and open it again. The first time you do this the Termux App will reinstall your base system inside your encrypted dist.

Congratulations you are now in your encrypted filesystem. You will need to run this script again after a restart.

#### Find your su binary

Since mounting a filesystem at `/data/data/com.termux/files` will cause all Termux command to temporarily break, we need to make sure we're not running any Termux commands in this script. Therefore you need to specify your su binary with an absolute path. In most cases this is `/sbin/su`, so you can use the script as is. If your `su` is somewhere else, check these paths and replace the command in the script accordingly:

* `/sbin/su`
* `/system/sbin/su`
* `/system/bin/su`
* `/system/xbin/su`
* `/su/bin/su`
* `/magisk/.core/bin/su`

### Restore your existing installation

If you've created a backup of your existing installation (described [here](https://glow.li/#Blank+Termux)) you can restore that backup now.

    rsync -a --delete /data/data/com.termux/files-backup/ /data/data/com.termux/files/

If everything worked, remember to delete this unencrypted backup.

    rm /data/data/com.termux/files-backup -rf

### Unmounting your filesystem

Unmounting your encrypted Termux is a bit annoying. Since it is always in-use you need to specify (`-l`) lazy mode.

    sudo umount /data/data/com.termux/files -l

After that can restart your Termux again to be in the unencrypted filesystem again. Your encrypted filesystem is still open however, so you need to close it now.

    sudo cryptsetup close termux-fs

If there are any processes still accessing your encrypted Termux, this will fail. You need to either find and close these processes, or restart your device.

### Accessing your unencrypted Termux while in the encrypted environment

It is sometimes necessary to do maintenance (updates for example) on the unencrypted Termux. Unmounting your filesystem is one possibility, but is quite annoying. You can however use `unshare` and `chroot` to access your unencrypted Termux while the encrypted Termux is still running. I created [this script](https://glow.li/media/files/termuxhost.sh) to do that:

    #!/usr/bin/env bash
    OPTIND=1
    UNSHARED=false
    while getopts ":U" opt; do
        case "$opt" in
            U)
                UNSHARED=true
                ;;
            *) ;;

        esac
    done

    shift $((OPTIND - 1))
    if [ ! "$UNSHARED" == "true" ]; then
        user="$(whoami)"
        vars=""
        vars+=" HOME=$HOME"
        vars+=" PATH=$PREFIX/bin"
        vars+=" PREFIX=$PREFIX"
        vars+=" TMPDIR=$TMPDIR"
        vars+=" SHELL=$PREFIX/bin/login"
        vars+=" exec $PREFIX/bin/login"
        args=""
        if [ -n "$1" ]; then
            args="-c '$@'"
        fi
        $PREFIX/bin/sudo unshare -m $0 -U "$user" "$HOME" "$vars $args"
    else
        mount --bind /data/data/com.termux /data/data/com.termux
        user="$1"
        user_home="$2"
        vars="$3"
        cd $user_home
        groups=${user},inet,everybody,${user}_cache,all_$(echo $user | cut -d "_" -f 2)
        exec chroot --skip-chdir --userspec=$user:$user --groups=$groups / sh -c "$vars"
    fi
Running this will drop you inside your unencrypted Termux. Since we used `unshare` this only applies to this process. Other sessions remain unaffected. To return to your encrypted Termux simply exit this process.

### Caveats

#### Termux:Tasker

If you install the Termux:Tasker add-on, Tasker will not be able to execute the tasks in `~/.termux/tasker`, because it checks your for these files in your unencrypted Termux. If you want to use this functionality you need to create blank executable files in your unencrypted Termux with the same name as the ones in your encrypted Termux. It will actually execute the scripts in your encrypted environment.

I think this is a really interesting bug. I wrote a detailed bug report here: <https://github.com/termux/termux-tasker/issues/45>

#### SELinux

I've run into issues using SELinux. It may be necessary to run this command after mounting:

    /sbin/su -c "/system/bin/restorecon -R /data/data/com.termux/files"

If you run into continuing issues, add this to your mounting script (edit the path to `su` as described [here](https://glow.li/#Find+your+su+binary))  
[#Technology](https://glow.li/tags/technology/) [#Termux](https://glow.li/tags/termux/) [#CLI](https://glow.li/tags/cli/) [#Android](https://glow.li/tags/android/) [#Tutorial](https://glow.li/tags/tutorial/) [#Snippet](https://glow.li/tags/snippet/) [#2021](https://glow.li/tags/2021/)
[\<\< Next](https://glow.li/posts/ksp-f18/ "Kerbal Space Program: F/A 18") [Previous \>\>](https://glow.li/posts/global-push-to-talk/ "Global push to talk with i3 and pulseaudio")  
-----------------------------------------------------------------------  
A blog by [glow](https://glow.li/about/).
Madeon[Termux](https://termux.com).  
