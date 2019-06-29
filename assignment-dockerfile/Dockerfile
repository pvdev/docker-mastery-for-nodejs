# fill in the blanks to dockerize this node app
FROM node:10.15.0-alpine

EXPOSE 3000

RUN apk add --no-cache tini

WORKDIR /node

COPY package.json package-lock.json* ./

RUN npm install && npm cache clean --force

COPY app.js .

#ENTRYPOINT ["/sbin/tini", "--"]

CMD ["node", "app.js"]
