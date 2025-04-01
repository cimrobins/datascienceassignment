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
I write below my conversation with Chat GPT. Between each generation, I compared the codes and their similarity to the original to create a closer match. 

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

dont import. 

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

dont make any package imports and dont include comments. 

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

