###################################################
# Command to build image
# $ docker build -t spring-boot . -f ./openshift/Dockerfile
##################################################
FROM maven:3.6.0-jdk-11-slim AS builder
WORKDIR source
ARG JAR_FILE=target/spring-boot-*.jar
COPY $JAR_FILE application.jar
RUN java -Djarmode=layertools -jar application.jar extract

FROM openjdk:11
WORKDIR /opt/app
COPY --from=builder source/dependencies/ ./
COPY --from=builder source/spring-boot-loader ./
COPY --from=builder source/snapshot-dependencies/ ./
COPY --from=builder source/application/ ./
ENTRYPOINT ["java","org.springframework.boot.loader.JarLauncher"]