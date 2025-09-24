FROM openjdk:21-jdk-slim-bullseye as build
WORKDIR application
LABEL maintainer="Denys Khmara <khmaradenis64@gmail.com>"
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} application.jar
RUN java -Djarmode=layertools -jar application.jar extract

FROM openjdk:21-jdk-slim-bullseye
WORKDIR application
COPY --from=build application/dependencies/ ./
COPY --from=build application/spring-boot-loader/ ./
COPY --from=build application/snapshot-dependencies/ ./
COPY --from=build application/application/ ./

ENTRYPOINT  ["java", "org.springframework.boot.loader.launch.JarLauncher"]