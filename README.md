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




### Ejemplo a revisar, consultor del tiempo

https://github.com/KeithGalli/GUI

https://github.com/KeithGalli?tab=repositories

```

import tkinter as tk
import requests

HEIGHT = 500
WIDTH = 600

def test_function(entry):
	print("This is the entry:", entry)

# api.openweathermap.org/data/2.5/forecast?q={city name},{country code}
# a4aa5e3d83ffefaba8c00284de6ef7c3

def format_response(weather):
	try:
		name = weather['name']
		desc = weather['weather'][0]['description']
		temp = weather['main']['temp']

		final_str = 'City: %s \nConditions: %s \nTemperature (°F): %s' % (name, desc, temp)
	except:
		final_str = 'There was a problem retrieving that information'

	return final_str

def get_weather(city):
	weather_key = 'a4aa5e3d83ffefaba8c00284de6ef7c3'
	url = 'https://api.openweathermap.org/data/2.5/weather'
	params = {'APPID': weather_key, 'q': city, 'units': 'imperial'}
	response = requests.get(url, params=params)
	weather = response.json()

	label['text'] = format_response(weather)



root = tk.Tk()

canvas = tk.Canvas(root, height=HEIGHT, width=WIDTH)
canvas.pack()

background_image = tk.PhotoImage(file='landscape.png')
background_label = tk.Label(root, image=background_image)
background_label.place(relwidth=1, relheight=1)

frame = tk.Frame(root, bg='#80c1ff', bd=5)
frame.place(relx=0.5, rely=0.1, relwidth=0.75, relheight=0.1, anchor='n')

entry = tk.Entry(frame, font=40)
entry.place(relwidth=0.65, relheight=1)

button = tk.Button(frame, text="Get Weather", font=40, command=lambda: get_weather(entry.get()))
button.place(relx=0.7, relheight=1, relwidth=0.3)

lower_frame = tk.Frame(root, bg='#80c1ff', bd=10)
lower_frame.place(relx=0.5, rely=0.25, relwidth=0.75, relheight=0.6, anchor='n')

label = tk.Label(lower_frame)
label.place(relwidth=1, relheight=1)

root.mainloop()

```


