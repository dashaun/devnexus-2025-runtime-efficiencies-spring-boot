## Java is too slow

---

## Cold Start

---

## GraalVM

---

## Spring Framework 6 and Spring Boot 3

### Rebase from Java 8 to Java 17

---

```bash
gh repo clone dashaun/hello-spring-boot-2-7
```
> Go back in time

---

```bash
management.endpoints.web.exposure.include=*
```
>Add this to src/main/resource/application.properties

---

```bash
sdk use java 8.0.442-librca
./mvnw clean package
java -jar target/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time -o 2-7-java-8.started.json
http :8080/actuator/metrics/jvm.memory.used -o 2-7-java-8.memory.json
```

---

```bash
sdk use java 23.0.2-librca
./mvnw clean package
java -jar target/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time \
-o 2-7-java-23.started.json

http :8080/actuator/metrics/jvm.memory.used \
-o 2-7-java-23.memory.json
```

---

## Upgrade Java first

The JVM keeps getting better!
