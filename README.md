

```python
import pandas as pd
import json
from config import api_key
import random
import openweathermapy.core as owm
import requests
import matplotlib.pyplot as plt
```


```python
cities = pd.read_csv("cities_list.csv", sep='\t', engine='python', delimiter=',')
cities.head(5)
num_cities = random.sample(range(0, 74072), 500)
lat = []
lng = []
city_name = []
city_id = []
```


```python
for city in num_cities:
    lat.append(cities.iloc[city]['lat'])
    lng.append(cities.iloc[city]['lon'])
    city_name.append(cities.iloc[city]['nm'])
    city_id.append(cities.iloc[city]['id'])
```


```python
weather_dict = {
    "city id": city_id,
    "city": city_name,
    "lat": lat,
    "lng": lng
}

city_data = pd.DataFrame(weather_dict)
city_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>city id</th>
      <th>lat</th>
      <th>lng</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Burbure</td>
      <td>3029548</td>
      <td>50.536629</td>
      <td>2.468970</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bojnice</td>
      <td>3061015</td>
      <td>48.785110</td>
      <td>18.586399</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ilowo -Osada</td>
      <td>7534560</td>
      <td>53.168079</td>
      <td>20.292950</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Santa Cruz del Quiche</td>
      <td>3589404</td>
      <td>15.030560</td>
      <td>-91.148888</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Itatskiy</td>
      <td>1505383</td>
      <td>56.070000</td>
      <td>89.036942</td>
    </tr>
  </tbody>
</table>
</div>




```python
url = "http://api.openweathermap.org/data/2.5/weather?"
units = "imperial"

query_url = f"{url}appid={api_key}&units={units}&id="

temp = []
hum = []
cloudiness = []
windspeed = []

for city in city_id:
        response = requests.get(query_url + str(city)).json()
        hum.append(response['main']['humidity'])
        temp.append(response['main']['temp'])
        cloudiness.append(response['clouds']['all'])
        windspeed.append(response['wind']['speed'])
        print(f"City: {response['name']}. City ID: {city}. Currently being processed at {query_url + str(city)}.")
