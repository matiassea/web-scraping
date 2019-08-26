## web-scraping

https://www.crummy.com/software/BeautifulSoup/bs4/doc/

https://beautiful-soup-4.readthedocs.io/en/latest/#id17

https://beautiful-soup-4.readthedocs.io/en/latest/


### Cotizador de cervezas de Tottus

```
"""
Created on Tue Aug  6 12:00:53 2019

@author: mvidal2
"""

"""
from bs4 import BeautifulSoup as soup
from urllib.request import urlopen as uReq, Request
from urllib.request import Request,urlopen as uReq

url_beer = 'https://www.tottus.cl/tottus/browse/Cervezas/115.1'
#req=Request(url_beer,headers={"User-Agent":"Mozilla/5.0"})

Revision de codigo
https://beautifier.io/
https://www.npmjs.com/package/http-status-codes
https://realpython.com/python-requests/
https://beautiful-soup-4.readthedocs.io/en/latest/
https://beautiful-soup-4.readthedocs.io/en/latest/#id17
https://www.crummy.com/software/BeautifulSoup/bs4/doc/

"""

import requests
from bs4 import BeautifulSoup as soup
import csv


url_beer = 'https://www.tottus.cl/tottus/browse/Cervezas/115.1'
page_html = requests.get(url_beer).text

# parses html into a soup data structure to traverse html
# as if it were a json data type.

page_soup = soup(page_html,"html.parser")

#print(page_html.status_code)     # To print http response code  
#print(page_html.text)            # To print formatted JSON response 

#Cada container contiene la informacion del producto 
"""
Para revisar los Tags
for tag in page_soup.find_all(True):
    print(tag.name)

"""

"""
#Busqueda por precio
containers2=page_soup.findAll("span",{"class":"active-price"})
print(len(containers2))

#Busqueda por marca
containers3=page_soup.findAll("div",{"class":"title"})
print(len(containers3))
"""

"""
with open('precio.csv','w') as csvFile:
    writer = csv.writer(csvFile)
    for container3 in containers3:
        brand=container3.div.stripped_strings
        writer.writerow(brand)
    for container2 in containers2:
        precio=container2.span.text.strip()
        writer.writerow(precio)
csvFile.close()
"""
#containers=page_soup.findAll("div",{"class":"item-product-caption"})
containers=page_soup.findAll("div",{"class":"caption-bottom-wrapper"})
#buscar un container global que anide a los otros

filename="cerveza.csv"
f=open(filename,"w")
headers="Marca,Precio,Formato\n"
f.write(headers)

for container in containers:
    
    #brand=containers.findAll("div",{"class":"title"})
    #marca=brand[0].div.stripped_strings
    brand=container.div.div.text.strip()
    
    precio=container.find(class_="active-price").span.text.strip().replace('$ ','').replace('.','')
    #precio=containers.findAll("span",{"class":"active-price"})
    #cost=precio[0].span.text.strip()
    formato=container.find(class_="statement").text.replace(',','.')
    
    print("Marca " + brand)
    print("Precio " + precio)
    print("Formato " + formato)
    f.write(brand+","+ precio +","+formato+"\n")

f.close()
"""
Data
https://www.youtube.com/watch?v=XQgXKtPSzUI&t=1463s

"""

```


