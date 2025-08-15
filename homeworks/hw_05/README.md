
# 🃏 Random Joke App in Docker

Простое Node.js приложение, которое при каждом запуске контейнера выводит случайную шутку.  
Весь процесс — **только через терминал**.

---

## 📂 1. Создание проекта

```bash
# 1. Создаём папку проекта и переходим в неё
mkdir hw_05 && cd hw_05

# 2. Создаём файл приложения
nano script.js
````

✏ **Вставляем код и сохраняем (CTRL+O → ENTER → CTRL+X):**

```javascript
const jokes = [
  "— Я программист. — И как это? — if (coffee) { code(); } else { coffee = true; }",
  "Вчера пытался пошутить на Java… но все просили интерфейсы для шуток.",
  "— Сколько нужно программистов, чтобы вкрутить лампочку? — Ни одного. Это аппаратная проблема.",
  "Доктор: «У вас выгорание». — «Можно stack trace?»",
  "— Почему прод не работает? — Потому что он работает не в моей среде.",
  "Я не ленивый — я в режиме энергосбережения.",
  'QA зашёл в бар: 0 пива, 1 пиво, 9999 пив, -1 пиво, "пиво"… Бар сгорел.',
  "Есть два сложных момента в IT: инвалидация кэша, нейминг и off-by-one ошибки.",
  "DevOps проснулся: «Где мои логи?»",
  "Код без багов — это код, который ещё никто не запускал.",
];

const randomIndex = Math.floor(Math.random() * jokes.length);
console.log(jokes[randomIndex]);
```

---

## 🐳 2. Создание Dockerfile

```bash
nano Dockerfile
```

📄 **Содержимое:**

```dockerfile
FROM node:22-alpine
WORKDIR /hw_05-app
COPY . .
CMD ["node", "script.js"]
```

💡 *Объяснение:*

* **node:22-alpine** — лёгкий официальный образ Node.js.
* **WORKDIR** — рабочая директория внутри контейнера.
* **COPY** — копируем файлы проекта.
* **CMD** — команда, которая будет выполняться при запуске контейнера.

---

## 📦 3. Создание `.dockerignore`

```bash
nano .dockerignore
```

📄 **Содержимое:**

```
# Исключить всё
*

# Разрешить только нужные файлы
!script.js
!Dockerfile
!.dockerignore
```

⚡ *Зачем нужно:*

* Уменьшает размер образа.
* Ускоряет сборку.
* Защищает от попадания лишних файлов (node\_modules, .git, логов и т.д.).

---

## 🛠 4. Сборка образа

```bash
docker build -t hw_05-app .
```

---

## ▶ 5. Запуск контейнера (локально)

```bash
docker run --rm hw_05-app
docker run --rm hw_05-app
```

💡 *При каждом запуске будет случайная шутка.*

---

## 🚀 6. Публикация в Docker Hub

```bash
# Вход в Docker Hub
docker login

# Тегируем образ (не забываем заменить USERNAME на свой логин Docker Hub)
docker tag hw_05-app USERNAME/random-joke:1.0
docker tag hw_05-app USERNAME/random-joke:latest

# Пушим в репозиторий
docker push USERNAME/random-joke:1.0
docker push USERNAME/random-joke:latest
```

---

## 🌍 7. Запуск образа с Docker Hub

```bash
docker run --rm USERNAME/random-joke:1.0
docker run --rm USERNAME/random-joke:latest
```

---

## 📌 Итог

✅ Мы создали Node.js приложение, упаковали его в минимальный Docker-образ, проверили локально и выложили в Docker Hub.
Теперь его можно запускать **в любой системе с Docker**, и оно всегда будет выводить случайную шутку.

