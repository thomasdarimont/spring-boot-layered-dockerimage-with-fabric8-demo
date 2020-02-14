FROM adoptopenjdk:11-jre-hotspot as builder
WORKDIR application
COPY maven/*.jar app.jar
RUN java -Djarmode=layertools -jar *.jar extract

FROM adoptopenjdk:11-jre-hotspot
WORKDIR application
COPY --from=builder application/dependencies/ ./
COPY --from=builder application/snapshot-dependencies/ ./
COPY --from=builder application/resources/ ./
COPY --from=builder application/application/ ./
ENTRYPOINT ["java", "org.springframework.boot.loader.JarLauncher"]