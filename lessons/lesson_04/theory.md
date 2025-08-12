## 📘 Основные понятия в Linux

| Понятие | Объяснение |
| --- | --- |
| **Linux** | Операционная система (ядро + утилиты). Основана на Unix. Используется на серверах, встраиваемых системах и на рабочих станциях. |
| **Ядро (Kernel)** | Сердце ОС — управляет ресурсами, процессами, памятью, устройствами. |
| **Дистрибутив** | Сборка ядра + утилит + пакетов (например: Ubuntu, Debian, Arch, Fedora). |
| **Файловая система** | Иерархическая структура из папок и файлов. Корень — `/`. |
| **Пользователь** | Каждый пользователь имеет имя, ID, домашнюю директорию (`/home/user`). |
| **root** | Главный администратор с полными правами. |
| **Shell (оболочка)** | Интерпретатор команд (например: `bash`, `zsh`). |
| **Процессы** | Запущенные программы. У каждого есть PID (Process ID). |
| **Права доступа** | На чтение, запись и выполнение. Делятся на: владелец / группа / остальные. |
| **Пакетный менеджер** | Утилита для установки и обновления ПО (например: `apt`, `yum`, `pacman`). |

___

```shell
apt update && apt install -y nano
apt install -y adduser
```

## 🧰 Основные команды Linux

### 🔍 Работа с файлами и каталогами

| Команда | Назначение |
| --- | --- |
| `ls` | Показать список файлов и папок |
| `ls -lh` | Показать список файлов и папок и права доступа |
| `cd имя_папки` | Перейти в папку |
| `pwd` | Показать текущий путь |
| `mkdir имя` | Создать папку |
| `rm файл` / `rm -r папка` | Удалить файл / папку рекурсивно |
| `cp источник назначение` | Копировать |
| `mv источник назначение` | Переместить или переименовать |
| `touch имя_файла` | Создать пустой файл |
| `cat файл` | Показать содержимое |
| `nano файл` / `vim файл` | Редактировать файл (в зависимости от редактора) |

___

### ⚙️ Система и процессы

| Команда | Назначение |
| --- | --- |
| `top` / `htop` | Показать активные процессы |
| `ps aux` | Все процессы |
| `kill PID` | Завершить процесс по PID |
| `df -h` | Информация о диске |
| `du -sh *` | Размер файлов и папок |
| `free -h` | Использование памяти |
| `uptime` | Время работы системы |
| `uname -a` | Информация о системе и ядре |

___

### 👥 Пользователи и права

| Команда | Назначение |
| --- | --- |
| `whoami` | Имя текущего пользователя |
| `adduser имя` | Добавить пользователя |
| `passwd имя` | Установить пароль |
| `su - имя` | Зайти под пользователем |
| `exit` | Выйти из сессии |
| `chmod 755 файл` | Изменить права доступа |
| `chown пользователь файл` | Изменить владельца |
| `groups имя` | Показать группы пользователя |
| `su` или `sudo` | Выполнить команду от имени root |

___

### 📦 Работа с пакетами (на Ubuntu/Debian)

| Команда | Назначение |
| --- | --- |
| `sudo apt update` | Обновить список пакетов |
| `sudo apt upgrade` | Обновить все пакеты |
| `sudo apt install имя` | Установить программу |
| `sudo apt remove имя` | Удалить программу |

___

## 🔐 Права доступа (символы)

-   `-` — тип (файл или папка)
-   `r` — read (чтение)
-   `w` — write (запись)
-   `x` — execute (запуск)
-   Тройки: владелец / группа / остальные

___

## 🧠 Рекомендуемые практики

-   Проверять, что вы удаляете: `rm` — безвозвратная

## Docker compose файл для линкус

```shell
version: "3.9"

services:
  linux:
    image: ubuntu
    container_name: my-linux
    tty: true
    stdin_open: true
    command: /bin/bash
```

```shell
docker exec -it my-linux /bin/sh
```

