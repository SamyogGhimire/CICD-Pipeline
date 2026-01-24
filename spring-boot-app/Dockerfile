FROM maven:3.8.7-openjdk-11 AS builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package

FROM eclipse-temurin:11-jre-alpine
WORKDIR /opt/app
COPY --from=builder /app/target/spring-boot-web.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
