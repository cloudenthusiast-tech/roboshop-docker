FROM maven:3.9 AS build
WORKDIR /opt/server
COPY pom.xml .
COPY src ./src 
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar 

FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build --chown=roboshop:roboshop /opt/server/shipping.jar .
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST=mysql
USER roboshop
ENTRYPOINT ["sh", "-c", "sleep 30 && java -jar shipping.jar"] 
#CMD ["sleep", "1000"]