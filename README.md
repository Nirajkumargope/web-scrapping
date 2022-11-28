# web-scrapping
used flipkart for laptop scrapping

# importing liberaries needed for web scrapping
# request helps to request web for session
# beautiful soup helps to convert text into structured HTMLcode
import requests
from bs4 import BeautifulSoup
import pandas as pd
import csv
# initiating session with help of url then using beautifulsoup to change it into HTML code
url="https://www.flipkart.com/search?q=laptop&sid=6bo%2Cb5g&as=on&as-show=on&otracker=AS_QueryStore_OrganicAutoSuggest_1_6_na_na_na&otracker1=AS_QueryStore_OrganicAutoSuggest_1_6_na_na_na&as-pos=1&as-type=RECENT&suggestionId=laptop%7CLaptops&requestId=7ec220e8-4f02-4150-9e0b-9e90cf692f4b&as-searchtext=laptop"
response = requests.get(url)
htmlcontent = response.content
soup = BeautifulSoup(htmlcontent,"html.parser")
# initializing empty list of different columns to be filled later on
products=[]
prices=[]
ratings=[]
# looping in the Main div tag in order to find other tags inside the tag
for a in soup.findAll('a',href=True, attrs={'class':'_1fQZEK'}):
    name=a.find('div',attrs={'class':'_4rR01T'})
    price=a.find('div',attrs={'class':'_30jeq3 _1_WHN1'})
    rating=a.find('div',attrs={'class':'_3LWZlK'})
    products.append(name.text)
    prices.append(price.text)
    ratings.append(rating.text)
# checking if number of entries are same or not
# it should be same for each initiated array
len(products)
24
len(prices)
24
len(ratings)
24
Creating Dataframe with help of initiated lists previously
table=pd.DataFrame({"PRODUCTS":products,"PRICES":prices,"RATINGS":ratings})
table
PRODUCTS	PRICES	RATINGS
0	Lenovo IdeaPad 3 Chromebook Celeron Dual Core ...	₹16,990	3.5
1	Lenovo IdeaPad 3 CB Celeron Dual Core - (4 GB/...	₹20,990	4
2	ASUS VivoBook 15 (2022) Core i3 10th Gen - (8 ...	₹33,990	4.3
3	ASUS TUF Gaming F15 Core i5 10th Gen - (8 GB/5...	₹54,990	4.4
4	ASUS VivoBook 15 (2022) Core i5 11th Gen - (8 ...	₹48,990	4.3
5	MSI Bravo 15 Ryzen 5 Hexa Core AMD R5-5600H - ...	₹49,990	4.4
6	MSI Core i5 11th Gen - (8 GB/512 GB SSD/Window...	₹55,990	4.5
7	Lenovo IdeaPad Flex 3 Chromebook Celeron Dual ...	₹28,490	3.6
8	RedmiBook Pro Core i3 11th Gen - (8 GB/256 GB ...	₹29,990	4.2
9	APPLE 2020 Macbook Air M1 - (8 GB/256 GB SSD/M...	₹88,990	4.7
10	HP 14s Intel Core i3 11th Gen - (8 GB/512 GB S...	₹41,999	4.2
11	Lenovo IdeaPad 3 Core i3 11th Gen - (8 GB/256 ...	₹37,228	4.2
12	HP Pavilion Ryzen 5 Hexa Core AMD R5-5600H - (...	₹62,990	4.5
13	ASUS ROG Strix G15 Ryzen 7 Octa Core AMD R7-48...	₹87,990	4.6
14	DELL Inspiron Athlon Dual Core 3050U - (8 GB/2...	₹30,929	4.2
15	RedmiBook Pro Core i5 11th Gen - (8 GB/512 GB ...	₹44,990	4.2
16	Lenovo IdeaPad 3 Ryzen 5 Hexa Core 5500U - (8 ...	₹43,018	4.3
17	acer Aspire 7 Ryzen 5 Hexa Core 5500U - (16 GB...	₹53,990	4.5
18	acer Aspire 7 Ryzen 5 Hexa Core AMD R5-5500U -...	₹49,990	4.5
19	MSI Ryzen 7 Octa Core 5700U - (8 GB/512 GB SSD...	₹52,990	4
20	HP Pavilion Ryzen 5 Hexa Core AMD R5-5600H - (...	₹54,990	4.4
21	ASUS Vivobook Pro 15 Ryzen 7 Octa Core AMD R7-...	₹62,990	4.5
22	acer Aspire Ryzen 5 Quad Core 3500U - (8 GB/51...	₹35,990	4.2
23	Lenovo IdeaPad 1 Ryzen 5 Quad Core 3500U - (8 ...	₹39,584	4.2
exporting created data frame in CSV form
table.to_csv("Flipkart_Laptops.csv")
 
