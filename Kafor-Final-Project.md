### Introduction

The objective is to look at the different venues between University of Chicago and Georgia Institute of Technology (Georgia Tech) since these are universities people as myself would want to attend for a degree. Both locations have good reputations as public institutions so the problem to solve was to find out what venues are available in the areas that does not require long travel. Many people who decide to stay near a campus ride a bike or use there four legs as a mode of transportation and need close by locations for daily activities and community.


To get started, before even running any code first library modules had to be imported.


```python
import pandas as pd
import numpy as np
import requests

!conda install -c conda-forge geopy --yes
import geopy as geopy
from geopy.geocoders import Nominatim 

# Matplotlib and associated plotting modules
import matplotlib.cm as cm
import matplotlib.colors as colors

!conda install -c conda-forge folium=0.5.0 --yes
import folium # map rendering library

print("Libraries Imported")
```

    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    
    ==> WARNING: A newer version of conda exists. <==
      current version: 4.8.3
      latest version: 4.8.4
    
    Please update conda by running
    
        $ conda update -n base -c defaults conda
    
    
    
    # All requested packages already installed.
    
    Collecting package metadata (current_repodata.json): done
    Solving environment: done
    
    
    ==> WARNING: A newer version of conda exists. <==
      current version: 4.8.3
      latest version: 4.8.4
    
    Please update conda by running
    
        $ conda update -n base -c defaults conda
    
    
    
    # All requested packages already installed.
    
    Libraries Imported


## Data Collection

The data for the venues was retrieved using the Foursquare Places API. The Places API offers real-time access to Foursquare's global database of rich venue data and user content to power your location-based experiences.

### Foursquare Credentials


```python
CLIENT_ID = 'MWBMLLHDCHCNOFVSO405PNGLHJP0EW0MAD1MEEO0SKMOFSJX'
CLIENT_SECRET = '3J3OZ5F4I5WW5OTRZOOWNMREHZEOANOANIOUC3VG2AN5DIM3'
VERSION = '20200825'

print('Credentials:')
print('CLIENT_ID: ' + CLIENT_ID)
print('CLIENT_SECRET:' + CLIENT_SECRET)
```

    Credentials:
    CLIENT_ID: MWBMLLHDCHCNOFVSO405PNGLHJP0EW0MAD1MEEO0SKMOFSJX
    CLIENT_SECRET:3J3OZ5F4I5WW5OTRZOOWNMREHZEOANOANIOUC3VG2AN5DIM3


### Coordinates

The addresses from both institutions were retrieved from Google Knowledge Graph through search. The Geocoder module was used to get the coordinates for both institutions.

Get nearby venues by Chicago - University of Chicago
Address: 5801 S Ellis Ave, Chicago, IL 60637


```python
address = "5801 S Ellis Ave, Chicago, IL 60637"

geolocator = Nominatim(user_agent="ca_explorer")
location = geolocator.geocode(address)
chi_latitude = location.latitude
chi_longitude = location.longitude
print('The geographical coordinate of University of Chicago are {}, {}.'.format(chi_latitude, chi_longitude))
```

    The geographical coordinate of University of Chicago are 41.784977, -87.5905237123017.



```python
#Map of Chicago using latitude and longitude values
map_chicago = folium.Map(location=[chi_latitude, chi_longitude], zoom_start=10)
map_chicago
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfOGEzZDU5NjE1MDI1NGIzMGJjMDBhYzM1YzIyN2M4YmUgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzhhM2Q1OTYxNTAyNTRiMzBiYzAwYWMzNWMyMjdjOGJlIiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF84YTNkNTk2MTUwMjU0YjMwYmMwMGFjMzVjMjI3YzhiZSA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF84YTNkNTk2MTUwMjU0YjMwYmMwMGFjMzVjMjI3YzhiZScsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbNDEuNzg0OTc3LC04Ny41OTA1MjM3MTIzMDE3XSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHpvb206IDEwLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbWF4Qm91bmRzOiBib3VuZHMsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBsYXllcnM6IFtdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgd29ybGRDb3B5SnVtcDogZmFsc2UsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBjcnM6IEwuQ1JTLkVQU0czODU3CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIH0pOwogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl84MDNjZmQ5MjA5ZmY0MDYwYjJkZjI5ZjBiYTI4YWM5YiA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgJ2h0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nJywKICAgICAgICAgICAgICAgIHsKICAiYXR0cmlidXRpb24iOiBudWxsLAogICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwKICAibWF4Wm9vbSI6IDE4LAogICJtaW5ab29tIjogMSwKICAibm9XcmFwIjogZmFsc2UsCiAgInN1YmRvbWFpbnMiOiAiYWJjIgp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF84YTNkNTk2MTUwMjU0YjMwYmMwMGFjMzVjMjI3YzhiZSk7CiAgICAgICAgCjwvc2NyaXB0Pg== onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



Get nearby venues by Atlanta - Georgia Institute of Technology
Address: North Ave NW, Atlanta, GA 30332


```python
address = "North Ave NW, Atlanta, GA 30332"

geolocator = Nominatim(user_agent="ca_explorer")
location = geolocator.geocode(address)
atl_latitude = location.latitude
atl_longitude = location.longitude
print('The geographical coordinates of Georgia Tech are {}, {}.'.format(atl_latitude, atl_longitude))
```

    The geographical coordinates of Georgia Tech are 33.7713526, -84.396345.



```python
#Map of Atlanta using latitude and longitude values
map_atlanta = folium.Map(location=[atl_latitude, atl_longitude], zoom_start=10)
map_atlanta
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfNGFjZDFmOTk5Yzc3NGJiMzhlNThhNWI2NmJmMjJlNDIgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzRhY2QxZjk5OWM3NzRiYjM4ZTU4YTViNjZiZjIyZTQyIiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF80YWNkMWY5OTljNzc0YmIzOGU1OGE1YjY2YmYyMmU0MiA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF80YWNkMWY5OTljNzc0YmIzOGU1OGE1YjY2YmYyMmU0MicsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbMzMuNzcxMzUyNiwtODQuMzk2MzQ1XSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHpvb206IDEwLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbWF4Qm91bmRzOiBib3VuZHMsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBsYXllcnM6IFtdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgd29ybGRDb3B5SnVtcDogZmFsc2UsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBjcnM6IEwuQ1JTLkVQU0czODU3CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIH0pOwogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl9jZjQwMjQ1ZjE3MDA0MTgxYTE1MjQ2MWFjMGViODYwYyA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgJ2h0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nJywKICAgICAgICAgICAgICAgIHsKICAiYXR0cmlidXRpb24iOiBudWxsLAogICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwKICAibWF4Wm9vbSI6IDE4LAogICJtaW5ab29tIjogMSwKICAibm9XcmFwIjogZmFsc2UsCiAgInN1YmRvbWFpbnMiOiAiYWJjIgp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80YWNkMWY5OTljNzc0YmIzOGU1OGE1YjY2YmYyMmU0Mik7CiAgICAgICAgCjwvc2NyaXB0Pg== onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



## Explore Venues 

 At first I reduced the radius and then increased it to 500 in order to generate enough venues nearby the universities. The campus size of University of Chicago is 217 acres and as for Georgia Institute of Technology (Georgia Tech), its almost twice as large with over 400 acres according to Google's Knowledge Graph. I completely forgot how large universities can be so this made sense to extend the radius to an appropriate size (500). Even within a 500 radius of the area there was only 13 venue listings nearby the University of Chicago and 17 nearby Georgia Institute of Technology (Georgia Tech). I did set the limit of venues to 100 although the cap was not necessary after seeing that not many locations were not available from either institution.