| Folder | Description |
| --- | --- |
| `/bin` | **Essential binaries** (commands) needed for basic system use (e.g. `ls`, `cp`, `mv`, `bash`) — available to all users. |
| `/boot` | Bootloader files and Linux kernel. Only needed during system startup. |
| `/dev` | Virtual files representing **hardware devices** (e.g. `/dev/sda` for disks, `/dev/null`). |
| `/etc` | **Configuration files** (system-wide). For example: `/etc/hosts`, `/etc/passwd`. |
| `/home` | Home directories for **regular users** (e.g. `/home/alice`, `/home/bob`). |
| `/lib` | Shared **libraries** (like DLLs in Windows) for essential programs in `/bin` and `/sbin`. |
| `/media` | Mount points for **external devices** (e.g. USB drives) automatically created. |
| `/mnt` | Temporary **mount points** for manually mounted file systems. |
| `/opt` | "Optional" software installed manually or third-party apps. Good place for your custom programs. |
| `/proc` | Virtual filesystem exposing **kernel and process info**. (e.g. `/proc/cpuinfo`) |
| `/root` | Home directory of the **root user** (admin). Not the same as `/`. |
| `/run` | Temporary system files and state during **boot**. Usually empty after shutdown. |
| `/sbin` | System binaries (e.g. `fsck`, `iptables`) — mostly for root user or system scripts. |
| `/srv` | "Service" data — for things like **web servers, FTP**, etc. (`/srv/www`, `/srv/ftp`). Rarely used in practice. |
| `/sys` | Exposes **system and hardware info** from the kernel (like `/proc`). |
| `/tmp` | Temporary files. Automatically cleared on reboot. Anyone can write here. |
| `/usr` | **User programs** and libraries. Includes `/usr/bin`, `/usr/lib`, etc. |
| `/var` | "Variable" files — log files, caches, databases (e.g. `/var/log`, `/var/lib/mysql`). |

## 🧮 Таблица `chmod` — числовые коды прав

| Код | Владелец (Owner) | Группа (Group) | Остальные (Others) | Что это значит |
| --- | --- | --- | --- | --- |
| `777` | `rwx` | `rwx` | `rwx` | Полный доступ для всех |
| `755` | `rwx` | `r-x` | `r-x` | Только владелец может изменять |
| `700` | `rwx` | `---` | `---` | Только владелец имеет доступ |
| `644` | `rw-` | `r--` | `r--` | Владелец может редактировать, остальные — только читать |
| `600` | `rw-` | `---` | `---` | Только владелец может читать и писать |
| `666` | `rw-` | `rw-` | `rw-` | Все могут читать и писать (⚠️ опасно) |
| `400` | `r--` | `---` | `---` | Только владелец может читать |
| `444` | `r--` | `r--` | `r--` | Только чтение для всех |
| `711` | `r-x` | `--x` | `--x` | Все могут запускать, но не читать содержимое |

___

## 📘 Как расшифровываются цифры

Каждая цифра = сумма прав:

| Цифра | Права | Значение |
| --- | --- | --- |
| `7` | `rwx` | 4 + 2 + 1 |
| `6` | `rw-` | 4 + 2 |
| `5` | `r-x` | 4 + 0 + 1 |
| `4` | `r--` | 4 |
| `3` | `-wx` | 2 + 1 |
| `2` | `-w-` | 2 |
| `1` | `--x` | 1 |
| `0` | `---` | 0 |

___

## 🔧 Как применять

```shell
chmod 644 file.txt
chmod 755 myscript.sh
chmod 700 secrets.env
```

___

## 🧠 Полезная команда для проверки

```shell
ls -l
```

Пример:

```shell
-rwxr-xr-- 1 user user  123 Aug 12 myscript.sh
```

Первая часть (`-rwxr-xr--`) показывает права:

-   `rwx` — владелец
-   `r-x` — группа
-   `r--` — остальные

___

Создайте внутри папки linux\_git папку example\_02 Внутри папки example\_02 создайте README.md Напишите в него следющий текст

## Hello Linux

Проверьте, что текст сохранился

Доп задание: переместите файл в папку linux\_git
