### Размещаем свой RPM в своем репозитории
#### Цель: 
  Часто в задачи администратора входит не только установка пакетов,
но и сборка и поддержка собственного репозитория. Этим и займемся в ДЗ.

1) создать свой RPM (можно взять свое приложение, либо собрать к примеру апач с определенными опциями)
2) создать свой репо и разместить там свой RPM

  Реализовать это все либо в вагранте, либо развернуть у себя через nginx и дать ссылку на репо 

* реализовать дополнительно пакет через docker

### Домашняя работа.
#### Цель: 
  Собрать и развернуть nginx в docker.

#### Решение:
  В Vagrantfile добавим команду  yum install -y docker. Создадим файлы для проброса в вм
Dockerfile и default.conf

  Подключаемся по ssh, меняем пользователя на root и меняем директорию
    - su
    - cd /vagrant/

  Запускаем сервис docker
    - systemctl start docker

  Собираем образ
    - docker build -t centos7/nginx .

  Запускаем собранный образ с редиректом портов
    - docker run -d -p 80:80 -p 443:443 centos7/nginx

  Просмотрим запущенные образы
    - docker container ls

  Это команда для проверки работы nginx
    - curl -a http://localhost

  Команда для останоовки всех образов
    - docker stop $(docker ps -a -q)

