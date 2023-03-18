# Сборка для docker-compose NGINX + PHP:FPM

## application - папка для проекта

Контейнер NGINX имеет:
- 8080 - port (http://localhost:8080)
- /var/www/public - www root directory для (Laravel, Symfony)  

Контейнер PHP имеет:
- composer
- sudo
- ping
- develop - группа
- develop - пользователь

Пароль для root - 123, develop - 123

# Полезные команды:

Интерактивный вход под рутом в консоль контейнера. Ctrl+d - выход или exit
```
docker exec -u 0 -it mycontainer bash

# user: develop:
docker exec -it php bash
```
Заходя под develop, рабочая папка уже /var/www (application)  
можно запускать composer для установки, и другие команды.

# Запуск:
Из папки docker, где находится файл docker-compose.yml
```
docker-compose build    - собрать контейнеры
docker-compose up -d    - запустить контейнеры
docker-compose down     - остановить контейнеры

//
docker ps               - список запущенных контейнеров
docker ps -a            - список всех контейнеров
docker image ls         - список всех образов
```
# Framework install:
Удалить файл application/delete_me.txt перед установкой фреймворка,
иначе, композер выдаст ошибку что выбранная папка не нуста.  
А git не добавит в себя пустую папку.
```
composer create-project laravel/laravel .   # "." - local folder
OR
composer create-project symfony/skeleton .   # "." - local folder
```

# DataBase conf:
В .env файле указать внешний IP хоста с БД что смотрит наружу.