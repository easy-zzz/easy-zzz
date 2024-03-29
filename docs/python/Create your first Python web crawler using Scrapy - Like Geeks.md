---
title: Создайте свой первый веб-сканер на Python с помощью Scrapy
tags: python, scrapy
author: easy-zzz
source: https://likegeeks.com/python-web-crawler-scrapy/
---
Создайте свой первый веб-сканер на Python с помощью Scrapy
Skip to content  
Search for:  
* [](https://www.pinterest.com/likegeeks/)
* [](https://www.youtube.com/channel/UC9g6sApRZ3Vib6vROG5YPaA)
* [](https://twitter.com/likegeeks)
* [](https://www.facebook.com/likegeeks)  
[![Create your first Python web crawler using Scrapy - Like Geeks](https://likegeeks.com/wp-content/uploads/2020/12/logo.png)](https://likegeeks.com/)

[](https://likegeeks.com/)  
Menu  
* [Home](https://likegeeks.com/ "Home")
* [Linux](https://likegeeks.com/linux/)
* [Server Administration](https://likegeeks.com/server-administration/)
* [Web Development](https://likegeeks.com/web-development/)
* [Python](https://likegeeks.com/python/)  
[Python](https://likegeeks.com/python/)

Create your first Python web crawler using Scrapy
=================================================

[Mokhtar Ebrahim](https://likegeeks.com/author/admin/) Published: February 6, 2019 Last updated: August 18, 2022  
In this tutorial, the focus will be on one of the best frameworks for web crawling called Scrapy. You will learn the basics of Scrapy and how to create your first web crawler or spider. Furthermore, the tutorial gives a demonstration of extracting and storing the scraped data.

Scrapy is a Python web framework that you can use to crawl websites and efficiently extract data.  

You can use the extracted data for further processing, data mining, and storing the data in spreadsheets or any other business need.

Table of Contents
1

* Scrapy Architecture
  * Scrapy Engine
  * Scheduler
  * Downloader
  * Spiders
  * Item Pipeline
* Installing Scrapy
* Create a Scrapy Project
* Create a Spider
* Scrapy Basics
  * Selectors
  * Items
  * Item Loaders
  * Scrapy Shell
* Storing the data

Scrapy Architecture
-------------------

The architecture of Scrapy contains five main components:

1. Scrapy Engine
2. Scheduler
3. Downloader
4. Spiders
5. Item Pipelines

### Scrapy Engine

The Scrapy engine is the main component of Scrapy, which controls the data flow between all other components. The engine generates requests and manages events against an action.

### Scheduler

The scheduler receives the requests sent by the engine and queues them.

### Downloader

The objective of the downloader is to fetch all the web pages and send them to the engine. The engine then sends the web pages to the spider.

### Spiders

Spiders are the codes you write to parse websites and extract data.

### Item Pipeline

The item pipeline processes the items side by side after the spiders extract them.

Installing Scrapy
-----------------

You can simply install Scrapy along with its dependencies by using the Python Package Manager (pip).

Run the following command to install Scrapy in Windows:

```
pip install scrapy
```

However, the [official Installation guide](https://docs.scrapy.org/en/latest/intro/install.html) recommends installing Scrapy in a virtual environment because the Scrapy dependencies may conflict with other Python system packages, which will affect other scripts and tools.

Therefore, we will create a virtual environment to provide an encapsulated development environment.

In this tutorial, we will install a virtual environment first and then continue with the installation of Scrapy.

1. Run the following command in the Python Scripts folder to install the virtual environment:

```
pip install virtualenv
```

![Install VirtualEnv](https://likegeeks.com/wp-content/uploads/2019/02/1InstallVirtualEnv.png)

2. Now install virtualenvwrapper-win which lets us create an isolated Python virtual environments.

```
pip install virtualenvwrapper-win
```

![Install VirtualEnv Wrapper](https://likegeeks.com/wp-content/uploads/2019/02/2InstallVirtualEnvWrapper.png)

3. Set the path within the scripts folder, so you can globally use the Python commands:

```
set PATH=%PATH%;C:\Users\hp\appdata\local\programs\python\python37-32\scripts
```

4. Create a virtual environment:

```
mkvirtualenv ScrapyTut
```

Where ScrapyTut is the name of our environment:

![Create VirtualEnv](https://likegeeks.com/wp-content/uploads/2019/02/3-VirtualEnv.png)

5. Create your project folder and connect it with the virtual environment:  
   ![Connect Project to VirtualEnv](https://likegeeks.com/wp-content/uploads/2019/02/4ConnectProjecttoVirtualEnv.png)
6. Bind the virtual environment with the current working directory:

```
setprojectdir .
```

![Bind Virtual to project](https://likegeeks.com/wp-content/uploads/2019/02/5BindVirtualtoproject.png)

7. If you want to turn off the virtual environment mode, simply use *deactivate* as below:

```
deactivate
```

![Deactivate Virtual](https://likegeeks.com/wp-content/uploads/2019/02/6DeactivateVirtual.png)  

8. If you want to work again on the project, use the *workon* command along with the name of your project:

```
workon ScrapyTut
```

![Workon command](https://likegeeks.com/wp-content/uploads/2019/02/7Workon.png)

Now we have our virtual environment; we can continue the installation of Scrapy.

1. For installation in Windows, you have to download [OpenSSL](https://slproweb.com/products/Win32OpenSSL.html) and install it. Choose the regular version that matches your version of Python. Also, install the Visual C++ 2008 redistributables. Otherwise, you will get an error when installing dependencies.
2. Add C:\\OpenSSL-Win32\\bin to the system PATH.
3. When installing Scrapy, there are a number of packages that Scrapy depends on, and you have to install them. These packages include pywin32, twisted, zope.interface, lxml and pyOpenSSL.
4. In the ScrapyTut directory run the following pip command to install Scrapy:

```
pip install scrapy
```

Note that when installing Twisted, you may encounter an error as:

```
Microsoft visual c++ 14.0 is required
```

To fix this error, you will have to install the following from Microsoft build Tools:

![Build Tools Requirements](https://likegeeks.com/wp-content/uploads/2019/02/8BuildToolsRequirements.png)

After this installation, if you get another error like the following:

```
error: command 'C:\\Program Files (x86)\\Microsoft Visual Studio 14.0\\VC\\BIN\\link.exe' failed with exit status 1158
```

Simply download the wheel for [Twisted](https://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted) that matches your version of Python. Paste this wheel into your current working directory as:

![Twisted Wheel](https://likegeeks.com/wp-content/uploads/2019/02/9TwistedWheel.png)

Now run the following command:

```
pip install Twisted-18.9.0-cp37-cp37m-win32.whl
```

![Twisted installed](https://likegeeks.com/wp-content/uploads/2019/02/10TwistedSuccess.png)  

Now, everything is ready to create our first crawler, so let's do it.

Create a Scrapy Project
-----------------------

Before writing a Scrapy code, you will have to create a Scrapy project using the startproject command like this:

```
scrapy startproject myFirstScrapy
```

![Create Scrapy Project](https://likegeeks.com/wp-content/uploads/2019/02/11ScrapyProject.png)

That will generate the project directory with the following contents:

![Project directory list](https://likegeeks.com/wp-content/uploads/2019/02/12Project-directoryList.png)

The spider folder contains the spiders.

Here the scrapy.cfg file is the configuration file. Inside the myFirstScrapy folder, we will have the following files:

![cfg file](https://likegeeks.com/wp-content/uploads/2019/02/13-cfg-file.png)

Create a Spider
---------------

After creating the project, navigate to the project directory and generate your spider along with the website URL that you want to crawl by executing the following command:  

```
scrapy genspider jobs www.python.org
```

The result will be like the following:

![Web Spider](https://likegeeks.com/wp-content/uploads/2019/02/13Spider.png)

Our "jobs" spider folder will be like this:

![Spider Directory](https://likegeeks.com/wp-content/uploads/2019/02/14SpiderDirectory.png)

In the Spiders folder, we can have multiple spiders within the same project.

Now let's go through the content of our newly created spider. Open the jobs.py file which contains the following code:

```
import scrapy
class JobsSpider(scrapy.Spider):
    name = 'jobs'
    allowed_domains = ['www.python.org']
    start_urls = ['http://www.python.org/']
    def parse(self, response):
        pass
```

Here the AccessoriesSpider is the subclass of scrapy.Spider. The 'jobs' is the name of the spider. The 'allowed_domains' is the domain accessible by this spider.

The start_urls is the URL from where the web crawling will be started, or you can say it is the initial URL where web crawling begins. Then we have the parse method, which parses through the content of the page.

To crawl the accessories page of our URL, we need to add one more link in the start_urls property as below:

```
start_urls = ['http://www.python.org/',
                  'https://www.python.org/jobs/']
```

As we want to crawl more than one page, it is recommended to subclass the spider from the CrawlSpider class instead of the scrapy.spider class. For this, you will have to import the following module:

```
from scrapy.spiders import CrawlSpider
```

Our class will look like the following:  

```
class JobsSpider(CrawlSpider): …
```

The next step is to initialize the *rules* variable. The rules variable defines the navigation rules that the spider will follow when crawling the site. To use the rules object, import the following class:

```
from scrapy.spiders import Rule
```

The rules variable further contains rule objects such as:

1. *link_extractor,* which is an object of the Link Extractor class. The link_extractor object specifies how to extract links from the crawled URL. For this, you will have to import the Link Extractor class like this:

```
from scrapy.linkextractors import LinkExtractor
```

The rule variable will look like the following:

```
rules = (
        Rule(LinkExtractor(allow=(), restrict_css=('.list-recent-jobs',)),
             callback="parse_item",
             follow=True),)
```

2. *callback* is a string that is called when a link is extracted. It specifies the methods that will be used when accessing the elements of the page.
3. *follow* is a Boolean which specifies if the extracted link should be followed or not after this rule.

Here we used *allow* to specify the link we will extract. But in our example, we have restricted by CSS class. So only extract the pages with the class we specified.

The callback parameter specifies the method that will be called when parsing the page. The *.list-recent-jobs* is the class for all the jobs listed on the page. You can check the class of an item by right-clicking on that item and select inspect on the web page.

![Inspect CSS](https://likegeeks.com/wp-content/uploads/2019/02/16InspectCSS.png)

In the example, we called the spider's *parse_item* method instead of *parse*.

The content of the parse_item method is as follows:

```
    def parse_item(self, response):
        print('Extracting…' + response.url)
```

This will print Extracting... along with the URL currently being extracted. For example, a link https://www.python.org/jobs/3698/ is extracted. So on the output screen,

```
Extracting…https://www.python.org/jobs/3698/
```

To run the spider, navigate to your project folder and type in the following command:

```
scrapy crawl jobs
```

The output will be like the following:

![Crawl result](https://likegeeks.com/wp-content/uploads/2019/02/15firstOUtput.png)

In this example, we set follow=true, which means the crawler will crawl the pages until the rule becomes false. That means when the list of jobs ends.

If you want to get only the print statement, you can use the following command:

```
scrapy crawl –nolog jobs
```

The output will be like the following:

![Crawl output](https://likegeeks.com/wp-content/uploads/2019/02/17output.png)

Congratulations! You've built your first web crawler.

Scrapy Basics
-------------

Now we can crawl web pages. Let's play with the crawled content for a little.

### Selectors

You can use selectors to select some parts of data from the crawled HTML. The selectors select data from HTML by using XPath and CSS through response.xpath() and response.css() respectively. Just like in the previous example, we used the css class to select the data.

Consider the following example where we declared a string with HTML tags. Using the selector class, we extracted the data in the **h1** tag using the *Selector.xpath*:

```
>>> from scrapy.selector import Selector
>>> body = '<html><body><h1>Heading 1</h1></body></html>'
>>> Selector(text = body).xpath('//h1/text()').get()

'Heading 1'
```

### Items

Scrapy uses Python dicts to return the extracted data.

To extract data, Scrapy provides the **Item** class, which provides item objects. We can use these item objects as containers for the scraped data.

Items provide a simple syntax to declare fields. The syntax is like the following:

```
>>> import scrapy
>>> class Job(scrapy.Item):
	company = scrapy.Field()
```

The Field object specifies the Metadata for each field.

You may notice when we created the Scrapy project, Scrapy creates items.py file in our project directory. We can modify this file to add our items as follows:

```
import scrapy
class MyfirstscrapyItem(scrapy.Item):
    # define the fields for your item here like:
location = scrapy.Field()
```

Here we have added one item. You can call this class from your spider file to initialize the items as follows:

```
    def parse_item(self, response):
        item_links = response.css('.text > .listing-company > .listing-location > a::text'').extract()
        for x in item_links:
            yield scrapy.Request(x, callback=self.MyfirstscrapyItem)
```

In the above code, we have used the css method of response to extract the data.

In our web page, we have a div with class *text* , inside this div, we have a heading with class *listing-company* , inside this heading, we have a span tag with class *listing-location* , and finally, we have a tag *a* that contains some text. We extract this text using the extract() method.

Finally, we will loop through all the items extracted and call the items class.

Instead of doing all this in the crawler, we can also test our crawler by using only one statement while working in the Scrapy shell. We will demonstrate Scrapy shell in a later section.

### Item Loaders

The data or items scrapped by the Item object is loaded or populated by using the Item Loader. You can use the item loader to extend the parsing rules.

After extracting items, we can populate the items in the item loader with the help of selectors.

The syntax for Item loader is as follows:

```
from scrapy.loader import ItemLoader
from jobs.items import Job
def parse(self, response):
	l = ItemLoader(item=Job(), response=response)
	l.add_css(‘name’, ‘//li[@class = ‘listing-company’]’)
	l.load_item()
```

### Scrapy Shell

Scrapy shell is a command line tool that lets the developers test the parser without going through the crawler itself. With Scrapy shell, you can debug your code easily. The main purpose of Scrapy shell is to test the data extraction code.

We use the Scrapy shell to test the data extracted by CSS and XPath expression when performing crawl operations on a website.

You can activate the Scrapy shell from the current project using the shell command:

```
scrapy shell
```

![Scrapy Command](https://likegeeks.com/wp-content/uploads/2019/02/18ScrapyCommand.png)

if you want to parse a web page, so you will use the shell command along with the link of the page:

```
scrapy shell https://www.python.org/jobs/3659/
```

To extract the location of the job, simply run the following command in the shell:

```
response.css('.text > .listing-company > .listing-location > a::text').extract()
```

The result will be like this:

![Select by CSS](https://likegeeks.com/wp-content/uploads/2019/02/19output.png)

Similarly, you can extract any data from the website.

To get the current working URL, you can use the command below:

```
response.url
```

![Current URL](https://likegeeks.com/wp-content/uploads/2019/02/20currenturl.png)

This is how you extract all the data in Scrapy. In the next section, we will save this data into a CSV file.

Storing the data
----------------

Let's use the response.css in our actual code. We will store the value returned by this statement into a variable, and after that, we will store this into a CSV file. Use the following code:

```
    def parse_detail_page(self, response):
        location = response.css('.text > .listing-company > .listing-location > a::text').extract()
        item = MyfirstscrapyItem()
        item['location'] = location
        item['url'] = response.url
        yield item
```

Here we stored the result of response.css into a variable called *location*. Then we assigned this variable to the location object of the item in the MyfirstscrapyItem() class.

Execute the following command to run your crawler and store the result into a CSV file:

```
scrapy crawl jobs -o ScrappedData.csv
```

The will generate a CSV file in the project directory:

![CSV file output](https://likegeeks.com/wp-content/uploads/2019/02/21csv.png)

Scrapy is a very easy framework to crawl web pages. That was just the beginning. If you liked the tutorial and hungry for more, tell us on the comments blew what the next Scrapy topic you would like to read about is.  

* [Share on Facebook](https://www.facebook.com/sharer/sharer.php?u=https://likegeeks.com/python-web-crawler-scrapy/)
* [Tweet on Twitter](https://twitter.com/intent/tweet?text=Create+your+first+Python+web+crawler+using+Scrapy&url=https://likegeeks.com/python-web-crawler-scrapy/&via=likegeeks)
* [](https://www.linkedin.com/shareArticle?mini=true&url=https://likegeeks.com/python-web-crawler-scrapy/&title=Create your first Python web crawler using Scrapy)
* [](mailto:?subject=Create your first Python web crawler using Scrapy&body= https://likegeeks.com/python-web-crawler-scrapy/ "Share by Email")
* [](https://pinterest.com/pin/create/button/?url=https://likegeeks.com/python-web-crawler-scrapy/&media=https://likegeeks.com/wp-content/uploads/2019/02/Python-web-crawler.jpg&description=Create your first Python web crawler using Scrapy)
* [](https://api.whatsapp.com/send?text=Create your first Python web crawler using Scrapy https://likegeeks.com/python-web-crawler-scrapy/)  
![Mokhtar Ebrahim](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=100&d=mm&r=g)  
[Mokhtar Ebrahim](https://likegeeks.com/author/admin/)  
Mokhtar is the founder of LikeGeeks.com. He works as a Linux system administrator since 2010. He is responsible for maintaining, securing, and troubleshooting Linux servers for multiple clients around the world. He loves writing shell and Python scripts to automate his work.  
[](https://www.linkedin.com/in/mokhtar-ibrahim/)  

##### 9 thoughts on "Create your first Python web crawler using Scrapy"

   1. ![](https://secure.gravatar.com/avatar/b8f4b03a96ff7fcfbb7ab12e463e69ad?s=45&d=mm&r=g) **Bala prasad** says:  
   [2019-02-13 at 6:58 am](https://likegeeks.com/python-web-crawler-scrapy/#comment-3008)  
   More illustrated example required, understood just starting project  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2019-02-13 at 8:32 am](https://likegeeks.com/python-web-crawler-scrapy/#comment-3010)  
      We will prepare another article.  
      Reply
   2. ![](https://secure.gravatar.com/avatar/924a279387a5bafb17953aa7699601b6?s=45&d=mm&r=g) **zhilun** says:  
   [2019-07-10 at 12:50 pm](https://likegeeks.com/python-web-crawler-scrapy/#comment-6457)  
   Can write a tutorial on creating a web crawler with pycurl?  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2019-07-10 at 2:24 pm](https://likegeeks.com/python-web-crawler-scrapy/#comment-6461)  
      Yes we can, but it's about the demand. You can say that it's all about the readers.  
      Reply
   3. ![](https://secure.gravatar.com/avatar/7bd895349f704cad0df9db41a8be05e9?s=45&d=mm&r=g) **Keron Cyst** says:  
   [2019-10-21 at 4:51 am](https://likegeeks.com/python-web-crawler-scrapy/#comment-16153)  
   What do I do now?

   (ScrapyTut) (base) C:\\scrapytut\>pip install Twisted-18.9.0-cp37-cp37m-win32.whl  
   WARNING: Requirement 'Twisted-18.9.0-cp37-cp37m-win32.whl' looks like a filename, but the file does not exist  
   ERROR: Twisted-18.9.0-cp37-cp37m-win32.whl is not a supported wheel on this platform.  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2019-10-21 at 12:48 pm](https://likegeeks.com/python-web-crawler-scrapy/#comment-16182)  
      Are you sure about your architecture? Here I'm using 32bit.  
      Reply
      2. ![](https://secure.gravatar.com/avatar/f9898b8aa0378f702007ed23c11f0700?s=45&d=mm&r=g) **Cristian Vultur** says:  
      [2019-11-12 at 11:59 am](https://likegeeks.com/python-web-crawler-scrapy/#comment-19002)  
      You probably have a win_amd64 machine so follow the provided link and switch to an appropriate one from the list.  
      Reply
   4. ![](https://secure.gravatar.com/avatar/8871caacaa785c917993d54f666b6d74?s=45&d=mm&r=g) **Evans Bwalya** says:  
   [2020-04-04 at 3:02 pm](https://likegeeks.com/python-web-crawler-scrapy/#comment-27437)  
   Hi, running the jobs produces no results. Please help.  
   Reply
      1. ![](https://secure.gravatar.com/avatar/34ca0a894f5a054e8d2bda344dd48c49?s=45&d=mm&r=g) **Mokhtar Ebrahim** says:  
      [2020-04-04 at 6:30 pm](https://likegeeks.com/python-web-crawler-scrapy/#comment-27438)  
      Did you follow the steps the same way?  
      Also, make sure you use the same Python version used.  
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

[Python NumPy array tutorial](https://likegeeks.com/numpy-array-tutorial/)  
[Downloading Files using Python (Simple Examples)](https://likegeeks.com/downloading-files-using-python/)  
* [Disclaimer](https://likegeeks.com/disclaimer/)
* [Privacy Policy](https://likegeeks.com/privacy-policy/)
* [About](https://likegeeks.com/about/)
* [Contact](https://likegeeks.com/contact/)  
* [](https://www.pinterest.com/likegeeks/)
* [](https://www.youtube.com/channel/UC9g6sApRZ3Vib6vROG5YPaA)
* [](https://twitter.com/likegeeks)
* [](https://www.facebook.com/likegeeks)
