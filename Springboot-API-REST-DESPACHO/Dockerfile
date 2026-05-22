# =========================
# ETAPA 1 - BUILD
# =========================
FROM maven:3.9.6-eclipse-temurin-21 AS builder

WORKDIR /app

COPY . .

RUN mvn clean package -DskipTests

# =========================
# ETAPA 2 - RUNTIME
# =========================
FROM eclipse-temurin:21-jre

WORKDIR /app

# usuario no root
RUN addgroup --system spring && adduser --system spring --ingroup spring

COPY --from=builder /app/target/*.jar app.jar

USER spring

EXPOSE 8081

ENTRYPOINT ["java","-jar","app.jar"]