Iniciamos con las dependencias del proyecto

```xml
<dependencies>  
    <dependency>  
        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-web</artifactId>  
    </dependency>  
  
    <dependency>  
        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-test</artifactId>  
        <scope>test</scope>  
    </dependency>  
  
    <dependency>  
        <groupId>org.springframework.boot</groupId>  
        <artifactId>spring-boot-starter-data-jpa</artifactId>  
    </dependency>  
  
    <dependency>  
        <groupId>org.postgresql</groupId>  
        <artifactId>postgresql</artifactId>  
        <scope>runtime</scope>  
    </dependency>  
</dependencies>
```

1. `spring-boot-starter-web`: REST controllers, necesario para endpoints HTTP
2. `spring-boot-starter-test`: Necesario para el testing del código
3. `spring-boot-starter-data-jpa`: Soporte para el Java Persistence API (JPA)
4. `postgresql`: Conectarnos con PostgreSQL