```python
#Limit 100
#Radius 500 miles

LIMIT = 100 
radius = 500
url = 'https://api.foursquare.com/v2/venues/explore?&client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}'.format(
    CLIENT_ID, 
    CLIENT_SECRET, 
    VERSION, 
    chi_latitude, 
    chi_longitude, 
    radius, 
    LIMIT)

# get the result to a json file
chi_results = requests.get(url).json()
chi_results
```




    {'meta': {'code': 200, 'requestId': '5f4e92bdcd73241163881aba'},
     'response': {'suggestedFilters': {'header': 'Tap to show:',
       'filters': [{'name': 'Open now', 'key': 'openNow'}]},
      'headerLocation': 'Woodlawn',
      'headerFullLocation': 'Woodlawn, Chicago',
      'headerLocationGranularity': 'neighborhood',
      'totalResults': 16,
      'suggestedBounds': {'ne': {'lat': 41.7894770045, 'lng': -87.58449997727499},
       'sw': {'lat': 41.780476995499995, 'lng': -87.59654744732842}},
      'groups': [{'type': 'Recommended Places',
        'name': 'recommended',
        'items': [{'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '594ac600419a9e72144fd6a7',
           'name': 'Build Coffee',
           'location': {'address': '6100 S Blackstone Ave',
            'lat': 41.78428847865535,
            'lng': -87.59041927423924,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78428847865535,
              'lng': -87.59041927423924},
             {'label': 'entrance', 'lat': 41.784157, 'lng': -87.590381}],
            'distance': 77,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['6100 S Blackstone Ave',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1e0931735',
             'name': 'Coffee Shop',
             'pluralName': 'Coffee Shops',
             'shortName': 'Coffee Shop',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/coffeeshop_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-594ac600419a9e72144fd6a7-0'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '518e7b9a498e001fc1a68809',
           'name': "61st Street Farmers' Market",
           'location': {'address': '61st between Dorchester and Blackstone',
            'lat': 41.784296089572855,
            'lng': -87.59079036498159,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.784296089572855,
              'lng': -87.59079036498159}],
            'distance': 78,
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['61st between Dorchester and Blackstone',
             'Chicago, IL',
             'United States']},
           'categories': [{'id': '50be8ee891d4fa8dcc7199a7',
             'name': 'Market',
             'pluralName': 'Markets',
             'shortName': 'Market',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/market_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-518e7b9a498e001fc1a68809-1'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4c3f6767ce54e21e4301081a',
           'name': 'Midway Plaisance Park',
           'location': {'address': '1130 Midway Plaisance',
            'crossStreet': 'East 59',
            'lat': 41.786525766685706,
            'lng': -87.59445752907632,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.786525766685706,
              'lng': -87.59445752907632}],
            'distance': 369,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1130 Midway Plaisance (East 59)',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d163941735',
             'name': 'Park',
             'pluralName': 'Parks',
             'shortName': 'Park',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/park_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4c3f6767ce54e21e4301081a-2'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4f191ac9e4b099f9dc3cfcf0',
           'name': 'University of Chicago @ Midway Plaisance',
           'location': {'address': '60th & Dorchester',
            'lat': 41.787751302023764,
            'lng': -87.5887820041004,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.787751302023764,
              'lng': -87.5887820041004}],
            'distance': 340,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['60th & Dorchester',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d163941735',
             'name': 'Park',
             'pluralName': 'Parks',
             'shortName': 'Park',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/park_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4f191ac9e4b099f9dc3cfcf0-3'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e67c9ea81dcaba7cca667a2',
           'name': "B'Gabs Goodies",
           'location': {'address': '6100 S Blackstone Ave',
            'lat': 41.78424509912927,
            'lng': -87.5903719551618,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78424509912927,
              'lng': -87.5903719551618}],
            'distance': 82,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['6100 S Blackstone Ave',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1f9941735',
             'name': 'Food & Drink Shop',
             'pluralName': 'Food & Drink Shops',
             'shortName': 'Food & Drink',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/foodanddrink_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e67c9ea81dcaba7cca667a2-4'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4bc5f37ed35d9c74badfe13a',
           'name': 'Plum Cafe at Chicago Press Building',
           'location': {'address': '1427 E 60th St',
            'crossStreet': 'Blackstone',
            'lat': 41.786028,
            'lng': -87.59003496666666,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.786028,
              'lng': -87.59003496666666},
             {'label': 'entrance', 'lat': 41.785884, 'lng': -87.590542}],
            'distance': 123,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1427 E 60th St (Blackstone)',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d16d941735',
             'name': 'Café',
             'pluralName': 'Cafés',
             'shortName': 'Café',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/cafe_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4bc5f37ed35d9c74badfe13a-5'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '5208e5be498ec4bb24440e34',
           'name': 'Jackson Towers Fitness',
           'location': {'address': '60th & Harper',
            'lat': 41.784878907879474,
            'lng': -87.58879937037533,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.784878907879474,
              'lng': -87.58879937037533}],
            'distance': 143,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['60th & Harper',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d175941735',
             'name': 'Gym / Fitness Center',
             'pluralName': 'Gyms or Fitness Centers',
             'shortName': 'Gym / Fitness',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/building/gym_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-5208e5be498ec4bb24440e34-6'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4b18688df964a5204fd223e3',
           'name': 'Metra - 59th St (University of Chicago)',
           'location': {'address': '59th St',
            'crossStreet': 'at Harper Ave',
            'lat': 41.787728868561125,
            'lng': -87.588788713734,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.787728868561125,
              'lng': -87.588788713734}],
            'distance': 338,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['59th St (at Harper Ave)',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d129951735',
             'name': 'Train Station',
             'pluralName': 'Train Stations',
             'shortName': 'Train Station',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/travel/trainstation_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4b18688df964a5204fd223e3-7'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '518d83c3498ef47c1a555894',
           'name': 'Jackson Park Track & Soccer Field',
           'location': {'address': '6100 S Stony Island Ave',
            'lat': 41.783367999999996,
            'lng': -87.58680600000001,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.783367999999996,
              'lng': -87.58680600000001},
             {'label': 'entrance', 'lat': 41.783612, 'lng': -87.586744}],
            'distance': 356,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['6100 S Stony Island Ave',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4cce455aebf7b749d5e191f5',
             'name': 'Soccer Field',
             'pluralName': 'Soccer Fields',
             'shortName': 'Soccer Field',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/stadium_soccer_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-518d83c3498ef47c1a555894-8'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e5d4dec31519cd0f266871a',
           'name': 'Tiffin Cafe',
           'location': {'address': '1414 E 59th St',
            'lat': 41.7882194519043,
            'lng': -87.5909652709961,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.7882194519043,
              'lng': -87.5909652709961}],
            'distance': 362,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1414 E 59th St',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1e0931735',
             'name': 'Coffee Shop',
             'pluralName': 'Coffee Shops',
             'shortName': 'Coffee Shop',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/coffeeshop_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e5d4dec31519cd0f266871a-9'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '504412dd222f63cf8739b2eb',
           'name': 'International House at the University of Chicago',
           'location': {'address': '1414 E 59th St',
            'lat': 41.78824,
            'lng': -87.590804,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78824,
              'lng': -87.590804}],
            'distance': 363,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1414 E 59th St',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '5032792091d4c4b30a586d5c',
             'name': 'Concert Hall',
             'pluralName': 'Concert Halls',
             'shortName': 'Concert Hall',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/musicvenue_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-504412dd222f63cf8739b2eb-10'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '56439c29cd109915f7fa2fc2',
           'name': 'Divvy Station',
           'location': {'address': '1607 E 59th St',
            'crossStreet': 'Harper Ave & 59th St',
            'lat': 41.78794281,
            'lng': -87.58831517,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78794281,
              'lng': -87.58831517}],
            'distance': 377,
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1607 E 59th St (Harper Ave & 59th St)',
             'Chicago, IL',
             'United States']},
           'categories': [{'id': '4e4c9077bd41f78e849722f9',
             'name': 'Bike Rental / Bike Share',
             'pluralName': 'Bike Rentals / Bike Shares',
             'shortName': 'Bike',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/bikeshop_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-56439c29cd109915f7fa2fc2-11'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e52c89962840c1260e1e164',
           'name': 'Huckleberry Park',
           'location': {'address': '6200 S Kimbark Ave',
            'crossStreet': 'at 62nd St.',
            'lat': 41.78232103190902,
            'lng': -87.59480953216553,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78232103190902,
              'lng': -87.59480953216553}],
            'distance': 462,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['6200 S Kimbark Ave (at 62nd St.)',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1e7941735',
             'name': 'Playground',
             'pluralName': 'Playgrounds',
             'shortName': 'Playground',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/playground_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e52c89962840c1260e1e164-12'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '5164a455e4b061c025433e20',
           'name': 'CTA Bus Stop 1513',
           'location': {'lat': 41.787987,
            'lng': -87.58656,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.787987,
              'lng': -87.58656}],
            'distance': 469,
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['Chicago, IL', 'United States']},
           'categories': [{'id': '4bf58dd8d48988d1fe931735',
             'name': 'Bus Station',
             'pluralName': 'Bus Stations',
             'shortName': 'Bus Station',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/travel/busstation_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-5164a455e4b061c025433e20-13'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '5aaff0bac58ed74dce15da95',
           'name': "Leon's Barbecue",
           'location': {'address': '63rd and Harper',
            'lat': 41.780854,
            'lng': -87.588451,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.780854,
              'lng': -87.588451}],
            'distance': 490,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['63rd and Harper',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1df931735',
             'name': 'BBQ Joint',
             'pluralName': 'BBQ Joints',
             'shortName': 'BBQ',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/bbqalt_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-5aaff0bac58ed74dce15da95-14'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4f324e9d19836c91c7caceed',
           'name': 'Tres Original Pancakes',
           'location': {'address': '1528 E 63rd St',
            'lat': 41.78086853027344,
            'lng': -87.58818817138672,
            'labeledLatLngs': [{'label': 'display',
              'lat': 41.78086853027344,
              'lng': -87.58818817138672}],
            'distance': 496,
            'postalCode': '60637',
            'cc': 'US',
            'city': 'Chicago',
            'state': 'IL',
            'country': 'United States',
            'formattedAddress': ['1528 E 63rd St',
             'Chicago, IL 60637',
             'United States']},
           'categories': [{'id': '4d4b7105d754a06374d81259',
             'name': 'Food',
             'pluralName': 'Food',
             'shortName': 'Food',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/default_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4f324e9d19836c91c7caceed-15'}]}]}}



### Explore Venues nearby Georgia Institute of Technology


```python
#Limit 100
#Radius 500 miles

LIMIT = 100 
radius = 500
url = 'https://api.foursquare.com/v2/venues/explore?&client_id={}&client_secret={}&v={}&ll={},{}&radius={}&limit={}'.format(
    CLIENT_ID, 
    CLIENT_SECRET, 
    VERSION, 
    atl_latitude, 
    atl_longitude, 
    radius, 
    LIMIT)

# get the result to a json file
atl_results = requests.get(url).json()
atl_results
```




    {'meta': {'code': 200, 'requestId': '5f4e94af1883f35ebf4e6afa'},
     'response': {'suggestedFilters': {'header': 'Tap to show:',
       'filters': [{'name': 'Open now', 'key': 'openNow'}]},
      'headerLocation': 'Marietta Street Artery',
      'headerFullLocation': 'Marietta Street Artery, Atlanta',
      'headerLocationGranularity': 'neighborhood',
      'totalResults': 18,
      'suggestedBounds': {'ne': {'lat': 33.7758526045, 'lng': -84.39094164975738},
       'sw': {'lat': 33.7668525955, 'lng': -84.40174835024261}},
      'groups': [{'type': 'Recommended Places',
        'name': 'recommended',
        'items': [{'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '555639d2498ea5420402bccd',
           'name': 'Coca-Cola Mainstreet @ AOC',
           'location': {'address': '1 Coca Cola Plz NW',
            'lat': 33.7709799841634,
            'lng': -84.39803676785081,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.7709799841634,
              'lng': -84.39803676785081}],
            'distance': 161,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['1 Coca Cola Plz NW',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d14e941735',
             'name': 'American Restaurant',
             'pluralName': 'American Restaurants',
             'shortName': 'American',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/default_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-555639d2498ea5420402bccd-0'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '512e4185e0e26a825ba3c825',
           'name': 'Highland Bakery',
           'location': {'address': '225 North Ave NW',
            'lat': 33.77264610481115,
            'lng': -84.39458549022675,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77264610481115,
              'lng': -84.39458549022675}],
            'distance': 217,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['225 North Ave NW',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d16a941735',
             'name': 'Bakery',
             'pluralName': 'Bakeries',
             'shortName': 'Bakery',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/bakery_',
              'suffix': '.png'},
             'primary': True}],
           'delivery': {'id': '1490525',
            'url': 'https://www.grubhub.com/restaurant/highland-bakery-224-uncle-heinie-way-northwest-atlanta/1490525?affiliate=1131&utm_source=foursquare-affiliate-network&utm_medium=affiliate&utm_campaign=1131&utm_content=1490525',
            'provider': {'name': 'grubhub',
             'icon': {'prefix': 'https://fastly.4sqi.net/img/general/cap/',
              'sizes': [40, 50],
              'name': '/delivery_provider_grubhub_20180129.png'}}},
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-512e4185e0e26a825ba3c825-1'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4b6a8415f964a5206ad72be3',
           'name': 'Ferst Center For The Arts',
           'location': {'address': '349 North Ave NW',
            'crossStreet': 'Georgia Tech',
            'lat': 33.774819876519174,
            'lng': -84.39919356481722,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.774819876519174,
              'lng': -84.39919356481722}],
            'distance': 467,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['349 North Ave NW (Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1ac941735',
             'name': 'College Theater',
             'pluralName': 'College Theaters',
             'shortName': 'Theater',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/performingarts_theater_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4b6a8415f964a5206ad72be3-2'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4b9ad39ef964a52097d935e3',
           'name': 'Hampton Inn by Hilton',
           'location': {'address': '244 North Ave NW',
            'lat': 33.77114566253568,
            'lng': -84.39578511197396,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77114566253568,
              'lng': -84.39578511197396}],
            'distance': 56,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['244 North Ave NW',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1fa931735',
             'name': 'Hotel',
             'pluralName': 'Hotels',
             'shortName': 'Hotel',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/travel/hotel_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4b9ad39ef964a52097d935e3-3'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e67acf0bd41e96a148c2889',
           'name': 'T-Mobile',
           'location': {'address': '1 Coca Cola Plz NW #CCP1',
            'lat': 33.77117919921875,
            'lng': -84.39620208740234,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77117919921875,
              'lng': -84.39620208740234}],
            'distance': 23,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['1 Coca Cola Plz NW #CCP1',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4f04afc02fb6e1c99f3db0bc',
             'name': 'Mobile Phone Shop',
             'pluralName': 'Mobile Phone Shops',
             'shortName': 'Mobile Phones',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/mobilephoneshop_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e67acf0bd41e96a148c2889-4'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4a82e9d7f964a52087f91fe3',
           'name': 'Wells Fargo',
           'location': {'address': '645 State St NW',
            'crossStreet': 'at Tech Pkwy NW',
            'lat': 33.77254846534218,
            'lng': -84.39843042541548,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77254846534218,
              'lng': -84.39843042541548},
             {'label': 'entrance', 'lat': 33.772487, 'lng': -84.398487}],
            'distance': 234,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['645 State St NW (at Tech Pkwy NW)',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d10a951735',
             'name': 'Bank',
             'pluralName': 'Banks',
             'shortName': 'Bank',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/financial_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4a82e9d7f964a52087f91fe3-5'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4d922924f5388cfae932c63d',
           'name': 'Chick-fil-A',
           'location': {'address': '350 Ferst Dr',
            'lat': 33.7736732,
            'lng': -84.3982027,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.7736732,
              'lng': -84.3982027}],
            'distance': 310,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['350 Ferst Dr',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d16e941735',
             'name': 'Fast Food Restaurant',
             'pluralName': 'Fast Food Restaurants',
             'shortName': 'Fast Food',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/fastfood_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4d922924f5388cfae932c63d-6'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e53a1b218a8c0ad8f70c448',
           'name': 'Starbucks',
           'location': {'address': '266 4th St NW',
            'lat': 33.774261,
            'lng': -84.396411,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.774261,
              'lng': -84.396411}],
            'distance': 323,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['266 4th St NW',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1e0931735',
             'name': 'Coffee Shop',
             'pluralName': 'Coffee Shops',
             'shortName': 'Coffee Shop',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/coffeeshop_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e53a1b218a8c0ad8f70c448-7'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '54beae0c498e8cea02522c8b',
           'name': 'Panda Express',
           'location': {'address': '350 Ferst Drive NW',
            'lat': 33.773779492893055,
            'lng': -84.39813668981611,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.773779492893055,
              'lng': -84.39813668981611}],
            'distance': 316,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['350 Ferst Drive NW',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d145941735',
             'name': 'Chinese Restaurant',
             'pluralName': 'Chinese Restaurants',
             'shortName': 'Chinese',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/asian_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-54beae0c498e8cea02522c8b-8'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4af4e0f5f964a52031f721e3',
           'name': 'Under The Couch',
           'location': {'address': 'North Ave NW',
            'crossStreet': 'at Georgia Tech',
            'lat': 33.773898208800745,
            'lng': -84.39886903792853,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.773898208800745,
              'lng': -84.39886903792853}],
            'distance': 367,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['North Ave NW (at Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1e5931735',
             'name': 'Music Venue',
             'pluralName': 'Music Venues',
             'shortName': 'Music Venue',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/arts_entertainment/musicvenue_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4af4e0f5f964a52031f721e3-9'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4c239bd9a852c928b2c5e16c',
           'name': 'Harrison Square',
           'location': {'address': 'Power Plant Dr NW',
            'lat': 33.77301871776581,
            'lng': -84.3952989578247,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77301871776581,
              'lng': -84.3952989578247}],
            'distance': 209,
            'postalCode': '30313',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['Power Plant Dr NW',
             'Atlanta, GA 30313',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d164941735',
             'name': 'Plaza',
             'pluralName': 'Plazas',
             'shortName': 'Plaza',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/plaza_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4c239bd9a852c928b2c5e16c-10'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4da46601bf22a14372c6dcf8',
           'name': 'Taco Bell',
           'location': {'address': 'North Ave NW',
            'crossStreet': 'Georgia Tech',
            'lat': 33.773780184594145,
            'lng': -84.39820597474531,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.773780184594145,
              'lng': -84.39820597474531}],
            'distance': 320,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['North Ave NW (Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d16e941735',
             'name': 'Fast Food Restaurant',
             'pluralName': 'Fast Food Restaurants',
             'shortName': 'Fast Food',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/fastfood_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4da46601bf22a14372c6dcf8-11'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4d7555fafc766a31b9268d1a',
           'name': "Burdell's",
           'location': {'address': '350 Ferst Drive NW',
            'crossStreet': 'at Georgia Tech',
            'lat': 33.77376958442543,
            'lng': -84.3980832286946,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77376958442543,
              'lng': -84.3980832286946}],
            'distance': 313,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['350 Ferst Drive NW (at Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d1b1941735',
             'name': 'College Bookstore',
             'pluralName': 'College Bookstores',
             'shortName': 'College Bookstore',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/bookstore_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4d7555fafc766a31b9268d1a-12'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4e820b5f7ee61ffc04f4c7d3',
           'name': 'Rooftop Garden',
           'location': {'address': 'North Ave NW',
            'crossStreet': 'at Georgia Tech',
            'lat': 33.7744282899713,
            'lng': -84.39655184225045,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.7744282899713,
              'lng': -84.39655184225045}],
            'distance': 342,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['North Ave NW (at Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d133951735',
             'name': 'Roof Deck',
             'pluralName': 'Roof Decks',
             'shortName': 'Roof Deck',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/travel/hotel_roofdeck_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4e820b5f7ee61ffc04f4c7d3-13'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '506b929eb0edcdd34cd227c8',
           'name': 'GT Stinger Stop - Techwood and North Ave',
           'location': {'address': 'Techwood Dr NW',
            'crossStreet': 'at North Ave NW',
            'lat': 33.771245913278335,
            'lng': -84.3920373916626,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.771245913278335,
              'lng': -84.3920373916626}],
            'distance': 398,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['Techwood Dr NW (at North Ave NW)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '52f2ab2ebcbc57f1066b8b4f',
             'name': 'Bus Stop',
             'pluralName': 'Bus Stops',
             'shortName': 'Bus Stop',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/travel/busstation_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-506b929eb0edcdd34cd227c8-14'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4dadda617abacefe5c8b201e',
           'name': 'Student Center Food Court',
           'location': {'address': '350 Ferst Dr NW',
            'crossStreet': 'at Georgia Tech',
            'lat': 33.77445091089932,
            'lng': -84.39890435841951,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77445091089932,
              'lng': -84.39890435841951}],
            'distance': 418,
            'postalCode': '30332',
            'cc': 'US',
            'neighborhood': 'Georgia Tech',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['350 Ferst Dr NW (at Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d120951735',
             'name': 'Food Court',
             'pluralName': 'Food Courts',
             'shortName': 'Food Court',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/shops/food_foodcourt_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4dadda617abacefe5c8b201e-15'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '4d5bd186fb186dcb8b03f89a',
           'name': "Dunkin'",
           'location': {'address': 'North Ave NW',
            'crossStreet': 'at Georgia Tech',
            'lat': 33.77442791392891,
            'lng': -84.39880812280745,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77442791392891,
              'lng': -84.39880812280745}],
            'distance': 411,
            'postalCode': '30332',
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['North Ave NW (at Georgia Tech)',
             'Atlanta, GA 30332',
             'United States']},
           'categories': [{'id': '4bf58dd8d48988d148941735',
             'name': 'Donut Shop',
             'pluralName': 'Donut Shops',
             'shortName': 'Donuts',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/food/donuts_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-4d5bd186fb186dcb8b03f89a-16'},
         {'reasons': {'count': 0,
           'items': [{'summary': 'This spot is popular',
             'type': 'general',
             'reasonName': 'globalInteractionReason'}]},
          'venue': {'id': '5701c802498ef642af8ca74c',
           'name': 'Einstein Statue',
           'location': {'lat': 33.77522394551474,
            'lng': -84.39718993342497,
            'labeledLatLngs': [{'label': 'display',
              'lat': 33.77522394551474,
              'lng': -84.39718993342497}],
            'distance': 437,
            'cc': 'US',
            'city': 'Atlanta',
            'state': 'GA',
            'country': 'United States',
            'formattedAddress': ['Atlanta, GA', 'United States']},
           'categories': [{'id': '52e81612bcbc57f1066b79ed',
             'name': 'Outdoor Sculpture',
             'pluralName': 'Outdoor Sculptures',
             'shortName': 'Outdoor Sculpture',
             'icon': {'prefix': 'https://ss3.4sqi.net/img/categories_v2/parks_outdoors/sculpture_',
              'suffix': '.png'},
             'primary': True}],
           'photos': {'count': 0, 'groups': []}},
          'referralId': 'e-0-5701c802498ef642af8ca74c-17'}]}]}}



## Data Preparation

### Venues Nearby 

The venues were grouped by categories in Foursquare to know what types are listed and available around each university. Then the venues were order by which are closer to the universities. After previewing the columns available in the JSON response I seen that we did not need all the columns. The name, categories, and coordinates should be efficient data to continue on for further data analysis.

We stored the venue results for University of Chicago and Georgia Institute of Technology (Georgia Tech) in a pandas dataframe.

Since the venues were not many I did not have to run any code to see unique or common categories and venues. There were not many similar category types. 


```python
chi_venues = chi_results['response']['groups'][0]['items']
#chi_nearby_venues = pd.json_normalize(chi_venues) #flatten JSON

chi_venues_list = []
chi_venues_list.append([
    (
    v['venue']['name'], 
    v['venue']['categories'][0]['name'],
    v['venue']['location']['lat'], 
    v['venue']['location']['lng'] 
    ) for v in chi_venues])

chi_df = pd.DataFrame([item for chi_venue_list in chi_venues_list for item in chi_venue_list])
chi_df.columns = ['Name', 'Category Type', 'Latitude', 'Longitude']
chi_df

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
      <th>Name</th>
      <th>Category Type</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Build Coffee</td>
      <td>Coffee Shop</td>
      <td>41.784288</td>
      <td>-87.590419</td>
    </tr>
    <tr>
      <th>1</th>
      <td>61st Street Farmers' Market</td>
      <td>Market</td>
      <td>41.784296</td>
      <td>-87.590790</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Midway Plaisance Park</td>
      <td>Park</td>
      <td>41.786526</td>
      <td>-87.594458</td>
    </tr>
    <tr>
      <th>3</th>
      <td>University of Chicago @ Midway Plaisance</td>
      <td>Park</td>
      <td>41.787751</td>
      <td>-87.588782</td>
    </tr>
    <tr>
      <th>4</th>
      <td>B'Gabs Goodies</td>
      <td>Food &amp; Drink Shop</td>
      <td>41.784245</td>
      <td>-87.590372</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Plum Cafe at Chicago Press Building</td>
      <td>Café</td>
      <td>41.786028</td>
      <td>-87.590035</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Jackson Towers Fitness</td>
      <td>Gym / Fitness Center</td>
      <td>41.784879</td>
      <td>-87.588799</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Metra - 59th St (University of Chicago)</td>
      <td>Train Station</td>
      <td>41.787729</td>
      <td>-87.588789</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Jackson Park Track &amp; Soccer Field</td>
      <td>Soccer Field</td>
      <td>41.783368</td>
      <td>-87.586806</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Tiffin Cafe</td>
      <td>Coffee Shop</td>
      <td>41.788219</td>
      <td>-87.590965</td>
    </tr>
    <tr>
      <th>10</th>
      <td>International House at the University of Chicago</td>
      <td>Concert Hall</td>
      <td>41.788240</td>
      <td>-87.590804</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Divvy Station</td>
      <td>Bike Rental / Bike Share</td>
      <td>41.787943</td>
      <td>-87.588315</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Huckleberry Park</td>
      <td>Playground</td>
      <td>41.782321</td>
      <td>-87.594810</td>
    </tr>
    <tr>
      <th>13</th>
      <td>CTA Bus Stop 1513</td>
      <td>Bus Station</td>
      <td>41.787987</td>
      <td>-87.586560</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Leon's Barbecue</td>
      <td>BBQ Joint</td>
      <td>41.780854</td>
      <td>-87.588451</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Tres Original Pancakes</td>
      <td>Food</td>
      <td>41.780869</td>
      <td>-87.588188</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(chi_df.shape)
```

    (16, 4)



```python
chi_df.groupby('Category Type').count()
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
      <th>Name</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Category Type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>BBQ Joint</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bike Rental / Bike Share</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bus Station</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Café</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Coffee Shop</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Concert Hall</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Food</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Food &amp; Drink Shop</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Gym / Fitness Center</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Market</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Park</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Playground</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Soccer Field</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Train Station</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



### Categories for Venues nearby Georgia Tech


```python
atl_venues = atl_results['response']['groups'][0]['items']

atl_venues_list = []
atl_venues_list.append([
    (
    v['venue']['name'], 
    v['venue']['categories'][0]['name'],
    v['venue']['location']['lat'], 
    v['venue']['location']['lng'] 
    ) for v in atl_venues])

atl_df = pd.DataFrame([item for atl_venue_list in atl_venues_list for item in atl_venue_list])
atl_df.columns = ['Name', 'Category Type', 'Latitude', 'Longitude']
atl_df
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
      <th>Name</th>
      <th>Category Type</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Coca-Cola Mainstreet @ AOC</td>
      <td>American Restaurant</td>
      <td>33.770980</td>
      <td>-84.398037</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Highland Bakery</td>
      <td>Bakery</td>
      <td>33.772646</td>
      <td>-84.394585</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Ferst Center For The Arts</td>
      <td>College Theater</td>
      <td>33.774820</td>
      <td>-84.399194</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hampton Inn by Hilton</td>
      <td>Hotel</td>
      <td>33.771146</td>
      <td>-84.395785</td>
    </tr>
    <tr>
      <th>4</th>
      <td>T-Mobile</td>
      <td>Mobile Phone Shop</td>
      <td>33.771179</td>
      <td>-84.396202</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wells Fargo</td>
      <td>Bank</td>
      <td>33.772548</td>
      <td>-84.398430</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Chick-fil-A</td>
      <td>Fast Food Restaurant</td>
      <td>33.773673</td>
      <td>-84.398203</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Starbucks</td>
      <td>Coffee Shop</td>
      <td>33.774261</td>
      <td>-84.396411</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Panda Express</td>
      <td>Chinese Restaurant</td>
      <td>33.773779</td>
      <td>-84.398137</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Under The Couch</td>
      <td>Music Venue</td>
      <td>33.773898</td>
      <td>-84.398869</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Harrison Square</td>
      <td>Plaza</td>
      <td>33.773019</td>
      <td>-84.395299</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Taco Bell</td>
      <td>Fast Food Restaurant</td>
      <td>33.773780</td>
      <td>-84.398206</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Burdell's</td>
      <td>College Bookstore</td>
      <td>33.773770</td>
      <td>-84.398083</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Rooftop Garden</td>
      <td>Roof Deck</td>
      <td>33.774428</td>
      <td>-84.396552</td>
    </tr>
    <tr>
      <th>14</th>
      <td>GT Stinger Stop - Techwood and North Ave</td>
      <td>Bus Stop</td>
      <td>33.771246</td>
      <td>-84.392037</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Student Center Food Court</td>
      <td>Food Court</td>
      <td>33.774451</td>
      <td>-84.398904</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Dunkin'</td>
      <td>Donut Shop</td>
      <td>33.774428</td>
      <td>-84.398808</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Einstein Statue</td>
      <td>Outdoor Sculpture</td>
      <td>33.775224</td>
      <td>-84.397190</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(atl_df.shape)
```

    (18, 4)



```python
atl_df.groupby('Category Type').count()
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
      <th>Name</th>
      <th>Latitude</th>
      <th>Longitude</th>
    </tr>
    <tr>
      <th>Category Type</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>American Restaurant</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bakery</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bank</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Bus Stop</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Chinese Restaurant</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Coffee Shop</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>College Bookstore</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>College Theater</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Donut Shop</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Fast Food Restaurant</th>
      <td>2</td>
      <td>2</td>
      <td>2</td>
    </tr>
    <tr>
      <th>Food Court</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Hotel</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Mobile Phone Shop</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Music Venue</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Outdoor Sculpture</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Plaza</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Roof Deck</th>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



## Data Exploration (Results)

The University of Chicago had only two repeated category types which were parks and coffee shops. 

There is a nearby bus station at the University of Chicago, so a user does not need a car or uber as much if there is a bus route and a gym, but most universities already have a recreation center that someone could use. If a break is needed a person has the choice of more than one park to walk or go running at. If they do not want to eat coffee shop food and want something more hearty there is a BBQ joint nearby.

At Georgia Institute of Technology (Georgia Tech), they have many different kind of restuarants nearby that are just not inside the college. One of the greatest perks is a music venue so people can probably get to hear local bands and if they do not want to stay at a dorm can have a night at the nearby hotel at the Hampton Inn and not too far from the hotel is a bank. 

There could be shopping center in the area.

## Data Analysis

### Maps with Markers

After looking at the venues for each university, maps were created with markers for each of the venues around each of the universities. We remove the 'Name' and 'Category Type' columns since we only need the coordinates for k-Means cluster labels. The maps will not be ordinary maps with markers, but will have clusters using k-Means with a initial k/clusters of 3. 

After creating the dataframes with the clusters we can see the clusters were color-coded and of course grouped by distances. The elbow method was not neccessary since the data points are very few. The perfect zoom size at 16 let us see some data points that were like outliers, but as you know they don't exist in k-Means. For instance, based on Google maps Leon's Barbecue takes 19 minutes by car and up to two hours walking distance. This venue is about 6.6 miles away from the University of Chicago. The venue with the farthest distance from Georgia Institute of Technology (Georgia Tech) would be Cocoa Cola Mainstreet at AOC although GT Stinger Shop was close and has it's own cluster group. The location for Coca Cola @ AOC was not easy to locate by name in Google Maps and the address was retrieved for the restaurant through Foursquare. Again, Georgia Tech wins with the farthest distance being less than 1.7 miles with only a 35 minute walk.


```python
from sklearn.cluster import KMeans

# set number of clusters
kclusters = 3

chi_df_clustering = chi_df.drop(['Name','Category Type'], 1)

# run k-means clustering
kmeans = KMeans(n_clusters=kclusters, random_state=0).fit(chi_df_clustering)

# check cluster labels generated for each row in the dataframe
kmeans.labels_[0:13]
```




    array([2, 2, 0, 1, 2, 1, 2, 1, 2, 1, 1, 1, 0], dtype=int32)



We then need to create a new dataframe with the cluster.


```python
chi_df_merged = chi_df_clustering
chi_df_merged.insert(0, 'Cluster Labels', kmeans.labels_)
name_column = chi_df['Name']
chi_df_with_clusters = pd.concat([chi_df_merged,name_column], axis = 1)
chi_df_with_clusters
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
      <th>Cluster Labels</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>41.784288</td>
      <td>-87.590419</td>
      <td>Build Coffee</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>41.784296</td>
      <td>-87.590790</td>
      <td>61st Street Farmers' Market</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>41.786526</td>
      <td>-87.594458</td>
      <td>Midway Plaisance Park</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>41.787751</td>
      <td>-87.588782</td>
      <td>University of Chicago @ Midway Plaisance</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>41.784245</td>
      <td>-87.590372</td>
      <td>B'Gabs Goodies</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>41.786028</td>
      <td>-87.590035</td>
      <td>Plum Cafe at Chicago Press Building</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2</td>
      <td>41.784879</td>
      <td>-87.588799</td>
      <td>Jackson Towers Fitness</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>41.787729</td>
      <td>-87.588789</td>
      <td>Metra - 59th St (University of Chicago)</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2</td>
      <td>41.783368</td>
      <td>-87.586806</td>
      <td>Jackson Park Track &amp; Soccer Field</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>41.788219</td>
      <td>-87.590965</td>
      <td>Tiffin Cafe</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1</td>
      <td>41.788240</td>
      <td>-87.590804</td>
      <td>International House at the University of Chicago</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1</td>
      <td>41.787943</td>
      <td>-87.588315</td>
      <td>Divvy Station</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>41.782321</td>
      <td>-87.594810</td>
      <td>Huckleberry Park</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1</td>
      <td>41.787987</td>
      <td>-87.586560</td>
      <td>CTA Bus Stop 1513</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2</td>
      <td>41.780854</td>
      <td>-87.588451</td>
      <td>Leon's Barbecue</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2</td>
      <td>41.780869</td>
      <td>-87.588188</td>
      <td>Tres Original Pancakes</td>
    </tr>
  </tbody>
</table>
</div>



One of the most distance locations are two restuarants in one cluster group (green). Many woud have though the bus station may have been closer to the University of Chicago. Midway Plaisance Park is the closest data point to the college while the Huckleberry Park is one of the farthest.


```python
# create map
map_clusters = folium.Map(location=[chi_latitude, chi_longitude], zoom_start=16)

# set color scheme for the clusters
x = np.arange(kclusters)
ys = [i + x + (i*x)**2 for i in range(kclusters)]
colors_array = cm.rainbow(np.linspace(0, 1, len(ys)))
rainbow = [colors.rgb2hex(i) for i in colors_array]

# add markers to the map
markers_colors = []
for lat, lon, poi, cluster in zip(chi_df_with_clusters['Latitude'], chi_df_with_clusters['Longitude'], chi_df_with_clusters['Name'], chi_df_with_clusters['Cluster Labels']):
    label = folium.Popup(str(poi) + ' Cluster ' + str(cluster), parse_html=True)
    folium.CircleMarker(
        [lat, lon],
        radius=5,
        popup=label,
        color=rainbow[cluster-1],
        fill=True,
        fill_color=rainbow[cluster-1],
        fill_opacity=0.7).add_to(map_clusters)
       
map_clusters
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzIiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5MyA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5MycsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbNDEuNzg0OTc3LC04Ny41OTA1MjM3MTIzMDE3XSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHpvb206IDE2LAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbWF4Qm91bmRzOiBib3VuZHMsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBsYXllcnM6IFtdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgd29ybGRDb3B5SnVtcDogZmFsc2UsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBjcnM6IEwuQ1JTLkVQU0czODU3CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIH0pOwogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl81MzJhZWE1ZWY1MmE0YWQzYTg3MDgzNDRkZDE2MTIxOSA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgJ2h0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nJywKICAgICAgICAgICAgICAgIHsKICAiYXR0cmlidXRpb24iOiBudWxsLAogICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwKICAibWF4Wm9vbSI6IDE4LAogICJtaW5ab29tIjogMSwKICAibm9XcmFwIjogZmFsc2UsCiAgInN1YmRvbWFpbnMiOiAiYWJjIgp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMDY4NDZkMjVhNzAxNDI5NzljNzhlNGI3MzNiMmE1ZDcgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODQyODg0Nzg2NTUzNSwtODcuNTkwNDE5Mjc0MjM5MjRdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwZmZiNCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MGZmYjQiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNjliM2IzOGRiYTg4NDdlY2FhZmFmZTZhODhlNTVhMjEgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNjUzMTliYzA0MGRhNDZjYmFhMzRjNzNmODM1M2RhNTYgPSAkKCc8ZGl2IGlkPSJodG1sXzY1MzE5YmMwNDBkYTQ2Y2JhYTM0YzczZjgzNTNkYTU2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5CdWlsZCBDb2ZmZWUgQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF82OWIzYjM4ZGJhODg0N2VjYWFmYWZlNmE4OGU1NWEyMS5zZXRDb250ZW50KGh0bWxfNjUzMTliYzA0MGRhNDZjYmFhMzRjNzNmODM1M2RhNTYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMDY4NDZkMjVhNzAxNDI5NzljNzhlNGI3MzNiMmE1ZDcuYmluZFBvcHVwKHBvcHVwXzY5YjNiMzhkYmE4ODQ3ZWNhYWZhZmU2YTg4ZTU1YTIxKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzA2MWQ2NDk1YmNiNTQyNDlhZDVlMzEzN2ViZjgwY2ZhID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDEuNzg0Mjk2MDg5NTcyODU1LC04Ny41OTA3OTAzNjQ5ODE1OV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODBmZmI0IiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwZmZiNCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kOWY1NjdhNTM5MjE0OTMyOTU1NTgwNjczNTkyNzk2ZiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9lOTdmZjk2OTIzMjY0MWRlOTZhYjI0ZjZiOTc0MDBiZSA9ICQoJzxkaXYgaWQ9Imh0bWxfZTk3ZmY5NjkyMzI2NDFkZTk2YWIyNGY2Yjk3NDAwYmUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPjYxc3QgU3RyZWV0IEZhcm1lcnMmIzM5OyBNYXJrZXQgQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9kOWY1NjdhNTM5MjE0OTMyOTU1NTgwNjczNTkyNzk2Zi5zZXRDb250ZW50KGh0bWxfZTk3ZmY5NjkyMzI2NDFkZTk2YWIyNGY2Yjk3NDAwYmUpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMDYxZDY0OTViY2I1NDI0OWFkNWUzMTM3ZWJmODBjZmEuYmluZFBvcHVwKHBvcHVwX2Q5ZjU2N2E1MzkyMTQ5MzI5NTU1ODA2NzM1OTI3OTZmKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2Y0OWZjNWJmNTRkNjQzMThhNzNmODUzOGI2OGI4MTVkID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDEuNzg2NTI1NzY2Njg1NzA2LC04Ny41OTQ0NTc1MjkwNzYzMl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF85NmQ4YmRlYTRmOGY0OThjOWFkNjYwZjhmOGJiMTdiNiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9iNzRjZmUwZmUyOWQ0YmM2YTA4ZjVmODQxYWRlNzRhNCA9ICQoJzxkaXYgaWQ9Imh0bWxfYjc0Y2ZlMGZlMjlkNGJjNmEwOGY1Zjg0MWFkZTc0YTQiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk1pZHdheSBQbGFpc2FuY2UgUGFyayBDbHVzdGVyIDA8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzk2ZDhiZGVhNGY4ZjQ5OGM5YWQ2NjBmOGY4YmIxN2I2LnNldENvbnRlbnQoaHRtbF9iNzRjZmUwZmUyOWQ0YmM2YTA4ZjVmODQxYWRlNzRhNCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9mNDlmYzViZjU0ZDY0MzE4YTczZjg1MzhiNjhiODE1ZC5iaW5kUG9wdXAocG9wdXBfOTZkOGJkZWE0ZjhmNDk4YzlhZDY2MGY4ZjhiYjE3YjYpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZDMyOGVhOThhOTJhNDYxMTkxYTMwOGQxYTA1MGFhMDQgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODc3NTEzMDIwMjM3NjQsLTg3LjU4ODc4MjAwNDEwMDRdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwMDBmZiIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MDAwZmYiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOTNkMTM3ZjQxZmFlNDZlYTkyNzkwZWExZDI5MDQxYzIgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfMzlkZmE1OTVlNGU3NGQ1NWJiNzYzZWZhODk0OWEwYmIgPSAkKCc8ZGl2IGlkPSJodG1sXzM5ZGZhNTk1ZTRlNzRkNTViYjc2M2VmYTg5NDlhMGJiIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Vbml2ZXJzaXR5IG9mIENoaWNhZ28gQCBNaWR3YXkgUGxhaXNhbmNlIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOTNkMTM3ZjQxZmFlNDZlYTkyNzkwZWExZDI5MDQxYzIuc2V0Q29udGVudChodG1sXzM5ZGZhNTk1ZTRlNzRkNTViYjc2M2VmYTg5NDlhMGJiKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2QzMjhlYTk4YTkyYTQ2MTE5MWEzMDhkMWEwNTBhYTA0LmJpbmRQb3B1cChwb3B1cF85M2QxMzdmNDFmYWU0NmVhOTI3OTBlYTFkMjkwNDFjMik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8wNWQzNzA3ZjYxNmI0ODFjYTdkNzU5Zjc2NjY0NjE4OSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQxLjc4NDI0NTA5OTEyOTI3LC04Ny41OTAzNzE5NTUxNjE4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzkyOTllNzQzYjNjMDRmYzc4Y2FlY2MzZTViMzc3Nzc4ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzk0ZTE1N2IxZTRkOTRlNjE4NDcxZTZkODE4OTMzNzA2ID0gJCgnPGRpdiBpZD0iaHRtbF85NGUxNTdiMWU0ZDk0ZTYxODQ3MWU2ZDgxODkzMzcwNiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+QiYjMzk7R2FicyBHb29kaWVzIENsdXN0ZXIgMjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOTI5OWU3NDNiM2MwNGZjNzhjYWVjYzNlNWIzNzc3Nzguc2V0Q29udGVudChodG1sXzk0ZTE1N2IxZTRkOTRlNjE4NDcxZTZkODE4OTMzNzA2KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzA1ZDM3MDdmNjE2YjQ4MWNhN2Q3NTlmNzY2NjQ2MTg5LmJpbmRQb3B1cChwb3B1cF85Mjk5ZTc0M2IzYzA0ZmM3OGNhZWNjM2U1YjM3Nzc3OCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81ODFkODljMmIyMjM0NDAyOWFmNDliMTM4NDAxNTE4NSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQxLjc4NjAyOCwtODcuNTkwMDM0OTY2NjY2NjZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwMDBmZiIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MDAwZmYiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNDIwYmM3Y2FmODRiNDlhNDk2NmQxMDQ0YzQyNjI5ZWUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNTk1NzA5MWE0M2Y4NGVmODg4NDBiYmVmZGMzM2ViYTEgPSAkKCc8ZGl2IGlkPSJodG1sXzU5NTcwOTFhNDNmODRlZjg4ODQwYmJlZmRjMzNlYmExIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5QbHVtIENhZmUgYXQgQ2hpY2FnbyBQcmVzcyBCdWlsZGluZyBDbHVzdGVyIDE8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzQyMGJjN2NhZjg0YjQ5YTQ5NjZkMTA0NGM0MjYyOWVlLnNldENvbnRlbnQoaHRtbF81OTU3MDkxYTQzZjg0ZWY4ODg0MGJiZWZkYzMzZWJhMSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl81ODFkODljMmIyMjM0NDAyOWFmNDliMTM4NDAxNTE4NS5iaW5kUG9wdXAocG9wdXBfNDIwYmM3Y2FmODRiNDlhNDk2NmQxMDQ0YzQyNjI5ZWUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfNmFiOTFkOGQ4MTcxNGVhZGI4ODk5M2QyYTZmODliMjMgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODQ4Nzg5MDc4Nzk0NzQsLTg3LjU4ODc5OTM3MDM3NTMzXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2E0NmU5ODk1NWFmNDQ2M2RhMjE0MWU3MDZiOTQxNDI1ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzQ4NTU0YjllMDVlYzQ0MTg4ZmIyNzAxZjk5ZDU5NjJmID0gJCgnPGRpdiBpZD0iaHRtbF80ODU1NGI5ZTA1ZWM0NDE4OGZiMjcwMWY5OWQ1OTYyZiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SmFja3NvbiBUb3dlcnMgRml0bmVzcyBDbHVzdGVyIDI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2E0NmU5ODk1NWFmNDQ2M2RhMjE0MWU3MDZiOTQxNDI1LnNldENvbnRlbnQoaHRtbF80ODU1NGI5ZTA1ZWM0NDE4OGZiMjcwMWY5OWQ1OTYyZik7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl82YWI5MWQ4ZDgxNzE0ZWFkYjg4OTkzZDJhNmY4OWIyMy5iaW5kUG9wdXAocG9wdXBfYTQ2ZTk4OTU1YWY0NDYzZGEyMTQxZTcwNmI5NDE0MjUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOWJjNmVhZGJkMTRiNDRjMWI1ZWQxMjJjM2ZlNjk2YTUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODc3Mjg4Njg1NjExMjUsLTg3LjU4ODc4ODcxMzczNF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODAwMGZmIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF8wODczNTljMjYyOGE0NDM3YWUwMDQzYWNkZWU4NzcyYSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF82MTUxM2NhYzliMzA0MTU3OTRmMGQxNmE1OGQwZGViOCA9ICQoJzxkaXYgaWQ9Imh0bWxfNjE1MTNjYWM5YjMwNDE1Nzk0ZjBkMTZhNThkMGRlYjgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPk1ldHJhIC0gNTl0aCBTdCAoVW5pdmVyc2l0eSBvZiBDaGljYWdvKSBDbHVzdGVyIDE8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzA4NzM1OWMyNjI4YTQ0MzdhZTAwNDNhY2RlZTg3NzJhLnNldENvbnRlbnQoaHRtbF82MTUxM2NhYzliMzA0MTU3OTRmMGQxNmE1OGQwZGViOCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl85YmM2ZWFkYmQxNGI0NGMxYjVlZDEyMmMzZmU2OTZhNS5iaW5kUG9wdXAocG9wdXBfMDg3MzU5YzI2MjhhNDQzN2FlMDA0M2FjZGVlODc3MmEpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfM2RmOGZmNDA2ZThjNGEzOThlZjFkYTNiZGE5ZjUzZDkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODMzNjc5OTk5OTk5OTYsLTg3LjU4NjgwNjAwMDAwMDAxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2E5ZTM2Mzk4N2FjMTQwOGY5ZTMxMjM2ODhlNDhlNGM4ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzU2NjVlNjNjODA3MTRjNDNhMWJjOGRjY2M2YWU2NzQ4ID0gJCgnPGRpdiBpZD0iaHRtbF81NjY1ZTYzYzgwNzE0YzQzYTFiYzhkY2NjNmFlNjc0OCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+SmFja3NvbiBQYXJrIFRyYWNrICZhbXA7IFNvY2NlciBGaWVsZCBDbHVzdGVyIDI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2E5ZTM2Mzk4N2FjMTQwOGY5ZTMxMjM2ODhlNDhlNGM4LnNldENvbnRlbnQoaHRtbF81NjY1ZTYzYzgwNzE0YzQzYTFiYzhkY2NjNmFlNjc0OCk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8zZGY4ZmY0MDZlOGM0YTM5OGVmMWRhM2JkYTlmNTNkOS5iaW5kUG9wdXAocG9wdXBfYTllMzYzOTg3YWMxNDA4ZjllMzEyMzY4OGU0OGU0YzgpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfZjVkY2RhNTQxMDhjNDI5YzhlMDcwZjAwNjFmNDMwZmEgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODgyMTk0NTE5MDQzLC04Ny41OTA5NjUyNzA5OTYxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MDAwZmYiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODAwMGZmIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2ViNGI5NWI2YWZiZDQ5NWRiYzFjYmZjZWQ1OGM3N2FiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2ZkM2JiOTA0NTI1MTRiYWQ4MjMzMzQ0MzZmNzlkYzA0ID0gJCgnPGRpdiBpZD0iaHRtbF9mZDNiYjkwNDUyNTE0YmFkODIzMzM0NDM2Zjc5ZGMwNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VGlmZmluIENhZmUgQ2x1c3RlciAxPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9lYjRiOTViNmFmYmQ0OTVkYmMxY2JmY2VkNThjNzdhYi5zZXRDb250ZW50KGh0bWxfZmQzYmI5MDQ1MjUxNGJhZDgyMzMzNDQzNmY3OWRjMDQpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfZjVkY2RhNTQxMDhjNDI5YzhlMDcwZjAwNjFmNDMwZmEuYmluZFBvcHVwKHBvcHVwX2ViNGI5NWI2YWZiZDQ5NWRiYzFjYmZjZWQ1OGM3N2FiKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2YwNjgzNGFiODE5OTRiNmQ5ODQ5MGNkMDVlZTE1MWM1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDEuNzg4MjQsLTg3LjU5MDgwNF0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODAwMGZmIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9mODU3ZDAwNjdhZjU0NjdlOTIwY2E0NjZkZjU1NGUwZSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9mNmYyOWZkYWNhZTM0N2FmOGM3MjIyMTBiNTMwMzg4NyA9ICQoJzxkaXYgaWQ9Imh0bWxfZjZmMjlmZGFjYWUzNDdhZjhjNzIyMjEwYjUzMDM4ODciIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkludGVybmF0aW9uYWwgSG91c2UgYXQgdGhlIFVuaXZlcnNpdHkgb2YgQ2hpY2FnbyBDbHVzdGVyIDE8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2Y4NTdkMDA2N2FmNTQ2N2U5MjBjYTQ2NmRmNTU0ZTBlLnNldENvbnRlbnQoaHRtbF9mNmYyOWZkYWNhZTM0N2FmOGM3MjIyMTBiNTMwMzg4Nyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9mMDY4MzRhYjgxOTk0YjZkOTg0OTBjZDA1ZWUxNTFjNS5iaW5kUG9wdXAocG9wdXBfZjg1N2QwMDY3YWY1NDY3ZTkyMGNhNDY2ZGY1NTRlMGUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfOGQxYmFjYjdhMzk3NDMzNDkxYmIyMTBlYzhkYTQ4MjcgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODc5NDI4MSwtODcuNTg4MzE1MTddLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwMDBmZiIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MDAwZmYiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMzA1NTA4N2Q0OGQ4NDA2OWEzZTIyMGMwN2JmYmMyN2UgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfZTVhOWEwYmE2NTNhNGNjZThlOTRiODIxZTYyMDEyN2IgPSAkKCc8ZGl2IGlkPSJodG1sX2U1YTlhMGJhNjUzYTRjY2U4ZTk0YjgyMWU2MjAxMjdiIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5EaXZ2eSBTdGF0aW9uIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMzA1NTA4N2Q0OGQ4NDA2OWEzZTIyMGMwN2JmYmMyN2Uuc2V0Q29udGVudChodG1sX2U1YTlhMGJhNjUzYTRjY2U4ZTk0YjgyMWU2MjAxMjdiKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzhkMWJhY2I3YTM5NzQzMzQ5MWJiMjEwZWM4ZGE0ODI3LmJpbmRQb3B1cChwb3B1cF8zMDU1MDg3ZDQ4ZDg0MDY5YTNlMjIwYzA3YmZiYzI3ZSk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl81NzNkMGViNTU1YWU0NmI0YmIzZjgzNGQyNDcwNmYwYSA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQxLjc4MjMyMTAzMTkwOTAyLC04Ny41OTQ4MDk1MzIxNjU1M10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF83OTEzYzkwNjU0NzY0NzhjYjUwZGRlMmZhYjhjM2Q1NCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8xODA1MGYyOWU3MTQ0N2U4ODcwY2U4OTg5YTRhMzljYSA9ICQoJzxkaXYgaWQ9Imh0bWxfMTgwNTBmMjllNzE0NDdlODg3MGNlODk4OWE0YTM5Y2EiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkh1Y2tsZWJlcnJ5IFBhcmsgQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF83OTEzYzkwNjU0NzY0NzhjYjUwZGRlMmZhYjhjM2Q1NC5zZXRDb250ZW50KGh0bWxfMTgwNTBmMjllNzE0NDdlODg3MGNlODk4OWE0YTM5Y2EpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNTczZDBlYjU1NWFlNDZiNGJiM2Y4MzRkMjQ3MDZmMGEuYmluZFBvcHVwKHBvcHVwXzc5MTNjOTA2NTQ3NjQ3OGNiNTBkZGUyZmFiOGMzZDU0KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzU0ZDFlNjNjYjUyNTQ0M2ViNzFjMGJiMTBjYjMyMGMxID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbNDEuNzg3OTg3LC04Ny41ODY1Nl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODAwMGZmIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwMDBmZiIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF80NWQ2ZDAwMDFkNmY0ZTQzYTkxYWZjMDJkYTQ5N2E5Myk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF85MmQyMjViZjhhZDQ0MTc4OGQxZTVkODAyODYwY2I3MiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9lMmM5ZWQ3NDEyMTE0ODZlOWI5NDlmN2Q4MDUwZDg5ZiA9ICQoJzxkaXYgaWQ9Imh0bWxfZTJjOWVkNzQxMjExNDg2ZTliOTQ5ZjdkODA1MGQ4OWYiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNUQSBCdXMgU3RvcCAxNTEzIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOTJkMjI1YmY4YWQ0NDE3ODhkMWU1ZDgwMjg2MGNiNzIuc2V0Q29udGVudChodG1sX2UyYzllZDc0MTIxMTQ4NmU5Yjk0OWY3ZDgwNTBkODlmKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzU0ZDFlNjNjYjUyNTQ0M2ViNzFjMGJiMTBjYjMyMGMxLmJpbmRQb3B1cChwb3B1cF85MmQyMjViZjhhZDQ0MTc4OGQxZTVkODAyODYwY2I3Mik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8zZmYxYjY5ZjkwMDE0NTU2ODYxOWM3ZmJmMTFkMjhiNCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzQxLjc4MDg1NCwtODcuNTg4NDUxXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzQ1ZDZkMDAwMWQ2ZjRlNDNhOTFhZmMwMmRhNDk3YTkzKTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzBiN2VlOWNjYjYzODQzMTE5YzQ3OGE2ZDk3MGI5OWViID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2ZlYjc2NjI1MDcwYTRkMDI5MWZlMTc1ZDY5MDQwOTgxID0gJCgnPGRpdiBpZD0iaHRtbF9mZWI3NjYyNTA3MGE0ZDAyOTFmZTE3NWQ2OTA0MDk4MSIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+TGVvbiYjMzk7cyBCYXJiZWN1ZSBDbHVzdGVyIDI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzBiN2VlOWNjYjYzODQzMTE5YzQ3OGE2ZDk3MGI5OWViLnNldENvbnRlbnQoaHRtbF9mZWI3NjYyNTA3MGE0ZDAyOTFmZTE3NWQ2OTA0MDk4MSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl8zZmYxYjY5ZjkwMDE0NTU2ODYxOWM3ZmJmMTFkMjhiNC5iaW5kUG9wdXAocG9wdXBfMGI3ZWU5Y2NiNjM4NDMxMTljNDc4YTZkOTcwYjk5ZWIpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTFlZGNhMmQzMmZjNGNmNGE2NTIxYmY1NWQzNzFkOTAgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFs0MS43ODA4Njg1MzAyNzM0NCwtODcuNTg4MTg4MTcxMzg2NzJdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwZmZiNCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MGZmYjQiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfNDVkNmQwMDAxZDZmNGU0M2E5MWFmYzAyZGE0OTdhOTMpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZTExYjAwNWEzZTlmNGM5YWE2MTAwOWYxOTFkNDQ5OGUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNmJjNTQ4NTg1ZTc1NGNhZmFkODZhODUzMDUwYWUyNDkgPSAkKCc8ZGl2IGlkPSJodG1sXzZiYzU0ODU4NWU3NTRjYWZhZDg2YTg1MzA1MGFlMjQ5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5UcmVzIE9yaWdpbmFsIFBhbmNha2VzIENsdXN0ZXIgMjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfZTExYjAwNWEzZTlmNGM5YWE2MTAwOWYxOTFkNDQ5OGUuc2V0Q29udGVudChodG1sXzZiYzU0ODU4NWU3NTRjYWZhZDg2YTg1MzA1MGFlMjQ5KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2ExZWRjYTJkMzJmYzRjZjRhNjUyMWJmNTVkMzcxZDkwLmJpbmRQb3B1cChwb3B1cF9lMTFiMDA1YTNlOWY0YzlhYTYxMDA5ZjE5MWQ0NDk4ZSk7CgogICAgICAgICAgICAKICAgICAgICAKPC9zY3JpcHQ+ onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>




```python
# set number of clusters
kclusters = 3

atl_df_clustering = atl_df.drop(['Name','Category Type'], 1)

# run k-means clustering
kmeans = KMeans(n_clusters=kclusters, random_state=0).fit(atl_df_clustering)

# check cluster labels generated for each row in the dataframe
kmeans.labels_[0:17]
```




    array([2, 2, 0, 2, 2, 0, 0, 0, 0, 0, 2, 0, 0, 0, 1, 0, 0], dtype=int32)



We then need to create a new dataframe with the clusters.


```python
atl_df_merged = atl_df_clustering
atl_df_merged.insert(0, 'Cluster Labels', kmeans.labels_)
name_column = atl_df['Name']
atl_df_with_clusters = pd.concat([atl_df_merged,name_column], axis = 1)
atl_df_with_clusters
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
      <th>Cluster Labels</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2</td>
      <td>33.770980</td>
      <td>-84.398037</td>
      <td>Coca-Cola Mainstreet @ AOC</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>33.772646</td>
      <td>-84.394585</td>
      <td>Highland Bakery</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>33.774820</td>
      <td>-84.399194</td>
      <td>Ferst Center For The Arts</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>33.771146</td>
      <td>-84.395785</td>
      <td>Hampton Inn by Hilton</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2</td>
      <td>33.771179</td>
      <td>-84.396202</td>
      <td>T-Mobile</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>33.772548</td>
      <td>-84.398430</td>
      <td>Wells Fargo</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>33.773673</td>
      <td>-84.398203</td>
      <td>Chick-fil-A</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0</td>
      <td>33.774261</td>
      <td>-84.396411</td>
      <td>Starbucks</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0</td>
      <td>33.773779</td>
      <td>-84.398137</td>
      <td>Panda Express</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0</td>
      <td>33.773898</td>
      <td>-84.398869</td>
      <td>Under The Couch</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2</td>
      <td>33.773019</td>
      <td>-84.395299</td>
      <td>Harrison Square</td>
    </tr>
    <tr>
      <th>11</th>
      <td>0</td>
      <td>33.773780</td>
      <td>-84.398206</td>
      <td>Taco Bell</td>
    </tr>
    <tr>
      <th>12</th>
      <td>0</td>
      <td>33.773770</td>
      <td>-84.398083</td>
      <td>Burdell's</td>
    </tr>
    <tr>
      <th>13</th>
      <td>0</td>
      <td>33.774428</td>
      <td>-84.396552</td>
      <td>Rooftop Garden</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1</td>
      <td>33.771246</td>
      <td>-84.392037</td>
      <td>GT Stinger Stop - Techwood and North Ave</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0</td>
      <td>33.774451</td>
      <td>-84.398904</td>
      <td>Student Center Food Court</td>
    </tr>
    <tr>
      <th>16</th>
      <td>0</td>
      <td>33.774428</td>
      <td>-84.398808</td>
      <td>Dunkin'</td>
    </tr>
    <tr>
      <th>17</th>
      <td>0</td>
      <td>33.775224</td>
      <td>-84.397190</td>
      <td>Einstein Statue</td>
    </tr>
  </tbody>
</table>
</div>



As you can see with the clusters, the prediction was correct that near Georgia Institute of Technology there is shopping enter based on the venues. There was a color coordinated data points and one outlier was present based on the map which is location GT Stringer Shop in its own cluster group as one data point.


```python
# create map
map_clusters = folium.Map(location=[atl_latitude, atl_longitude], zoom_start=16)

# set color scheme for the clusters
x = np.arange(kclusters)
ys = [i + x + (i*x)**2 for i in range(kclusters)]
colors_array = cm.rainbow(np.linspace(0, 1, len(ys)))
rainbow = [colors.rgb2hex(i) for i in colors_array]

# add markers to the map
markers_colors = []
for lat, lon, poi, cluster in zip(atl_df_with_clusters['Latitude'], atl_df_with_clusters['Longitude'], atl_df_with_clusters['Name'], atl_df_with_clusters['Cluster Labels']):
    label = folium.Popup(str(poi) + ' Cluster ' + str(cluster), parse_html=True)
    folium.CircleMarker(
        [lat, lon],
        radius=5,
        popup=label,
        color=rainbow[cluster-1],
        fill=True,
        fill_color=rainbow[cluster-1],
        fill_opacity=0.7).add_to(map_clusters)
       
map_clusters
```




<div style="width:100%;"><div style="position:relative;width:100%;height:0;padding-bottom:60%;"><span style="color:#565656">Make this Notebook Trusted to load map: File -> Trust Notebook</span><iframe src="about:blank" style="position:absolute;width:100%;height:100%;left:0;top:0;border:none !important;" data-html=PCFET0NUWVBFIGh0bWw+CjxoZWFkPiAgICAKICAgIDxtZXRhIGh0dHAtZXF1aXY9ImNvbnRlbnQtdHlwZSIgY29udGVudD0idGV4dC9odG1sOyBjaGFyc2V0PVVURi04IiAvPgogICAgPHNjcmlwdD5MX1BSRUZFUl9DQU5WQVMgPSBmYWxzZTsgTF9OT19UT1VDSCA9IGZhbHNlOyBMX0RJU0FCTEVfM0QgPSBmYWxzZTs8L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmpzIj48L3NjcmlwdD4KICAgIDxzY3JpcHQgc3JjPSJodHRwczovL2FqYXguZ29vZ2xlYXBpcy5jb20vYWpheC9saWJzL2pxdWVyeS8xLjExLjEvanF1ZXJ5Lm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvanMvYm9vdHN0cmFwLm1pbi5qcyI+PC9zY3JpcHQ+CiAgICA8c2NyaXB0IHNyYz0iaHR0cHM6Ly9jZG5qcy5jbG91ZGZsYXJlLmNvbS9hamF4L2xpYnMvTGVhZmxldC5hd2Vzb21lLW1hcmtlcnMvMi4wLjIvbGVhZmxldC5hd2Vzb21lLW1hcmtlcnMuanMiPjwvc2NyaXB0PgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2Nkbi5qc2RlbGl2ci5uZXQvbnBtL2xlYWZsZXRAMS4yLjAvZGlzdC9sZWFmbGV0LmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL21heGNkbi5ib290c3RyYXBjZG4uY29tL2Jvb3RzdHJhcC8zLjIuMC9jc3MvYm9vdHN0cmFwLm1pbi5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9tYXhjZG4uYm9vdHN0cmFwY2RuLmNvbS9ib290c3RyYXAvMy4yLjAvY3NzL2Jvb3RzdHJhcC10aGVtZS5taW4uY3NzIi8+CiAgICA8bGluayByZWw9InN0eWxlc2hlZXQiIGhyZWY9Imh0dHBzOi8vbWF4Y2RuLmJvb3RzdHJhcGNkbi5jb20vZm9udC1hd2Vzb21lLzQuNi4zL2Nzcy9mb250LWF3ZXNvbWUubWluLmNzcyIvPgogICAgPGxpbmsgcmVsPSJzdHlsZXNoZWV0IiBocmVmPSJodHRwczovL2NkbmpzLmNsb3VkZmxhcmUuY29tL2FqYXgvbGlicy9MZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy8yLjAuMi9sZWFmbGV0LmF3ZXNvbWUtbWFya2Vycy5jc3MiLz4KICAgIDxsaW5rIHJlbD0ic3R5bGVzaGVldCIgaHJlZj0iaHR0cHM6Ly9yYXdnaXQuY29tL3B5dGhvbi12aXN1YWxpemF0aW9uL2ZvbGl1bS9tYXN0ZXIvZm9saXVtL3RlbXBsYXRlcy9sZWFmbGV0LmF3ZXNvbWUucm90YXRlLmNzcyIvPgogICAgPHN0eWxlPmh0bWwsIGJvZHkge3dpZHRoOiAxMDAlO2hlaWdodDogMTAwJTttYXJnaW46IDA7cGFkZGluZzogMDt9PC9zdHlsZT4KICAgIDxzdHlsZT4jbWFwIHtwb3NpdGlvbjphYnNvbHV0ZTt0b3A6MDtib3R0b206MDtyaWdodDowO2xlZnQ6MDt9PC9zdHlsZT4KICAgIAogICAgICAgICAgICA8c3R5bGU+ICNtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUgewogICAgICAgICAgICAgICAgcG9zaXRpb24gOiByZWxhdGl2ZTsKICAgICAgICAgICAgICAgIHdpZHRoIDogMTAwLjAlOwogICAgICAgICAgICAgICAgaGVpZ2h0OiAxMDAuMCU7CiAgICAgICAgICAgICAgICBsZWZ0OiAwLjAlOwogICAgICAgICAgICAgICAgdG9wOiAwLjAlOwogICAgICAgICAgICAgICAgfQogICAgICAgICAgICA8L3N0eWxlPgogICAgICAgIAo8L2hlYWQ+Cjxib2R5PiAgICAKICAgIAogICAgICAgICAgICA8ZGl2IGNsYXNzPSJmb2xpdW0tbWFwIiBpZD0ibWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1IiA+PC9kaXY+CiAgICAgICAgCjwvYm9keT4KPHNjcmlwdD4gICAgCiAgICAKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGJvdW5kcyA9IG51bGw7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgdmFyIG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSA9IEwubWFwKAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgJ21hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NScsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICB7Y2VudGVyOiBbMzMuNzcxMzUyNiwtODQuMzk2MzQ1XSwKICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIHpvb206IDE2LAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgbWF4Qm91bmRzOiBib3VuZHMsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBsYXllcnM6IFtdLAogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgd29ybGRDb3B5SnVtcDogZmFsc2UsCiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICBjcnM6IEwuQ1JTLkVQU0czODU3CiAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgIH0pOwogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgdGlsZV9sYXllcl83ZDY0YWEzYmVlZGI0ZjE3ODU1OWFhNTllODRhZTk0NSA9IEwudGlsZUxheWVyKAogICAgICAgICAgICAgICAgJ2h0dHBzOi8ve3N9LnRpbGUub3BlbnN0cmVldG1hcC5vcmcve3p9L3t4fS97eX0ucG5nJywKICAgICAgICAgICAgICAgIHsKICAiYXR0cmlidXRpb24iOiBudWxsLAogICJkZXRlY3RSZXRpbmEiOiBmYWxzZSwKICAibWF4Wm9vbSI6IDE4LAogICJtaW5ab29tIjogMSwKICAibm9XcmFwIjogZmFsc2UsCiAgInN1YmRvbWFpbnMiOiAiYWJjIgp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYTJhNTc4ZTlmMTM0NDFlNzlhOTVlMDcwNGE1OWVmNTkgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFszMy43NzA5Nzk5ODQxNjM0LC04NC4zOTgwMzY3Njc4NTA4MV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODBmZmI0IiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwZmZiNCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9iMmMyYWJjY2ZmZGE0NWIxYjcwNDRjZjk0NTM0YTE2ZiA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9lZTFjNTkwZDUyN2Q0MmRiOGM1Y2JlZTM4NmEyNWQwZSA9ICQoJzxkaXYgaWQ9Imh0bWxfZWUxYzU5MGQ1MjdkNDJkYjhjNWNiZWUzODZhMjVkMGUiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNvY2EtQ29sYSBNYWluc3RyZWV0IEAgQU9DIENsdXN0ZXIgMjwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYjJjMmFiY2NmZmRhNDViMWI3MDQ0Y2Y5NDUzNGExNmYuc2V0Q29udGVudChodG1sX2VlMWM1OTBkNTI3ZDQyZGI4YzVjYmVlMzg2YTI1ZDBlKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2EyYTU3OGU5ZjEzNDQxZTc5YTk1ZTA3MDRhNTllZjU5LmJpbmRQb3B1cChwb3B1cF9iMmMyYWJjY2ZmZGE0NWIxYjcwNDRjZjk0NTM0YTE2Zik7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl9lYjA2YmViZmM4Mjk0NmYzOGU3NmJmZTQ0OTFkNTM2MCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzMzLjc3MjY0NjEwNDgxMTE1LC04NC4zOTQ1ODU0OTAyMjY3NV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjODBmZmI0IiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiIzgwZmZiNCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9lZGY0ZTgwMjgxMzk0ZGJkODA2YzQ4YmUwZTM5N2NmOSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF85NDIzYzg1MzU1MTE0NGEyOThiZjUwMGRmNDI0NmJhOSA9ICQoJzxkaXYgaWQ9Imh0bWxfOTQyM2M4NTM1NTExNDRhMjk4YmY1MDBkZjQyNDZiYTkiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkhpZ2hsYW5kIEJha2VyeSBDbHVzdGVyIDI8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2VkZjRlODAyODEzOTRkYmQ4MDZjNDhiZTBlMzk3Y2Y5LnNldENvbnRlbnQoaHRtbF85NDIzYzg1MzU1MTE0NGEyOThiZjUwMGRmNDI0NmJhOSk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9lYjA2YmViZmM4Mjk0NmYzOGU3NmJmZTQ0OTFkNTM2MC5iaW5kUG9wdXAocG9wdXBfZWRmNGU4MDI4MTM5NGRiZDgwNmM0OGJlMGUzOTdjZjkpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYzI5OTYzNGY4YWRlNDUxZTg3ZTFjYzQ1OTY5YmVhY2UgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFszMy43NzQ4MTk4NzY1MTkxNzQsLTg0LjM5OTE5MzU2NDgxNzIyXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2EyMzA3YjkwMzAxNDQxNTU4MzRjNTM3YjMzOTI2MjFmID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2JmYTJiOWY1MDJmOTQyMTM5Nzk4NTQyYjhmZGQ2NWU3ID0gJCgnPGRpdiBpZD0iaHRtbF9iZmEyYjlmNTAyZjk0MjEzOTc5ODU0MmI4ZmRkNjVlNyIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RmVyc3QgQ2VudGVyIEZvciBUaGUgQXJ0cyBDbHVzdGVyIDA8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2EyMzA3YjkwMzAxNDQxNTU4MzRjNTM3YjMzOTI2MjFmLnNldENvbnRlbnQoaHRtbF9iZmEyYjlmNTAyZjk0MjEzOTc5ODU0MmI4ZmRkNjVlNyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl9jMjk5NjM0ZjhhZGU0NTFlODdlMWNjNDU5NjliZWFjZS5iaW5kUG9wdXAocG9wdXBfYTIzMDdiOTAzMDE0NDE1NTgzNGM1MzdiMzM5MjYyMWYpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfODk5MjhlNzhiODNjNDllMGJmMTA0YjVlMzhjMTMwMmUgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFszMy43NzExNDU2NjI1MzU2OCwtODQuMzk1Nzg1MTExOTczOTZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwZmZiNCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MGZmYjQiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMGI4MTczYTMyMzI2NGJhNWI5OWEyNDY3NDcyZjJjZDcgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNDhkMjU3MTQ1OWM3NGY1MThlM2MyMjM3N2IxMWE3NGYgPSAkKCc8ZGl2IGlkPSJodG1sXzQ4ZDI1NzE0NTljNzRmNTE4ZTNjMjIzNzdiMTFhNzRmIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IYW1wdG9uIElubiBieSBIaWx0b24gQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8wYjgxNzNhMzIzMjY0YmE1Yjk5YTI0Njc0NzJmMmNkNy5zZXRDb250ZW50KGh0bWxfNDhkMjU3MTQ1OWM3NGY1MThlM2MyMjM3N2IxMWE3NGYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfODk5MjhlNzhiODNjNDllMGJmMTA0YjVlMzhjMTMwMmUuYmluZFBvcHVwKHBvcHVwXzBiODE3M2EzMjMyNjRiYTViOTlhMjQ2NzQ3MmYyY2Q3KTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzk3ZjI2MTAwZGI2NjQ5MjdhYzhkNDhhZjkzMWYxMDJmID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzcxMTc5MTk5MjE4NzUsLTg0LjM5NjIwMjA4NzQwMjM0XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiM4MGZmYjQiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjODBmZmI0IiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzc1ZmExZjQzNjFmNzRjNzY5MTM1OGYwMTZiOGFkNzhiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzVmMGEwNGM0Mjg4YjRiYWJiZTM5ZjJmYWVmOGRmM2E2ID0gJCgnPGRpdiBpZD0iaHRtbF81ZjBhMDRjNDI4OGI0YmFiYmUzOWYyZmFlZjhkZjNhNiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+VC1Nb2JpbGUgQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF83NWZhMWY0MzYxZjc0Yzc2OTEzNThmMDE2YjhhZDc4Yi5zZXRDb250ZW50KGh0bWxfNWYwYTA0YzQyODhiNGJhYmJlMzlmMmZhZWY4ZGYzYTYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfOTdmMjYxMDBkYjY2NDkyN2FjOGQ0OGFmOTMxZjEwMmYuYmluZFBvcHVwKHBvcHVwXzc1ZmExZjQzNjFmNzRjNzY5MTM1OGYwMTZiOGFkNzhiKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzJlZGYyMjI5YWE2ZDQxNzZiZGQ0YjViYmFmN2FhMTllID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzcyNTQ4NDY1MzQyMTgsLTg0LjM5ODQzMDQyNTQxNTQ4XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzM0ZWYzNWNkOWRhMDQ4MDM4MmU5NTZmYjVmYWQ0ODFiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzc2NTY2ZjRhYzE3YTQyZDk4NzAyNDdhYjY5MmI2YzE0ID0gJCgnPGRpdiBpZD0iaHRtbF83NjU2NmY0YWMxN2E0MmQ5ODcwMjQ3YWI2OTJiNmMxNCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+V2VsbHMgRmFyZ28gQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8zNGVmMzVjZDlkYTA0ODAzODJlOTU2ZmI1ZmFkNDgxYi5zZXRDb250ZW50KGh0bWxfNzY1NjZmNGFjMTdhNDJkOTg3MDI0N2FiNjkyYjZjMTQpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMmVkZjIyMjlhYTZkNDE3NmJkZDRiNWJiYWY3YWExOWUuYmluZFBvcHVwKHBvcHVwXzM0ZWYzNWNkOWRhMDQ4MDM4MmU5NTZmYjVmYWQ0ODFiKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2I2NzlhMmYwYTljNzQ5YThhZmQ1OTk2NjQ4YzQwZmQyID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzczNjczMiwtODQuMzk4MjAyN10sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF81Mzk0NDM3YmZkMWM0OTdhYjU3NWIzMjc5ZGQ3MjhlNCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF9mMDQ4ZTk5YzMzMGI0YmNkOWQyYjE5ODFiYzRmM2Y3YiA9ICQoJzxkaXYgaWQ9Imh0bWxfZjA0OGU5OWMzMzBiNGJjZDlkMmIxOTgxYmM0ZjNmN2IiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkNoaWNrLWZpbC1BIENsdXN0ZXIgMDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfNTM5NDQzN2JmZDFjNDk3YWI1NzViMzI3OWRkNzI4ZTQuc2V0Q29udGVudChodG1sX2YwNDhlOTljMzMwYjRiY2Q5ZDJiMTk4MWJjNGYzZjdiKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2I2NzlhMmYwYTljNzQ5YThhZmQ1OTk2NjQ4YzQwZmQyLmJpbmRQb3B1cChwb3B1cF81Mzk0NDM3YmZkMWM0OTdhYjU3NWIzMjc5ZGQ3MjhlNCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8yYjZmNjgyMzI5YWM0ZTk3OTlhODkwMWU0Njk3OTJiMCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzMzLjc3NDI2MSwtODQuMzk2NDExXSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2E3YTg3M2YwNDY3ZTRhMDNhM2ZjZmE2MjFhMmQ1MjNjID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzljYTE3MGQzN2UxODQ3NDNiNTQyNjZmY2FmMmQ2YjdmID0gJCgnPGRpdiBpZD0iaHRtbF85Y2ExNzBkMzdlMTg0NzQzYjU0MjY2ZmNhZjJkNmI3ZiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+U3RhcmJ1Y2tzIENsdXN0ZXIgMDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYTdhODczZjA0NjdlNGEwM2EzZmNmYTYyMWEyZDUyM2Muc2V0Q29udGVudChodG1sXzljYTE3MGQzN2UxODQ3NDNiNTQyNjZmY2FmMmQ2YjdmKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzJiNmY2ODIzMjlhYzRlOTc5OWE4OTAxZTQ2OTc5MmIwLmJpbmRQb3B1cChwb3B1cF9hN2E4NzNmMDQ2N2U0YTAzYTNmY2ZhNjIxYTJkNTIzYyk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl8xYmFkODgwNTQ2NDU0MjNlYTU5OGI0M2VkZjBlNGJmZiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzMzLjc3Mzc3OTQ5Mjg5MzA1NSwtODQuMzk4MTM2Njg5ODE2MTFdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiI2ZmMDAwMCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiNmZjAwMDAiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfOTM3YjM4MTlhYTRmNDgwZmJjOGRkMmEwM2I2YWRiZDAgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNjU3ZTdkNjMxYjRiNGE3NTliZWExZTIxMWM5NWQ2ODAgPSAkKCc8ZGl2IGlkPSJodG1sXzY1N2U3ZDYzMWI0YjRhNzU5YmVhMWUyMTFjOTVkNjgwIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5QYW5kYSBFeHByZXNzIENsdXN0ZXIgMDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfOTM3YjM4MTlhYTRmNDgwZmJjOGRkMmEwM2I2YWRiZDAuc2V0Q29udGVudChodG1sXzY1N2U3ZDYzMWI0YjRhNzU5YmVhMWUyMTFjOTVkNjgwKTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzFiYWQ4ODA1NDY0NTQyM2VhNTk4YjQzZWRmMGU0YmZmLmJpbmRQb3B1cChwb3B1cF85MzdiMzgxOWFhNGY0ODBmYmM4ZGQyYTAzYjZhZGJkMCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl80NTUyMjU2MDFiMTE0NzA4ODFlNjRhMTEyMmYyZDZmNiA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzMzLjc3Mzg5ODIwODgwMDc0NSwtODQuMzk4ODY5MDM3OTI4NTNdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiI2ZmMDAwMCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiNmZjAwMDAiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfNTMzN2MwYTRlYzE5NDA1YmFmYzNhNjNiODIzYTQ3NGYgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfYWFlMjhkMTkwZDM3NGFlMzk3MDI3MTRiMzhlNmM1ZjYgPSAkKCc8ZGl2IGlkPSJodG1sX2FhZTI4ZDE5MGQzNzRhZTM5NzAyNzE0YjM4ZTZjNWY2IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5VbmRlciBUaGUgQ291Y2ggQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF81MzM3YzBhNGVjMTk0MDViYWZjM2E2M2I4MjNhNDc0Zi5zZXRDb250ZW50KGh0bWxfYWFlMjhkMTkwZDM3NGFlMzk3MDI3MTRiMzhlNmM1ZjYpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNDU1MjI1NjAxYjExNDcwODgxZTY0YTExMjJmMmQ2ZjYuYmluZFBvcHVwKHBvcHVwXzUzMzdjMGE0ZWMxOTQwNWJhZmMzYTYzYjgyM2E0NzRmKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyX2NiYmJhY2Y4MWE1MjQ0NTJhMDY4OTQ3OWEzMzg1YjE3ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzczMDE4NzE3NzY1ODEsLTg0LjM5NTI5ODk1NzgyNDddLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwZmZiNCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MGZmYjQiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfZDZmNTVmY2I0YWI2NDg0OTk2ZWJlOWJhNTFmYjBjODEgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfOWVjMmFjMzFlZDRhNDllNzhhOGZhZjU0Y2Q4NTE0NWEgPSAkKCc8ZGl2IGlkPSJodG1sXzllYzJhYzMxZWQ0YTQ5ZTc4YThmYWY1NGNkODUxNDVhIiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5IYXJyaXNvbiBTcXVhcmUgQ2x1c3RlciAyPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9kNmY1NWZjYjRhYjY0ODQ5OTZlYmU5YmE1MWZiMGM4MS5zZXRDb250ZW50KGh0bWxfOWVjMmFjMzFlZDRhNDllNzhhOGZhZjU0Y2Q4NTE0NWEpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfY2JiYmFjZjgxYTUyNDQ1MmEwNjg5NDc5YTMzODViMTcuYmluZFBvcHVwKHBvcHVwX2Q2ZjU1ZmNiNGFiNjQ4NDk5NmViZTliYTUxZmIwYzgxKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzgzMzY5ZDY5YmUxZDQ4ZmNhMDJjNGNhYjc2NzM3MzYwID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzczNzgwMTg0NTk0MTQ1LC04NC4zOTgyMDU5NzQ3NDUzMV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9jMmVhNGViNjUwNTg0ZTVlOWE4YzJhMzQ5NmQ1NzhhOSA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF82ZWJjMmY0YzhiNTU0NTA4OWIwNDMzZDg0MjA4NDhhMyA9ICQoJzxkaXYgaWQ9Imh0bWxfNmViYzJmNGM4YjU1NDUwODliMDQzM2Q4NDIwODQ4YTMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlRhY28gQmVsbCBDbHVzdGVyIDA8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwX2MyZWE0ZWI2NTA1ODRlNWU5YThjMmEzNDk2ZDU3OGE5LnNldENvbnRlbnQoaHRtbF82ZWJjMmY0YzhiNTU0NTA4OWIwNDMzZDg0MjA4NDhhMyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl84MzM2OWQ2OWJlMWQ0OGZjYTAyYzRjYWI3NjczNzM2MC5iaW5kUG9wdXAocG9wdXBfYzJlYTRlYjY1MDU4NGU1ZTlhOGMyYTM0OTZkNTc4YTkpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfMmRjY2Q5NzkyOTRhNGJkMDkzZjFkODE5MTIyYmY1M2UgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFszMy43NzM3Njk1ODQ0MjU0MywtODQuMzk4MDgzMjI4Njk0Nl0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF8zODA1NThmZTM4YWM0YmMwODg3NWE1Mjk1MTJkYmQwZCA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF82NTQxNTBkOWQ5MjQ0ZjM4OThkZGNiNmMxZWU2ODY2YyA9ICQoJzxkaXYgaWQ9Imh0bWxfNjU0MTUwZDlkOTI0NGYzODk4ZGRjYjZjMWVlNjg2NmMiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPkJ1cmRlbGwmIzM5O3MgQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF8zODA1NThmZTM4YWM0YmMwODg3NWE1Mjk1MTJkYmQwZC5zZXRDb250ZW50KGh0bWxfNjU0MTUwZDlkOTI0NGYzODk4ZGRjYjZjMWVlNjg2NmMpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfMmRjY2Q5NzkyOTRhNGJkMDkzZjFkODE5MTIyYmY1M2UuYmluZFBvcHVwKHBvcHVwXzM4MDU1OGZlMzhhYzRiYzA4ODc1YTUyOTUxMmRiZDBkKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzdhMDQ5YTdlZGY3NjQwOTU4M2I1MWY5NTVjYmM0N2I1ID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzc0NDI4Mjg5OTcxMywtODQuMzk2NTUxODQyMjUwNDVdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiI2ZmMDAwMCIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiNmZjAwMDAiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMTQwODljMGE5ZTkyNDJhZWFiOTA2YWZhYjAzN2UzZGUgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfNGFkMjQ5NTc3YjY4NDZhNDk1NWQ4YTE5OTBjYzFmMDcgPSAkKCc8ZGl2IGlkPSJodG1sXzRhZDI0OTU3N2I2ODQ2YTQ5NTVkOGExOTkwY2MxZjA3IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5Sb29mdG9wIEdhcmRlbiBDbHVzdGVyIDA8L2Rpdj4nKVswXTsKICAgICAgICAgICAgICAgIHBvcHVwXzE0MDg5YzBhOWU5MjQyYWVhYjkwNmFmYWIwMzdlM2RlLnNldENvbnRlbnQoaHRtbF80YWQyNDk1NzdiNjg0NmE0OTU1ZDhhMTk5MGNjMWYwNyk7CiAgICAgICAgICAgIAoKICAgICAgICAgICAgY2lyY2xlX21hcmtlcl83YTA0OWE3ZWRmNzY0MDk1ODNiNTFmOTU1Y2JjNDdiNS5iaW5kUG9wdXAocG9wdXBfMTQwODljMGE5ZTkyNDJhZWFiOTA2YWZhYjAzN2UzZGUpOwoKICAgICAgICAgICAgCiAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIGNpcmNsZV9tYXJrZXJfYjI2YWZmZmU5YmU3NGRiNmJiOWU0NzhkNzhmNDJlZWIgPSBMLmNpcmNsZU1hcmtlcigKICAgICAgICAgICAgICAgIFszMy43NzEyNDU5MTMyNzgzMzUsLTg0LjM5MjAzNzM5MTY2MjZdLAogICAgICAgICAgICAgICAgewogICJidWJibGluZ01vdXNlRXZlbnRzIjogdHJ1ZSwKICAiY29sb3IiOiAiIzgwMDBmZiIsCiAgImRhc2hBcnJheSI6IG51bGwsCiAgImRhc2hPZmZzZXQiOiBudWxsLAogICJmaWxsIjogdHJ1ZSwKICAiZmlsbENvbG9yIjogIiM4MDAwZmYiLAogICJmaWxsT3BhY2l0eSI6IDAuNywKICAiZmlsbFJ1bGUiOiAiZXZlbm9kZCIsCiAgImxpbmVDYXAiOiAicm91bmQiLAogICJsaW5lSm9pbiI6ICJyb3VuZCIsCiAgIm9wYWNpdHkiOiAxLjAsCiAgInJhZGl1cyI6IDUsCiAgInN0cm9rZSI6IHRydWUsCiAgIndlaWdodCI6IDMKfQogICAgICAgICAgICAgICAgKS5hZGRUbyhtYXBfMjA0NWY5MGU4MWFlNDI2NGE4MDZkMDg1NDkzNTM0NjUpOwogICAgICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgcG9wdXBfMWQ2NzczNzZiNzY0NDkxNTk5NjViNTAzNWNiZjNlNWQgPSBMLnBvcHVwKHttYXhXaWR0aDogJzMwMCd9KTsKCiAgICAgICAgICAgIAogICAgICAgICAgICAgICAgdmFyIGh0bWxfMmYxMDkyN2FjZDA1NDBhYzkwMDkyMzY1YmUxYjEwNTkgPSAkKCc8ZGl2IGlkPSJodG1sXzJmMTA5MjdhY2QwNTQwYWM5MDA5MjM2NWJlMWIxMDU5IiBzdHlsZT0id2lkdGg6IDEwMC4wJTsgaGVpZ2h0OiAxMDAuMCU7Ij5HVCBTdGluZ2VyIFN0b3AgLSBUZWNod29vZCBhbmQgTm9ydGggQXZlIENsdXN0ZXIgMTwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfMWQ2NzczNzZiNzY0NDkxNTk5NjViNTAzNWNiZjNlNWQuc2V0Q29udGVudChodG1sXzJmMTA5MjdhY2QwNTQwYWM5MDA5MjM2NWJlMWIxMDU5KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyX2IyNmFmZmZlOWJlNzRkYjZiYjllNDc4ZDc4ZjQyZWViLmJpbmRQb3B1cChwb3B1cF8xZDY3NzM3NmI3NjQ0OTE1OTk2NWI1MDM1Y2JmM2U1ZCk7CgogICAgICAgICAgICAKICAgICAgICAKICAgIAogICAgICAgICAgICB2YXIgY2lyY2xlX21hcmtlcl83N2JjNTNjNjUzYzc0MjdiYjk5MjNkZmM0ODViZWU5OCA9IEwuY2lyY2xlTWFya2VyKAogICAgICAgICAgICAgICAgWzMzLjc3NDQ1MDkxMDg5OTMyLC04NC4zOTg5MDQzNTg0MTk1MV0sCiAgICAgICAgICAgICAgICB7CiAgImJ1YmJsaW5nTW91c2VFdmVudHMiOiB0cnVlLAogICJjb2xvciI6ICIjZmYwMDAwIiwKICAiZGFzaEFycmF5IjogbnVsbCwKICAiZGFzaE9mZnNldCI6IG51bGwsCiAgImZpbGwiOiB0cnVlLAogICJmaWxsQ29sb3IiOiAiI2ZmMDAwMCIsCiAgImZpbGxPcGFjaXR5IjogMC43LAogICJmaWxsUnVsZSI6ICJldmVub2RkIiwKICAibGluZUNhcCI6ICJyb3VuZCIsCiAgImxpbmVKb2luIjogInJvdW5kIiwKICAib3BhY2l0eSI6IDEuMCwKICAicmFkaXVzIjogNSwKICAic3Ryb2tlIjogdHJ1ZSwKICAid2VpZ2h0IjogMwp9CiAgICAgICAgICAgICAgICApLmFkZFRvKG1hcF8yMDQ1ZjkwZTgxYWU0MjY0YTgwNmQwODU0OTM1MzQ2NSk7CiAgICAgICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBwb3B1cF9kNGY0YTQyN2EzMTQ0OTM0ODI5MDk1MzQwNDMxZmUxMyA9IEwucG9wdXAoe21heFdpZHRoOiAnMzAwJ30pOwoKICAgICAgICAgICAgCiAgICAgICAgICAgICAgICB2YXIgaHRtbF8wZmU5OGI2MmVjMTI0MDQ4YWJjOGU1M2Q3OGQ5YmQxOCA9ICQoJzxkaXYgaWQ9Imh0bWxfMGZlOThiNjJlYzEyNDA0OGFiYzhlNTNkNzhkOWJkMTgiIHN0eWxlPSJ3aWR0aDogMTAwLjAlOyBoZWlnaHQ6IDEwMC4wJTsiPlN0dWRlbnQgQ2VudGVyIEZvb2QgQ291cnQgQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF9kNGY0YTQyN2EzMTQ0OTM0ODI5MDk1MzQwNDMxZmUxMy5zZXRDb250ZW50KGh0bWxfMGZlOThiNjJlYzEyNDA0OGFiYzhlNTNkNzhkOWJkMTgpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNzdiYzUzYzY1M2M3NDI3YmI5OTIzZGZjNDg1YmVlOTguYmluZFBvcHVwKHBvcHVwX2Q0ZjRhNDI3YTMxNDQ5MzQ4MjkwOTUzNDA0MzFmZTEzKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzZkOGVlZGUzNTZlNzRlZWRiYzYyMjQ1ZGIyN2FkMzYzID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzc0NDI3OTEzOTI4OTEsLTg0LjM5ODgwODEyMjgwNzQ1XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwXzZkMzAxNWMzYWYzYjQyNzdhNjkyNTFmZjkzMjdjMGFiID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sX2I5ZDY5MGQxZTZiMjQzNTE4ZmNiZWE3MWFiNWE1YzRiID0gJCgnPGRpdiBpZD0iaHRtbF9iOWQ2OTBkMWU2YjI0MzUxOGZjYmVhNzFhYjVhNWM0YiIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RHVua2luJiMzOTsgQ2x1c3RlciAwPC9kaXY+JylbMF07CiAgICAgICAgICAgICAgICBwb3B1cF82ZDMwMTVjM2FmM2I0Mjc3YTY5MjUxZmY5MzI3YzBhYi5zZXRDb250ZW50KGh0bWxfYjlkNjkwZDFlNmIyNDM1MThmY2JlYTcxYWI1YTVjNGIpOwogICAgICAgICAgICAKCiAgICAgICAgICAgIGNpcmNsZV9tYXJrZXJfNmQ4ZWVkZTM1NmU3NGVlZGJjNjIyNDVkYjI3YWQzNjMuYmluZFBvcHVwKHBvcHVwXzZkMzAxNWMzYWYzYjQyNzdhNjkyNTFmZjkzMjdjMGFiKTsKCiAgICAgICAgICAgIAogICAgICAgIAogICAgCiAgICAgICAgICAgIHZhciBjaXJjbGVfbWFya2VyXzhlMDdmM2Q5MjZkYTQxY2VhYmFjODc5Mzc3ZGQ1NDZiID0gTC5jaXJjbGVNYXJrZXIoCiAgICAgICAgICAgICAgICBbMzMuNzc1MjIzOTQ1NTE0NzQsLTg0LjM5NzE4OTkzMzQyNDk3XSwKICAgICAgICAgICAgICAgIHsKICAiYnViYmxpbmdNb3VzZUV2ZW50cyI6IHRydWUsCiAgImNvbG9yIjogIiNmZjAwMDAiLAogICJkYXNoQXJyYXkiOiBudWxsLAogICJkYXNoT2Zmc2V0IjogbnVsbCwKICAiZmlsbCI6IHRydWUsCiAgImZpbGxDb2xvciI6ICIjZmYwMDAwIiwKICAiZmlsbE9wYWNpdHkiOiAwLjcsCiAgImZpbGxSdWxlIjogImV2ZW5vZGQiLAogICJsaW5lQ2FwIjogInJvdW5kIiwKICAibGluZUpvaW4iOiAicm91bmQiLAogICJvcGFjaXR5IjogMS4wLAogICJyYWRpdXMiOiA1LAogICJzdHJva2UiOiB0cnVlLAogICJ3ZWlnaHQiOiAzCn0KICAgICAgICAgICAgICAgICkuYWRkVG8obWFwXzIwNDVmOTBlODFhZTQyNjRhODA2ZDA4NTQ5MzUzNDY1KTsKICAgICAgICAgICAgCiAgICAKICAgICAgICAgICAgdmFyIHBvcHVwX2FjYzAxYmVkNzJkNTQwZjM5ZWNhMDc2MzdkZjBmZTE4ID0gTC5wb3B1cCh7bWF4V2lkdGg6ICczMDAnfSk7CgogICAgICAgICAgICAKICAgICAgICAgICAgICAgIHZhciBodG1sXzNhOWE3YzllZjUwNzQ4OWQ4NDRmNTY1NmY5ZjhkYmY4ID0gJCgnPGRpdiBpZD0iaHRtbF8zYTlhN2M5ZWY1MDc0ODlkODQ0ZjU2NTZmOWY4ZGJmOCIgc3R5bGU9IndpZHRoOiAxMDAuMCU7IGhlaWdodDogMTAwLjAlOyI+RWluc3RlaW4gU3RhdHVlIENsdXN0ZXIgMDwvZGl2PicpWzBdOwogICAgICAgICAgICAgICAgcG9wdXBfYWNjMDFiZWQ3MmQ1NDBmMzllY2EwNzYzN2RmMGZlMTguc2V0Q29udGVudChodG1sXzNhOWE3YzllZjUwNzQ4OWQ4NDRmNTY1NmY5ZjhkYmY4KTsKICAgICAgICAgICAgCgogICAgICAgICAgICBjaXJjbGVfbWFya2VyXzhlMDdmM2Q5MjZkYTQxY2VhYmFjODc5Mzc3ZGQ1NDZiLmJpbmRQb3B1cChwb3B1cF9hY2MwMWJlZDcyZDU0MGYzOWVjYTA3NjM3ZGYwZmUxOCk7CgogICAgICAgICAgICAKICAgICAgICAKPC9zY3JpcHQ+ onload="this.contentDocument.open();this.contentDocument.write(atob(this.getAttribute('data-html')));this.contentDocument.close();" allowfullscreen webkitallowfullscreen mozallowfullscreen></iframe></div></div>



## Conclusion

After viewing both universities and the only option was to choose one it would due to mobility it would definitely be Georgia Institute of Technology (Georgia Tech) since there is a shopping center that is walking distance from the institution. As a foodie, I would have preferred Chicago, but as you can see two of the nice restuarants are quite far. They do have the Divvy Station and bus route nearby for easy transportation if you do not want to commute by foot.

Many people have different threshold of what is too far to travel without having a bike, vehicle or public transportation. Overall the venues surrounding both institutions (University of Chicago and Georgia Institute of Technology (Georgia Tech)) are good for pedestrians who need commutable distances to get around.  
