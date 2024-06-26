# Fake Storage

This is a fake storage implementation that can be used for testing purposes.

## Usage by docker file

### build the docker image

```bash
docker build -t app-storage .
```

### create logs directory and data directory
```bash
mkdir logs
mkdir data
```

### run the docker container
```bash
docker run -it --rm --name storage-container -p 80:80 -v ${PWD}/data:/app/data -v ${PWD}/logs:/app/logs -e API_KEY=secret app-storage
```
- it: interactive mode
- rm: remove the container after it stops
- name: name of the container
- p: port mapping (host_port:container_port)
- v: volume mapping (host_dir:container_dir)
- e: environment variable
- app-storage: image name

## Endpoints Overview

### API Endpoints

- /uploadTeamConfig (POST): Upload a team config file.
- /downloadTeamConfig/{config_id} (GET): Download a team config file by ID.
- /uploadBaseTeam (POST): Upload a base team file.
- /downloadBaseTeam/{base_name} (GET): Download a base team file by name.
- /downloadServer (GET): Download a server file.
- /uploadServer (POST): Upload a server file.

###  UI Endpoints

- /ui (GET): Main UI page.
- /downloadTeamConfigFromUi/{config_name} (GET): Download a team config file by name from UI.
- /uploadTeamConfigUi (GET): UI for uploading team config files.
- /uploadTeamConfigUiPost (POST): Endpoint for uploading team config files via UI.
- /downloadTeamConfigUi (GET): UI for listing and downloading team config files.
- /downloadBaseTeamFromUi/{base_name} (GET): Download a base team file by name from UI.
- /uploadBaseTeamUi (GET): UI for uploading base team files.
- /uploadBaseTeamUiPost (POST): Endpoint for uploading base team files via UI.
- /downloadBaseTeamUi (GET): UI for listing and downloading base team files.

## How to Call Each Endpoint

### 1. `/uploadTeamConfig` (POST)

**Description**: Upload a team config file.

- Browser
Not directly accessible via a browser.

- Curl
```bash
curl -X POST "http://localhost/uploadTeamConfig" -H "api_key: secret" -F "file=@path/to/your/file.zip"
```

- Python
```python
import requests

url = "http://localhost/uploadTeamConfig"
files = {'file': open('path/to/your/file.zip', 'rb')}
headers = {'api_key': 'secret'}
response = requests.post(url, files=files, headers=headers)
print(response.json())
```

### 2. /downloadTeamConfig/{config_id} (GET)
Description: Download a team config file by ID.

- Browser: http://localhost/downloadTeamConfig/1?api_key=secret
- Curl
```bash
curl -X GET "http://localhost/downloadTeamConfig/1?api_key=secret" -o file.zip
```
- Python
```python
import requests

url = "http://localhost/downloadTeamConfig/1"
params = {'api_key': 'secret'}
response = requests.get(url, params=params)
with open('file.zip', 'wb') as f:
    f.write(response.content)
```

### 3. /uploadBaseTeam (POST)
Description: Upload a base team file.

- Browser
Not directly accessible via a browser.

- Curl
```bash
curl -X POST "http://localhost/uploadBaseTeam" -H "api_key: secret" -F "file=@path/to/your/file.zip"
```
- Python
```python

import requests

url = "http://localhost/uploadBaseTeam"
files = {'file': open('path/to/your/file.zip', 'rb')}
headers = {'api_key': 'secret'}
response = requests.post(url, files=files, headers=headers)
print(response.json())
```
### 4. /downloadBaseTeam/{base_name} (GET)
Description: Download a base team file by name.

- Browser: http://localhost/downloadBaseTeam/base_team_name?api_key=secret

- Curl
```bash
curl -X GET "http://localhost/downloadBaseTeam/base_team_name?api_key=secret" -o file.zip
```
- Python
```python
import requests

url = "http://localhost/downloadBaseTeam/base_team_name"
params = {'api_key': 'secret'}
response = requests.get(url, params=params)
with open('file.zip', 'wb') as f:
    f.write(response.content)
```

### 5. /downloadServer (GET)
Description: Download a server file.

- Browser: http://localhost/downloadServer?api_key=secret
- Curl
```bash
curl -X GET "http://localhost/downloadServer?api_key=secret" -o rcssserver
```

- Python
```python
import requests

url = "http://localhost/downloadServer"
params = {'api_key': 'secret'}
response = requests.get(url, params=params)
with open('rcssserver', 'wb') as f:
    f.write(response.content)
```

### 6. /uploadServer (POST)
Description: Upload a server file.

- Browser Not directly accessible via a browser.
- Curl
```bash
curl -X POST "http://localhost/uploadServer" 
-H "api_key: secret" 
-F "file=@path/to/your/file"
```
- Python
```python

import requests

url = "http://localhost/uploadServer"
files = {'file': open('path/to/your/rcssserver', 'rb')}
headers = {'api_key': 'secret'}
response = requests.post(url, files=files, headers=headers)
print(response.json())
```


### 7. /ui (GET)
Description: Main UI page.

- Browser: http://localhost/ui?api_key=secret
- Curl
Not applicable.

- Python
Not applicable.
