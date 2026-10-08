# Этап 1 подготовка
```bash
cd ~/docker-lesson-02
docker pull wordpress:apache
docker pull mariadb:11.4
docker version
docker compose version
```
![](../sourse/2.1.png)
![](../sourse/2.2.png)

# Этап 2 файл Compose
```bash
nano compose.yaml
```
```bash
name: docker-lesson-02

services:
  db:
    image: mariadb:11.4
    environment:
      MARIADB_DATABASE: wordpress
      MARIADB_USER: student
      MARIADB_PASSWORD: lab-db-pass
      MARIADB_ROOT_PASSWORD: lab-root-pass
    volumes:
      - db_data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "healthcheck.sh", "--connect", "--innodb_initialized"]
      interval: 5s
      timeout: 5s
      retries: 30
      start_period: 30s

  wordpress:
    image: wordpress:apache
    ports:
      - "127.0.0.1:8090:80"
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_NAME: wordpress
      WORDPRESS_DB_USER: student
      WORDPRESS_DB_PASSWORD: lab-db-pass
    depends_on:
      db:
        condition: service_healthy
    volumes:
      - wp_data:/var/www/html

volumes:
  db_data:
  wp_data:
```
![](../sourse/2.3.png)
```bash
docker compose up -d
docker compose ps
```
![](../sourse/2.4.png)
```bash
```

# Этап 3 запуск сервисов
```bash
docker compose up -d
docker compose ps
```
![](../sourse/2.5.png)

# Этап 4 установка
WordPress установлен. Дальше:
![](../sourse/2.6.png)

# Этап 5 логи и остановка wordpress
```bash
docker compose stop wordpress
docker compose ps -a
```
![](../sourse/2.7.png)
```bash
docker compose start wordpress
docker compose ps
```
![](../sourse/2.8.png)

# Этап 6 пересоздание контейнера
```bash
docker compose ps -q > containers-before.txt
docker compose down
docker compose ps -a
docker volume ls --filter label=com.docker.compose.project=docker-lesson-02
```
![](../sourse/2.9.png)

```bash
docker compose up -d
docker compose ps
docker compose ps -q > containers-after.txt
cat containers-before.txt
cat containers-after.txt
```
![](../sourse/2.10.png)

# Этап 7 остановка и восстановление базы
```bash
docker compose stop db
docker compose ps -a
```
![](../sourse/2.11.png)
```bash
docker compose start db
docker compose ps
```
![](../sourse/2.12.png)
![](../sourse/2.13.png)
![](../sourse/2.14.png)

# Этап 8 result.txt
```bash
cd ~/docker-lesson-02
nano result.txt
```
![](../sourse/2.15.png)