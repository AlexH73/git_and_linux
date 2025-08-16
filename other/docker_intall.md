# 🐳 Установка Docker Desktop (Windows / macOS / Linux)

---

## 🔹 Общие требования

- Поддержка виртуализации (BIOS/UEFI → включить **Intel VT-x** или **AMD-V**).
- 64-битная ОС.
- Учётная запись Docker Hub (https://hub.docker.com/).

---

## 🪟 1. Установка Docker Desktop на Windows

### 1.1 Системные требования
- Windows 10 **64-bit Pro, Enterprise, Education** (2004+) или Windows 11.
- Для Windows 10 Home требуется **WSL 2**.
- Минимум 4 GB RAM.

### 1.2 Установка
```bash
# 1. Скачать установщик
https://www.docker.com/products/docker-desktop/

# 2. Запустить .exe файл и пройти установку
# 3. При установке поставить галочки:
#    ✅ Use WSL 2 instead of Hyper-V
#    ✅ Add shortcut to Desktop
```

### 1.3 Настройка WSL2 (если Windows 10 Home)
```powershell
# Установить WSL2
wsl --install

# Проверить версию
wsl -l -v
```

### 1.4 Проверка
```powershell
docker --version
docker run hello-world
```

---

## 🍏 2. Установка Docker Desktop на macOS

### 2.1 Системные требования
- macOS Monterey (12) или новее.
- Архитектуры: Intel или Apple Silicon (M1/M2/M3).
- Минимум 4 GB RAM.

### 2.2 Установка
```bash
# 1. Скачать dmg-пакет
https://www.docker.com/products/docker-desktop/

# 2. Открыть .dmg → перетащить Docker в Applications
# 3. Запустить Docker Desktop (первый запуск может занять время)
```

### 2.3 Проверка
```bash
docker --version
docker run hello-world
```

---

## 🐧 3. Установка Docker Desktop на Linux

### 3.1 Системные требования
- Ubuntu, Debian, Fedora, Arch Linux (современные версии).
- 64-bit CPU.
- Kernel 5.10+.

### 3.2 Установка (Ubuntu / Debian)
```bash
# Обновить систему
sudo apt update && sudo apt upgrade -y

# Установить зависимости
sudo apt install ca-certificates curl gnupg lsb-release -y

# Добавить GPG ключ Docker
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Добавить репозиторий
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg]   https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"   | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Установка Docker Engine и Docker Compose
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

### 3.3 Установка Docker Desktop (GUI)
```bash
# Скачать .deb пакет с официального сайта
https://www.docker.com/products/docker-desktop/

# Установить
sudo apt install ./docker-desktop-<version>-<arch>.deb
```

### 3.4 Проверка
```bash
docker --version
docker compose version
docker run hello-world
```

---

## ⚙️ 4. Пост-установка (Linux)

Разрешить запуск Docker без `sudo`:
```bash
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```

---

## 🧪 Проверка работы на всех ОС
```bash
docker run hello-world
```

Ожидаемый результат:  
Docker скачает тестовый образ и выведет сообщение:  
**"Hello from Docker!"**

---

## 📌 Советы
- Обновляй Docker Desktop через встроенный апдейтер или заново скачивай с сайта.
- Для работы с проектами удобнее войти в Docker Hub прямо из Docker Desktop.
- На Linux можно использовать как **Docker Engine + CLI**, так и **Docker Desktop** (с GUI).

---
