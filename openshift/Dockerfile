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
COPY --from=builder source/BOOT-INF/lib BOOT-INF/lib
COPY --from=builder source/BOOT-INF/classpath.idx BOOT-INF
COPY --from=builder source/BOOT-INF/layers.idx BOOT-INF
COPY --from=builder source/org org
COPY --from=builder source/META-INF META-INF
COPY --from=builder source/BOOT-INF/classes BOOT-INF/classes
ENTRYPOINT ["java","org.springframework.boot.loader.JarLauncher"]

#FROM maven:3.6.0-jdk-11-slim AS builder
#WORKDIR source
#ARG JAR_FILE=target/spring-boot-*.jar
#COPY $JAR_FILE application.jar
#RUN java -Djarmode=layertools -jar application.jar extract
#
#
#FROM openjdk:11
#WORKDIR /opt/app
#COPY --from=builder source/dependencies/ ./
#COPY --from=builder source/spring-boot-loader ./
#COPY --from=builder source/snapshot-dependencies/ ./
#COPY --from=builder source/application/ ./
#ENTRYPOINT ["java","org.springframework.boot.loader.JarLauncher"]