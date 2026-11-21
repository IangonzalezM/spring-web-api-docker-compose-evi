FROM eclipse-temurin:25-jre

WORKDIR /app

COPY target/sbapp11-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 4455

ENTRYPOINT ["java","-jar","app.jar"]