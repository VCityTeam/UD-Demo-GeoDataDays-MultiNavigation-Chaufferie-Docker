FROM ubuntu:focal

LABEL maintainer "VCityTeam"
LABEL source.repo "https://github.com/VCityTeam/UD-Demo-GeoDataDays-MultiNavigation-Chaufferie-Docker"

RUN apt-get update

# The container will serve (through http) the client code 

######### Install the UD-Viz demo per se (client code) and build it
# Node version 14 is required. For its installation (on focal) refer to e.g.
#  https://computingforgeeks.com/install-node-js-14-on-ubuntu-debian-linux/
RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get install -y nodejs
RUN node --version
RUN npm --version
RUN apt-get install -y git
RUN git --version

######### Install the ExpressJS server
WORKDIR /
RUN git clone https://github.com/VCityTeam/UD-SimpleServer.git
WORKDIR /UD-SimpleServer
RUN npm install

######### Install UD-Demo-GeoDataDays-MultiNavigation-Chaufferie-Docker
ARG checkoutName=master
WORKDIR /
RUN git clone https://github.com/VCityTeam/UD-Demo-GeoDataDays-MultiNavigation-Chaufferie.git
WORKDIR /UD-Demo-GeoDataDays-MultiNavigation-Chaufferie
RUN git checkout $checkoutName
ADD bootstrap.js /UD-Demo-GeoDataDays-MultiNavigation-Chaufferie/src/
RUN npm install
RUN npm run build
ADD config.json /UD-Demo-GeoDataDays-MultiNavigation-Chaufferie/assets/config

WORKDIR /
EXPOSE 80
CMD [ "node", "/UD-SimpleServer/index.js", "/UD-Demo-GeoDataDays-MultiNavigation-Chaufferie", "80" ]