```

    City: Burbure. City ID: 3029548. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3029548.
    City: Bojnice. City ID: 3061015. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3061015.
    City: Ilowo -Osada. City ID: 7534560. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=7534560.
    City: Santa Cruz del Quiche. City ID: 3589404. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3589404.
    City: Itatskiy. City ID: 1505383. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1505383.
    City: Ponts. City ID: 3113231. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3113231.
    City: Uinskoye. City ID: 479442. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=479442.
    City: San Antonio. City ID: 3670107. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3670107.
    City: Zidlochovice. City ID: 3061472. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3061472.
    City: Chateaubriant. City ID: 3026303. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3026303.
    City: Chester. City ID: 4351248. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4351248.
    City: Dourdan. City ID: 3020925. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3020925.
    City: Porteirinha. City ID: 3452956. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3452956.
    City: Old Harbour Bay. City ID: 3489225. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3489225.
    City: Sankt Wolfgang. City ID: 2841457. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2841457.
    City: Sainte-Therese. City ID: 6138121. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=6138121.
    City: Dragomiresti. City ID: 678924. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=678924.
    City: Maroubra. City ID: 2158651. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2158651.
    City: Yangzhong. City ID: 1787230. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1787230.
    City: Lake Erie Beach. City ID: 5123788. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5123788.
    City: Agios Athanasios. City ID: 736621. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=736621.
    City: Ragay. City ID: 1691941. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1691941.
    City: Jimena de la Frontera. City ID: 2516315. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2516315.
    City: Herouville-Saint-Clair. City ID: 3013403. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3013403.
    City: Celles-sur-Durolle. City ID: 3027988. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3027988.
    City: Sernur. City ID: 496561. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=496561.
    City: Montagnana. City ID: 3173110. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3173110.
    City: Volgograd. City ID: 472757. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=472757.
    City: Masaguisi. City ID: 1700786. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1700786.
    City: Alrewas. City ID: 2657432. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2657432.
    City: Panukulan. City ID: 1694895. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1694895.
    City: Ticala-an. City ID: 1682122. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1682122.
    City: Rheda-Wiedenbruck. City ID: 2847690. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2847690.
    City: Anyama. City ID: 2292852. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2292852.
    City: Rivera. City ID: 3440781. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3440781.
    City: Banks. City ID: 2656388. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2656388.
    City: Beaver Creek. City ID: 5713224. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5713224.
    City: Steenwerck. City ID: 2973821. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2973821.
    City: Namsos. City ID: 3145023. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3145023.
    City: Bagahanlad. City ID: 1729228. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1729228.
    City: Nereju. City ID: 672301. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=672301.
    City: Vizcachane. City ID: 3925955. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3925955.
    City: Catio. City ID: 2373526. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2373526.
    City: Essex. City ID: 4354428. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4354428.
    City: Peranampattu. City ID: 1259892. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1259892.
    City: Druzhinino. City ID: 564878. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=564878.
    City: Szalkszentmarton. City ID: 3044941. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3044941.
    City: Podhom. City ID: 3193011. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3193011.
    City: Warrenton. City ID: 941931. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=941931.
    City: Quitang. City ID: 1691968. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1691968.
    City: Coatbridge. City ID: 2652696. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2652696.
    City: Gorseinon. City ID: 2648290. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2648290.
    City: Lehtimaki. City ID: 648554. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=648554.
    City: Windesheim. City ID: 2808219. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2808219.
    City: Nadezhda. City ID: 523715. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=523715.
    City: Mindyak. City ID: 526489. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=526489.
    City: Park Hills. City ID: 4402479. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4402479.
    City: Cordun. City ID: 680831. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=680831.
    City: San Ciro de Acosta. City ID: 3519570. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3519570.
    City: Bergeyk. City ID: 2759132. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2759132.
    City: La Longueville. City ID: 3008426. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3008426.
    City: Schutterwald. City ID: 2835596. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2835596.
    City: Varkkallai. City ID: 1253392. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1253392.
    City: Itaquaquecetuba. City ID: 3460644. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3460644.
    City: Sura Mare. City ID: 665752. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=665752.
    City: Lunao. City ID: 1705089. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1705089.
    City: Santiago Pinotepa Nacional. City ID: 3516926. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3516926.
    City: Kirkliston. City ID: 2645249. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2645249.
    City: Pohorelice. City ID: 3067953. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3067953.
    City: Sindi. City ID: 1256206. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1256206.
    City: Baishan. City ID: 2038584. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2038584.
    City: Ixtapa. City ID: 4004294. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4004294.
    City: Limours. City ID: 2998269. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2998269.
    City: Helmstedt. City ID: 2906676. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2906676.
    City: Balite. City ID: 1728019. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1728019.
    City: Pignataro Interamna. City ID: 3170719. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3170719.
    City: Summerville. City ID: 4597919. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4597919.
    City: Korgan. City ID: 742658. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=742658.
    City: Sora. City ID: 3166387. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3166387.
    City: Palmito. City ID: 3673143. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3673143.
    City: Nereto. City ID: 3172311. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3172311.
    City: Yavatmal. City ID: 1252770. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1252770.
    City: Moonachie. City ID: 5101376. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5101376.
    City: Moldava nad Bodvou. City ID: 724111. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=724111.
    City: Bokaro. City ID: 1275362. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1275362.
    City: Naduvattam. City ID: 1262284. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1262284.
    City: Ledenice. City ID: 3072234. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3072234.
    City: Pribrezhnyy. City ID: 7117224. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=7117224.
    City: Redziny. City ID: 3087256. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3087256.
    City: Lima Duarte. City ID: 3458591. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3458591.
    City: Silongin. City ID: 1686455. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1686455.
    City: Malapag. City ID: 1703062. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1703062.
    City: Triebes. City ID: 2821192. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2821192.
    City: Santa Lucia Milpas Altas. City ID: 3589285. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3589285.
    City: Rakitovo. City ID: 727801. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=727801.
    City: Agueda. City ID: 2743292. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2743292.
    City: Tortolita. City ID: 5317867. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5317867.
    City: Apison. City ID: 4602916. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4602916.
    City: Plagiarion. City ID: 734564. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=734564.
    City: Montorso Vicentino. City ID: 3172638. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3172638.
    City: Urussu. City ID: 478565. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=478565.
    City: Tuxford. City ID: 2635321. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2635321.
    City: Sladna. City ID: 3190652. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3190652.
    City: Riantec. City ID: 2983730. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2983730.
    City: La Paz. City ID: 3442098. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3442098.
    City: Mamadysh. City ID: 529709. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=529709.
    City: San Fernando. City ID: 1690043. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1690043.
    City: Szombathely. City ID: 3044310. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3044310.
    City: Cerna Hora. City ID: 3078085. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3078085.
    City: Osnago. City ID: 3171844. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3171844.
    City: Haciqabul. City ID: 585225. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=585225.
    City: Smolino. City ID: 491660. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=491660.
    City: Ablis. City ID: 3038756. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3038756.
    City: Porto Calvo. City ID: 3391397. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3391397.
    City: Lieskau. City ID: 2877767. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2877767.
    City: Sagard. City ID: 2842434. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2842434.
    City: Varadero. City ID: 3534632. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3534632.
    City: Voskresensk. City ID: 471656. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=471656.
    City: Gostyn. City ID: 3098625. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3098625.
    City: Seth Ward. City ID: 5530469. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5530469.
    City: Hazel Crest. City ID: 4895416. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4895416.
    City: El Galpon. City ID: 3857974. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3857974.
    City: Irshava. City ID: 707559. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=707559.
    City: Alamosa. City ID: 5411479. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5411479.
    City: Malahide. City ID: 2962725. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2962725.
    City: East Greenville. City ID: 5187925. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5187925.
    City: Buena Vista. City ID: 4749715. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4749715.
    City: Tumarbong. City ID: 1680763. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1680763.
    City: Moses Lake North. City ID: 7261921. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=7261921.
    City: Piedmont. City ID: 4547969. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4547969.
    City: Mariani. City ID: 1263522. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1263522.
    City: Lapoutroie. City ID: 3007160. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3007160.
    City: Nustar. City ID: 3194310. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3194310.
    City: Loucovice. City ID: 3071532. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3071532.
    City: Florissant. City ID: 4386802. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4386802.
    City: Pueblo Nuevo. City ID: 3991567. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3991567.
    City: Angleton. City ID: 4670866. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4670866.
    City: Eckbolsheim. City ID: 3020489. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3020489.
    City: Arumuganeri. City ID: 1278343. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1278343.
    City: Cittiglio. City ID: 3178611. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3178611.
    City: Highland Lake. City ID: 5099052. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5099052.
    City: Sao Mateus. City ID: 3448519. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3448519.
    City: Misantla. City ID: 3523141. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3523141.
    City: Ukholovo. City ID: 479426. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=479426.
    City: Cherepovets. City ID: 569223. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=569223.
    City: Ust-Katav. City ID: 478071. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=478071.
    City: Baeza. City ID: 2521413. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2521413.
    City: Hilliard. City ID: 5157588. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5157588.
    City: El Estor. City ID: 3597078. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3597078.
    City: Easingwold. City ID: 2650517. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2650517.
    City: Kozhva. City ID: 543246. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=543246.
    City: Kilstett. City ID: 3011458. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3011458.
    City: Narcao. City ID: 2524024. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2524024.
    City: Hindley. City ID: 2646862. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2646862.
    City: Ouanani. City ID: 921654. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=921654.
    City: Novy Bydzov. City ID: 3069377. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3069377.
    City: Crosby. City ID: 4684301. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4684301.
    City: Freedom. City ID: 5350678. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5350678.
    City: Sedkyrkeshch. City ID: 497971. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=497971.
    City: Aosta. City ID: 3182997. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3182997.
    City: Pochep. City ID: 508656. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=508656.
    City: Caxhuacan. City ID: 3531398. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3531398.
    City: Celica. City ID: 3659544. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3659544.
    City: Lesznowola. City ID: 766369. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=766369.
    City: Sungailiat. City ID: 1625958. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1625958.
    City: Herriman. City ID: 5775782. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5775782.
    City: Urbiztondo. City ID: 1680200. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1680200.
    City: Ashland. City ID: 5063229. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5063229.
    City: Rietschen. City ID: 2846806. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2846806.
    City: Warrenton. City ID: 5759289. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5759289.
    City: Sanchez. City ID: 3493198. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3493198.
    City: Saint-Pierre-sur-Dives. City ID: 2977411. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2977411.
    City: Sychevka. City ID: 485280. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=485280.
    City: Alsterdorf. City ID: 2958105. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2958105.
    City: Rottingdean. City ID: 2639069. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2639069.
    City: Rakovnik. City ID: 3067051. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3067051.
    City: Fenouillet. City ID: 3018713. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3018713.
    City: Qingyuan. City ID: 1797945. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1797945.
    City: Grijpskerk. City ID: 2755317. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2755317.
    City: Placentia. City ID: 5383527. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5383527.
    City: Vrutky. City ID: 3056683. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3056683.
    City: Lazise. City ID: 3174975. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3174975.
    City: Prundu. City ID: 669545. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=669545.
    City: Brzesc Kujawski. City ID: 3102447. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3102447.
    City: Asuncion Nochixtlan. City ID: 3532656. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3532656.
    City: Sierning. City ID: 2765080. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2765080.
    City: Rednitzhembach. City ID: 2849568. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2849568.
    City: Niemegk. City ID: 2862640. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2862640.
    City: Ivanishchi. City ID: 555610. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=555610.
    City: Menzelinsk. City ID: 527529. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=527529.
    City: Karanja. City ID: 1267853. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1267853.
    City: Ammon. City ID: 5583997. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5583997.
    City: Seymour. City ID: 4408117. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4408117.
    City: Syrskoye. City ID: 485153. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=485153.
    City: Algemesi. City ID: 2522012. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2522012.
    City: Archi. City ID: 3182915. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3182915.
    City: Reo. City ID: 2356228. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2356228.
    City: Gornau. City ID: 2918970. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2918970.
    City: Singani. City ID: 921674. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=921674.
    City: Darova Noua. City ID: 679714. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=679714.
    City: Burla. City ID: 1275050. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1275050.
    City: Hillandale. City ID: 4358066. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4358066.
    City: Saint-Amarin. City ID: 2981815. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2981815.
    City: Madridejos. City ID: 1704127. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1704127.
    City: Pau Brasil. City ID: 3454743. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3454743.
    City: Trnava. City ID: 3057124. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3057124.
    City: Nozay. City ID: 2989876. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2989876.
    City: Ahus. City ID: 2727363. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2727363.
    City: Borger. City ID: 2758621. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2758621.
    City: Mkokotoni. City ID: 153585. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=153585.
    City: Victoria. City ID: 3666075. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3666075.
    City: Villa Maria Grande. City ID: 3427399. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3427399.
    City: Camandag. City ID: 1719908. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1719908.
    City: Dorfen. City ID: 2936103. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2936103.
    City: Mercogliano. City ID: 3173555. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3173555.
    City: General Acha. City ID: 3855143. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3855143.
    City: Newport. City ID: 5804693. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5804693.
    City: Friedberg. City ID: 2924802. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2924802.
    City: Apozol. City ID: 4018380. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4018380.
    City: Skarnes. City ID: 3139244. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3139244.
    City: Viradouro. City ID: 3444997. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3444997.
    City: Villa Juarez. City ID: 4021449. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4021449.
    City: Gedinne. City ID: 2797781. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2797781.
    City: Bad Liebenzell. City ID: 2953407. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2953407.
    City: Jiangwakou. City ID: 1806245. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1806245.
    City: Chicama. City ID: 3698359. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3698359.
    City: Rossdorf. City ID: 2844756. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2844756.
    City: Castiglione Messer Raimondo. City ID: 3179408. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3179408.
    City: Ganapi. City ID: 1719433. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1719433.
    City: Lambarene. City ID: 2399888. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2399888.
    City: Leticia. City ID: 3676623. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3676623.
    City: Saint-Martin-de-Re. City ID: 2978361. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2978361.
    City: Spantov. City ID: 666385. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=666385.
    City: Lubasz. City ID: 3093029. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3093029.
    City: Golden Hills. City ID: 5352875. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5352875.
    City: San Pascual. City ID: 1688800. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1688800.
    City: Nemesnadudvar. City ID: 3047399. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3047399.
    City: Herradura. City ID: 3433567. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3433567.
    City: Golhisar. City ID: 314072. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=314072.
    City: Pemangkat. City ID: 1631637. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1631637.
    City: Emmelshausen. City ID: 2930528. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2930528.
    City: Svitavy. City ID: 3064454. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3064454.
    City: Herentals. City ID: 2796009. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2796009.
    City: Tonyrefail. City ID: 2635689. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2635689.
    City: Ottrau. City ID: 2855923. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2855923.
    City: Leninskiy. City ID: 536111. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=536111.
    City: Ruskeala. City ID: 500502. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=500502.
    City: Bere. City ID: 2435474. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2435474.
    City: Paderborn. City ID: 2855745. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2855745.
    City: Skarzysko-Kamienna. City ID: 759141. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=759141.
    City: Craiova. City ID: 680332. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=680332.
    City: Bobon. City ID: 1724519. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1724519.
    City: Syamzha. City ID: 485351. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=485351.
    City: Balaka. City ID: 931865. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=931865.
    City: Stavnsholt. City ID: 2612710. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2612710.
    City: Lac du Flambeau. City ID: 5259036. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5259036.
    City: Saint-Eustache. City ID: 6138175. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=6138175.
    City: Adelia Maria. City ID: 3866935. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3866935.
    City: San Isidro. City ID: 3621889. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3621889.
    City: Jersey City. City ID: 5099836. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5099836.
    City: Toledo. City ID: 5757007. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5757007.
    City: Palenque. City ID: 3522164. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3522164.
    City: Wyoming. City ID: 5220236. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5220236.
    City: Brentford. City ID: 2654787. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2654787.
    City: Shahganj. City ID: 1256735. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1256735.
    City: Kamysh-Zarya. City ID: 706914. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=706914.
    City: Vorontsovka. City ID: 471909. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=471909.
    City: Eloyes. City ID: 3020275. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3020275.
    City: Quartz Hill. City ID: 5385393. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5385393.
    City: Springville. City ID: 4091542. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4091542.
    City: Karapinar. City ID: 309415. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=309415.
    City: Trittau. City ID: 2821085. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2821085.
    City: Balatonfured. City ID: 3055566. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3055566.
    City: Palazuelos de Eresma. City ID: 3114535. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3114535.
    City: Kanzaki. City ID: 1860095. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1860095.
    City: Turkheim. City ID: 2820752. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2820752.
    City: Jaruco. City ID: 3556351. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3556351.
    City: Peoria. City ID: 4905687. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4905687.
    City: Muniz Freire. City ID: 3456530. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3456530.
    City: Trementines. City ID: 2971861. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2971861.
    City: Richland Hills. City ID: 4722668. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4722668.
    City: Marietta. City ID: 5199879. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5199879.
    City: Hayrat. City ID: 745693. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=745693.
    City: Krasni Okny. City ID: 860012. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=860012.
    City: Sejenane. City ID: 2467368. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2467368.
    City: Ete. City ID: 2343073. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2343073.
    City: Ostrowy nad Oksza. City ID: 3089681. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3089681.
    City: Commerce. City ID: 4682762. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4682762.
    City: Andrijasevci. City ID: 3204817. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3204817.
    City: Butazon. City ID: 1722228. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1722228.
    City: Klyuchevsk. City ID: 1503169. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1503169.
    City: Evangelista. City ID: 1713702. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1713702.
    City: Pottsville. City ID: 5207080. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5207080.
    City: Strunga. City ID: 665914. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=665914.
    City: Temryuk. City ID: 483661. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=483661.
    City: Hope Valley. City ID: 2069646. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2069646.
    City: Wareham. City ID: 2634776. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2634776.
    City: Novokubansk. City ID: 518682. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=518682.
    City: Nizamabad. City ID: 1261258. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1261258.
    City: Pionerskiy. City ID: 509437. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=509437.
    City: Taissy. City ID: 2973524. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2973524.
    City: West Athens. City ID: 5407841. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5407841.
    City: Kaimganj. City ID: 1268616. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1268616.
    City: Le Luc. City ID: 3003650. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3003650.
    City: Lakeway. City ID: 4705041. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4705041.
    City: Los Reyes. City ID: 3997220. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3997220.
    City: Yacopi. City ID: 3665813. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3665813.
    City: Nottuln. City ID: 2861733. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2861733.
    City: Belgern. City ID: 2951258. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2951258.
    City: Venosa. City ID: 3164592. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3164592.
    City: Canoinhas. City ID: 3467452. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3467452.
    City: Ladik. City ID: 741892. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=741892.
    City: Charles Town. City ID: 4801850. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4801850.
    City: Nossen. City ID: 2861788. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2861788.
    City: Skutec. City ID: 3065921. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3065921.
    City: Malterdingen. City ID: 2874028. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2874028.
    City: Betera. City ID: 2520968. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2520968.
    City: Westford. City ID: 4955219. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4955219.
    City: Bujoru. City ID: 683342. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=683342.
    City: Fortuna. City ID: 3623716. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3623716.
    City: Mont Albert North. City ID: 7932630. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=7932630.
    City: Kurayyimah. City ID: 248414. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=248414.
    City: Warlingham. City ID: 2634759. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2634759.
    City: Ar Ramtha. City ID: 250336. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=250336.
    City: Malmkoping. City ID: 2692972. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2692972.
    City: Grandview Heights. City ID: 4513057. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4513057.
    City: Okawara. City ID: 2111461. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2111461.
    City: Edgemont Park. City ID: 4991823. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4991823.
    City: Lawson. City ID: 4394716. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4394716.
    City: Pymble. City ID: 2152361. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2152361.
    City: Halmagiu. City ID: 676356. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=676356.
    City: Tobolsk. City ID: 1489530. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1489530.
    City: Senirkent. City ID: 301172. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=301172.
    City: Bridgeton. City ID: 4378391. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4378391.
    City: Short Hills. City ID: 5104630. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5104630.
    City: Kyle. City ID: 4703811. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4703811.
    City: Lynnwood. City ID: 5802049. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5802049.
    City: Ratoath. City ID: 2961872. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2961872.
    City: Diveyevo. City ID: 566165. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=566165.
    City: Waterloo. City ID: 4266643. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4266643.
    City: Herne. City ID: 2795956. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2795956.
    City: Nicoresti. City ID: 672246. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=672246.
    City: Paulton. City ID: 2640559. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2640559.
    City: Dewsbury. City ID: 2651286. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2651286.
    City: Detroit. City ID: 4990729. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4990729.
    City: Jomala. City ID: 3041760. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3041760.
    City: Elburn. City ID: 4890835. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4890835.
    City: Kepanjen. City ID: 1640296. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1640296.
    City: Altopascio. City ID: 3183147. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3183147.
    City: Verucchio. City ID: 3164502. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3164502.
    City: Udesti. City ID: 664372. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=664372.
    City: Ranchuelo. City ID: 3542744. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3542744.
    City: Kulpin. City ID: 3196959. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3196959.
    City: Prado. City ID: 1692800. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1692800.
    City: Garibaldi. City ID: 3462557. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3462557.
    City: Hushitai. City ID: 2036619. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2036619.
    City: Herrljunga. City ID: 2706523. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2706523.
    City: Ilminster. City ID: 2646265. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2646265.
    City: Deagon. City ID: 2169237. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2169237.
    City: Dadunqiu. City ID: 1814456. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1814456.
    City: Sorang. City ID: 1519725. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1519725.
    City: Bilgi. City ID: 1275619. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1275619.
    City: Machinda. City ID: 2308626. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2308626.
    City: Fobes Hill. City ID: 5794675. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5794675.
    City: Atizapan. City ID: 3532625. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3532625.
    City: Tain. City ID: 2636321. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2636321.
    City: Munera. City ID: 2513421. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2513421.
    City: Park Forest Village. City ID: 5205094. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5205094.
    City: Haisnes. City ID: 3014060. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3014060.
    City: Arpasu de Jos. City ID: 686126. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=686126.
    City: Villefontaine. City ID: 2968771. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2968771.
    City: Emod. City ID: 721161. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=721161.
    City: Duchcov. City ID: 3076311. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3076311.
    City: Masaurhi Buzurg. City ID: 1263427. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1263427.
    City: Coaraci. City ID: 3466041. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3466041.
    City: Scheia. City ID: 667706. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=667706.
    City: Hettingen. City ID: 2905215. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2905215.
    City: Jamestown. City ID: 4515427. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4515427.
    City: Rockcreek. City ID: 5749017. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5749017.
    City: La Libertad. City ID: 3655131. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3655131.
    City: Balezino. City ID: 579432. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=579432.
    City: Tha Muang. City ID: 1150246. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1150246.
    City: Rosny-sur-Seine. City ID: 2982756. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2982756.
    City: Romille. City ID: 2982977. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2982977.
    City: Del Pilar. City ID: 1958738. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1958738.
    City: Folignano. City ID: 3176855. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3176855.
    City: Doberlug-Kirchhain. City ID: 2936631. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2936631.
    City: Northeim. City ID: 2861814. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2861814.
    City: Sanger. City ID: 4726957. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4726957.
    City: Albion. City ID: 4917523. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4917523.
    City: Buena Vista. City ID: 5415306. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5415306.
    City: Pedernales. City ID: 3653307. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3653307.
    City: Rioja. City ID: 3692863. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3692863.
    City: Fort Dodge. City ID: 4857486. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4857486.
    City: Seloncourt. City ID: 2975204. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2975204.
    City: Owosso. City ID: 5004792. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5004792.
    City: Rodersheim-Gronau. City ID: 3272457. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3272457.
    City: Al Birah. City ID: 285108. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=285108.
    City: Dinkelsbuhl. City ID: 2936886. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2936886.
    City: Pula. City ID: 3192224. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3192224.
    City: Carroll. City ID: 4850478. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4850478.
    City: Jones Creek. City ID: 4701510. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4701510.
    City: Chiria. City ID: 1274098. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1274098.
    City: Casper. City ID: 5820705. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5820705.
    City: Furiani. City ID: 3016890. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3016890.
    City: Le Grand-Quevilly. City ID: 3003952. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3003952.
    City: Arroio do Meio. City ID: 3471428. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3471428.
    City: Amasra. City ID: 752016. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=752016.
    City: Ramanayyapeta. City ID: 7302846. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=7302846.
    City: Al Kiswah. City ID: 173598. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=173598.
    City: Tall Kalakh. City ID: 163533. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=163533.
    City: Cochabamba. City ID: 3919968. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3919968.
    City: Chino Valley. City ID: 5289658. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5289658.
    City: Spezzano Piccolo. City ID: 2523022. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2523022.
    City: Asubulaq. City ID: 1526055. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1526055.
    City: Gonba. City ID: 1506418. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1506418.
    City: Pedro Meoqui. City ID: 3996234. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3996234.
    City: Grande Cache. City ID: 5964304. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5964304.
    City: Queniborough. City ID: 2639779. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2639779.
    City: Zhabinka. City ID: 618913. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=618913.
    City: Friedrichstadt. City ID: 2924477. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2924477.
    City: Wendell. City ID: 4498084. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4498084.
    City: Meiganga. City ID: 2227402. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2227402.
    City: Phitsanulok. City ID: 1607708. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1607708.
    City: Dinagat. City ID: 1714795. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1714795.
    City: Banga. City ID: 1727400. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1727400.
    City: Bela Crkva. City ID: 792794. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=792794.
    City: Buhi. City ID: 1723166. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1723166.
    City: Resolven. City ID: 2639482. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2639482.
    City: Gallargues-le-Montueux. City ID: 3015119. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3015119.
    City: Mira. City ID: 2737651. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2737651.
    City: Buerarema. City ID: 3468858. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3468858.
    City: Kenmar. City ID: 5195982. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5195982.
    City: Duingen. City ID: 2934697. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2934697.
    City: Taytayan. City ID: 1682594. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1682594.
    City: Schaftlarn. City ID: 2840634. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2840634.
    City: Mouchamps. City ID: 2991575. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2991575.
    City: Wani. City ID: 1252960. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1252960.
    City: Taoudenni. City ID: 2450173. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2450173.
    City: Stryi. City ID: 692372. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=692372.
    City: Hedge End. City ID: 6620360. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=6620360.
    City: Bellevue. City ID: 5146978. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5146978.
    City: Partapur. City ID: 1260232. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1260232.
    City: Perkins. City ID: 4547849. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4547849.
    City: Lokhvytsya. City ID: 702874. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=702874.
    City: Vila-seca. City ID: 3105803. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3105803.
    City: Tarragona. City ID: 3108288. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3108288.
    City: Encsencs. City ID: 721158. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=721158.
    City: Obroshyne. City ID: 698790. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=698790.
    City: Waldkirch. City ID: 2658067. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2658067.
    City: Lianran. City ID: 1803886. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1803886.
    City: Chopinzinho. City ID: 3466196. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3466196.
    City: Havre de Grace. City ID: 4357617. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4357617.
    City: Ninoy. City ID: 1697663. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1697663.
    City: Sao Joao do Paraiso. City ID: 3448861. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3448861.
    City: Shakhunya. City ID: 496012. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=496012.
    City: Reconvilier. City ID: 2659085. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2659085.
    City: Hohen Neuendorf. City ID: 2901588. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2901588.
    City: McFarland. City ID: 5371530. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5371530.
    City: Certosa di Pavia. City ID: 3179020. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3179020.
    City: Daru. City ID: 2409663. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2409663.
    City: Panaba. City ID: 3521972. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3521972.
    City: Hammel. City ID: 2620835. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2620835.
    City: Papanasam. City ID: 1260417. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1260417.
    City: Vacszentlaszlo. City ID: 3043278. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3043278.
    City: Actlzayanca de Hidalgo. City ID: 3533393. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3533393.
    City: Cammeray. City ID: 2207822. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2207822.
    City: Bro. City ID: 2719245. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2719245.
    City: Banisilan. City ID: 1727161. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1727161.
    City: Sochtenau. City ID: 2831731. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2831731.
    City: Rindge. City ID: 5091744. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5091744.
    City: Varna. City ID: 3164691. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3164691.
    City: Rouissat. City ID: 2482886. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2482886.
    City: Pietrosani. City ID: 670821. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=670821.
    City: Entroncamento. City ID: 2268575. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2268575.
    City: Popesti-Leordeni. City ID: 669870. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=669870.
    City: Larkana. City ID: 1172128. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1172128.
    City: Warden. City ID: 5815020. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5815020.
    City: Kawasaki. City ID: 1859647. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1859647.
    City: Grape Creek. City ID: 5522392. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5522392.
    City: Laboulaye. City ID: 3852468. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3852468.
    City: Hosenfeld. City ID: 2898483. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2898483.
    City: Iraucuba. City ID: 3398028. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3398028.
    City: Sambuluan. City ID: 1690607. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1690607.
    City: Hoxie. City ID: 4115508. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4115508.
    City: Hambach. City ID: 3014026. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3014026.
    City: Wilmington Island. City ID: 4231354. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4231354.
    City: Brant. City ID: 5907983. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=5907983.
    City: Ambleve. City ID: 2803242. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=2803242.
    City: Tarso. City ID: 3667380. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3667380.
    City: Zhytomyr. City ID: 686967. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=686967.
    City: Waterbury. City ID: 4845193. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4845193.
    City: Numaran. City ID: 3994581. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3994581.
    City: Al Jahra. City ID: 285799. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=285799.
    City: Cumberland. City ID: 4352681. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=4352681.
    City: Casay. City ID: 1709159. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1709159.
    City: Bancal. City ID: 1727471. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1727471.
    City: Remuna. City ID: 1258229. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1258229.
    City: Cornuda. City ID: 3178039. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=3178039.
    City: Utran. City ID: 1253640. Currently being processed at http://api.openweathermap.org/data/2.5/weather?appid=a2021fb15b43f9477b09ace30ada63a1&units=imperial&id=1253640.
    


```python
city_data['temp'] = temp
city_data['humidity'] = hum
city_data['wind speed'] = windspeed
city_data['cloudiness'] = cloudiness
```


```python
city_data.to_csv("City_Info.csv")
```


```python
plt.scatter(city_data["lat"], city_data["temp"], marker="o")

