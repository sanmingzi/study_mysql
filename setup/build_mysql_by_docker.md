# build mysql by docker

## docker-compose.yml

```m
version: "3.3"

services:
  mysql_development:
    image: mysql:5.7
    container_name: mysql_development
    restart: always
    network_mode: "host"
    environment:
      MYSQL_DATABASE: "mysql_development"
      MYSQL_ROOT_PASSWORD: "root"
      # MYSQL_USER: 'development'
      # MYSQL_PASS: 'development'
    volumes:
      - mysql_development:/var/lib/mysql
    # ports:
    #   - "3306:3306"
      
volumes:
  mysql_development:
```

## command

```m
docker-compose up -d
docker exec -it mysql_development bash
mysql -u root -p
Enter password: root
```
