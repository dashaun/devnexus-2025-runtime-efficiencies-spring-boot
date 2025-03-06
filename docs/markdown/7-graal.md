<img src="images/graal.png" alt="Extract, AOT, CDS" width="600"/>

---

```bash
# Native Image Kit
sdk use java 24.1.2.r23-nik

./mvnw -Pnative clean native:compile

./target/hello-spring

http :8080/actuator/metrics/application.started.time \
-o 3-4-java-23-native.started.json
http :8080/actuator/metrics/jvm.memory.used \
-o 3-4-java-23-native.memory.json
```
