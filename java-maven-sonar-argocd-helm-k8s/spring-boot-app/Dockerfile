From maven:3.8.1-jdk-11-openj9 as buildImage
Label MAINTAINER = "preetham"

WORKDIR CICD/java-maven-sonar-argocd-helm-k8s/spring-boot-app/
COPY .  /usr/spring-boot-app/

# Compile and package the application to an executable JAR
RUN mvn -f /usr/spring-boot-app/pom.xml package


FROM openjdk:11
Label MAINTAINER = "preetham"
ARG JAR_FILE=spring-boot-web.jar
WORKDIR /opt/app
EXPOSE 8080
COPY --from=buildImage /usr/spring-boot-app/target/${JAR_FILE}  /opt/app/
ENTRYPOINT ["java", "-jar", "spring-boot-web.jar"]
