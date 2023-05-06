# Python Webscraping Tutorial

## About
I followed a [video tutorial](https://youtu.be/A1s1aGHoODs)  which implements BeautifulSoup, a Python database based on the foundation of HTML analytics engine, used for extracting, analyzing, and editing information in the document object model (DOM) tree of web pages to collect the data. Specifically, this tutorial uses BeautifulSoup to extract the title and transcript from a text box on this [webpage](https://subslikescript.com/movie/Titanic-120338) and exports the data to a txt file. 

### Installation
Open terminal on your local machine and run the following commands:
```
pip install BeautifulSoup
pip install requests
pip install lxml
```
Now you should have all the packages installed. 

### Script
1. Open up a new Python file in a text editor or IDE of choice. I am using [VSCode](https://code.visualstudio.com/).
2. Import the required libraries for webscraping by including these lines of code at the top of your file:
```
from bs4 import BeautifulSoup
import requests
```
3. Define the URL you want to scrape. We will be scraping the webpage https://subslikescript.com/movie/Titanic-120338. So, our code will look like this: 
```
website = 'https://subslikescript.com/movie/Titanic-120338'
```
4. To request data from the webpage, we need to use the requests() method. Include the following line of code:
```
result = requests.get(website)
```

Store this in a variable called 'content'
```
content = result.text
```

5. Now we will use BeautifulSoup and an HTML parser on the data. 
```
soup = BeautifulSoup(content, "lxml")
```
6. At any point you can print the data using to check the HTML using the following line of code:
```
print(soup.prettify())
```

7. We want to locate the box that contains the title and transcript on the webpage. Thus, we will use the following line of code:
```
box = soup.find('article', class_='main-article')
```
The find() method is used to get one element and the find\_all() method  is used to get all the elements. We used the find() method since there is only one title we want to get. 

The parameters for the find() method are the ID, class name, tag name, CSS Selector, and/or the Xpath. These are found by right clicking the webpage and pressing inspect. The HTML code associated with the content on the webpage appears informing users of the references.

8. Now that we have the text box found we can extract the title and transcript using these lines of code:
```
title = box.find('h1').get_text()
transcript = box.find('div', class_='full-script').get_text(strip=True, separator=' ')
```
The paramters for the find() method are found following the same process as Step 8. 

The parameters for 'get\_text()' are 'strip=True' which deletes spaces at the beginning and ending of the transcript. The other is 'separator=" "' which replaces a new line with a blank space. These are personal preference formatting resources. 

9. Now we can export the data to a new txt file with the following lines of code:
```
with open(f'{title}.txt', 'w', encoding="utf-8") as file:
    file.write(transcript)
```
This creates a new file with the transcript in it called Titanic (1997) - full transcript.txt since that is the title extracted. 
