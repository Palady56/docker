# Клиент-серверная архитектура Веб-приложения

Клиент-серверная архитектура приложения состоит из серверов:
- NGINX
- NodeJS (Framework NEXT.JS)
- NodeJS (API)
- Postgres (DataBase)
- Minio (S3 AWS Storage)

<br>

![Docker servers](/assets/container.png)

<br>
<br>

# Создание окружения для разработки Веб-приложения

<br>

## 1 Установка Docker

- 1.1 Скачиваем установщик **[Docker](https://docs.docker.com/get-docker/)**

- 1.2 Проверяем включена ли виртуализация, если выключена нужно включить (BIOS) *Опционально

- 1.3 Запустить установщик и пройти все этапы 

- 1.4 Запустить докер и дождаться когда он запустится

<br>
<br>

## 2 Скачиваем Git реплозиторий
<br>

- 2.1 Запускаем терминал Git Bash
<br>

- 2.2 В терминале выполняем команду клонирования репозитория
```
git clone git@github.com:Zeonlb426/docker.git
```
<br>

- 2.3 Переходим в склонированную директорию
```
cd docker/
```

<br>
<br>

## 3 Настройка протокола HTTPS
<br>

- 3.1 Выполняем в терминале команду установки центра сертификации(если еще не установлен), в процессе соглашаемся с установкой
```
.\mkcert.exe -install
```
<br>

- 3.2 Выполняем в терминале команду создания ключей-сертификатов для необходимого вам домена. Рекомендуется использовать домен второго уровня (например: *.exemple.dev)
```
.\mkcert.exe *.exemple.dev
```
<br>

- 3.3 Два созданных файла (_wildcard.exemple.dev.pem и _wildcard.exemple.dev-key.pem в корне директории \docker), перемещаем в папку ***\config\nginx\ssl***

<br>
<br>

## 4 Настройка конфигурации
<br>

- 4.1 В файле *default.conf*, находящийся в папке *\config\nginx\conf.d*, находим директиву ***server_name*** и заменяем домен ***instagram.lern.dev*** на ваш домен приложения (***например: application.exemple.dev***)

<br>

>
> Если ваша операционная система - Windows, выполняем следующее:
> - переходим в ***C:\Windows\System32\drivers\etc***
> - открываем файл hosts с правами администратора
> - в конец файла добавляем запись с новой строки и сохраняем изменения:
>```
>127.0.0.1 application.exemple.dev
>```
>***где application.exemple.dev домен вашего приложения***
>
<br>

- 4.2 В корне директории \docker, переименовываем файл настроек окружения .env.example  в .env
<br>

- 4.3 Открываем .env файл на редактирование, в директиве PROJECT_DIR заменяем *path_to_projects* на путь к директории, где хранятся ваши проекты. (*например: C:\work\projects*) Сохраняем изменения.
<br>

- 4.4 Создаем в папке с вашими проектами папку, где будет находиться код вашего приложения
<br>

- 4.5 Создаем в папке вашего проекта две подпапки: api и app, в папке api будет находиться код для api-сервера, в папке app соответственно код для frontend
<br>
<br>

## 5 Запуск контейнеров
<br>

- 5.1 Открываем терминал в корне директории \docker, там где храниться файл docker-compose.yml и выполняем команду:
```
docker-compose up --build -d
```
<br>

- 5.2 Проверяем запустились ли все контейнеры, должны быть зеленого цвета со статусом running

<br>

![Docker containers](/assets/docker.png)

<br>

- 5.3 Заходим в нутрь контейнера **client** c node.js
```
docker-compose exec client sh
```
<br>

в терминале должен отобразиться следующий путь:
```
/opt/server #
```

- 5.4 Переходим в проект, в папку ***app*** с помощю команды ***cd***
```
cd project_dir/app/
```
где project_dir - папка с вашим проектом

<br>

- 5.5 Находясь в папке ***app*** вашего проекта, запускаем команду установки Next.js
```
npx create-next-app@latest .
```
<br>

- 5.6 В процессе установки, отвечаем на вопросы установщика, согласно нужной вам конфигурации

- 5.7 После завершения установки, запускаем команду на выполнение:
```
npm run dev
```
<br>


- 5.8 После запуска сервера Next, открываем браузер и заходим на домен вашего приложения. Должна отобразиться стартовая страница фреймворка Next.js

Смена владельца директории
(sudo chown -R youreusername /path/to/working/directory)

Установка пользователя root (для wsl)
ubuntu2204 config --default-user root

 
