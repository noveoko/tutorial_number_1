# Let's Learn Python #1: Web Scraping with Data Analysis

# Requirements

*   You must have Python 3.x [installed](https://www.python.org/downloads/).
*   No prior programming experience is required, nor expected

# The Project

*   Open up a new file in a **text editor** (I suggest you use [Notepad++](https://notepad-plus-plus.org/download/v7.4.2.html))
*   Save the file as **myscraper.py**
*   Write the following code in your file:

`import requests`

That will import the [requests library](http://docs.python-requests.org/en/master/) so that you can start using it in your program. A library is a pre-built set of tools that let's you do powerful things quickly without having to reinvent the wheel.

*   add the following lines to your file to open a web page and download it's contents:

`r = requests.get('https://en.wikipedia.org/wiki/Resume_screening')`

That will grab the [resume screening](https://en.wikipedia.org/wiki/Resume_screening) page of [wikipedia.org](http://wikipedia.org) and return the entire HTML file as a requests object under the variable name _request_. If we try to print the content of _request_ we simply get `<Response [200]>` This is the way that Python stores the data we just grabbed. If you had this object in a terminal window you could type `request.content` and you'd print the entire contents of the response object (a bunch of HTML in this case. For this project we'd like to parse the data. In order to do that we'd like to use another library. Go back to your code and amend the file as follows:

```import requests
from bs4 import BeautifulSoup
```

This will import the BeautifulSoup library which will parse the request object so that we can work with it more easily, and with more precision. Next add the following lines to your program:

```r = r.content
soup = BeautifulSoup(request, 'html.parser')
```

The first line converts the request object into a bytes object. The bytes object is then parsed by BeautifulSoup allowing more control and precision when working with the data. For example in order to grab the title of the Wikipedia home page we would simple use the command `soup.title`. As we are interested in grabbing all the text content from the paragraphs (and none of the HTML/CSS/etc.) we will have to add the following to our program:

paragraphs

```paragraphs = soup.find_all('p')
all_words = ''
```

This will take all of the paragraphs and return them to us as a BeautifulSoup return object. The next line will create an empty string, which we will use to store all the words we extract from the paragraphs using the following:

```for paragraph in paragraphs:
    all_words += str(paragraph.text)
```

Next we split the giant string of words into a list of individual words:

```all_words = all_words.split(' ')
```

Now all we have to do is import our last library

```from Collections import counter
```

This library will allow us to quickly and easily take our list of words, and tally up the frequency of each word in the list as follows:

```frequency = Counter(all_words)
```

In order to retrieve the 10 most common words we simply make a slight modification:

```frequency = Counter(all_words).most_common(10)
```

If we print frequency we get

```[('the', 56), ('of', 39), ('to', 26), ('a', 26), ('job', 18), ('and', 17), ('are', 15), ('is', 12), ('candidates', 11), ('for', 9)]
```

Let's make the data more presentable

```for word in frequency:
    print('{:<20}{:<4}'.format(a[0],a[1]))
```

Our final output will look like:

```the                 56
of                  39
to                  26
a                   26
job                 18
and                 17
are                 15
is                  12
candidates          11
for                 9
```

The completed project should resemble that found below

```import requests
from bs4 import BeautifulSoup
from collections import Counter

r = requests.get('https://en.wikipedia.org/wiki/Resume_screening')
r = r.content
soup = BeautifulSoup(request, 'html.parser')
paragraphs = soup.find_all('p')
all_words = ''
for paragraph in paragraphs:
    all_words += str(paragraph.text)
all_words = all_words.split(' ')
frequency = Counter(all_words).most_common(10)
for word in frequency:
    print('{:<20}{:<4}'.format(a[0],a[1]))</pre>
```

So in about 14 lines of code we wrote a little program that will:

*   grab a web page from the internet
*   extract words from all paragraphs
*   present a report featuring the 10 most common words and their frequency

# Challenge!

In order to make this program more useful figure out a way to ignore stop-words. These are words like _at_, _the_, and _it_ that provide little of value to a data analyst. Remove those words from the frequency calculation and present the new top 10 words.

If you succeed in doing that, your next challenge will be to rewrite the program (using the same dependencies (libraries) as above) but with fewer lines of code.

Next week, I will release Project #2 Data Scraping and Analysis App. We will learn how to take what we learned today and combine it with the Bottle.py web development framework to create a really simple (but fully functional) web application.

### If you have feedback for me regarding this project or have other questions for me you can find me on Twitter: [@Skilenstein](https://twitter.com/Skilenstein)
