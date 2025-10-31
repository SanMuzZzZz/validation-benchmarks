FROM php:5-apache

RUN echo "deb http://archive.debian.org/debian bullseye main" > /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian-security bullseye-security main" >> /etc/apt/sources.list

COPY . . 
WORKDIR /var/www/html

ARG FLAG

RUN sed -i s/@FLAG@/$FLAG/g index.php

EXPOSE 80
