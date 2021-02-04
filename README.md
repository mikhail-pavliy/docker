# Docker
1. Создайте свой кастомный образ nginx на базе alpine. После запуска nginx должен отдавать кастомную страницу (достаточно изменить дефолтную страницу nginx)
2. Определите разницу между контейнером и образом. Вывод опишите в домашнем задании.
3. Ответьте на вопрос: Можно ли в контейнере собрать ядро?
4. Собранный образ необходимо запушить в docker hub и дать ссылку на ваш репозиторий.

# 1. Создаем свой образ на базе alpine
Создаем отдельную директорию и кладем туда все файлы:
Создаем файл Dockerfile (во вложении)
Создаем файл index.html с измененным содержимым
Создаем конфиг nginx
собираем наш образ командой
<code>[root@selinux nginx-alpine]# sudo docker build -t otus:nginx .</code>
видим что наш docker image собран 
<code>REPOSITORY    TAG       IMAGE ID       CREATED         SIZE
otus          nginx     def1e027eb8e   2 minutes ago   6.99MB
alpine        3.12      389fef711851   7 weeks ago     5.58MB
hello-world   latest    bf756fb1ae65   13 months ago   13.3kB </code>
