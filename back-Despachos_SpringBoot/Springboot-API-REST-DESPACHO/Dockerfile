# --- ETAPA 1: Compilación ---
FROM maven:3.9-eclipse-temurin-17-alpine AS builder
WORKDIR /app
COPY pom.xml .
# Descargamos las dependencias para aprovechar la caché de Docker
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn package -DskipTests

# --- ETAPA 2: Ejecución ---
FROM eclipse-temurin:17-jre-alpine
WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8082
ENTRYPOINT ["java", "-jar", "app.jar"]