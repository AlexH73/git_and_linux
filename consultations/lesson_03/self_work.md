## выполнение [самостоятельной работы](task.md) (пошагово)

- В папке team60 в корневой директории создайте  файл с информацией о юзере и названии версии linux (имя возьмите из команд) {"user": …, "system": …}

```shell
# перейти в корень
cd /

# создать папку в корне
sudo mkdir -p /team60

# собрать значения из команд
USER_NAME="$(whoami)"
SYS_NAME="$(uname -sr)"   # ядро + релиз (кросс-дистрово)

# записать JSON атомарно и красиво
printf '{"user":"%s","system":"%s"}\n' "$USER_NAME" "$SYS_NAME" | sudo tee /team60/info.json > /dev/null

# проверка
sudo cat /team60/info.json
```

- Создайте несколько вложенных каталогов в одну команду - в домашней директории storage/system/process

```shell
mkdir -p ~/storage/system/process   
```
- В папке storage создайте текстовый файл с информацией о свободном месте на диске

```shell
df -h > ~/storage/disk_free.txt

# проверка
head -n 20 ~/storage/disk_free.txt # вывод первых 20 строк
# или
cat ~/storage/disk_free.txt # вывод всего файла
```
- В папке system с информацией о системе.

```shell
{
  echo "DATE:   $(date 2>/dev/null || true)"
  echo "KERNEL: $(uname -srmo 2>/dev/null || uname -a)"
  echo "UPTIME: $(uptime 2>/dev/null || true)"
  echo "CPU:    $(grep -m1 'model name' /proc/cpuinfo 2>/dev/null || true)"
  echo "MEMINFO (first lines):"
  head -n 5 /proc/meminfo 2>/dev/null || true
} > ~/storage/system/system_info.txt

# проверка
sed -n '1,20p' ~/storage/system/system_info.txt
# вывод первых 20 строк
```

- В папке process файл с информацией о трех самых затратных процессах в системе.

```shell
top -b -n 1 | sed -n '8,10p' > ~/storage/system/process/top3_processes.txt
# проверка
cat ~/storage/system/process/top3_processes.txt
```

### быстрая проверка структуры каталогов
```shell
echo "---- /team60"; sudo ls -l /team60
echo "---- ~/storage"; ls -l ~/storage
echo "---- ~/storage/system"; ls -l ~/storage/system
echo "---- ~/storage/system/process"; ls -l ~/storage/system/process
```