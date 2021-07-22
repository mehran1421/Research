

.. image:: https://github.com/mehran1421/Research/blob/master/scrapy/pic/scrap.png
   :target: https://github.com/mehran1421/Research/blob/master/scrapy/pic/scrap.png

★ Research For Web Scraping By Scrapy Library ★

        Build It ∘ Cross It ∘ Update It</span>

.. contents:: Overview
   :depth: 3

**********************
how to install Scrapy
**********************

for install scrapy package::

    pip install Scrapy
    scrapy startproject your_project_name


**************************
project structure
**************************
in scrapy folder and file structure is::

    your_project_name
                ------- spiders
                            ------- __init__.py

                ------- __init__.py
                ------- items.py
                ------- middlewares.py
                ------- pipelines.py
                ------- settings.py
    scrapy.cfg



****************************
first app scraping by scrap
****************************
in this simple code, request to `https://quotes.toscrape.com/` site and take title information

this is a example code of scrapy

.. code-block:: python

    import scrapy

    class QuoteScrap(scrapy.Spider):
        name = 'quotes'
        start_urls = [
            'https://quotes.toscrape.com/'
        ]

        def parse(self, response, **kwargs):
            title = response.css('title').extract()
            yield {
                'title_text': title
            }
in this code make a **quotes** app and sey that attack in `start_urls`

using SelectorGadget extension You will find query in **response.css(query)** easier

***********************
How to Run example code
***********************
for run and attack to site::

    cd your_project_name
    scrapy crawl app_name  # name variable in class


***************************************
Extracting data with css class in site
***************************************
using by `response.css(my_query).extract(), we can take element that in site.

for more example by `scrapy shell "https://quotes.toscrape.com/"` can scrap in shell::

    # take title( tag + answer)
    >>> response.css("title").extract()
    ---['<title>Quotes to Scrape</title>']

    # take just answer of tag
    >>> response.css("title::text").extract()
    ---['Quotes to Scrape']

    # using slice
    >>> response.css("title::text")[0].extract()
    ---'Quotes to Scrape'

    # if want take tag with class
    >>> response.css("span.text::text")[2].extract()
    ---'“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”'


*****************************************
Extracting data with xpath class in site
*****************************************
we can extracting data with xpath::

    # take title( tag + answer)
    >>> response.xpath("//title").extract()
    ---['<title>Quotes to Scrape</title>']

    # take just answer of tag
    >>> response.xpath("//title/text()").extract()
    ---['Quotes to Scrape']

    # if want take tag with class
    >>> response.xpath("//span[@class='text']/text()")[2].extract()
    ---'“There are only two ways to live your life. One is as though nothing is a miracle. The other is as though everything is a miracle.”'

we can use both of them for example::

    # For convenience, we do not use only xpath
    >>> response.css("li.next a").xpath("@href").extract()
    ---['/page/2/']

    # take all <a> tag
    >>> response.css("a").xpath("@href")[2].extract()
    ---'/author/Albert-Einstein'

************************************************
take author and title in **quote.toscrape.com**
************************************************
in this example, take `title` and `author` and `tag` in site

.. code-block:: python

        def parse(self, response, **kwargs):
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css('.tag::text').extract()
                yield {
                    'title': title,
                    'author': author,
                    'tag': tag
                }

*********************************
**storing data** to json,csv,xml
*********************************
for storing data, in `items.py`

.. code-block:: python

    class ScrapItem(scrapy.Item):
    # define the fields for your item here like:
        title = scrapy.Field()
        author = scrapy.Field()
        tag = scrapy.Field()

and in `quete.py` must This is how we should change

.. code-block:: python

        def parse(self, response, **kwargs):
            items = ScrapItem()
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css('.tag::text').extract()

                items['title'] = title
                items['author'] = author
                items['tag'] = tag
                yield items

this is mean, extract data in site and pure it to items.py class for save or storing::

    scrapy crawl quotes -o items.json
    scrapy crawl quotes -o items.csv
    scrapy crawl quotes -o items.xml

*************************
storing data to database
*************************
for save or storing data to database must in `pipelines.py` file, change default class
this means first Scraped data in `quotes.py` and save to database in `pipelines.py`

in pipeline.py, connect to sqlite3 and insert data from items.py
this means that Extract data in **quotes.py** --> storing data in **items.py** --> saving data to database in **pipelines.py**

.. code-block:: python

    import sqlite3

    class ScrapPipeline(object):
        def __init__(self):
            self.create_connection()
            self.create_table()

        def create_connection(self):
            self.conn = sqlite3.connect("quotes.db")
            self.curr = self.conn.cursor()

        def create_table(self):
            self.curr.execute("""DROP TABLE IF EXISTS quotes_tb""")
            self.curr.execute("""create table quotes_tb(
                                 title text,
                                 author text,
                                 tag text
                                 )""")

        def store_db(self, item):
            self.curr.execute("""insert into quotes_tb values (?,?,?)""", (
                item['title'][0],
                item['author'][0],
                item['tag'][0],
            ))
            self.conn.commit()

        def process_item(self, item, spider):
            self.store_db(item=item)
            return item

******************************
pagination and following link
******************************
for take other page in scrap library, use following and callback

.. code-block:: python

        def parse(self, response, **kwargs):
            items = ScrapItem()
            all_div_quotes = response.css('div.quote')
            for quotes in all_div_quotes:
                title = quotes.css('span.text::text').extract()
                author = quotes.css('.author::text').extract()
                tag = quotes.css('.tag::text').extract()

                items['title'] = title
                items['author'] = author
                items['tag'] = tag
                yield items

                next_page = response.css('li.next a::attr(href)').get()
                if next_page is not None:
                    yield response.follow(next_page,callback=self.parse)

query in next_page is select `li` tag with `next` class then from it select `<a/>` tag with `href` attr

if you want Script the desired page number must ust this way

.. code-block:: python

    next_page = 'https://quotes.toscrape.com/page/' + str(QuoteScrap.page_number) + '/'
    if QuoteScrap.page_number < 11:
         QuoteScrap.page_number += 1
         yield response.follow(next_page, callback=self.parse)

`page_number` variable is define in class

************************
Set user-agent in robot
************************
install **scrapy-user-agent** package::

    pip install scrapy-user-agents

and copy this config to settings.py::

    DOWNLOADER_MIDDLEWARES = {
        'scrapy.downloadermiddlewares.useragent.UserAgentMiddleware': None,
        'scrapy_user_agents.middlewares.RandomUserAgentMiddleware': 400,
    }
this package take many(2200) user-agent for attack to site

**********************
using proxy to scrapy
**********************
install `scrapy-proxy-pool` package::

    pip install scrapy_proxy_pool
for more information, go to github 