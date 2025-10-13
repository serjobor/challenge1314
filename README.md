# Челлендж. 1.3. 1.4

Предоставьте решение в виде содержимого yml-файла actions.yml, который бы позволял развертывать собранный статический сайт на сервисе play-with-docker. 

## Что было сделано
- зашел на сайт labs.play-with-docker.com

- Создал новый инстанс

- Создал папку my-site

```bash
mkdir my-site && cd my-site
```

- Создал actions.yml

```bash
vim actions.yml
```

- Внес изменения в файл actions.yml

```yml
version: '3.8'
services:
  static-website:
    build: .
    ports:
      - "80:80"
    volumes:
      - ./site:/usr/share/nginx/html
    restart: always
    labels:
      - "description=Static Website"
```

- Создал Dockerfile

```bash
vim Dockerfile
```

- Внес изменения в Dockerfile

```bash
FROM nginx:alpine
COPY site/ /usr/share/nginx/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

- Создал папку site 

```bash
mkdir site && cd site
```

- Создал index.html

```bash
vim index.html
```

- Внес изменения в файл index.html

```html
<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <title>Мой сайт</title>
</head>
<body>
    <h1>Добро пожаловать!</h1>
    <p>Сайт работает через Docker Compose</p>
</body>
</html>
```

- Вышел из папки site и запустил actions.yml через докер компоуз

```bash
docker-compose -f actions.yml up -d
```