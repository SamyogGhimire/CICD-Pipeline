FROM adoptopenjdk/openjdk11:alpine-jre
WORKDIR /opt/app
COPY target/spring-boot-web.jar spring-boot-web.jar
ENTRYPOINT ["java","-jar","spring-boot-web.jar"]