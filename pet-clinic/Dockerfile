From tomcat:8.0.51-jre8-alpine
WORKDIR /app
COPY mvnw pom.xml ./
COPY src ./src

# Copy jar files
COPY /app/target/spring-petclinic-*.jar /spring-petclinic.jar
EXPOSE 8082
CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/spring-petclinic.jar"]
