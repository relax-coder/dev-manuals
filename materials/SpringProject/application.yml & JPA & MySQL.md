application.yml & JPA & MySQL


```
spring:
  jpa:
    database-platform: org.hibernate.dialect.MySQL8Dialect
    show-sql: true
    hibernate:
      ddl-auto: create-drop
  datasource:
    url: jdbc:mysql://localhost:3306/app_db?createDatabaseIfNotExist=true
    driverClassName: com.mysql.cj.jdbc.Driver
    username: [your username]
    password: [your password]
```



```
spring:
  jpa:
    database-platform: org.hibernate.dialect.H2Dialect
    show-sql: true
    hibernate:
      ddl-auto: create-drop
  datasource:
    url: jdbc:h2:mem:testdb
    driverClassName: org.h2.Driver
    username: sa
    password: password
  h2:
    console:
      enabled: true
```

