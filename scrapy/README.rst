============================================
                **SCRAPY**
============================================

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

***********************
How to Run example code
***********************
for run and attack to site::

    cd your_project_name
    scrapy crawl app_name  # name variable in class

