# === Stage 1: Build (बड़ा किचन) ===
FROM eclipse-temurin:21-jdk AS builder
WORKDIR /app
# अपना सारा कोड और टूल्स कंटेनर के अंदर कॉपी करें
COPY . .
# कंटेनर के अंदर ही .jar फाइल बनाएं (आपके Mac की ज़रूरत नहीं!)
RUN ./mvnw clean package -DskipTests

# === Stage 2: Run (छोटा डाइनिंग रूम) ===
FROM eclipse-temurin:21-jre
WORKDIR /app
# 'builder' (किचन) से सिर्फ तैयार .jar फाइल को इस नए छोटे कंटेनर में लाएं
COPY --from=builder /app/target/*.jar app.jar
EXPOSE 8080
# ऐप को चालू करने का आदेश
CMD ["java", "-jar", "app.jar"]