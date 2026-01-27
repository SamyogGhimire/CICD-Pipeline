FROM adoptopenjdk/openjdk11:alpine-jre
WORKDIR /opt/app
COPY target/app.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]