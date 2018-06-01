
# Weather in relation to closeness to the Ecuator
-  It is important to note that there is a very important factor affecting the max temperature graph: It is currently summer north of the ecuator and winter south of the Ecuator. That explains the higher temperature concentrated on the right side. However, we can still notice the 'n' shape that we would expect, indicating that temperatures are indeed higher close to the Ecuator.
-  It is also important to take into consideration that population density is greater north of the Ecuator. Therefore, there are is a greater concentration of markers on the right side of all th graphs.
- There is no noticeable correlation between cloudiness and latitutde. We would probably have to analyze cloudiness in relation to closeness to the coast and mountanious areas.


```python
# Dependencies
import json
import requests
import random
import csv
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import openweathermapy.core as owm
from pprint import pprint
from config import api_key
from citipy import citipy
```

# Generate Cities List


```python
# Turn citipy data into data frame for easier utilization
df = pd.read_csv("worldcities.csv")

# Pull a sample of 620 random cities
cities = random.sample(list(df["City"]),620)
```

# Perform API Calls


```python
# Base url
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "Imperial"
query_url = f"{url}units={units}&appid={api_key}&q="
cloud = []
country = []
date = []
humidity = []
lat = []
lon = []
max_tem =[]
wind = []
weather_data = []
cities_found = []
count = 0
settings = {"units": units, "appid": api_key}
```