plt.title("Latitude vs Temp(F) (3/26/2018)")
plt.ylabel("Temperature (Fahrenheit)")
plt.xlabel("Latitude")
plt.xlim(-60, 90)
plt.grid(True)

plt.savefig("Lat_vs_Temp 3-26-2018.png")

plt.show()
```


![png](output_7_0.png)



```python
plt.scatter(city_data["lat"], city_data["humidity"], marker="o")

plt.title("Latitude vs Humidity (3/26/2018)")
plt.ylabel("Humidity")
plt.xlabel("Latitude")
plt.xlim(-60, 90)
plt.grid(True)

plt.savefig("Lat_vs_humidity 3-26-2018.png")

plt.show()
```


![png](output_8_0.png)



```python
plt.scatter(city_data["lat"], city_data["wind speed"], marker="o")

plt.title("Latitude vs Wind Speed (MPH) (3/26/2018)")
plt.ylabel("Wind Speed (MPH )")
plt.xlabel("Latitude")
plt.xlim(-60, 90)
plt.grid(True)

plt.savefig("Lat_vs_Wind_Speed 3-26-2018.png")

plt.show()
```


![png](output_9_0.png)



```python
plt.scatter(city_data["lat"], city_data["cloudiness"], marker="o")

plt.title("Latitude vs Cloudiness (3/26/2018)")
plt.ylabel("Cloudiness %")
plt.xlabel("Latitude")
plt.xlim(-60, 90)
plt.grid(True)

plt.savefig("Lat_vs_Cloudiness 3-26-2018.png")

plt.show()
```


![png](output_10_0.png)

