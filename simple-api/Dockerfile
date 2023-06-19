# Build
# Java jdk + maven image to be able to build the application
FROM maven:3.8.6-amazoncorretto-17 AS myapp-build
# Set the app directory used as env then specify it as the working directory
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME
# Copy all necessary files the build the app
COPY pom.xml .
COPY src ./src
# Package the application as a jar, skipping the tests as they will be made in the pipeline separately
# Added dependency:go-offline to use cached dependencies
RUN mvn package -DskipTests dependency:go-offline

# Run
# Java JDK image only (could use a Java JRE image instead, but couldn't make it work during the TP)
FROM amazoncorretto:17
# Same as before, set the working directory
ENV MYAPP_HOME /opt/myapp
WORKDIR $MYAPP_HOME
# Copy the jar from the previous stage with this option --from=myapp-build
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

# Run the jar to launch the app
ENTRYPOINT java -jar myapp.jar