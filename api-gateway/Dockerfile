FROM maven:3.9.8-amazoncorretto-21 AS build

# Copy source code and pom.xml file to /app folder
WORKDIR /app
COPY pom.xml .
COPY src ./src

# Build source code with maven
RUN mvn package -DskipTests

#Stage 2: create image
# Start with Amazon Correto JDK 21
FROM amazoncorretto:21.0.4

# Set working folder to App and copy complied file from above step
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar

ARG SPRING_PROFILE=staging
ENV SPRING_PROFILE=${SPRING_PROFILE}

# EXPOSE 8888
# Command to run the application
ENTRYPOINT ["java", "-jar", "-Dspring.profiles.active=${SPRING_PROFILE}", "app.jar"]
