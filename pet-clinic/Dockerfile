FROM eclipse-temurin:17-jdk-jammy as base
WORKDIR /app
COPY mvnw pom.xml ./
COPY src ./src

# Copy jar files
COPY /app/target/spring-petclinic-*.jar /spring-petclinic.jar
EXPOSE 8082
CMD ["java", "-Djava.security.egd=file:/dev/./urandom", "-jar", "/spring-petclinic.jar"]
