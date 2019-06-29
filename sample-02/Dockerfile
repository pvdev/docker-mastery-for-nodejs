FROM node:10-alpine

# do all OS install at top of file always with update and versions
RUN apk add --update curl

EXPOSE 3000

WORKDIR /node

# the * says create file even if not there
COPY package.json package-lock.json* ./ 

RUN npm install && npm cache clean --force

WORKDIR /node/app

# copy source files last for build efficiency 
COPY . .

CMD [ "node", "./bin/www" ]