```python
print("Beginning Data Retrieval")
print("-"*50)

for city in cities:
    try:
        city = city.replace(" ", "%20")
        city_url = query_url + city
        response = requests.get(city_url).json()
        count = count + 1
        print(f"Processing Record of city #{count}")
        print(city_url)
        lat.append(response['coord']['lat'])
        cloud.append(response['clouds']['all'])
        country.append(response['sys']['country'])
        date.append(response['dt'])
        humidity.append(response['main']['humidity'])
        lon.append(response['coord']['lon'])
        max_tem.append(response['main']['temp_max'])
        wind.append(response['wind']['speed'])
        cities_found.append(response['name'])
        #weather_data = [owm.get_current(city,**settings)]
        
    except:
        continue
print("-"*50)
print("Data Retrieval Complete")
print("-"*50)   
```

    Beginning Data Retrieval
    --------------------------------------------------
    Processing Record of city #1
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=darmanesti
    Processing Record of city #2
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hienghene
    Processing Record of city #3
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20jose%20de%20rio%20tinto
    Processing Record of city #4
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=south%20lyon
    Processing Record of city #5
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vammala
    Processing Record of city #6
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=goa
    Processing Record of city #7
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fraijanes
    Processing Record of city #8
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cuautitlan%20izcalli
    Processing Record of city #9
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mayskiy
    Processing Record of city #10
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=khrisokhorafa
    Processing Record of city #11
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=megala%20kalivia
    Processing Record of city #12
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=moshenskoye
    Processing Record of city #13
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=darabani
    Processing Record of city #14
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=xichang
    Processing Record of city #15
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=livezile
    Processing Record of city #16
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=prunisor
    Processing Record of city #17
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=guaitarilla
    Processing Record of city #18
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=novosedlice
    Processing Record of city #19
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lanaken
    Processing Record of city #20
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zilupe
    Processing Record of city #21
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kinalansan
    Processing Record of city #22
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=asifabad
    Processing Record of city #23
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mavur
    Processing Record of city #24
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tangermunde
    Processing Record of city #25
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chotebor
    Processing Record of city #26
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dambulla
    Processing Record of city #27
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=platikambos
    Processing Record of city #28
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chandler
    Processing Record of city #29
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=raxaul
    Processing Record of city #30
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=masaki
    Processing Record of city #31
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tamiami
    Processing Record of city #32
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=porto%20alegre
    Processing Record of city #33
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=plopii%20slavitesti
    Processing Record of city #34
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20matias
    Processing Record of city #35
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=indaial
    Processing Record of city #36
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=recas
    Processing Record of city #37
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=krasnyy%20yar
    Processing Record of city #38
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bajah
    Processing Record of city #39
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=botolan
    Processing Record of city #40
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=akom
    Processing Record of city #41
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=houlung
    Processing Record of city #42
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=saint%20louis%20park
    Processing Record of city #43
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tabontabon
    Processing Record of city #44
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dunavecse
    Processing Record of city #45
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=makiling
    Processing Record of city #46
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=morales
    Processing Record of city #47
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ano%20mera
    Processing Record of city #48
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gmunden
    Processing Record of city #49
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lodja
    Processing Record of city #50
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bougouni
    Processing Record of city #51
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=basiad
    Processing Record of city #52
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=polonnaruwa
    Processing Record of city #53
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tandahimba
    Processing Record of city #54
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=town%20and%20country
    Processing Record of city #55
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=aroysund
    Processing Record of city #56
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=workington
    Processing Record of city #57
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=monchique
    Processing Record of city #58
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shetpe
    Processing Record of city #59
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sinilian
    Processing Record of city #60
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=candelaria
    Processing Record of city #61
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chene-bougeries
    Processing Record of city #62
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=viadana
    Processing Record of city #63
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=la%20tebaida
    Processing Record of city #64
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=girov
    Processing Record of city #65
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mobo
    Processing Record of city #66
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=popesti
    Processing Record of city #67
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=balili
    Processing Record of city #68
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kildare
    Processing Record of city #69
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20nicolas
    Processing Record of city #70
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lawang%20kupang
    Processing Record of city #71
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=paiporta
    Processing Record of city #72
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pomi
    Processing Record of city #73
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=neuville-en-ferrain
    Processing Record of city #74
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=upig
    Processing Record of city #75
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=biga
    Processing Record of city #76
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kapuvar
    Processing Record of city #77
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cataingan
    Processing Record of city #78
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sinaia
    Processing Record of city #79
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=brovary
    Processing Record of city #80
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=barawe
    Processing Record of city #81
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ascension
    Processing Record of city #82
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vamberk
    Processing Record of city #83
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=svit
    Processing Record of city #84
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mulheim-karlich
    Processing Record of city #85
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=calmatuiu
    Processing Record of city #86
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=batasan
    Processing Record of city #87
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=copandaro
    Processing Record of city #88
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bungahan
    Processing Record of city #89
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=araruama
    Processing Record of city #90
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nyzhni%20petrivtsi
    Processing Record of city #91
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nepomuceno
    Processing Record of city #92
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chichi
    Processing Record of city #93
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ramgarh
    Processing Record of city #94
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=villorba
    Processing Record of city #95
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tananger
    Processing Record of city #96
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=taungdwingyi
    Processing Record of city #97
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bela%20cruz
    Processing Record of city #98
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gulod
    Processing Record of city #99
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tarqui
    Processing Record of city #100
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=yuzhou
    Processing Record of city #101
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sebrovo
    Processing Record of city #102
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vytegra
    Processing Record of city #103
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kostolac
    Processing Record of city #104
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=albury
    Processing Record of city #105
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=washington
    Processing Record of city #106
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kagalnik
    Processing Record of city #107
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ustek
    Processing Record of city #108
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lysva
    Processing Record of city #109
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=verl
    Processing Record of city #110
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=podlesnoye
    Processing Record of city #111
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=neftekumsk
    Processing Record of city #112
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=soponya
    Processing Record of city #113
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=destin
    Processing Record of city #114
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=iowa%20city
    Processing Record of city #115
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cabanas
    Processing Record of city #116
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=maricaban
    Processing Record of city #117
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=teitipac
    Processing Record of city #118
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=palhi
    Processing Record of city #119
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nagato
    Processing Record of city #120
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=doembang%20nangbuat
    Processing Record of city #121
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=peterborough
    Processing Record of city #122
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=miglamin
    Processing Record of city #123
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rasra
    Processing Record of city #124
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cluses
    Processing Record of city #125
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=abinsk
    Processing Record of city #126
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=thompson
    Processing Record of city #127
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=basseterre
    Processing Record of city #128
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kilcullen
    Processing Record of city #129
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fiesole
    Processing Record of city #130
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bolcske
    Processing Record of city #131
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=novovyazniki
    Processing Record of city #132
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=caudry
    Processing Record of city #133
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shiggaon
    Processing Record of city #134
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=astros
    Processing Record of city #135
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=morant%20bay
    Processing Record of city #136
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=krasnoye
    Processing Record of city #137
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=karasuk
    Processing Record of city #138
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=glenview
    Processing Record of city #139
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=janja
    Processing Record of city #140
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=palmeirais
    Processing Record of city #141
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=makarska
    Processing Record of city #142
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bang%20rakam
    Processing Record of city #143
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jiangyin
    Processing Record of city #144
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tooele
    Processing Record of city #145
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=elgin
    Processing Record of city #146
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=glenvar%20heights
    Processing Record of city #147
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=seraing
    Processing Record of city #148
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rishikesh
    Processing Record of city #149
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=can
    Processing Record of city #150
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=malegaon
    Processing Record of city #151
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kannur
    Processing Record of city #152
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=invercargill
    Processing Record of city #153
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kodala
    Processing Record of city #154
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=narwana
    Processing Record of city #155
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=karakulino
    Processing Record of city #156
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dno
    Processing Record of city #157
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=macatbong
    Processing Record of city #158
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mandsaur
    Processing Record of city #159
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=calarasi
    Processing Record of city #160
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=esil
    Processing Record of city #161
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rudiskes
    Processing Record of city #162
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=salcininkai
    Processing Record of city #163
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=surat
    Processing Record of city #164
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=manaure
    Processing Record of city #165
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=aros
    Processing Record of city #166
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=greenlaw
    Processing Record of city #167
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=albanel
    Processing Record of city #168
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sabang
    Processing Record of city #169
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gali
    Processing Record of city #170
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fredonia
    Processing Record of city #171
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=corlu
    Processing Record of city #172
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=devyatka
    Processing Record of city #173
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=puliyur
    Processing Record of city #174
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=weymouth
    Processing Record of city #175
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=viersen
    Processing Record of city #176
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zhumadian
    Processing Record of city #177
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=getulio
    Processing Record of city #178
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gotemba
    Processing Record of city #179
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bollene
    Processing Record of city #180
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vokhtoga
    Processing Record of city #181
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=somes-odorhei
    Processing Record of city #182
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=newark
    Processing Record of city #183
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=xalpa
    Processing Record of city #184
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hernadnemeti
    Processing Record of city #185
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=alford
    Processing Record of city #186
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=white%20oak
    Processing Record of city #187
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bad%20durrheim
    Processing Record of city #188
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=prenza
    Processing Record of city #189
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bahjoi
    Processing Record of city #190
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=la%20concepcion
    Processing Record of city #191
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bakel
    Processing Record of city #192
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cabuyaro
    Processing Record of city #193
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cachoeiro%20de%20itapemirim
    Processing Record of city #194
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=utraula
    Processing Record of city #195
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bucov
    Processing Record of city #196
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=amersfoort
    Processing Record of city #197
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=matiompong
    Processing Record of city #198
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=boxtel
    Processing Record of city #199
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gastonia
    Processing Record of city #200
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20pedro%20del%20pinatar
    Processing Record of city #201
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lavumisa
    Processing Record of city #202
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mange
    Processing Record of city #203
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fulopszallas
    Processing Record of city #204
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pacos%20de%20brandao
    Processing Record of city #205
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zumarraga
    Processing Record of city #206
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=brumadinho
    Processing Record of city #207
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=deulgaon%20raja
    Processing Record of city #208
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pumiao
    Processing Record of city #209
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nejdek
    Processing Record of city #210
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tiquicheo
    Processing Record of city #211
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pag-asa
    Processing Record of city #212
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mikonos
    Processing Record of city #213
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=popova
    Processing Record of city #214
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pottsville
    Processing Record of city #215
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rayon
    Processing Record of city #216
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=clayton
    Processing Record of city #217
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=merritt%20island
    Processing Record of city #218
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=joigny
    Processing Record of city #219
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=miyata
    Processing Record of city #220
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=trondheim
    Processing Record of city #221
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ahmadpur
    Processing Record of city #222
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=erwitte
    Processing Record of city #223
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=yenagoa
    Processing Record of city #224
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nikolayevka
    Processing Record of city #225
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gavardo
    Processing Record of city #226
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=unity
    Processing Record of city #227
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=balogo
    Processing Record of city #228
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=karcag
    Processing Record of city #229
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=komarovo
    Processing Record of city #230
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sirsaganj
    Processing Record of city #231
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nedryhayliv
    Processing Record of city #232
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=asheboro
    Processing Record of city #233
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=balinsasayao
    Processing Record of city #234
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=titagarh
    Processing Record of city #235
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=trinidad
    Processing Record of city #236
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=istres
    Processing Record of city #237
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=heythuysen
    Processing Record of city #238
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=coite%20do%20noia
    Processing Record of city #239
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=viline
    Processing Record of city #240
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=geraldton
    Processing Record of city #241
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=akhtanizovskaya
    Processing Record of city #242
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=delaware
    Processing Record of city #243
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=maxingal
    Processing Record of city #244
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=martano
    Processing Record of city #245
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=waounde
    Processing Record of city #246
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jork
    Processing Record of city #247
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nyalikungu
    Processing Record of city #248
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=maracacume
    Processing Record of city #249
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bosanski%20novi
    Processing Record of city #250
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sao%20joao%20de%20ver
    Processing Record of city #251
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lichinga
    Processing Record of city #252
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bassersdorf
    Processing Record of city #253
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=urazovo
    Processing Record of city #254
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=volax
    Processing Record of city #255
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=steubenville
    Processing Record of city #256
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hamilton
    Processing Record of city #257
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=aykhal
    Processing Record of city #258
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jenbach
    Processing Record of city #259
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=aranos
    Processing Record of city #260
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=calapi
    Processing Record of city #261
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=arevik
    Processing Record of city #262
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bayanga
    Processing Record of city #263
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gornesti
    Processing Record of city #264
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jiuquan
    Processing Record of city #265
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=betulia
    Processing Record of city #266
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=brejning
    Processing Record of city #267
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sarasota
    Processing Record of city #268
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=svetlyy
    Processing Record of city #269
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ust-koksa
    Processing Record of city #270
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=narino
    Processing Record of city #271
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sehnde
    Processing Record of city #272
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=la%20ermita
    Processing Record of city #273
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tharad
    Processing Record of city #274
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nyircsaholy
    Processing Record of city #275
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=volovat
    Processing Record of city #276
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=campos%20gerais
    Processing Record of city #277
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tiruppur
    Processing Record of city #278
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=plesna
    Processing Record of city #279
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=romanshorn
    Processing Record of city #280
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=prochnookopskaya
    Processing Record of city #281
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=palm%20beach
    Processing Record of city #282
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nioaque
    Processing Record of city #283
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kranuan
    Processing Record of city #284
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=conselheiro%20lafaiete
    Processing Record of city #285
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=machico
    Processing Record of city #286
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=qadirpur%20ran
    Processing Record of city #287
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=socorro
    Processing Record of city #288
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=danlugan
    Processing Record of city #289
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=valea%20argovei
    Processing Record of city #290
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bagnes
    Processing Record of city #291
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ubaque
    Processing Record of city #292
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ermont
    Processing Record of city #293
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=westlake
    Processing Record of city #294
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=amatitlan
    Processing Record of city #295
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=idio
    Processing Record of city #296
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kegayli
    Processing Record of city #297
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=botad
    Processing Record of city #298
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=razam
    Processing Record of city #299
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=terrassa
    Processing Record of city #300
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chesterfield
    Processing Record of city #301
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kissamos
    Processing Record of city #302
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=haan
    Processing Record of city #303
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=beernem
    Processing Record of city #304
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=idah
    Processing Record of city #305
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ketsch
    Processing Record of city #306
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=athlone
    Processing Record of city #307
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shaunavon
    Processing Record of city #308
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mehkerek
    Processing Record of city #309
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=maimbung
    Processing Record of city #310
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chaves
    Processing Record of city #311
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=westerly
    Processing Record of city #312
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=balingcanaway
    Processing Record of city #313
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=punang
    Processing Record of city #314
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=waggaman
    Processing Record of city #315
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=madrid
    Processing Record of city #316
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=evinayong
    Processing Record of city #317
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=leichlingen
    Processing Record of city #318
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tulua
    Processing Record of city #319
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bjornevatn
    Processing Record of city #320
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=busko-zdroj
    Processing Record of city #321
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gekhi
    Processing Record of city #322
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pines
    Processing Record of city #323
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cary
    Processing Record of city #324
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hamilton
    Processing Record of city #325
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=balete
    Processing Record of city #326
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=maplewood
    Processing Record of city #327
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=leominster
    Processing Record of city #328
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=firminy
    Processing Record of city #329
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zaliztsi
    Processing Record of city #330
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=el%20progreso
    Processing Record of city #331
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=karwar
    Processing Record of city #332
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=leninsk
    Processing Record of city #333
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tanjong%20tokong
    Processing Record of city #334
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pundaguitan
    Processing Record of city #335
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=farah
    Processing Record of city #336
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=branesti
    Processing Record of city #337
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=apia
    Processing Record of city #338
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zabbar
    Processing Record of city #339
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=newark
    Processing Record of city #340
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=orneta
    Processing Record of city #341
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=indang
    Processing Record of city #342
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=wiener%20neustadt
    Processing Record of city #343
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=roldanillo
    Processing Record of city #344
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rio%20grande%20city
    Processing Record of city #345
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lahan
    Processing Record of city #346
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jizan
    Processing Record of city #347
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nkayi
    Processing Record of city #348
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=springdale
    Processing Record of city #349
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=siilinjarvi
    Processing Record of city #350
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vaikam
    Processing Record of city #351
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hjortshoj
    Processing Record of city #352
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ramsey
    Processing Record of city #353
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=skofljica
    Processing Record of city #354
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=asamankese
    Processing Record of city #355
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tibagon
    Processing Record of city #356
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=betafo
    Processing Record of city #357
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=doncaster
    Processing Record of city #358
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=charter%20oak
    Processing Record of city #359
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=krosno
    Processing Record of city #360
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=quime
    Processing Record of city #361
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kuchurhan
    Processing Record of city #362
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=surendranagar
    Processing Record of city #363
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ilava
    Processing Record of city #364
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=marhaura
    Processing Record of city #365
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=novomikhaylovskiy
    Processing Record of city #366
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=riachao%20do%20jacuipe
    Processing Record of city #367
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mokrous
    Processing Record of city #368
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=horqueta
    Processing Record of city #369
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chimoio
    Processing Record of city #370
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=abraveses
    Processing Record of city #371
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sultanpur
    Processing Record of city #372
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=krasna
    Processing Record of city #373
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=belgaum
    Processing Record of city #374
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kibiti
    Processing Record of city #375
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sieut
    Processing Record of city #376
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=embu
    Processing Record of city #377
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=khandela
    Processing Record of city #378
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=blieskastel
    Processing Record of city #379
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=banos
    Processing Record of city #380
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=caminawit
    Processing Record of city #381
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=the%20hammocks
    Processing Record of city #382
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=csenger
    Processing Record of city #383
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sumatac
    Processing Record of city #384
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gosforth
    Processing Record of city #385
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=prigorodnyy
    Processing Record of city #386
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cocobeach
    Processing Record of city #387
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nucsoara
    Processing Record of city #388
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=langenzersdorf
    Processing Record of city #389
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=witu
    Processing Record of city #390
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tomislavgrad
    Processing Record of city #391
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=novi
    Processing Record of city #392
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nizhniy%20kislyay
    Processing Record of city #393
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bijapur
    Processing Record of city #394
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=grdelica
    Processing Record of city #395
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shostka
    Processing Record of city #396
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=guanay
    Processing Record of city #397
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rovereto
    Processing Record of city #398
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=grindavik
    Processing Record of city #399
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=duekoue
    Processing Record of city #400
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=svarychiv
    Processing Record of city #401
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=caratinga
    Processing Record of city #402
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shaoguan
    Processing Record of city #403
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=idar
    Processing Record of city #404
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=marabba
    Processing Record of city #405
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20vicente
    Processing Record of city #406
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sharya
    Processing Record of city #407
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=konstantinovskiy
    Processing Record of city #408
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chochkan
    Processing Record of city #409
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cosoveni
    Processing Record of city #410
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=staryy%20biser
    Processing Record of city #411
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=suditi
    Processing Record of city #412
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rumes
    Processing Record of city #413
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=qiryat%20yam
    Processing Record of city #414
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=saint-gabriel
    Processing Record of city #415
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=manamadurai
    Processing Record of city #416
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=warren
    Processing Record of city #417
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=garmsar
    Processing Record of city #418
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shorkot
    Processing Record of city #419
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=burla
    Processing Record of city #420
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=luzilandia
    Processing Record of city #421
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=todiresti
    Processing Record of city #422
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=thies
    Processing Record of city #423
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20salvo
    Processing Record of city #424
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pailon
    Processing Record of city #425
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hosingen
    Processing Record of city #426
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=teror
    Processing Record of city #427
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=castle%20douglas
    Processing Record of city #428
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ojitlan
    Processing Record of city #429
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=manaring
    Processing Record of city #430
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=slavuta
    Processing Record of city #431
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=iaciara
    Processing Record of city #432
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fleury-merogis
    Processing Record of city #433
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=axixa%20do%20tocantins
    Processing Record of city #434
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=puerto%20berrio
    Processing Record of city #435
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kimberley
    Processing Record of city #436
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=oxilithos
    Processing Record of city #437
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=el%20banco
    Processing Record of city #438
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=acaxochitlan
    Processing Record of city #439
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=soyapango
    Processing Record of city #440
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=baindur
    Processing Record of city #441
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=turzovka
    Processing Record of city #442
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kajaani
    Processing Record of city #443
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=quintong
    Processing Record of city #444
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tarn%20taran
    Processing Record of city #445
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kaita
    Processing Record of city #446
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=romita
    Processing Record of city #447
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=forth
    Processing Record of city #448
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cartago
    Processing Record of city #449
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sibi
    Processing Record of city #450
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=littleton
    Processing Record of city #451
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=moinesti
    Processing Record of city #452
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gemena
    Processing Record of city #453
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=norden
    Processing Record of city #454
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=norheimsund
    Processing Record of city #455
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=turek
    Processing Record of city #456
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sayansk
    Processing Record of city #457
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=yiyang
    Processing Record of city #458
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=norfolk
    Processing Record of city #459
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jerantut
    Processing Record of city #460
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=niugan
    Processing Record of city #461
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=samalaeulu
    Processing Record of city #462
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=billerica
    Processing Record of city #463
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nuh
    Processing Record of city #464
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hajdudorog
    Processing Record of city #465
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=woonsocket
    Processing Record of city #466
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=narathiwat
    Processing Record of city #467
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=haskovo
    Processing Record of city #468
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chengzihe
    Processing Record of city #469
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kolosovka
    Processing Record of city #470
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kalach-na-donu
    Processing Record of city #471
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=velden%20am%20worthersee
    Processing Record of city #472
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=baraolt
    Processing Record of city #473
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=velesin
    Processing Record of city #474
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=brodek%20u%20prerova
    Processing Record of city #475
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=livadiya
    Processing Record of city #476
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=anekal
    Processing Record of city #477
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tingambato
    Processing Record of city #478
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=jyderup
    Processing Record of city #479
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=uplawmoor
    Processing Record of city #480
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zarand
    Processing Record of city #481
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=clausthal-zellerfeld
    Processing Record of city #482
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=madhupur
    Processing Record of city #483
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=manati
    Processing Record of city #484
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tamayo
    Processing Record of city #485
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=timiryazevskoye
    Processing Record of city #486
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=deqing
    Processing Record of city #487
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kiwira
    Processing Record of city #488
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vyshhorod
    Processing Record of city #489
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=halmstad
    Processing Record of city #490
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=schaffhausen
    Processing Record of city #491
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cacota
    Processing Record of city #492
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=barra%20velha
    Processing Record of city #493
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=vijayapuri
    Processing Record of city #494
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lighthouse%20point
    Processing Record of city #495
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ticuantepe
    Processing Record of city #496
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=santiago
    Processing Record of city #497
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nejapa
    Processing Record of city #498
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=melzo
    Processing Record of city #499
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mozirje
    Processing Record of city #500
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pawa
    Processing Record of city #501
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bree
    Processing Record of city #502
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=gostyn
    Processing Record of city #503
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=college%20place
    Processing Record of city #504
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nea%20peramos
    Processing Record of city #505
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=harseni
    Processing Record of city #506
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=atri
    Processing Record of city #507
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tucano
    Processing Record of city #508
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rende
    Processing Record of city #509
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=sagurong
    Processing Record of city #510
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pasching
    Processing Record of city #511
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=biberach
    Processing Record of city #512
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tremembe
    Processing Record of city #513
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=woodway
    Processing Record of city #514
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zaqatala
    Processing Record of city #515
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=roding
    Processing Record of city #516
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ulverstone
    Processing Record of city #517
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=erkelenz
    Processing Record of city #518
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=santa%20ana
    Processing Record of city #519
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kiknur
    Processing Record of city #520
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tomohon
    Processing Record of city #521
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nocupetaro
    Processing Record of city #522
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=cajititlan
    Processing Record of city #523
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=muskegon%20heights
    Processing Record of city #524
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chiapa
    Processing Record of city #525
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lipova
    Processing Record of city #526
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dudesti
    Processing Record of city #527
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=predivinsk
    Processing Record of city #528
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dumarais
    Processing Record of city #529
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=valletta
    Processing Record of city #530
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mehndawal
    Processing Record of city #531
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lordelo
    Processing Record of city #532
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=petrovice%20u%20karvine
    Processing Record of city #533
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=imeni%20zhelyabova
    Processing Record of city #534
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=el%20rosario
    Processing Record of city #535
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=siraha
    Processing Record of city #536
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=laplace
    Processing Record of city #537
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=shasta%20lake
    Processing Record of city #538
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20joaquin
    Processing Record of city #539
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=oud-beijerland
    Processing Record of city #540
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=zheleznodorozhnyy
    Processing Record of city #541
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lhokseumawe
    Processing Record of city #542
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=juru
    Processing Record of city #543
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=general%20roca
    Processing Record of city #544
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mallig
    Processing Record of city #545
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=matanza
    Processing Record of city #546
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chegutu
    Processing Record of city #547
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=upper%20arlington
    Processing Record of city #548
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mazara%20del%20vallo
    Processing Record of city #549
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ghauspur
    Processing Record of city #550
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nove%20mesto%20pod%20smrkem
    Processing Record of city #551
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20simon
    Processing Record of city #552
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lainate
    Processing Record of city #553
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=santa%20maria
    Processing Record of city #554
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=juniyah
    Processing Record of city #555
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kurganinsk
    Processing Record of city #556
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=voula
    Processing Record of city #557
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bad%20sankt%20leonhard
    Processing Record of city #558
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bogoroditsk
    Processing Record of city #559
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=batas
    Processing Record of city #560
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rio%20de%20mouro
    Processing Record of city #561
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=abapo
    Processing Record of city #562
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mayya
    Processing Record of city #563
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=suchiapa
    Processing Record of city #564
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=glomfjord
    Processing Record of city #565
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=lampa
    Processing Record of city #566
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=byureghavan
    Processing Record of city #567
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pellerd
    Processing Record of city #568
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kladovo
    Processing Record of city #569
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=oxford
    Processing Record of city #570
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=krasnovka
    Processing Record of city #571
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ano%20siros
    Processing Record of city #572
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=banjaran
    Processing Record of city #573
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=szada
    Processing Record of city #574
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=odawara
    Processing Record of city #575
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=biberist
    Processing Record of city #576
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=helmsdale
    Processing Record of city #577
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=luzzi
    Processing Record of city #578
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=aalsmeer
    Processing Record of city #579
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nioki
    Processing Record of city #580
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=dagami
    Processing Record of city #581
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pottstown
    Processing Record of city #582
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=verbilki
    Processing Record of city #583
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=san%20diego
    Processing Record of city #584
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=pellezzano
    Processing Record of city #585
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=spa
    Processing Record of city #586
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kranjska%20gora
    Processing Record of city #587
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=leshukonskoye
    Processing Record of city #588
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tagab
    Processing Record of city #589
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tataranu
    Processing Record of city #590
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=belo%20jardim
    Processing Record of city #591
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=akhalgori
    Processing Record of city #592
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=rastede
    Processing Record of city #593
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ikon-khalk
    Processing Record of city #594
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bunnik
    Processing Record of city #595
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=islamkot
    Processing Record of city #596
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=nagyrede
    Processing Record of city #597
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=la%20celia
    Processing Record of city #598
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=snizhne
    Processing Record of city #599
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=viby
    Processing Record of city #600
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=constitucion
    Processing Record of city #601
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=oria
    Processing Record of city #602
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=north%20olmsted
    Processing Record of city #603
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=puck
    Processing Record of city #604
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=khatassy
    Processing Record of city #605
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=huite
    Processing Record of city #606
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=tuy
    Processing Record of city #607
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mae%20chan
    Processing Record of city #608
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=bulod
    Processing Record of city #609
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=stroesti
    Processing Record of city #610
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=ramnagar
    Processing Record of city #611
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=kariapatti
    Processing Record of city #612
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=albestii-pamanteni
    Processing Record of city #613
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=charsadda
    Processing Record of city #614
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=chamonix-mont-blanc
    Processing Record of city #615
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=khurai
    Processing Record of city #616
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=casiguran
    Processing Record of city #617
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=fujinomiya
    Processing Record of city #618
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=xapuri
    Processing Record of city #619
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=mosina
    Processing Record of city #620
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=d9b061a6efeb326320550b5951c4aeee&q=hajdunanas
    --------------------------------------------------
    Data Retrieval Complete
    --------------------------------------------------
    


