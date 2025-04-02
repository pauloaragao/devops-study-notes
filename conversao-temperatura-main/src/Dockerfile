FROM ubuntu:20.04

# Install nodejs
RUN apt-get update && apt-get install -y nodejs npm

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]
