FROM node:20.19.6-alpine3.23 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
# this command add extra cache memory
RUN npm install



FROM node:20.19.6-alpine3.23
WORKDIR /opt/server
COPY --from=build /opt/server /opt/server/
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node", "server.js"]