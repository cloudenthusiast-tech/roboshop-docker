FROM node:20.19.6-alpine3.23 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


FROM node:20.19.6-alpine3.23
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build /opt/server /opt/server
ENV REDIS_HOST=redis \
    CATALOGUE_HOST=catalogue \
    CATALOGUE_PORT=8080 
RUN chown -R roboshop:roboshop /opt/server 
USER roboshop
CMD [ "node", "server.js" ]