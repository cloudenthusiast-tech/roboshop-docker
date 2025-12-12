FROM python:3.9.25-alpine3.21 AS builder
WORKDIR /opt/server
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
# using --prefix=/install for better management of dependencies 
RUN pip3 install --prefix=/install-r requirements.txt

FROM python:3.9.25-alpine3.21 
EXPOSE 8080
WORKDIR /opt/server
#runtime deps only
RUN apk add --no-cache pcre
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop   
COPY --from=builder /install /usr/local
# Copy app files
COPY --chown=roboshop:roboshop payment.ini *.py requirements.txt . 
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123" 

USER roboshop
CMD ["uwsgi", "--ini", "payment.ini"]