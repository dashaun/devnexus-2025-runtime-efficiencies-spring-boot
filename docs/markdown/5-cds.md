<img src="images/cds.png" alt="CDS" width="600"/>

---

Class Data Sharing (CDS) is a JVM feature that can help reduce the startup time and memory footprint of Java applications.

---

To use it, you should first perform a training run on your application in extracted form.

---

```bash
./mvnw clean package
java -Djarmode=tools -jar ./target/hello-spring-0.0.1-SNAPSHOT.jar extract --destination application
java -XX:ArchiveClassesAtExit=application.jsa -Dspring.context.exit=onRefresh -jar application/hello-spring-0.0.1-SNAPSHOT.jar
```
> Create the shared archive

---

```bash
java -XX:SharedArchiveFile=application.jsa -jar applicatin/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time -o 3-4-java-23-cds.started.json
http :8080/actuator/metrics/jvm.memory.used -o 3-4-java-23-cds.memory.json
```
