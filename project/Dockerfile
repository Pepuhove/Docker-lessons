# -------------------------
# 1. BUILD STAGE
# -------------------------
FROM maven:3.9.9-eclipse-temurin-8 AS builder

WORKDIR /app

# Copy pom.xml and download dependencies first (to cache layers)
COPY . .
# Build WAR file
RUN mvn clean package -DskipTests

# -------------------------
# 2. RUNTIME STAGE
# -------------------------
FROM tomcat:8.5-jre8

# Remove default apps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy built WAR into Tomcat
COPY --from=builder /app/target/*.war /usr/local/tomcat/webapps/ROOT.war

# Expose port
EXPOSE 8080

# Run Tomcat
CMD ["catalina.sh", "run"]

