---
title: 
tags: 
author: easy-zzz
source: https://guruadmin.ru/page/avtokomandy-v-vi-i-vim-avtomaticheski-dobavljaem-v-fajl-zagolovok
---
Автокоманды в Vi и Vim: автоматически добавляем в файл заголовок  
* Главная
* О сайте
* Комментарии
* Контакты
* Архив  

Linux и Windows: помощь админам и пользователям
===============================================

Администрируем и настраиваем Windows, Linux.
--------------------------------------------

﻿  

Автокоманды в Vi и Vim: автоматически добавляем в файл заголовок
================================================================

Рубрика: Редакторы   
Метки: Linux \| tips \| vi \| vim   
Вторник, 31 марта 2009 г.   
Просмотров: 9228   
Подписаться на комментарии по RSS

<br />

Используя возмжность автоматического выполнения команд в Vi / Vim, вы можете указать определенные какие команды Vim будет выполнять автоматически в случае если произошло нужное событие: создан файл с определенным расширением, файл открыт или закрыт, и многое другое.

В данной статье, всего в три шага, мы используем функцию автокоманды для создания заголовка файла с именем файла, датой создания, датой последней модификации.

**Синтаксис autocmd :**

```
autocmd  {event} {pattern} {cmd}
```

**Events:** Существует более 40 различных событий. Подробнее о них читайте в :help, здесь приведены просто некоторые примеры:

```
BufNewFile	
FileReadPre
BufWritePre	
FileWritePre	
BufDelete	
BufWipeout	
BufNew	
BufEnter	
BufLeave
```

В данной статье мы рассматриваем такой пример: допустим вы программист на С и хотели бы, чтобы при создании файл с расширением .с автоматически в начало файла добавлялся заголовок с автором, именем файла и проче. Вы легко сделаете это, дочитав статью до конца. В конце мы получим следующий заголовок:

```
/* -.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
* File Name : 1.c
* Purpose :
* Creation Date : 22-12-2008
* Last Modified : Mon 22 Dec 2008 10:36:49 PM PST
* Created By :  
_._._._._._._._._._._._._._._._._._._._._.*/
```

### Шаг 1: Создаем файл шаблона

Сохраните шаблон, выложенный ниже в текстовый файл c_header.txt. Обратите внимание, первой строкой идет ":insert", а в последней строке точка - ".":

```
$ cat c_header.txt
:insert
/* -.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
* File Name :
* Purpose :
* Creation Date :
* Last Modified :
* Created By :  
_._._._._._._._._._._._._._._._._._._._._.*/
.
```

### Шаг 2: Добавляем команды autocmd в \~/.vimrc

Добавьте следующие строки в файл \~/.vimrc. Пока оставим данные строки без пояснений и выясним их значение ниже в этой статье.

```
$ cat ~/.vimrc
autocmd bufnewfile *.c so /home/jsmith/c_header.txt
autocmd bufnewfile *.c exe "1," . 10 . "g/File Name :.*/s//File Name : " .expand("%")
autocmd bufnewfile *.c exe "1," . 10 . "g/Creation Date :.*/s//Creation Date : " .strftime("%d-%m-%Y")
autocmd Bufwritepre,filewritepre *.c execute "normal ma"
autocmd Bufwritepre,filewritepre *.c exe "1," . 10 . "g/Last Modified :.*/s/Last Modified :.*/Last Modified : " .strftime("%c")
autocmd bufwritepost,filewritepost *.c execute "normal `a"
```

### Щаг 3: Создайте новый файл с расширением \*.c

Теперь, если вы создаете новый файл с нужным расширением используя vim, в начало файла будет автоматически добавлен заголовок, определенный в шаге 1 и добавлены имя файла и дата создания.

```
$ vi myfile.c
/* -.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
* File Name : myfile.c
* Purpose :
* Creation Date : 20-12-2008
* Last Modified :
* Created By :
_._._._._._._._._._._._._._._._._._._._._.*/
```

После того как вы сохраните файл myfile.c, он будет автоматически обновлен в поле Last Modified.

```
$ vi myfile.c
/* -.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.-.
* File Name : myfile.c
* Purpose :
* Creation Date : 20-12-2008
* Last Modified : Sat 20 Dec 2008 09:37:30 AM PST
* Created By :
_._._._._._._._._._._._._._._._._._._._._.*/
```

### Пояснения по командам autocmd в \~/.vimrc

```
$ cat -n ~/.vimrc
     1  autocmd bufnewfile *.c so /home/jsmith/c_header.txt
     2  autocmd bufnewfile *.c exe "1," . 10 . "g/File Name :.*/s//File Name : " .expand("%")
     3  autocmd bufnewfile *.c exe "1," . 10 . "g/Creation Date :.*/s//Creation Date : " .strftime("%d-%m-%Y")
     4  autocmd Bufwritepre,filewritepre *.c execute "normal ma"
     5  autocmd Bufwritepre,filewritepre *.c exe "1," . 10 . "g/Last Modified :.*/s/Last Modified :.*/Last Modified : " .strftime("%c")
     6  autocmd bufwritepost,filewritepost *.c execute "normal `a"
