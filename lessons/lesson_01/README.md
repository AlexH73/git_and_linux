# Основные команды гит
- инициализировать: git init
- git add . -выбирает файлы с изменениями, которые вы будете сохранять
- git add README.md - можно указать конкретный файл, который вы хотите сохранить
- git commit -m "текст сообщения"


Сообщение коммита:
- add - добавили 
- fix - починили
- remove - удалили

git log --oneline -это посмотреть список коммитов
git checkout номер_коммита -это переключиться в коммит - в определенную версию

// staged - то что будет добавлено в комит

// changes - все изменения

Локальный репозиторий - на компьютере конкретного человека
Удаленный репозиторий - remote repo

Мы создать удаленный репозиторий и связать его с нашим локальным

git branch -m master main -если хотим переименовать ветка мастер

git remote add origin ссылка_на_репо
git branch -M main
git push -u origin main
