# =============================================================================
# Taller Evaluativo 2 - Fase 2: Empaquetamiento Inmutable Multi-Stage
# Backend: studytrack-api
#
# Complete los TODOs siguiendo las buenas prácticas vistas en el curso:
# reducción de peso, cache de dependencias, usuario no root y ausencia
# total del SDK/compilador en la imagen final de runtime.
# =============================================================================

# ---------- Stage 1: Builder ----------
# TODO

# ---------- Stage 2: Runtime ----------
# TODO

#

#  Stage 1: Builder 
FROM maven:3.9.6-alpine AS builder

WORKDIR /app

# Primero copiamos el pom para aprovechar la caché de Docker
COPY pom.xml .

# Descarga las dependencias
RUN mvn dependency:go-offline

# Ahora copiamos el código fuente
COPY src ./src

# Construimos el JAR sin ejecutar las pruebas
RUN mvn package -DskipTests

#  Runtime
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Crear usuario y grupo sin privilegios
RUN addgroup -S appuser && adduser -S appuser -G appuser

# Copiar únicamente el JAR generado por Maven
COPY --from=builder /app/target/*.jar app.jar

# Ejecutar como usuario no root
USER appuser

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]