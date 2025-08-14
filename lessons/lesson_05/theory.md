## Docker

**1\. Docker Desktop** Это как красивая кухня с плитой, духовкой и панелью управления. На ней есть кнопки, окна и всё удобно для работы — чтобы повар (ты) мог видеть, что готовится, и быстро запускать/останавливать процессы. 📌 Это программа с графическим интерфейсом для Windows и macOS, которая упрощает работу с Docker.

___

**2\. Docker Engine** Это сама «плита» и «духовка» внутри кухни. Она реально греет, варит и печёт, когда ты ей даёшь рецепт. 📌 Это основной механизм Docker, который запускает и управляет контейнерами. Работает на фоне, без красивых кнопок.

___

**3\. Image (образ)** Это как рецепт блюда 📖. В нём написано: какие продукты нужны, в каком порядке их класть и как готовить. 📌 Образ — это «застывший» шаблон программы со всем, что ей нужно для работы (код, библиотеки, конфиги).

___

**4\. Container (контейнер)** Это уже готовое блюдо 🍲, сделанное по рецепту (образу). 📌 Контейнер — это запущенная копия образа, которая реально работает и выполняет задачи.

___

**5\. Process / Server** Это как официант, который разносит еду, пока ты готовишь новые блюда. 📌 Внутри контейнера обычно запускается процесс (например, веб-сервер), который принимает запросы и отвечает на них.

___

💡 **Если собрать всё вместе:**

-   **Docker Desktop** — красивая кухня, где видно, что готовишь.
-   **Docker Engine** — мотор кухни, который всё реально делает.
-   **Image** — рецепт.
-   **Container** — готовое блюдо по рецепту.

## Основные команды Docker

___

## 📦 Работа с образами

```
docker build -t имя_образа .      # Собрать образ из Dockerfile
docker images                     # Показать список образов
docker rmi имя_образа             # Удалить образ
```

___

## 🏃 Запуск контейнеров

```
docker run имя_образа                     # Запустить контейнер
docker run --rm имя_образа                 # Запустить и удалить после завершения
docker run -it имя_образа /bin/sh          # Запустить с интерактивным терминалом
docker ps                                  # Показать запущенные контейнеры
docker ps -a                               # Показать все контейнеры
docker stop id_или_имя                     # Остановить контейнер
docker rm id_или_имя                       # Удалить контейнер
```

___

## 📤 Работа с Docker Hub

```
docker login                               # Войти в Docker Hub
docker tag имя_образа user/репо:тег        # Переименовать (тегировать) образ
docker push user/репо:тег                  # Отправить образ в Docker Hub
docker pull user/репо:тег                  # Скачать образ с Docker Hub
```

___

## 🛠 Полезное

```
docker exec -it id_или_имя bash            # Зайти внутрь запущенного контейнера
docker logs id_или_имя                     # Посмотреть логи контейнера
docker system prune -a                     # Очистить все неиспользуемые образы/контейнеры
```

___

## Инструкция - как создать простое докер приложение, выводящее в консоль. Выложить его на докер-хаб

___

## 1\. Создаём папку и заходим в неё

```shell
mkdir console-log-app
cd console-log-app
```

___

## 2\. Создаём файл **app.js**

**app.js**:

```javascript
console.log("Hello from inside Docker!");
```

___

## 3\. Создаём файл **Dockerfile**

**Dockerfile**:

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY . .
CMD ["node", "app.js"]
```

___

## 4\. Собираем образ

```shell
docker build -t console-log-app .
```

___

## 5\. Логинимся в Docker Hub
```shell
docker login
```

## 6\. Тегируем образ под свой репозиторий

```shell
docker tag console-log-app myname/console-log-app:latest
```

_(замени `myname` на свой Docker Hub username)_

___

## 7\. Пушим на Docker Hub

```shell
docker push myname/console-log-app:latest
```

___

## 8\. Проверка

```shell
docker run --rm myname/console-log-app
```

Ожидаемый вывод:

```shell
Hello from inside Docker!
```

___

## 🗂 Структура Dockerfile

| Инструкция | Описание |
| --- | --- |
| **FROM** | Базовый образ, с которого начинаем. Пример: `FROM node:18-alpine` |
| **WORKDIR** | Рабочая директория внутри контейнера. Если нет — создаётся. Пример: `WORKDIR /app` |
| **COPY** | Копирует файлы с хоста в контейнер. Пример: `COPY . .` (всё в текущую рабочую папку) |
| **RUN** | Выполняет команду при сборке образа. Пример: `RUN npm install` |
| **CMD** | Команда, которая запускается **по умолчанию** при старте контейнера. Пример: `CMD ["node", "app.js"]` |
| **ENTRYPOINT** | Основная команда, которую можно дополнять аргументами при запуске контейнера. Пример: `ENTRYPOINT ["npm", "start"]` |
| **EXPOSE** | Документирует, какие порты контейнер использует. Пример: `EXPOSE 3000` |
| **ENV** | Переменные окружения. Пример: `ENV NODE_ENV=production` |

___

## 🔹 Минимальный пример

```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "server.js"]
```

**Как это работает:**

1.  **FROM** — берём официальный образ Node.js.
2.  **WORKDIR** — создаём и переходим в `/app`.
3.  \*_COPY package_.json ./\*\* — копируем файлы с зависимостями.
4.  **RUN npm install** — устанавливаем зависимости.
5.  **COPY . .** — копируем весь проект в контейнер.
6.  **EXPOSE 3000** — указываем порт приложения.
7.  **CMD** — запускаем сервер.

___

## Пример: простой Node.js сервер + Dockerfile, который его запускает.

___

## 1\. Структура проекта

```
simple-server/
├── server.js
├── package.json
└── Dockerfile
```

___

## 2\. Код простого сервера

**`server.js`**

```javascript
const http = require('http');

const PORT = 3000;

const server = http.createServer((req, res) => {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello from Docker server!\n');
});

server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}/`);
});
```

___

**`package.json`**

```json
{
  "name": "simple-server",
  "version": "1.0.0",
  "main": "server.js"
}
```

_(Здесь нет зависимостей, так как мы используем встроенный модуль `http`.)_

___

## 3\. Dockerfile

**`Dockerfile`**

```dockerfile
# 1. Базовый образ Node.js
FROM node:18-alpine

# 2. Рабочая директория
WORKDIR /app

# 3. Копируем package.json
COPY package.json .

# 4. (Нет npm install, т.к. зависимостей нет)
# Если бы были — добавили бы:
# RUN npm install

# 5. Копируем остальной код
COPY . .

# 6. Открываем порт 3000
EXPOSE 3000

# 7. Запуск сервера
CMD ["node", "server.js"]
```

___

## 4\. Сборка и запуск

```shell
docker build -t simple-server .
docker run -p 3000:3000 simple-server
```

Теперь сервер доступен на [http://localhost:3000](http://localhost:3000/) Ответ:

```
Hello from Docker server!
```

___

## Если хотим - можем добавить **docker-compose** для `simple-server`.

___

**`docker-compose.yml`**

```dockerfile
version: "3.8"

services:
  simple-server:
    build: .
    container_name: simple-server-container
    ports:
      - "3000:3000"
```

___

### Как использовать

1.  Убедись, что рядом с этим файлом есть твой
    
    -   `Dockerfile`
    -   `server.js`
    -   `package.json`
2.  Запусти:
  ```shell
  docker-compose up
  ```

3.  Перейди в браузере на:

```
http://localhost:3000
```

Ты увидишь:

```
Hello from Docker server!
```

4.  Остановить:

```shell
docker-compose down
```
