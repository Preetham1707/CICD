FROM maven:3.8.1-jdk-11-openj9 AS buildImage
LABEL MAINTAINER = "preetham"

WORKDIR /var/lib/jenkins/workspace/CICD/java-maven-sonar-argocd-helm-k8s/spring-boot-app
COPY .  .
RUN echo "PWD is: $PWD" && ls $PWD

# Compile and package the application to an executable JAR
RUN mvn -f pom.xml package


FROM openjdk:11
LABEL MAINTAINER = "preetham"
ARG JAR_FILE=spring-boot-web.jar

WORKDIR /opt/app
EXPOSE 8080
COPY --from=buildImage spring-boot-app/target/${JAR_FILE}  /opt/app/
ENTRYPOINT ["java", "-jar", "spring-boot-web.jar"]
