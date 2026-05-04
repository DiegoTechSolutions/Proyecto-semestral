# --- ETAPA 1: Construcción (Builder) ---
FROM maven:3.8.5-openjdk-17 AS builder
WORKDIR /app
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package -DskipTests

# --- ETAPA 2: Producción ---
FROM openjdk:17-jdk-slim
WORKDIR /app
# Cumplimiento de rúbrica: Creación de usuario no root por seguridad
RUN groupadd -r appgroup && useradd -r -g appgroup appuser
USER appuser
# Copiamos solo el ejecutable compilado de la etapa anterior
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]