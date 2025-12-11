FROM python:3.10-slim AS build
WORKDIR /opt/server
EXPOSE 8080
COPY payment.ini .
COPY *.py .
COPY requirements.txt .
RUN pip3 install -r requirements.txt

FROM python:3.10-slim
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
WORKDIR /opt/server
COPY --from=build /opt/server /opt/server
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
RUN chown -R roboshop:roboshop /opt/server 
USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]



