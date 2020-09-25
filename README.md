# Flight_Scraper

Flight_Scraper is a Python script for scraping Google Flights to notify the user through email when a certain flight is available for a good price.

## Installation

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install smtplib for email and selenium for the webdriver.


```bash
pip install smtplib
pip install selenium
```

## Secrets
A secrets.py file is included containing an email address and password. To safely send emails from a Gmail account you can enable [2-step-verification](https://www.google.com/landing/2step/) and create an [app password](https://support.google.com/accounts/answer/185833?hl=nl) for your email only.

## Use
#### Setting up

First you might need to change the directory name in the import statement for secrets.py
```python
from [DirectoryName].secrets import email, password
```

Then you need to create a dict for the flight you will be scraping.
```python
dict_name = {
    'to': 'Belo Horizonte', # Destination City
    'type': 'return', # 'return' or 'single'
    'url1': 'https://www.google.com/flights?lite=0#flt=/m/0k3p./m/0l3q2.', # First part of the URL *
    'middleBit': '*/m/0l3q2./m/0k3p.', # Middle part of the URL
    'url2': ';c:EUR;e:1;sd:1;t:f', # Remainder of the URL
    'price': 700, # Desired maximum pricepoint in your currency
    'toDates': [ # Options for desired departure dates (YYYY-MM-DD)
        '2020-06-27',
        '2020-06-28',
        '2020-06-29',
    ],
    'fromDates': [ # Options for desired return dates (YYYY-MM-DD) (null if it is a single flight/one-way ticket)
        '2020-08-04',
        '2020-08-05',
        '2020-08-06'
    ]
}
```
\* The URL of a Google Flights looks something like this: 

**https://www.google.com/flights?lite=0#flt=/m/0k3p./m/0l3q2.2020-10-11*/m/0l3q2./m/0k3p.2020-10-15;c:EUR;e:1;sd:1;t:f**

This URL consists of a first part: **https://www.google.com/flights?lite=0#flt=/m/0k3p./m/0l3q2.**

The departure date: **2020-10-11**

A middle part: ***/m/0l3q2./m/0k3p.** 

The return date: **2020-10-15** 

And then the remainder:**;c:EUR;e:1;sd:1;t:f**

Note: In the case that you are looking for a single/one-way flight, then there will be no middle part and no return date.


#### Running the code

To run the code, make a new instance of the Flight class containing your dict and then run the scrape function of this instance.

```python
instance_name = Flight(dict_name)
instance_name.scrape()
```
