MySQL by Docker Compose

create a file and naming "docker-compose.yml"

Template 
```yaml
version: '3.3'

services:
  db:
    image: [image from DockerHub]
    container_name: [your container name]
    environment:
      MYSQL_ROOT_PASSWORD: [password for root]
      MYSQL_DATABASE: [database name]
    ports:
      - "[local port]:[container port]"
```

Sample 
```yaml
version: '3.3'

services:
  db:
    image: mysql:8.0.22
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: "password"
      MYSQL_DATABASE: "myDatabase"
    ports:
      - "3307:3306"
```
