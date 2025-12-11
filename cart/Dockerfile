FROM node:20.19.6-alpine3.23 AS build
WORKDIR /opt/server
COPY package.json .
COPY *.js .
RUN npm install


FROM node:20.19.6-alpine3.23
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /opt/server 
EXPOSE 8080
LABEL com.project="roboshop" \
      component="cart" \
      created_by="ARAVIND"
COPY --from=build /opt/server /opt/server
ENV REDIS_HOST=redis \
    CATALOGUE_HOST=catalogue \
    CATALOGUE_PORT=8080 
USER roboshop
CMD ["server.js"] 
ENTRYPOINT ["node"]