
# 🚀 Установка и запуск Node.js

Node.js позволяет запускать JavaScript-код вне браузера (например, в терминале).

---

## 🪟 1. Windows

### 1.1 Установка
1. Перейди на официальный сайт: https://nodejs.org/
2. Скачай **LTS (рекомендуемую) версию**.
3. Запусти установщик `.msi` → далее → далее → готово.
4. После установки Node.js автоматически добавляется в `PATH`.

### 1.2 Проверка
Открой PowerShell или Git Bash:
```powershell
node -v     # версия Node.js
npm -v      # версия npm (менеджер пакетов)
````

### 1.3 Запуск скрипта

```powershell
# Создаём файл
nano app.js
```

Пример содержимого:

```javascript
console.log("Hello from Node.js!");
```

Запуск:

```powershell
node app.js
```

---

## 🍏 2. macOS

### 2.1 Установка через Homebrew

```bash
brew install node
```

Либо скачать с сайта: [https://nodejs.org/](https://nodejs.org/)

### 2.2 Проверка

```bash
node -v
npm -v
```

### 2.3 Запуск скрипта

```bash
nano app.js
```

Код:

```javascript
console.log("Hello from Node.js!");
```

Запуск:

```bash
node app.js
```

---

## 🐧 3. Linux (Ubuntu/Debian)

### 3.1 Установка (через apt)

```bash
sudo apt update
sudo apt install -y nodejs npm
```

> ⚡ Лучше использовать NodeSource для актуальной версии:

```bash
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
```

### 3.2 Проверка

```bash
node -v
npm -v
```

### 3.3 Запуск скрипта

```bash
nano app.js
```

Код:

```javascript
console.log("Hello from Node.js!");
```

Запуск:

```bash
node app.js
```

---

## 📦 4. Проверка через npm

Node.js идёт с `npm` (Node Package Manager). Проверим работу:

```bash
npm init -y             # создать package.json
npm install cowsay      # установить библиотеку cowsay
npx cowsay "Node.js OK"
```

Ожидаемый результат: ASCII-корова с текстом.

---

## ✅ Итог

* Установили Node.js + npm.
* Проверили версии.
* Создали и запустили первый скрипт.
* Попробовали пакет через npm.
