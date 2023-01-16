---
title: 
tags: ssh,gpg
author: easy-zzz
source: https://glow.li/posts/run-an-ssh-server-on-your-android-with-termux/
---
Run an SSH server on your Android with Termux - glow.li  

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

× Search requires Javascript  
[× All Posts](https://glow.li/) [× Technology](https://glow.li/tags/technology/) [× Photography](https://glow.li/tags/photography/) [× Short](https://glow.li/tags/short/) [× About](https://glow.li/about/) [× Feeds](https://glow.li/feeds/) [× Fedi Posts](https://glow.li/fedi/)  
-----------------------------------------------------------------------  
[Technology](https://glow.li/tags/technology/) • [2015-11-06](https://glow.li/posts/run-an-ssh-server-on-your-android-with-termux/)  
[Signed](https://glow.li/posts/run-an-ssh-server-on-your-android-with-termux/index.html.asc)
[![Avatar of glow](https://glow.li/media/images/thumb/Glow-2022-green.webp?chash=977f7)](https://glow.li/about/ "glow/")  

[Run an SSH server on your Android with Termux](https://glow.li/posts/run-an-ssh-server-on-your-android-with-termux/)
---------------------------------------------------------------------------------------------------------------------

With the brilliant [Termux](https://termux.com/) terminal emulator app you can run an SSH server on your Android.

Previously I used [SSHDroid](https://play.google.com/store/apps/details?id=berserker.android.apps.sshdroid) to achieve this, but with Termux is much nicer because you have access to a working package manager.

## Запустите службу

Вам необходимо установить пакет OpenSSH

```sh
apt install openssh
```

и используйте следующую команду для запуска ssh-сервера.

```sh
sshd
```

И вот ты здесь. Ваша служба ssh теперь запущена на порту 8022.

```sh
ssh localhost -p 8022
```

## Добавление вашего открытого ключа

Вы не можете выполнить аутентификацию по паролю в Termux, поэтому вам необходимо поместить свой открытый ключ OpenSSH в файл `~/.ssh/authorized_keys`.

Этот файл необходимо будет создать и установить разрешения на 600.

```sh
touch ~/.ssh/authorized_keys
# Установите права доступа к файлу
chmod 600 ~/.ssh/authorized_keys
# Убедитесь, что папка .ssh имеет правильные разрешения
chmod 700 ~/.ssh
```
   
Если у вас еще нет пары ключей OpenSSH, вы можете сгенерировать ее с помощью следующей команды:

```sh
ssh-keygen
```

Вы можете вводить или не вводить кодовую фразу, и если вы не укажете иное, ваша пара ключей будет сохранена в  `~/.ssh/id_rsa` и  `~/.ssh/id_rsa.pub`. Затем вы можете добавить его в `~/.ssh/authorized_keys` :

```sh
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

Затем вы можете протестировать его, подключившись к своему ssh-сервису

        # -i $PATH_TO_FILE/filename is only required if the id_rsa file is not ~/.ssh/id_rsa
        ssh localhost -p 8022 -i %PATH_TO_KEY-FILE%/%NAME_OF_KEY%
You can now use your private key (\~/.ssh/id_rsa) to login to your Termux SSH Server. Simply copy it to your computer (by copying it to internal storage first `cp ~/.ssh/id_rsa /sdcard`) and use it in your ssh client.

### OpenSSH

If you're using OpenSSH (on Linux or Cygwin) you can use it directly:

        # -i $PATH_TO_FILE/filename is only required if the id_rsa file is not ~/.ssh/id_rsa
        ssh $IP -p 8022 -i %PATH_TO_KEY-FILE%/%NAME_OF_KEY%
### PuTTY

If you're using PuTTY you will need to convert it to the PuTTY Private Key format first.

1. Download and run [PuTTYgen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
2. Load the private key (id_rsa)
3. Save the private key as a \*.ppk file.
4. Download and run [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
5. Enter the IP address of your Android device and use port 8022
6. Under Connection\>SSH\>Auth you can browse for the \*.pkk file
7. Click open
8. You can leave "login as:" blank

You should now be connected to your Android device via SSH.

### If it still doesn't work

        killall sshd
        sshd -d
If it is still prompts you for a password you can enter sshd's debug mode with the above command and see exactly why your key has been rejected. The reason usually are bad permission on either your home directory, your .ssh folder or your authorized_keys file.

The correct permissions are:

        chmod 700 ~
        chmod 700 ~/.ssh
        chmod 600 ~/.ssh/*
I hope in the future Termux will allow us to register sshd as a proper service which would automatically start on system boot. Right now I have the 'sshd' command in my .bashrc file and I am using [Tasker](https://play.google.com/store/apps/details?id=net.dinglisch.android.taskerm)to launch Termux after boot. You can also use the [Termux widget](https://play.google.com/store/apps/details?id=com.termux.widget&hl=en) to quickly start sshd with a widget.

See also: [Access the SSH server via USB instead of WiFi](https://glow.li/posts/access-termux-via-usb/)  
[#Technology](https://glow.li/tags/technology/) [#Android](https://glow.li/tags/android/) [#Termux](https://glow.li/tags/termux/) [#CLI](https://glow.li/tags/cli/) [#SSH](https://glow.li/tags/ssh/) [#Tutorial](https://glow.li/tags/tutorial/) [#2015](https://glow.li/tags/2015/)
[\<\< Next](https://glow.li/posts/short-99e3f-disk0s2_io_error_on_Christmas_Eve./) [Previous \>\>](https://glow.li/posts/beats-with-zooper/ "How to get Zooper to display Swatch Internet Time (beats)")  
-----------------------------------------------------------------------  
A blog by [glow](https://glow.li/about/).
Madeon[Termux](https://termux.com).  
