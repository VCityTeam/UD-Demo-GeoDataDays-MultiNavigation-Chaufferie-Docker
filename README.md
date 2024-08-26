# UD-Demo-GeoDataDays-MultiNavigation-Chaufferie-Docker
Fully dockerized version of UD-Demo-GeoDataDays-MultiNavigation-Chaufferie

## Installation

This demo requires the Docker Engine. Installation instructions can be found [here](https://docs.docker.com/engine/install/).

Once Docker is installed, clone this repository:
```
git clone https://github.com/VCityTeam/UD-Demo-GeoDataDays-MultiNavigation-Chaufferie-Docker.git
cd UD-Demo-GeoDataDays-MultiNavigation-Chaufferie-Docker
```

To configure the databases, edit `./.env` file to set appropriate passwords and ports for each service. For example:
```
#### PostGIS
POSTGRES_DB_NAME=endpoint
POSTGRES_USER=postgres
POSTGRES_PASSWORD=p0$tgr3$
POSTGRES_PORT=8002
POSTGRES_HOST=postgres
POSTGRES_ORDBMS=postgis
POSTGRES_VOLUME_NAME=ud_demo_geodatadays_multinavigation_chaufferie_docker_pg_volume_1

#### Strabon
STRABON_CREDENTIALS_username=endpoint
STRABON_CREDENTIALS_password=3ndpo1nt
STRABON_PORT=8001

#### UD-Viz
# The port providing access to the web-gl demo (thus accessible through the
# http://localhost:{UD_VIZ_PORT} URL) 
UD_VIZ_PORT=8000
```
Use docker compose to build and run the demo containers
```
docker compose up 
```

Next load graph data into Strabon. The docker image volume is automatically loaded with the relevant data files for the demo, however they need to be manually loaded into the Strabon database itself (automation will be implemented eventually for this step). To upload these files into Strabon to be used by the sparqlModule:
1. Open a web browser and navigate to [http://localhost:8001/strabon](http://localhost:8001/strabon)
2. From the left menu, click *Explore/Modify operations* then *Store*
3. Copy and paste the first filepath below into the *URI Input* field and click *Store from URI*. Repeat this process for each filepath
   1. `file:///DOUA_BATI_2009_stripped_split.rdf`
   2. `file:///DOUA_BATI_2012_stripped_split.rdf`
   3. `file:///DOUA_BATI_2015_stripped_split.rdf`
   4. `file:///DOUA_BATI_2018_stripped_split.rdf`
   5. `file:///DOUA_2009-2018_Workspace.rdf`
   6. `file:///ifc_doua.rdf`
   - ⚠️ You may be asked to enter the Strabon administrative credentials here. However, these credentials currently cannot be changed from the `.env` file. See issue [#1](https://github.com/VCityTeam/UD-Demo-Graph-SPARQL/issues/1).
   - Also note that some of these files are quite large and may take a while to load so be patient. A successfully uploaded file should read "Data stored successfully!" at the top of the interface unless there is a **504 Gateway Time-out** error. If there is a timeout error refer to the docker logs from the strabon container searching for the line `STORE was successful` to confirm the dataset was successfully uploaded.
   - ![image](https://user-images.githubusercontent.com/23373264/193312585-402e87ec-ccc3-48cd-a200-b26d17fe2554.png)
   
The demo can be open by navigating to [http://localhost:8000](http://localhost:8000)
