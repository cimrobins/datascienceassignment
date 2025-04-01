# Assignment 1: Reproducing DS4SDGs Notebook Examples with Generative AI
## Contents
1. Brief analysis of the original notebook
2. Chosen code to replicate and transcript of conversation with ChatGPT
3. Levenshtein measure to compare the scripts
4. Reflection report
# Task 1: Original Notebook Analysis 
## 1. Examples of key code sections
The notebook contains explanations on how to fetch data related to SDGs from different libraries, sort and process it, and visualise in simple graphs. Here, I give brief description of key codes and examples from the original notebook.  
### A) import/ install libraries that contain data for tracking SDGS: 
for example:
```python
#install request
!pip install requests
#imprt relevant library
import requests
import pandas as pd
```
### B) fetching data: from an API, using info, search, query, fetch and requests to find specific data or indicators
for example: 
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
for example: 
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
for example: 
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

# 2. Prompt Engineering
I selected a specific code snippet for this task. It retrieves geographical areas that have data available for SDG1 from UN SDG API.
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
I chose this section of code because I initially did not understand it, and thought it was a good level of compexity to try and get Chat GPT to produce with my prompting.  It is closely related to the main purpose of the notebook, to retrieve data from an external API, includes pandas dataframes and also error handling. 

## My conversation with ChatGPT 
I write below my conversation with Chat GPT. Between each of the three generations, I compared the codes and their similarity to the original to create a closer match. The new additions in each iteration of my prompt are shown in bold. 

### **Prompt 1:**  
**Me:** Imagine you are my coding assistant and I require you for some help when writing some EDA code for a homework assignment:

The overarching goal of this code is the retrieve a list of geocode cities and countries that have observations for a specific SDG goal

Lets establish some variables now:
the sdg goal code  (goal_code) is 1 
and the endpoint geoareas (endpoint_geoareas)  is  an f_string  that uses goal_code as shown here - f'/v1/sdg/Goal/{goal_code}/GeoAreas'

The aim is to make a request using a base_url var and endpoint_geoareas,
check for status 200, if true
get the json, convert it to a df,
and print the head.

chose suitable variable names 

if the status isn't 200 print an f-string which says error followed by the status code and response text.

Show me the code and the code only

### **Answer:**  
**ChatGPT:**  
```python
import requests
import pandas as pd

# Define variables
goal_code = 1
base_url = "https://example.com/api"  # Replace with actual base URL
endpoint_geoareas = f"/v1/sdg/Goal/{goal_code}/GeoAreas"

# Make request
response = requests.get(f"{base_url}{endpoint_geoareas}")

# Check response status
if response.status_code == 200:
    data = response.json()
    df = pd.DataFrame(data)
    print(df.head())
else:
    print(f"Error: {response.status_code} - {response.text}")
```
---

### **Prompt 2:**  
**Me:** Imagine you are my coding assistant and I require you for some help when writing some EDA code for a homework assignment:

The overarching goal of this code is the retrieve a list of geocode cities and countries that have observations for a specific SDG goal

Lets establish some variables now:
the sdg goal code  (goal_code) is 1 
and the endpoint geoareas (endpoint_geoareas)  is  an f_string  that uses goal_code as shown here - f'/v1/sdg/Goal/{goal_code}/GeoAreas'

**dont import.**

The aim is to make a request using a base_url var and endpoint_geoareas,
check for status 200, if true
get the json, convert it to a df,
and print the head.

chose suitable variable names 

### **Answer:**  
**ChatGPT:**  
```python
# Define variables
goal_code = 1
base_url = "https://example.com/api"  # Replace with actual base URL
endpoint_geoareas = f"/v1/sdg/Goal/{goal_code}/GeoAreas"

# Make request
response = requests.get(f"{base_url}{endpoint_geoareas}")

# Check response status
if response.status_code == 200:
    geo_data = response.json()
    geo_df = pd.DataFrame(geo_data)
    print(geo_df.head())
else:
    print(f"Error: {response.status_code} - {response.text}")

```
### **Prompt 3:**  
**Me:** Imagine you are my coding assistant and I require you for some help when writing some EDA code for a homework assignment:

The overarching goal of this code is the retrieve a list of geocode cities and countries that have observations for a specific SDG goal

Lets establish some variables now:
the sdg goal code  (goal_code) is 1 
and the endpoint geoareas (endpoint_geoareas)  is  an f_string  that uses goal_code as shown here - f'/v1/sdg/Goal/{goal_code}/GeoAreas'

**dont make any package imports and dont include comments.**

