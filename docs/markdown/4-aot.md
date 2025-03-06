<img src="images/aot.png" alt="AOT" width="600"/>

---

Typical Spring Boot applications are quite dynamic and configuration is performed at runtime.

---

In fact, the concept of Spring Boot auto-configuration depends heavily on reacting to the state of the runtime in order to configure things correctly.

---

With Ahead Of Time (AOT) Processing, tradeoffs are made.

---

```java
@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

	@Bean
	public MyBean myBean() {
		return new MyBean();
	}

}
```

---

Generated code creates equivalent bean definitions to the @Configuration class,
but in a direct way that can be understood by GraalVM.

---

```java
/**
 * Bean definitions for {@link MyConfiguration}.
 */
public class MyConfiguration__BeanDefinitions {

	/**
	 * Get the bean definition for 'myConfiguration'.
	 */
	public static BeanDefinition getMyConfigurationBeanDefinition() {
		Class<?> beanType = MyConfiguration.class;
		RootBeanDefinition beanDefinition = new RootBeanDefinition(beanType);
		beanDefinition.setInstanceSupplier(MyConfiguration::new);
		return beanDefinition;
	}

	/**
	 * Get the bean instance supplier for 'myBean'.
	 */
	private static BeanInstanceSupplier<MyBean> getMyBeanInstanceSupplier() {
		return BeanInstanceSupplier.<MyBean>forFactoryMethod(MyConfiguration.class, "myBean")
			.withGenerator((registeredBean) -> registeredBean.getBeanFactory().getBean(MyConfiguration.class).myBean());
	}

	/**
	 * Get the bean definition for 'myBean'.
	 */
	public static BeanDefinition getMyBeanBeanDefinition() {
		Class<?> beanType = MyBean.class;
		RootBeanDefinition beanDefinition = new RootBeanDefinition(beanType);
		beanDefinition.setInstanceSupplier(getMyBeanInstanceSupplier());
		return beanDefinition;
	}

}
```

---

Spring AOT will generate code like this for all your bean definitions.

---

```bash
./mvnw -q -Pnative clean package -DskipTests

java -Dspring.aot.enabled=true \
-jar ./target/hello-spring-0.0.1-SNAPSHOT.jar

http :8080/actuator/metrics/application.started.time \
-o 3-4-java-23-aot.started.json
http :8080/actuator/metrics/jvm.memory.used \
-o 3-4-java-23-aot.memory.json
```
