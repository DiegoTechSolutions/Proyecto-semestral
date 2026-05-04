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
# Cumplimiento de rúbrica: Creación de usuario no root
RUN groupadd -r appgroup && useradd -r -g appgroup appuser
USER appuser
COPY --from=builder /app/target/*.jar app.jar
# Usamos el puerto 8081 para que no choque con el de ventas
EXPOSE 8081
ENTRYPOINT ["java", "-jar", "app.jar"]