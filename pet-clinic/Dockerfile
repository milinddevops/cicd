From tomcat:8.0.51-jre8-alpine
USER root
RUN rm -rf /usr/local/tomcat/webapps/*
COPY ./target/petclinic.war /usr/local/tomcat/webapps/petclinic.war
EXPOSE 8082
CMD ["catalina.sh","run"]
