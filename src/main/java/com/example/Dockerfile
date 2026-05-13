# Use Tomcat as the base image
FROM tomcat:9.0-jdk11-openjdk

# Remove default Tomcat apps to keep it clean
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy your successful build artifact (the .war file) into Tomcat
COPY target/*.war /usr/local/tomcat/webapps/ROOT.war

# Start Tomcat
EXPOSE 8080
CMD ["catalina.sh", "run"]