```python
cities_df = pd.DataFrame({"City": cities_found,
                          "Cloudiness": cloud,
                         "Country": country,
                         "Date": date,
                         "Humidity": humidity,
                         "Latitude": lat,
                         "Longitude": lon,
                         "Max Temperature": max_tem,
                         "Wind Speed": wind})
cities_df.count()
```




    City               591
    Cloudiness         591
    Country            591
    Date               591
    Humidity           591
    Latitude           591
    Longitude          591
    Max Temperature    591
    Wind Speed         591
    dtype: int64




```python
# Save the data frame
cities_df.to_csv("cities_output.csv", index=False, header=True)
# Display the City Data Frame
cities_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Max Temperature</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Darmanesti</td>
      <td>0</td>
      <td>RO</td>
      <td>1527823800</td>
      <td>63</td>
      <td>46.37</td>
      <td>26.48</td>
      <td>60.80</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hienghene</td>
      <td>0</td>
      <td>NC</td>
      <td>1527825341</td>
      <td>100</td>
      <td>-20.68</td>
      <td>164.93</td>
      <td>74.63</td>
      <td>1.59</td>
    </tr>
    <tr>
      <th>2</th>
      <td>San Jose de Rio Tinto</td>
      <td>40</td>
      <td>HN</td>
      <td>1527822000</td>
      <td>88</td>
      <td>14.93</td>
      <td>-85.70</td>
      <td>78.80</td>
      <td>4.70</td>
    </tr>
    <tr>
      <th>3</th>
      <td>South Lyon</td>
      <td>90</td>
      <td>US</td>
      <td>1527824700</td>
      <td>61</td>
      <td>42.45</td>
      <td>-83.66</td>
      <td>78.80</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Vammala</td>
      <td>0</td>
      <td>FI</td>
      <td>1527823200</td>
      <td>66</td>
      <td>61.34</td>
      <td>22.91</td>
      <td>50.00</td>
      <td>4.70</td>
    </tr>
  </tbody>
</table>
</div>



# Latitude vs Temperature Plot


```python
# Plot
plt.scatter(lat,max_tem,marker="o",facecolors="blue",edgecolors="black")
plt.ylim(0,140)
plt.xlim(-60,80)
plt.title("City Latitude vs. Max Temperature (05/31/18)")
plt.xlabel("Latitude")
plt.ylabel("Max Temperature (F)")
plt.grid()
plt.savefig("temp.png")
plt.show()
```


![png](output_10_0.png)


# Latitude vs Humidity Plot


```python
# Plot
plt.scatter(lat,humidity,marker="o",facecolors="blue",edgecolors="black")
plt.ylim(0,120)
plt.xlim(-60,80)
plt.title("City Latitude vs. Humidity (05/31/18)")
plt.xlabel("Latitude")
plt.ylabel("Humidity (%)")
plt.grid()
plt.savefig("humidity.png")
plt.show()
```


![png](output_12_0.png)


# Latitude vs. Cloudiness Plot


```python
# Plot
plt.scatter(lat,cloud,marker="o",facecolors="blue",edgecolors="black")
plt.ylim(-10,120)
plt.xlim(-60,80)
plt.title("City Latitude vs. Cloudiness (05/31/18)")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness (%)")
plt.grid()
plt.savefig("cloudiness.png")
plt.show()
```


![png](output_14_0.png)


# Latitude vs. Wind Speed Plot


```python
# Plot
plt.scatter(lat,wind,marker="o",facecolors="blue",edgecolors="black")
plt.ylim(0,25)
plt.xlim(-60,80)
plt.title("City Latitude vs. Wind Speed (05/31/18)")
plt.xlabel("Latitude")
plt.ylabel("Cloudiness (mph)")
plt.grid()
plt.savefig("wind_speed.png")
plt.show()
```


![png](output_16_0.png)

