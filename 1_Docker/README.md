# 1 Установока wls и настройка Docker

### Установка wls
```bash
wsl --install -d Ubuntu
```
![](../sourse/1.1.png)

### Первый запуск Ubuntu

![](../sourse/1.2.png)

### Настройка Docker Desktop
1. Settings  
2. Resources 
3. WSL Integration 
4. Ubuntu, 
5. Apply restart.
![](../sourse/1.3.png)

### Проверка 
```bash
wsl.exe -l -v
docker pull hello-world
docker pull nginx:stable-alpine
docker version
docker run --rm hello-world
```
![](../sourse/1.4.png)
Ubuntu работает на WSL версии 2, оба образа скачаны. У Docker есть разделы Client и Server + выведено Hello from Docker!

# 2 Запуск готового сайта

```bash
docker run -d --name lab-web -p 127.0.0.1:8080:80 nginx:stable-alpine
docker ps
```
![](../sourse/1.5.png)
![](../sourse/1.6.png)
```bash
docker logs --tail 20 lab-web
```
![](../sourse/1.7.png)

# 3 Остановите и снова запустите сайт

Остановка
```bash
docker stop lab-web
docker ps
docker ps -a
```
![](../sourse/1.8.png)

Запуск
```bash
docker start lab-web
docker ps
docker exec lab-web cat /usr/share/nginx/html/index.html
```
![](../sourse/1.9.png)

# Этап 4. Файлы сайта

```bash
mkdir -p ~/docker-lesson-01
cd ~/docker-lesson-01
nano index.html
```
![](../sourse/1.10.png)
![](../sourse/1.11.png)

```bash
cd ~/docker-lesson-01
ls -l
nano Dockerfile
```
```bash
FROM nginx:stable-alpine
COPY index.html /usr/share/nginx/html/index.html
```
![](../sourse/1.12.png)
![](../sourse/1.13.png)
```bash
ls -l
cat Dockerfile
cat index.html
```
![](../sourse/1.14.png)

# Этап 5. Сборка образа и запуск
```bash
docker build -t student-site:v1 .
docker image ls student-site
```
![](../sourse/1.15.png)

```bash
docker run -d --name my-site -p 127.0.0.1:8081:80 student-site:v1
docker ps
```
![](../sourse/1.16.png)
![](../sourse/1.17.png)
# Этап 6. Вторая версия

```bash
nano index.html
```
![](../sourse/1.18.png)

```bash
docker restart my-site
```
![](../sourse/1.19.png)
![](../sourse/1.20.png)

# Этап 7. Второй контейнер

```bash
docker run -d --name my-copy -p 127.0.0.1:8082:80 student-site:v2
docker ps
```
![](../sourse/1.21.png)
![](../sourse/1.22.png)

```bash
docker stop my-site
docker ps -a
```
![](../sourse/1.23.png)
![](../sourse/1.24.png)

```bash
docker stop my-site
docker ps -a
```
![](../sourse/1.25.png)

```bash
docker start my-site
docker ps
```
![](../sourse/1.26.png)

# Этап 8. result.txt

```bash
cd ~/docker-lesson-01
nano result.txt
```
![](../sourse/1.27.png)
![](../sourse/1.28.png)

# Завершение работы 
```bash
docker stop lab-web my-site my-copy
docker rm lab-web my-site my-copy
```
