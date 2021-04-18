FROM maven:3.6.0-jdk-11-slim AS build
ENV APP_PATH=customer-service
WORKDIR /
COPY $APP_PATH/src src
COPY $APP_PATH/pom.xml pom.xml
RUN mvn -f pom.xml package
RUN mkdir -p target && (cd target; cp *.jar ../*.jar)

FROM openjdk:11
WORKDIR /
ARG JAR_FILE=target/spring-boot-0.0.1-SNAPSHOT
COPY --from=build ${JAR_FILE} app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]