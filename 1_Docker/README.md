# 1 Установока wls и настройка Docker

### Установка wls
```bash
wsl --install -d Ubuntu
```
[1.1]

### Первый запуск Ubuntu

[1.2]

### Настройка Docker Desktop
1. Settings  
2. Resources 
3. WSL Integration 
4. Ubuntu, 
5. Apply restart.
[1.3]

### Проверка 
```bash
wsl.exe -l -v
docker pull hello-world
docker pull nginx:stable-alpine
docker version
docker run --rm hello-world
```
[1.4]
Ubuntu работает на WSL версии 2, оба образа скачаны. У Docker есть разделы Client и Server + выведено Hello from Docker!

# 2 Запуск готового сайта

```bash
docker run -d --name lab-web -p 127.0.0.1:8080:80 nginx:stable-alpine
docker ps
```
[1.5]
[1.6]

```bash
docker logs --tail 20 lab-web
```
[1.7]

# 3 Остановите и снова запустите сайт

Остановка
```bash
docker stop lab-web
docker ps
docker ps -a
```
[1.8]

Запуск
```bash
docker start lab-web
docker ps
docker exec lab-web cat /usr/share/nginx/html/index.html
```
[1.9]

# Этап 4. Файлы сайта

```bash
mkdir -p ~/docker-lesson-01
cd ~/docker-lesson-01
nano index.html
```
[1.10]
[1.11]

```bash
cd ~/docker-lesson-01
ls -l
nano Dockerfile
```
```bash
FROM nginx:stable-alpine
COPY index.html /usr/share/nginx/html/index.html
```
[1.12]
[1.13]
```bash
ls -l
cat Dockerfile
cat index.html
```
[1.14]

# Этап 5. Сборка образа и запуск
```bash
docker build -t student-site:v1 .
docker image ls student-site
```
[1.15]

```bash
docker run -d --name my-site -p 127.0.0.1:8081:80 student-site:v1
docker ps
```
[1.16]

# Этап 6. Вторая версия

```bash
nano index.html
```
[1.18]

```bash
docker restart my-site
```
[1.19]
[1.20]

# Этап 7. Второй контейнер

```bash
docker run -d --name my-copy -p 127.0.0.1:8082:80 student-site:v2
docker ps
```
[1.21]
[1.22]

```bash
docker stop my-site
docker ps -a
```
[1.23]
[1.24]

```bash
docker stop my-site
docker ps -a
```
[1.25]

```bash
docker start my-site
docker ps
```
[1.26]

# Этап 8. result.txt

```bash
cd ~/docker-lesson-01
nano result.txt
```
[1.27]
[1.28]

# Завершение работы 
```bash
docker stop lab-web my-site my-copy
docker rm lab-web my-site my-copy
```
