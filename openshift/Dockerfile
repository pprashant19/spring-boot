###################################################
# Command to build image
# $ docker build -t spring-boot . -f ./openshift/Dockerfile
##################################################
FROM openjdk:11
WORKDIR /opt/app
ARG JAR_FILE=target/spring-boot-0.0.1-SNAPSHOT.jar
COPY $JAR_FILE application.jar
ENTRYPOINT ["java","-jar","application.jar"]