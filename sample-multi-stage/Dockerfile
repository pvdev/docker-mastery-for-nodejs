FROM node:10-slim as prod
ENV NODE_ENV=production
EXPOSE 3000
#RUN apt-get update -q && apt-get install -q -y tini
# Add Tini
ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
WORKDIR /node
COPY package.json package-lock.json* ./
RUN npm install --only=production && npm cache clean --force
COPY . .
ENTRYPOINT ["/tini", "--"]
CMD ["node", "./bin/www"]


FROM prod as dev
ENV NODE_ENV=development
#Install Dev dependencies
RUN npm install --only=${NODE_ENV} && npm cache clean --force
CMD ["./node_modules/nodemon/bin/nodemon.js", "./bin/www", "--inspect=0.0.0.0:9229"]


FROM dev as test
ENV NODE_ENV=development
CMD ["npm", "test"]