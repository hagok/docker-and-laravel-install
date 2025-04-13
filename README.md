# Установка laravel с использованием Docker-compose

Здесь готовые файлы для установки на Docker проекта laravel 12:
1. php:8.2-fpm
2. nginx:latest
3. mysql:8.0
4. composer
##

<br/>

0. Клонируем на свою машину
```
git clone https://github.com/hagok/docker-and-laravel-install.git
```
1. Копируем всё (кроме .git и README.md) из репозитория в папку где будет лежать проект. В Windows для отличной работы, нужно ложить в файловую систему Linux.
2. Через терминал заходим в эту папку. 
3. Поднимаем контейнер через docker-compose:
```
docker-compose up -d
```
4. Заходим в контейнер проекта app_project:
```
docker exec -it app_project bash
```
5. Внутри создаем новый проект laravel:
```
composer create-project laravel/laravel
```
6. Выходим из контейнера
```
exit
```
7. Опускаем контейнер:
```
docker-compose down
```
8. Копируем всё из папки laravel в корневую папку проекта, после удаляем папку laravel.
9. Открываем файл `_docker/.env` и копируем от туда конфигурацию MySql, добавляем в файл `.env` в корне проекта:
```
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laradocker
DB_USERNAME=root
DB_PASSWORD=root
```
10. Опять поднимаем контейнер:
```
docker-compose up -d
``` 
11. Переходим на 
```
http://localhost:777/
```
12. Если ошибка `Permission denied`, то открываем права для пользователя Linux:
```
sudo chmod 777 -R ./
```
13. Вводим пароль от Linux.
14. Заходим в контейнер проекта app_project:
```
docker exec -it app_project bash
```
14. Делаем стандартные миграции Laravel:
```
php artisan migrate
```
15. Обновляем `http://localhost:777/`.
16. Вуаля! Laravel на базе!