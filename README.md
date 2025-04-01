# Assignment 1: Reproducing DS4SDGs Notebook Examples with Generative AI
## Contents
1. Brief analysis of the original notebook
2. Choice of code to replicate and discussion of Chat GPT replication process
3. Comparison of the AI-generated code and the original
4. Brief reflection report
# Task 1: Original Notebook Analysis 
## 1. Key code sections to define notebook's functionality
The notebook contains explanations on how to fetch data related to SDGs from different libraries, sort and process it, and visualise in simple graphs. 
### A) import/ install libraries that contain data for tracking SDGS: 
```python
#install request
!pip install requests
#imprt relevant library
import requests
import pandas as pd
```
### B) fetching data: from an API, using info, search, query, fetch and requests to find specific data or indicators
```python
base_url = "https://unstats.un.org/sdgs/UNSDGAPIV5"

#get list of SDGs
response = requests.get(f"{base_url}/v1/sdg/Goal/List")

#check returned request
if response.status_code == 200:
    goals = response.json()
else:
    print(f"Request failed with status code {response.status_code}: {response.text}")

print(goals)
```
### C) fetching data from a specific geography or time period
```python
goal_code = 1  # For SDG Goal 1

endpoint_geoareas = f'/v1/sdg/Goal/{goal_code}/GeoAreas'

response_geoareas = requests.get(base_url + endpoint_geoareas)

if response_geoareas.status_code == 200:
    geoareas_data = response_geoareas.json()
    geoareas_df = pd.DataFrame(geoareas_data)
    print(geoareas_df.head())
else:
    print(f"Error {response_geoareas.status_code}: {response_geoareas.text}")
```
### D) visualising data
```python
import matplotlib.pyplot as plt
import wbgapi as wb

# Fetch data for the GDP per capita for Brazil, Argentina, and Colombia from 2000 to 2020
df = wb.data.DataFrame('NY.GDP.PCAP.CD', ['BRA', 'ARG', 'COL'], range(2000, 2020), index='time')

# Plot the data
df.plot(figsize=(10, 6), title="GDP Per Capita (2000-2020)", grid=True)
plt.ylabel('GDP Per Capita (current US$)')
plt.xlabel('Year')
plt.legend(title="Countries")
plt.show()
```
## 2. Logic
The notebook is logical: it progresses through the steps of importing relevant libraries and packages for a specific example, then carries out the process of finding specific data/ indicators, then fetches and processes the data,  then visualises it. It also follows a logic of basing each section on a different key dataset, rather than jumping between them. 

## 3. Libraries
The notebook explains how to use key libraries: pandas,  matplotlib, wbgapi, heatmapz, requests. These perform different functions, from fetching specific data to organising the data or processing it through e.g. creating heat maps. 

## 4. Dependencies
The notebook depends upon various python packages, for example pip. These need to be installed in Jupyter for the code to run. 
