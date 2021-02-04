# Docker
1. Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)
2. Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.
3. Ответьте на вопрос: Можно ли в контейнере собрать ядро?
4. Определите разницу между контейнером и образом. Вывод опишите в домашнем задании.

# 1. Создаем свой образ на базе alpine
Создаем отдельную директорию и кладем туда все файлы:
Создаем файл Dockerfile (во вложении)
Создаем файл index.html с измененным содержимым
Создаем конфиг nginx
собираем наш образ командой
<code>vagrant@ubuntu  ~  docker build -t otus:nginx .</code>
видим что наш docker image собран 
```ruby
 vagrant@ubuntu  ~  docker images                                                                             
REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
otus          nginx     24a86ce2c245   4 seconds ago   6.99MB
alpine        3.12      389fef711851   7 weeks ago     5.58MB
hello-world   latest    bf756fb1ae65   13 months ago   13.3kB
```
Далее можем запустить наш контейнер командой
```ruby
vagrant@ubuntu  ~  docker run -d -p 8080:8080 24a86ce2c245                                            
a1f7b54b0ec25d7741906f60e494fb01b7f72860e81673d4459d22e757acc2c3
```
Смотрим, что контейнер запущен.
```ruby
vagrant@ubuntu  ~  docker ps                                                                                   
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                    NAMES
a1f7b54b0ec2   24a86ce2c245   "nginx -g 'daemon of…"   8 seconds ago   Up 7 seconds   0.0.0.0:8080->8080/tcp   priceless_rubin
```
постучимся курлом
```ruby
vagrant@ubuntu  ~  curl -I http://localhost:8080                                                                
HTTP/1.1 200 OK
Server: nginx/1.18.0
Date: Thu, 04 Feb 2021 15:23:13 GMT
Content-Type: text/html
Content-Length: 34
Last-Modified: Thu, 04 Feb 2021 15:20:44 GMT
Connection: keep-alive
ETag: "601c10cc-22"
Accept-Ranges: bytes
```
# 2. Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.
ссылка на репозиторий
<code>https://hub.docker.com/r/mpavliy/nginx</code>
Выполняем команду docker login, и вводим логин и пароль от нашего зарегистрированного аккаунта из docker-hub:
```ruby
 vagrant@ubuntu  ~  docker login                                                                   
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: mpavliy
Password:
WARNING! Your password will be stored unencrypted in /home/vagrant/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store
```
делаем PUSH
```ruby
vagrant@ubuntu  ~  docker tag 24a86ce2c245 mpavliy/nginx                                                 
 vagrant@ubuntu  ~  docker push mpavliy/nginx                                                       
Using default tag: latest
The push refers to repository [docker.io/mpavliy/nginx]
09f7e1e848c7: Pushed
cce426158cde: Pushed
aa41c6709af6: Pushed
fd92995ef1e9: Pushed
d17d80907810: Pushed
777b2c648970: Mounted from library/alpine
latest: digest: sha256:c1123fe249d822aaef4b7ee58bea06ec0e17548fd326e08dd025b20bb989f030 size: 1566
```
