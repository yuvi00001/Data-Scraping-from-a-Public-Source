# Data-Scraping-from-Amazon.in

This project scrapes data for any searched product from Amazon.in and saves it in a .csv format.

The csv file generated has 513 records, with columns as ['description','price','rating','review_count','url']

Libraries used for this projects were :- 
csv, from time -> sleep, from datetime -> datetime, from selenium.common -> exceptions, from selenium -> webdriver.

This project follows an object oriented approach, where a class name AmazonScraper has several methods and once an object is been made of the class(AmazonScraper), all processes can be initiated by calling the run() method.
The run() method also takes an argument which is the name of the item to be searched, most of the work is done within this method by calling other member methods.

A unique filename is generated by the generate_filename() method, which returns 'name_of_the_item_searched'_timestamp(%Y%m%d%H%S%M).

save_data_to_csv() method initializes a new csv file with a unique name.
The create_wedriver() methods generates a driver from selenium.webdriver.Firefox(). This scraper scrapes 40 pages, but that can be increased or decreased by changing the range parameter in for() loop.

The get_url() method takes two argument as name of the item searched and page number and returns a url with a base template formated with item_name and page_number.

The collect_product_cards_from_page() method takes the driver as argument and find_elements_by_xpath on the current page. After looking at the inspect option form our browser, we find html tag that encloses the entire record. The appropriate tag for this problem turns out to be the 'div' tag, now to uniquly identify the record from all of the div tags we search for 'data-component-type="s-search-results"' inside the div tags, this method returns collection of records from the page as 'cards'.

The extract_card_data() takes 'cards' as argument and work for the extraction of a single record. From further inspecting the webpage we find that the h2 tag contains a single record, so we again find_elements_by_xpath and search for '//h2/a'. 
After find the record we extract the description, url, price, review_counts and ratings, we through exception selenium.common.exceptions.NoSuchElementException if there is no particular value in the record and return a empty string. 
Each record is saves into the csv file by calling the save_data_to_csv() method.



