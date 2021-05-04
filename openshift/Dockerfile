###################################################
# Command to build image
# $ docker build -t spring-boot . -f ./openshift/Dockerfile
##################################################
FROM maven:3.6.0-jdk-11-slim AS builder
WORKDIR source
ARG JAR_FILE=target/spring-boot-*.jar
COPY $JAR_FILE application.jar
RUN jar -xf ./application.jar

FROM openjdk:11
WORKDIR /opt/app
COPY --from=builder source/BOOT-INF/lib lib
COPY --from=builder source/META-INF app/META-INF
COPY --from=builder source/BOOT-INF/classes app
ENTRYPOINT ["java","-cp","app/lib/*","com.example.springboot.Application"]