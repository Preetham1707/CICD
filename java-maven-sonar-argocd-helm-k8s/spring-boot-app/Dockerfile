FROM maven:3.8.1-jdk-11-openj9 AS buildImage
LABEL MAINTAINER = "preetham"

WORKDIR /java-maven-sonar-argocd-helm-k8s/
COPY .  /usr/
RUN ls -l /usr/

# Compile and package the application to an executable JAR
RUN mvn -f /usr/java-maven-sonar-argocd-helm-k8s/spring-boot-app/pom.xml package


FROM openjdk:11
LABEL MAINTAINER = "preetham"
ARG JAR_FILE=spring-boot-web.jar

WORKDIR /opt/app
EXPOSE 8080
COPY --from=buildImage /usr/java-maven-sonar-argocd-helm-k8s/spring-boot-app/target/${JAR_FILE}  /opt/app/
ENTRYPOINT ["java", "-jar", "spring-boot-web.jar"]
