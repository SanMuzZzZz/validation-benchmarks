FROM maven:3.8.4-openjdk-17-slim AS builder

WORKDIR /app

COPY . .

ADD https://repo1.maven.org/maven2/ognl/ognl/3.2.12/ognl-3.2.12.jar /usr/local/tomcat/lib/

RUN mvn package

FROM tomcat:9-jdk17-openjdk-slim

COPY --from=builder /app/target/*.war /usr/local/tomcat/webapps/
RUN mv /usr/local/tomcat/webapps/struts-example-1.0-SNAPSHOT.war /usr/local/tomcat/webapps/ROOT.war

RUN sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list \
    && sed -i 's/security.debian.org/archive.debian.org/g' /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian buster main" > /etc/apt/sources.list \
    && echo "deb http://archive.debian.org/debian-security buster/updates main" >> /etc/apt/sources.list 
RUN apt-get update -y

RUN apt-get install -y curl

ARG FLAG
RUN echo "$FLAG" > /tmp/flag

EXPOSE 8080
