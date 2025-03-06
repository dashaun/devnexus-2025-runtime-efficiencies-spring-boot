<img src="images/extract.png" alt="extracting jar" width="600"/>

---

By "extract" -ing the Jar file, we can improve the startup time.

---

This is where I got messed up during the presentation.

This works, slightly different, with Spring Boot 2.7
[layertools](https://docs.spring.io/spring-boot/docs/2.7.18/reference/html/container-images.html#container-images.dockerfiles) with Spring Boot 2.7.

Upgrade the pom.xml to Spring Boot 3.4.3 and Java 23.

---

```bash
./mvnw clean package 

java -Djarmode=layertools \
-jar ./target/hello-spring-0.0.1-SNAPSHOT.jar \
extract --destination application

java -jar ./application/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time \
-o 2-7-java-23-extract.started.json

http :8080/actuator/metrics/jvm.memory.used \
-o 2-7-java-23-extract.memory.json

rm -rf application
```