From tomcat:8.0.51-jre8-alpine
WORKDIR /app
COPY mvnw pom.xml ./
COPY target ./target

RUN ls -lrt /app/target

# Copy jar files
COPY ./target/spring-petclinic-*.jar /spring-petclinic.jar
EXPOSE 8082
CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/spring-petclinic.jar", "--server.port=8082"]
