---
title: 
tags: 
author: easy-zzz
source: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04-ru
---
Установка Node.js в Ubuntu 20.04 \| DigitalOcean  
SnapShooter is now a part of DigitalOcean! Easily backup your multi-cloud stack. Read more -\>

* We're hiring
* Blog
* [Docs](https://docs.digitalocean.com/products/)
* [Get Support](https://www.digitalocean.com/support/)
* Sales  

* Products  
  Featured Products
  * DropletsScalable virtual machines
  * KubernetesManaged Kubernetes clusters
  * CloudwaysManaged cloud hosting
  * App PlatformGet apps to market faster
  * DatabasesWorry-free setup \& maintenance
  * SpacesSimple object storage  
  Compute

  <br />

  * Droplets
  * Kubernetes
  * App Platform
  * Functions  
  Cloud Website Hosting

  <br />

  * Cloudways  
  Storage

  <br />

  * Spaces Object Storage
  * Volumes Block Storage  
  Networking

  <br />

  * Virtual Private Cloud (VPC)
  * Cloud Firewalls
  * Load Balancers
  * [DNS](https://www.digitalocean.com/docs/networking/dns/)  
  Managed Databases

  <br />

  * MongoDB
  * MySQL
  * PostgreSQL
  * Redis™  
  Developer Tools

  <br />

  * [API](https://docs.digitalocean.com/reference/api/)
  * CLI
  * Support Plans
  * Monitoring
  * Uptime  
  See all products
* Solutions  
  Our Business Solutions
  * Website HostingSimple and reliable cloud website hosting
  * VPS HostingVPS hosting options suited to every need  
  Cloudways

  <br />

  * [Managed WordPress](https://www.cloudways.com/en/wordpress-hosting.php?id=1227510)
  * [Managed Woocommerce](https://www.cloudways.com/en/woocommerce-hosting.php?id=1227510)
  * [Managed Magento](https://www.cloudways.com/en/magento-hosting.php?id=1227510)  
  By use case

  <br />

  * Cloud VPN
  * Web \& Mobile Apps
  * Game Development
  * Video Streaming
  * SaaS Platforms
  * Blockchain  
  Resources

  <br />

  * Customers
  * Security
  * Startup Resources
  * Questions?  
  Speak With An Expert Today  
  See all solutions
* [Marketplace](https://marketplace.digitalocean.com/)
* Community  
  Our community
  * Community HomeDevOps and development guides
  * [CSS-TricksAll things web design](https://css-tricks.com/)  
  Resources

  <br />

  * Tutorials
  * Questions And Answers
  * Tools
  * Write for DOnations
  * Customer Stories
  * DigitalOcean Blog  
  Get Involved

  <br />

  * Hatch Startup Program
  * Open Source Sponsorships
  * [Hacktoberfest](https://hacktoberfest.digitalocean.com/)
  * Deploy
  * DO Impact  
  Documentation

  <br />

  * [Quick Start](https://docs.digitalocean.com/products/getting-started/)
  * [Droplets](https://docs.digitalocean.com/products/droplets/)
  * [Storage](https://docs.digitalocean.com/products/storage/)
  * [App Platform](https://docs.digitalocean.com/products/app-platform/)
  * [API Reference](https://docs.digitalocean.com/reference/api/)
  * [Domains and DNS](https://docs.digitalocean.com/products/networking/dns/)
* Pricing

<!-- -->

* Log in
  * Sign in
  Community [DigitalOcean](https://cloud.digitalocean.com/login)
* Sign up
  * Sign up
  Community [DigitalOcean](https://cloud.digitalocean.com/registrations/new)

<!-- -->

* We're hiring
* Blog
* [Docs](https://docs.digitalocean.com/products/)
* [Get Support](https://www.digitalocean.com/support/)
* Sales

* Tutorials
* Questions
* Learning Paths
* For Businesses
* [Product Docs](https://docs.digitalocean.com/products/)
* Social Impact
* Search Community  
CONTENTS
* Предварительные требования
* Вариант 1 --- Установка Node.js с помощью Apt из репозиториев по умолчанию
* Вариант 2 --- Установка Node.js с помощью Apt через архив NodeSource PPA
* Вариант 3 --- Установка Node с помощью Node Version Manager
* Заключение  

### Related


Использование объектных методов в JavaScript

View
Создание самоподписанных сертификатов SSL для Apache в Ubuntu 18.04

View  

#### // Tutorial //

Установка Node.js в Ubuntu 20.04
================================

Published on June 11, 2020

* JavaScript
* Ubuntu
* Ubuntu 20.04
* Node.js

![Default avatar](https://doimages.nyc3.digitaloceanspaces.com/46f22fba-7718-478b-86ae-e8b875f0473e_default-avatar.jpeg)  
By Brian Boucheron  
Developer and author at DigitalOcean.  
Русский  

### Введение

[Node.js](https://nodejs.org/) --- это среда выполнения JavaScript для программирования на стороне сервера. Она позволяет разработчикам создавать масштабируемый серверный функционал с помощью JavaScript, языка, который многим уже знаком по веб-разработке под браузер.

В этом обучающем модуле мы покажем вам три разных варианта установки Node.js на сервере Ubuntu 20.04:

* использование `apt` для установки пакета `nodejs` из репозитория ПО Ubuntu по умолчанию
* использование `apt` с альтернативным репозиторием ПО PPA для установки определенных версий пакета `nodejs`
* установка диспетчера `nvm` (Node Version Manager) и его использование для установки нескольких версий node и управления ими

Для многих пользователей будет достаточно использовать `apt` с репозиторием по умолчанию. Если вам требуется определенная более новая (или старая) версия Node, вам следует использовать репозиторий PPA. Если вы занимаетесь активной разработкой приложений Node, и вам нужно часто переключаться между версиями `node`, используйте метод `nvm`.

Предварительные требования
--------------------------

Для целей этого обучающего модуля предполагается, что вы используете ОС Ubuntu 20.04. Для начала вам потребуется учетная запись пользователя без привилегий root с привилегиями sudo. Чтобы создать такую учетную запись следуйте указаниям [обучающего модуля \<\<Начальная настройка сервера Ubuntu 20.04\>\>](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04).

Вариант 1 --- Установка Node.js с помощью Apt из репозиториев по умолчанию
--------------------------------------------------------------------------

В репозиториях Ubuntu 20.04 по умолчанию содержится версия Node.js, обеспечивающая согласованную работу в разных системах. На момент составления этого обучающего модуля в репозиториях хранится версия 10.19. Это не самая последняя версия, но она должна быть стабильной и подходить для небольших экспериментов с языком.

Для получения этой версии можно использовать диспетчер пакетов `apt`. Обновите указатель локальных пакетов с помощью следующей команды:


             
           
              
            
    1. sudo apt update


             
           
Выполните установку Node.js:


             
           
              
            
    1. sudo apt install nodejs


             
           
Проверьте, что установка выполнена успешно, запросив у `node` номер версии:


             
           
              
            
    1. nodejs -v


             
           

             
           
            
              Output
             
           v10.19.0
Если пакет из репозитория отвечает вашим потребностям, для начала работы с Node.js ничего больше не потребуется. В большинстве случаев также нужно установить `npm`, диспетчер пакетов Node.js. Для этого установите пакет `npm` с помощью `apt`:


             
           
              
            
    1. sudo apt install npm


             
           
Это позволит вам устанавливать модули и пакеты для использования с Node.js.

Вы успешно установили Node.js и `npm`, используя `apt` и репозитории ПО Ubuntu по умолчанию. В следующем разделе мы покажем, как использовать альтернативный репозиторий для установки разных версий Node.js.

Вариант 2 --- Установка Node.js с помощью Apt через архив NodeSource PPA
------------------------------------------------------------------------

Для установки другой версии Node.js вы можете использовать архив *PPA* (архив персональных пакетов), обслуживаемый NodeSource. Через PPA можно установить другие версии Node.js, кроме доступных в официальных репозиториях Ubuntu. На момент составления этого обучающего модуля доступны версии Node.js v10, v12, v13 и v14.

Вначале установим PPA для получения доступа к его пакетам. Используйте в домашнем каталоге команду `curl` для получения скрипта установки предпочитаемой версии. Замените `14.x` предпочитаемым номером версии (если он отличается).


             
           
              
            
    1. cd ~


              
            
    2. curl -sL https://deb.nodesource.com/setup_14.x -o nodesource_setup.sh


             
           
Дополнительную информацию о доступных версиях можно найти в [документации по NodeSource](https://github.com/nodesource/distributions/blob/master/README.md).

Просмотрите содержимое загруженного скрипта в `nano` (или другом предпочитаемом текстовом редакторе):


             
           
              
            
    1. nano nodesource_setup.sh


             
           
Убедившись в безопасности запуска скрипта, закройте редактор и запустите скрипт с привилегиями `sudo`:


             
           
              
            
    1. sudo bash nodesource_setup.sh


             
           
Архив PPA будет добавлен в вашу конфигурацию, и кэш локальных пакетов автоматически обновится. Теперь вы можете установить пакет Node.js, как описывалось в предыдущем разделе:


             
           
              
            
    1. sudo apt install nodejs


             
           
Убедитесь в установке новой версии, запустив `node` с флагом версии `-v`:


             
           
              
            
    1. node -v


             
           

             
           
            
              Output
             
           v14.2.0
Пакет NodeSource `nodejs` содержит двоичный код `node` и `npm`, так что не нужно устанавливать `npm` отдельно.

Вы успешно установили Node.js и `npm`, используя `apt` и архив NodeSource PPA. В следующем разделе мы покажем, как использовать диспетчер версий Node Version Manager для установки нескольких версий Node.js и управления ими.

Вариант 3 --- Установка Node с помощью Node Version Manager
-----------------------------------------------------------

Еще одним способом установки Node.js, который является достаточно гибким, является использование nvm, или Node Version Manager. Это программное обеспечение позволяет устанавливать и поддерживать несколько разных независимых версий Node.js и связанных с ними пакетов Node.

Чтобы установить NVM на ваш сервер Ubuntu 20.04, откройте [страницу проекта на GitHub](https://github.com/nvm-sh/nvm). Скопируйте команду `curl` из файла README, отображаемого на главной странице. Она позволит получить самую последнюю версию скрипта установки.

Прежде чем передавать команду в `bash`, рекомендуется проверить скрипт, чтобы убедиться, что он не делает ничего, с чем вы не согласны. Вы можете сделать это, удалив сегмент `| bash` в конце команды `curl`:


             
           
              
            
    1. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh


             
           
Проверьте и убедитесь, что вы не возражаете против изменений, которые вносит скрипт. Если вас удовлетворит результат, запустите команду еще раз с добавлением `| bash` в конце. URL-адрес, который вы используете, будет меняться в зависимости от последней версии NVM, но в настоящий момент скрипт можно загрузить и запустить с помощью следующей команды:


             
           
              
            
    1. curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash


             
           
Она устанавливает скрипт `nvm` для вашей учетной записи. Для его использования необходимо сначала получить ваш файл `.bashrc`:


             
           
              
            
    1. source ~/.bashrc


             
           
Теперь вы можете спросить у NVM, какие версии Node доступны:


             
           
              
            
    1. nvm list-remote


             
           

             
           
            
              Output
             
           . . .
           v12.13.0   (LTS: Erbium)
           v12.13.1   (LTS: Erbium)
           v12.14.0   (LTS: Erbium)
           v12.14.1   (LTS: Erbium)
           v12.15.0   (LTS: Erbium)
           v12.16.0   (LTS: Erbium)
           v12.16.1   (LTS: Erbium)
           v12.16.2   (LTS: Erbium)
           v12.16.3   (Latest LTS: Erbium)
            v13.0.0
            v13.0.1
            v13.1.0
            v13.2.0
            v13.3.0
            v13.4.0
            v13.5.0
            v13.6.0
            v13.7.0
            v13.8.0
            v13.9.0
           v13.10.0
           v13.10.1
           v13.11.0
           v13.12.0
           v13.13.0
           v13.14.0
            v14.0.0
            v14.1.0
            v14.2.0
Это очень длинный список! Вы можете установить версию Node, введя любую версию релиза, которую вы видите. Например, для получения версии 13.6.0 воспользуйтесь следующей командой:


             
           
              
            
    1. nvm install v13.6.0


             
           
Вы можете увидеть установленные вами различные версии с помощью следующей команды:

    nvm list


             
           
            
              Output
             
           ->      v13.6.0
    default -> v13.6.0
    node -> stable (-> v13.6.0) (default)
    stable -> 13.6 (-> v13.6.0) (default)
    . . .
Она отображает текущую активную версию на первой строке (`-> v13.6.0`), за которой следуют псевдонимы и версии, на которые указывают эти псевдонимы.  
**Примечание.** Если у вас также имеется версия Node.js, установленная с помощью `apt`, здесь вы сможете увидеть `системную` запись. Вы всегда можете активировать установленную системой версию Node с помощью команды `nvm use system`​​​.

Также вы увидите псевдонимы для различных [релизов Node с длительной поддержкой (LTS)](https://nodejs.org/en/about/releases/):


             
           
            
              Output
             
           . . .
    lts/* -> lts/erbium (-> N/A)
    lts/argon -> v4.9.1 (-> N/A)
    lts/boron -> v6.17.1 (-> N/A)
    lts/carbon -> v8.17.0 (-> N/A)
    lts/dubnium -> v10.20.1 (-> N/A)
    lts/erbium -> v12.16.3 (-> N/A)
Мы можем установить релиз на основе этих псевдонимов. Например, для установки последней версии с долгосрочной поддержкой, `erbium`, запустите следующую команду:


             
           
              
            
    1. nvm install lts/erbium


             
           

             
           
            
              Output
             
           Downloading and installing node v12.16.3...
    . . .
    Now using node v12.16.3 (npm v6.14.4)
Вы можете переключаться между установленными версиями с помощью `nvm use`:

    nvm use v13.6.0

    Now using node v13.6.0 (npm v6.13.4)

Вы можете проверить, что установка выполнена успешно, с помощью того же метода, использованного в других разделах. Введите следующую команду:


             
           
              
            
    1. node -v


             
           

             
           
            
              Output
             
           v13.6.0
Корректная версия Node установлена на нашем компьютере, как мы и ожидали. Совместимая версия `npm` также доступна.

Заключение
----------

Существует несколько способов запустить и начать использование Node.js на сервере Ubuntu 20.04. Наиболее подходящий метод из вышеперечисленных определяется в зависимости от обстоятельств. Хотя использование упакованной версии из репозитория Ubuntu --- самый простой метод, использование `nvm` или архива NodeSource PPA дает дополнительную гибкость.

Дополнительную информацию о программировании с помощью Node.js можно найти в нашей серии обучающих материалов [\<\<Программирование на Node.js\>\>](https://www.digitalocean.com/community/tutorial_series/how-to-code-in-node-js).  
If you've enjoyed this tutorial and our broader community, consider checking out our DigitalOcean products which can also help you achieve your development goals.

[Learn more here](https://www.digitalocean.com/)  
About the authors  
![Default avatar](https://doimages.nyc3.digitaloceanspaces.com/46f22fba-7718-478b-86ae-e8b875f0473e_default-avatar.jpeg)  
Brian Boucheron

author  
Developer and author at DigitalOcean.  

#### Still looking for an answer?

Ask a question Search for more help  
Was this helpful?  
Yes No  
[](https://twitter.com/share?text=%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0%20Node.js%20%D0%B2%20Ubuntu%2020.04&url=https%3A%2F%2Fwww.digitalocean.com%2Fcommunity%2Ftutorials%2Fhow-to-install-node-js-on-ubuntu-20-04-ru%3Futm_medium%3Dcommunity%26utm_source%3Dtwshare%26utm_content%3Dhow-to-install-node-js-on-ubuntu-20-04-ru) [](https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fwww.digitalocean.com%2Fcommunity%2Ftutorials%2Fhow-to-install-node-js-on-ubuntu-20-04-ru%3Futm_medium%3Dcommunity%26utm_source%3Dtwshare%26utm_content%3Dhow-to-install-node-js-on-ubuntu-20-04-ru)  
Comments  
Leave a comment  
This textbox defaults to using **Markdown** to format your answer.

You can type **!ref** in this text area to quickly search our full set of tutorials, documentation \& marketplace offerings and insert the link!  
Sign In or Sign Up to Comment  
[](https://creativecommons.org/licenses/by-nc-sa/4.0/) [This work is licensed under a Creative Commons Attribution-NonCommercial- ShareAlike 4.0 International License.](https://creativecommons.org/licenses/by-nc-sa/4.0/)  

### Popular Topics

* Ubuntu
* Linux Basics
* JavaScript
* React
* Python
* Security
* MySQL
* Docker
* Kubernetes
* Browse all topic tags
* [Free Managed Hosting](https://www.cloudways.com/en/managed-hosting-for-digital-ocean.php?id=1227510&data1=community_site&data2=--side-nav&utm_source=digitalocean.com&utm_medium=referral&utm_campaign=do-ing-website-community_site-side-nav&utm_content=-)
* All tutorials  

### Questions

* Q\&A Forum
* Ask a question
* [DigitalOcean Support](https://docs.digitalocean.com/support/)  

#### Try DigitalOcean for free

Click here to [Sign up](https://cloud.digitalocean.com/registrations/new?refcode=f6fcd01aaffb) and get $200 of credit to try our products over 60 days!  

##### Join the Tech Talk

**Success!** Thank you! Please check your email for further details.

Please complete your information!

Get our biweekly newsletter

Sign up for Infrastructure as a Newsletter.

Hollie's Hub for Good

Working on improving health and education, reducing inequality, and spurring economic growth? We'd like to help.

Become a contributor

You get paid; we donate to tech nonprofits.
Featured on Community Kubernetes Course Learn Python 3 Machine Learning in Python Getting started with Go Intro to Kubernetes DigitalOcean Products Virtual Machines Managed Databases Managed Kubernetes Block Storage Object Storage [Marketplace](https://marketplace.digitalocean.com/) VPC Load Balancers

### Welcome to the developer cloud

DigitalOcean makes it simple to launch in the cloud and scale up as you grow -- whether you're running one virtual machine or ten thousand.
Learn More  

###### Company

* About
* [Leadership](https://investors.digitalocean.com/governance/executive-management/default.aspx)
* Blog
* Careers
* Customers
* Partners
* Channel Partners
* Referral Program
* Affiliate Program
* Press
* Legal
* Security
* [Investor Relations](https://investors.digitalocean.com/)
* DO Impact  

###### Products

* Products Overview
* Droplets
* Kubernetes
* App Platform
* Functions
* [Cloudways](https://www.cloudways.com/?id=1227510)
* Managed Databases
* Spaces
* Marketplace
* Load Balancers
* Block Storage
* Tools \& Integrations
* [API](https://docs.digitalocean.com/reference/api/)
* Pricing
* [Documentation](https://docs.digitalocean.com/)
* [Release Notes](https://docs.digitalocean.com/release-notes/)
* Uptime  

###### Community

* Tutorials
* Q\&A
* [CSS-Tricks](https://css-tricks.com/)
* Write for DOnations
* Currents Research
* Hatch Startup Program
* deploy by DigitalOcean
* [Shop Swag](http://store.digitalocean.com/)
* Research Program
* Open Source
* Code of Conduct
* Newsletter Signup
* [Meetups](https://www.meetup.com/pro/digitalocean/?utm_source=do_www)  

###### Solutions

* Website Hosting
* VPS Hosting
* Web \& Mobile Apps
* Game Development
* Streaming
* VPN
* SaaS Platforms
* Cloud Hosting for Blockchain
* Startup Resources  

###### Contact

* [Support](https://www.digitalocean.com/support)
* Sales
* Report Abuse
* [System Status](https://status.digitalocean.com/)
* [Share your ideas](https://ideas.digitalocean.com/)  

###### Company

* About
* [Leadership](https://investors.digitalocean.com/governance/executive-management/default.aspx)
* Blog
* Careers
* Customers
* Partners
* Channel Partners
* Referral Program
* Affiliate Program
* Press
* Legal
* Security
* [Investor Relations](https://investors.digitalocean.com/)
* DO Impact  

###### Products

* Products Overview
* Droplets
* Kubernetes
* App Platform
* Functions
* [Cloudways](https://www.cloudways.com/?id=1227510)
* Managed Databases
* Spaces
* Marketplace
* Load Balancers
* Block Storage
* Tools \& Integrations
* [API](https://docs.digitalocean.com/reference/api/)
* Pricing
* [Documentation](https://docs.digitalocean.com/)
* [Release Notes](https://docs.digitalocean.com/release-notes/)
* Uptime  

###### Community

* Tutorials
* Q\&A
* [CSS-Tricks](https://css-tricks.com/)
* Write for DOnations
* Currents Research
* Hatch Startup Program
* deploy by DigitalOcean
* [Shop Swag](http://store.digitalocean.com/)
* Research Program
* Open Source
* Code of Conduct
* Newsletter Signup
* [Meetups](https://www.meetup.com/pro/digitalocean/?utm_source=do_www)  

###### Solutions

* Website Hosting
* VPS Hosting
* Web \& Mobile Apps
* Game Development
* Streaming
* VPN
* SaaS Platforms
* Cloud Hosting for Blockchain
* Startup Resources  

###### Contact

* [Support](https://www.digitalocean.com/support)
* Sales
* Report Abuse
* [System Status](https://status.digitalocean.com/)
* [Share your ideas](https://ideas.digitalocean.com/)  

© 2023 DigitalOcean, LLC. All rights reserved.

* [](https://www.twitch.tv/digitaloceantv)
* [](https://twitter.com/digitalocean)
* [](https://www.facebook.com/DigitalOceanCloudHosting)
* [](https://www.instagram.com/thedigitalocean/)
* [](https://www.youtube.com/user/DigitalOceanVideos)
* [](https://www.linkedin.com/company/digitalocean/)
* [](https://dev.to/digitalocean)
* [](https://www.glassdoor.com/Overview/Working-at-DigitalOcean-EI_IE823482.11,23.htm)
* [](https://www.builtinnyc.com/company/digitalocean)  
