FROM eclipse-temurin:21.0.8_9-jdk-alpine AS builder

WORKDIR /app

COPY .mvn/ .mvn
COPY mvnw pom.xml ./

RUN ./mvnw dependency:go-offline

COPY src ./src

RUN ./mvnw clean install


FROM eclipse-temurin:21.0.8_9-jre-alpine AS final

WORKDIR /app

EXPOSE 8080

COPY --from=builder /app/target/*.jar /app/*.jar

ENTRYPOINT ["java", "-jar", "/app/*.jar"]

