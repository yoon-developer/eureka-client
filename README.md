Spring Cloud Netflix Eureka (Client)
==========

# 1. build.gradle
> 버전  
- spring cloud: 2020.0.1  
- spring-boot-starter-web: 2.4.3
- spring-cloud-starter-netflix-eureka-client: 3.0.1

> dependencies 추가
- org.springframework.cloud:spring-cloud-starter-netflix-eureka-client

```text
ext {
	set('springCloudVersion', "2020.0.1")
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	implementation 'org.springframework.cloud:spring-cloud-starter-netflix-eureka-client'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
}

dependencyManagement {
	imports {
		mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
	}
}
```

# 2. Application.yml

> 서버 포트 설정
```yaml
server:
  port: 8080
```

> eureka 설정
- spring.applicaion.name: eureka 서비스 등록시 서비스 이름 설정
- eureka.client.serviceUrl.defaultZone: DefaultZone Url 설정을 통해 동일한 zone의 eureka server clustering 설정
- eureka.instance.instance-id: 서비스 ID 설정

```yaml
spring:
  application:
    name: eureka-client

eureka:
  instance:
    instance-id: ${spring.application.name}:${spring.application.instance_id:${random.value}}
  client:
    serviceUrl:
      defaultZone: ${EUREKA_URL:http://127.0.0.1:8761/eureka/}
```

# 3. Code

> @EnableDiscoveryClient 추가
```java
@EnableDiscoveryClient
@SpringBootApplication
public class EurekaClientApplication {

  public static void main(String[] args) {
    SpringApplication.run(EurekaClientApplication.class, args);
  }

}
```