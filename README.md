# README

## installation
To install, do the following:
```
git clone
cd alexandra
pip install -r requirements.txt
```

*Note: this program is supported only on Python 3.6+.*

## usage
The `config.yml` file contains all the necessary information to run. The most important
configurations are `data_file` and `products`. If you have an existing Excel and want to
append the new information onto that Excel file, place that file into the same folder
and change `data_file` to the name (not the file path!) of the file.

The `products` section is organized by type of item. The `name` subsection represents a
worksheet in the Excel file and is the name of a particular type of item. The ASINs of
each product you want to examine are listed underneath. An ASIN is the ID value Amazon
gives all products offered on its site; you can find it on the webpage of that product.

To run, simply execute:
```
python scrape.py
```

If the program isn't able to find some information about a product, it will print a
warning while executing, as well as a full list of the ASINs of products where the
information gathered was incomplete (labeled as "Errors"). If an exception occurs in the
middle, or if the data can't be written to the file, the program will print a
JSON-serialized string that can be copied and written in manually, as described below.
Periodically, especially when not using proxies, Amazon may detect the scraper and block
webpages, requiring you to enter a CAPTCHA. The program will stop at this point and wait
for the user to do this manually (just go to any Amazon webpage and enter the CAPTCHA)
before continuing.

To stop the program while running, use `Ctrl-C`.

# options
- `-p`/`--proxy`: The program will scrape for some free proxies to use when accessing
Amazon, making it harder for them to detect the scraping. However, these proxies
frequently don't work, so in general it's better not to use this option for now.
- `-n`/`--new`: Instead of appending the data gathered to an existing Excel file, the
program instead creates a new Excel file. This option gives a cleaner collection of data;
when appendng, oftentimes new data is entered a few lines too low (you'll see what I
mean).
- `-d`/`--debug [ASIN]`: This allows you to test a single ASIN to see if there are any
problems. It will print the Amazon webpage's HTML (it's very very long), as well as
whatever data was gathered.
- `-w`/`--write [JSON]`: If an error occurs and the data already gathered doesn't get
written to the Excel sheet, you can copy the JSON of data that gets printed and use this
option to write it to file directly. Use single-quotes around the JSON.
