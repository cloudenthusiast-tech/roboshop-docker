FROM node:20.19.6-alpine3.23 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
# this command add extra cache memory
RUN npm install


FROM node:20.19.6-alpine3.23
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server
EXPOSE 8080
LABEL com.project="roboshop" \
      component="catalogue" \
      created_by="Aravind"
COPY --from=build /opt/server /opt/server 
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
    # needs root access to run chown command
 
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"] 