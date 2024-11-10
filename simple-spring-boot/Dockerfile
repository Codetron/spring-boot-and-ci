# First stage: build the application
FROM maven:3.9.9-eclipse-temurin-21-alpine AS build
COPY . /app
WORKDIR /app

# Extract version from pom.xml and use it to build the JAR file
RUN VERSION=$(mvn -q -Dexec.executable=echo -Dexec.args='${project.version}' --non-recursive exec:exec) && \
    echo "Building version $VERSION" && \
    mvn package -DskipTests && \
    echo "Looking for JAR with version $VERSION:" && \
    ls ./target/ | grep "${VERSION}.jar" && \
    cp ./target/*${VERSION}.jar ./app.jar

# Second stage: create a slim image
FROM eclipse-temurin:21-jre-alpine

# Copy the built JAR file to the final image
COPY --from=build /app/app.jar /app.jar
ENTRYPOINT ["java", "-jar", "/app.jar"]
