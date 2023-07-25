FROM amazoncorretto:8-alpine as build-stage

RUN apk add git maven

RUN git clone https://github.com/OCR4all/Larex

RUN mvn clean install -f /Larex/pom.xml

FROM tomcat:9.0-jdk8 as production-stage
COPY --from=build-stage /Larex/target/Larex.war /usr/local/tomcat/webapps/Larex.war

EXPOSE 8080

RUN mkdir /home/books /home/savedir

COPY larex.properties /larex.properties
ENV LAREX_CONFIG=/larex.properties