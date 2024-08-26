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

Next, load the knowledge graph data into Blazegraph:
```bash
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/PsDzN27tqSQg3CW/download/ifc_doua.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/RAakYgzR8wno6SM/download?files=DOUA_BATI_2009_stripped_split.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/RAakYgzR8wno6SM/download?files=DOUA_BATI_2012_stripped_split.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/RAakYgzR8wno6SM/download?files=DOUA_BATI_2015_stripped_split.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/RAakYgzR8wno6SM/download?files=DOUA_BATI_2018_stripped_split.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
curl -X POST --data-binary 'uri=https://partage.liris.cnrs.fr/index.php/s/RAakYgzR8wno6SM/download?files=DOUA_2009-2018_Workspace.rdf' "http://127.0.0.1:8001/blazegraph/sparql"
```