```

* Строка 1 определяет где находиться файл шаблона. Она также указывает что данный шаблон используется для всех файлов с расширением \*.c.
* Строка 2 ищет шаблон "File Name :" с первой строки по десятую. Если находит, то дописывает текущее имя файла.
* Строка 3 по аналогии с строкой 2 обновляет Creation Date.
* Строка 5 обновляет поле Last Modified текущей датой и временем когда вы сохраняете файл.
* Строки 4 \& 6: когда вы сохраняете файл, курсор перемещается на поле "Last modified :" (потому что это последняя операция записи). Если вы хотите вернуть курсор назад на предыдущую позицию, вам необходимо добавить строки 4 и 6 в файл .vimrc.
* Строка 4 отмечает позицию курсора перед сохранением файла.
* Строка 6 возвращает позицию курсора на отмеченное в строке 4 место.

### Полезные советы:

* **Проверьте включена ли функция autocmd в Vi / Vim** - Выполните :version в vi / vim. Если функция autocommand включена, отобразится +autocmd.
* **Помощь по Autocommand** - Выполните **:help au** из vi / vim.

**Постовой**

Делайте Бизнес с Орифлейм по новому. Теперь вы можете использовать все возможности интернета.

Лучшие шкафы купе на заказ в Москве. Купим продукцию в компании \<\<АВ-Стиль\>\> вы покупаете мебель от ведущих производителей по самым низким ценам.  

### Еще записи по теме

* Замораживаем сессию vi
* Графическая подборка команд vi-vim
* Как установить редактор Vim в Windows
* Список команд Vim  

### Комментариев: 3

   1. Аноним \| 2010-07-04 в 13:25:27  
   ![](http://www.gravatar.com/avatar.php?gravatar_id=9d13dc2208a6838d9f9d54123cd88c0d&size=80)

   Ещё бы узнать, как переместиться внутрь функции main после автоматической вставки её заготовки, было бы вообще хорошо.  
   2. Elena.rema \| 2012-08-14 в 17:49:42  
   ![](http://www.gravatar.com/avatar.php?gravatar_id=a28de37571bdca6e29af0811fd6a64c8&size=80)

   При попытке применить настройки получаю вот такую ошибку:

   # source !$

   source ../.vimrc

   autocmd: команда не найдена

   bash: ../.vimrc: строка 2: ошибка синтаксиса около неожиданной лексемы \`('

   bash: ../.vimrc: строка 2: \`autocmd bufnewfile \*.py exe "1," . 10 . "g/File Name :.\*/s//File Name : " .expand("%")'

   Подскажите, в чем проблема?  
   3. KodopiK \| 2013-10-16 в 21:52:18  
   ![](http://www.gravatar.com/avatar.php?gravatar_id=79956f6dc12799733af4816251804e69&size=80)

   Спасибо! Всё работает. Единственная проблема: "с первой строки по десятую". Если в файле меньше 10 строк, то выдаётся ошибка "E16: Недопустимый диапазон" (например, это актуально для нового файла). Я решил проблему, добавив вместо 10 число строк заголовка (у меня это 7). Возможно, можно это как-то автоматизировать, но пока мне не требуется.  

### Оставьте комментарий!

B I U S Цитата Код  
Ваше имя

Используйте нормальные имена.

Вход/регистрация (войти без комментирования)

E-mail \> Пароль

Ваше имя Сайт

Имя и сайт используются только при регистрации

Если вы уже зарегистрированы как комментатор или хотите зарегистрироваться, укажите пароль и свой действующий email. При регистрации на указанный адрес придет письмо с кодом активации и ссылкой на ваш персональный аккаунт, где вы сможете изменить свои данные, включая адрес сайта, ник, описание, контакты и т.д., а также подписку на новые комментарии.  
Введите нижние символы (обязательно)   

Отправить  

3D метки
--------

<br />

Категории
---------

Apache BSD Backup Data Protection Manager Exchange Server Fedora Firewall ForeFront Maxsite CMS Perl RHEL, CentOS SBS SCCM SCOM SQL SSH Sharepoint Shell Suse TMG Ubuntu Windows 7 Windows Server 2008 Windows Vista Windows XP Администрирование Windows Виртуализация Разное Редакторы Сети Управление пакетами  

Рейтинг страниц
---------------

* Отключение Internet Explorer Enhanced Security Configuration (IE ESC) в Windows Server 2008 ^10^
* Ввод Mac в домен Windows ^10^
* Переводим Ubuntu в постоянный root-режим ^10^
* Настраиваем SSH клиент ^10^
* Как выбрать VPS ^10^
* Удаленный доступ к вашему MySQL серверу через ssh ^10^
* Контролируем виртуальные машины в Virtualbox используя VBoxManage ^10^
* Блокировка IP адресов и подсететей в Nginx ^10^
* Семь незаменимых бесплатных программ для администраторов сети ^10^
* HoverIP -- GUI для ipconfig, nslookup, таблицы маршрутизации, ping, traceroute, сканирования портов ^10^  

Случайные статьи
----------------

* Как создать VHD в Windows 7
* Вебсервер Apache не перезагружается или не стартует - диагностика
* Настраиваем передачу зон с помощью DNSCMD  

Присоединение Windows 7 к домену
--------------------------------

* **wpavelOn \>\>** Официальное трудоустройство, работа через интернет.

15 команд для управления PostgreSQL
-----------------------------------

* **mpavelOn \>\>** Официальная работа в интернете с обучением.

Добавление DNS серверов с помощью DNS-add
-----------------------------------------

* **tpavelOn \>\>** Заработок через интернет официальное трудоустройство.

Добавление алиасов IP адресов в Windows XP
------------------------------------------

* **npavelOn \>\>** Работа через интернет официальное трудоустройство.

AD Tidy
-------

* **rpavelOn \>\>** Работа на дому официальное трудоустройство.  
**Сегодня:** 0   
**Вчера:** 0  

Самое читаемое
--------------

* Быстрая установка драйверов с помощью DriverPack Solution 12 ^89^
* Linux: как добавить пользователя в группу ^81^
* Взламываем WPA2 PSK используя Backtrack 4, aircrack-ng и John The Ripper ^73^
* 15 команд для управления PostgreSQL ^53^
* 10 примеров использования команды Ping ^46^
* О сайте ^39^
* 5 способов поиска файлов в Linux, используя терминал. ^34^
* MySQL: Как создать пользователя в MySQL ^33^
* Настройка автоматического интервала отправки и получения в Outlook ^33^
* Ввод Mac в домен Windows ^31^  

Счетчики и кнопки
-----------------

![Majordomo.ru - надёжный хостинг](http://www.majordomo.ru/bt/new/button_01.gif)  

Рейтинг страниц
---------------

* Отключение Internet Explorer Enhanced Security Configuration (IE ESC) в Windows Server 2008 ^10^
* Ввод Mac в домен Windows ^10^
* Переводим Ubuntu в постоянный root-режим ^10^
* Настраиваем SSH клиент ^10^
* Как выбрать VPS ^10^
* Удаленный доступ к вашему MySQL серверу через ssh ^10^
* Контролируем виртуальные машины в Virtualbox используя VBoxManage ^10^
* Блокировка IP адресов и подсететей в Nginx ^10^
* Семь незаменимых бесплатных программ для администраторов сети ^10^
* HoverIP -- GUI для ipconfig, nslookup, таблицы маршрутизации, ping, traceroute, сканирования портов ^10^  

Полезная информация
-------------------

Метки
-----

Active Directory Apache Aptitude BIND Backtrack Backtrack 2 Backup CentOS Citrix DHCP DNS DPM 2007 DPM 2010 Data Protection Manager Debian Dropbox Easy Print Exchange 2007 Exchange Server FTP Fedora FreeBSD GPO Gnome Google Chrome Grub IIS ISA Server Java LDAP LVM Linux Linux утилиты MDT Maxsite CMS MySQL NPS Nautilus OpenBSD Openfiler Outlook Perl RHEL RODC SBS SCCM SCOM SQL Samba Server 2008 Server Core Sharepoint Suse Linux Synaptic TMG Ubuntu Ubuntu Hardy VMware ESX VMware ESXi VMware Server VPN VirtualBox VirtualCenter Vista Vmware Vyatta WDS WSUS Windows Windows 2008 Windows 2008 R2 Windows 2008 R2Sysprep in Windows Server 2008 R2 Windows 7 Windows 8 Windows XP X Windows Xen XenServer bsod cacti cheat sheet cisco dpkg dsquery ebox exchange exchange 2010 exchange 2013 firewall forefront hyper-v iptables ipv6 kernel mac microsoft monitoring mysqladmin netsh nfs  

Любопытное
----------

© Linux и Windows: помощь админам и пользователям, 2017   
Работает на MaxSite CMS \| Время: 1.5411 \| SQL: 29 \| Память: 9.62MB \| Вход  
