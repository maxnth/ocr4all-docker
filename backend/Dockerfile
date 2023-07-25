FROM amazoncorretto:11.0.19-alpine3.17 as build-stage

RUN apk add git maven

RUN git clone --recurse-submodules --remote-submodules https://github.com/OCR4all/ocr4all-backend
WORKDIR ocr4all-backend
RUN mvn -f ocr4all-app-persistence/pom.xml clean install
RUN mvn -f ocr4all-app-spi/pom.xml clean install
RUN mvn -f ocr4all-app-ocrd-spi/pom.xml clean install
RUN mvn -f ocr4all-app/pom.xml clean package

FROM amazoncorretto:11.0.19-alpine3.17 as production-stage

EXPOSE 9090

RUN apk add imagemagick

COPY --from=build-stage /ocr4all-backend/ocr4all-app/target/ocr4all-app-1.0-SNAPSHOT.jar ocr4all.jar
CMD ["java", "-jar", "ocr4all.jar"]