The aim is to make a request using a base_url var and endpoint_geoareas,
check for status 200, if true
get the json, convert it to a df,
and print the head.

chose suitable variable names 
### **Answer:**  
**ChatGPT:**  
```python
goal_code = 1
base_url = "https://example.com/api"
endpoint_geoareas = f"/v1/sdg/Goal/{goal_code}/GeoAreas"

response = requests.get(f"{base_url}{endpoint_geoareas}")

if response.status_code == 200:
    geo_data = response.json()
    geo_df = pd.DataFrame(geo_data)
    print(geo_df.head())
else:
    print(f"Error: {response.status_code} - {response.text}")
```
# 3. Comparison of the Chat GPT-generated code with the original

I used the following Chat GPT prompt on a new chat to help me compare the texts between each  code-creation prompt:
**Me:** I want a measure for how dissimilar two pieces of text are

ChatGPT recommended me to use 'Levenshtein Distance', stating:
'1. Edit Distance (Levenshtein Distance)
Measures how many single-character edits (insertions, deletions, substitutions) are needed to transform one text into another.
Works well for short strings but not ideal for meaning-based comparisons.'

In this way, I used the Levenshtein Distance on python to compare the similarity between the strings after each iteration. It produced a Levenshtein ratio between 0 and 1. At first iteration, there was a value of 0.7. After iteration, the value reached 0.83. This suggests a strong similarity between the two code strings. This was only three iterations, and with another three, it would get really close. I expect that if I created a graph to visualise the level of similarity between the two, this would produce a curve that 'tailed off', as initial re-iterations produced larger improvements to the final iterations. 

```python
!pip install levenshtein
import Levenshtein


true_string = '''
goal_code = 1  # For SDG Goal 1

endpoint_geoareas = f'/v1/sdg/Goal/{goal_code}/GeoAreas'

response_geoareas = requests.get(base_url + endpoint_geoareas)

if response_geoareas.status_code == 200:
    geoareas_data = response_geoareas.json()
    geoareas_df = pd.DataFrame(geoareas_data)
    print(geoareas_df.head())
else:
    print(f"Error {response_geoareas.status_code}: {response_geoareas.text}")
'''


gpt_string = '''import requests
import pandas as pd

# Define variables
goal_code = 1
base_url = "https://example.com/api"  # Replace with actual base URL
endpoint_geoareas = f"/v1/sdg/Goal/{goal_code}/GeoAreas"

# Make request
response = requests.get(f"{base_url}{endpoint_geoareas}")

# Check response status
if response.status_code == 200:
    data = response.json()
    df = pd.DataFrame(data)
    print(df.head())
else:
    print(f"Error: {response.status_code} - {response.text}")'''


gpt_string_2 = '''goal_code = 1
base_url = "https://example.com/api"
endpoint_geoareas = f"/v1/sdg/Goal/{goal_code}/GeoAreas"

response = requests.get(f"{base_url}{endpoint_geoareas}")

if response.status_code == 200:
    geo_data = response.json()
    geo_df = pd.DataFrame(geo_data)
    print(geo_df.head())
else:
    print(f"Error: {response.status_code} - {response.text}") '''


Levenshtein.ratio(s1=true_string, s2=gpt_string_2)
```

# 4. Reflection: comparing the codes and my process

From my attempts to replicate a preexisting code using ChatGPT I learnt the following:
When replicating a code, it works to first create a general code, and then work on quick iterations based on the previous output. 
When comparing the two codes myself, without the Levenshtein measure, I can see that the AI generated response includes variables that were defined higher up in the script on the original notebook. This could easily be removed by iterating on the prompt again, by telling it to assume certain variables are predefined. 

ChatGPT, an LLM, took a different approach to forming the final string: it fomulated it as a concatenated f-string instead of adding. Perhaps it has been biased towards this form of generation through its training process? I imagine that prompts could probably steer it to use plus signs-- although I don't know why this would actually be necessary in practice! 

There was a slight discrepancy between the variable names chosen- ChatGPT went for slightly more parsomonious names. It also seems to be keen on using (more common) f-string operations instead of variable names. This might be because I mentioned the f-strings several times in my prompts. I more experienced coder/ user of LLMs would probably have foreseen that this might guide the LLM to prefer a certain formulation. If I was to attempt this again, I would try to prompt without mentioning the f-strings so much, to see whether it would still use them. 

Finally, the Levenshtein measure turned out to be a useful method of objectively examining my code's similarity to the original, providing a measure to justify the closeness. It worked well to combine the quantitative measure of similarity with my own qualitative comparison, to complement each other. I would be interested to learn more about the different uses of measures, as well as different types and their uses. 

