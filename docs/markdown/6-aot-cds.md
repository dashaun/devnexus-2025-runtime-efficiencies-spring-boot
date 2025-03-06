<img src="images/combined.png" alt="Extract, AOT, CDS" width="600"/>

---

AOT and CDS can be used together for even more benefits!

---

```bash
# AOT processing first
./mvnw -q -Pnative clean package -DskipTests
# Extract the jar
java -Djarmode=tools -jar ./target/hello-spring-0.0.1-SNAPSHOT.jar extract --destination application
# Create CDS archive
java -XX:ArchiveClassesAtExit=application.jsa -Dspring.context.exit=onRefresh -jar application/hello-spring-0.0.1-SNAPSHOT.jar
# Run using AOT+CDS archive
java -XX:SharedArchiveFile=application.jsa -jar applicatin/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time -o 3-4-java-23-combined.started.json
http :8080/actuator/metrics/jvm.memory.used -o 3-4-java-23-combined.memory.json
```
