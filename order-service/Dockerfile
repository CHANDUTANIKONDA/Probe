# ---- Build stage ----
FROM maven:3.9.6-amazoncorretto-21 AS build
WORKDIR /src
COPY pom.xml .
RUN mvn -q -B -DskipTests dependency:go-offline
COPY src ./src
RUN mvn -q -B -DskipTests package

# ---- Runtime stage ----
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
# If your jar name differs, adjust the pattern below:
COPY --from=build /src/target/*-SNAPSHOT.jar /app/order-service.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","/app/order-service.jar"]
