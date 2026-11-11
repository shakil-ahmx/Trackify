# syntax=docker/dockerfile:1

# ── Stage 1: Build ──────────────────────────────────────────────
FROM maven:3.9.9-eclipse-temurin-21 AS builder
WORKDIR /app
COPY pom.xml .
# BuildKit cache: Maven deps are downloaded once, reused on every rebuild
RUN --mount=type=cache,target=/root/.m2 mvn -B -q dependency:go-offline
COPY src ./src
RUN --mount=type=cache,target=/root/.m2 mvn -B -q clean package -DskipTests \
    && java -Djarmode=layertools -jar target/trackify-backend-1.0.0.jar extract --destination /layers

# ── Stage 2: Run (small JRE, non-root) ──────────────────────────
FROM eclipse-temurin:21-jre-alpine
RUN addgroup -S app && adduser -S app -G app
WORKDIR /app
RUN mkdir -p /app/uploads && chown -R app:app /app
COPY --from=builder --chown=app:app /layers/dependencies/ ./
COPY --from=builder --chown=app:app /layers/spring-boot-loader/ ./
COPY --from=builder --chown=app:app /layers/snapshot-dependencies/ ./
COPY --from=builder --chown=app:app /layers/application/ ./
USER app
EXPOSE 8080

# Low-memory JVM settings: fits comfortably in ~350 MB
ENV JAVA_TOOL_OPTIONS="-XX:+UseSerialGC -XX:MaxRAMPercentage=70 -XX:TieredStopAtLevel=1 -Xss512k -XX:+ExitOnOutOfMemoryError"
ENTRYPOINT ["java", "org.springframework.boot.loader.launch.JarLauncher"]
