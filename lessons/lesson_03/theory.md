# 🌿 Git Branching & Workflow Guide

## 📌 Конвенция по именованию коммитов

Добавляй **префиксы** к названиям коммитов для ясности:

| Префикс     | Назначение                             | Пример                           |
| ----------- | -------------------------------------- | -------------------------------- |
| `feat:`     | Новый функционал                       | `feat: add search bar`           |
| `fix:`      | Исправление бага                       | `fix: search bar validation`     |
| `docs:`     | Изменения в документации               | `docs: add info on loading`      |
| `chore:`    | Поддержка, обновления зависимостей     | `chore: add prettier`            |
| `refactor:` | Рефакторинг без нового функционала     | `refactor: cleanup user service` |
| `style:`    | Изменения стилей (CSS, форматирование) | `style: fix button margin`       |
| `build:`    | Исправление ошибок сборки              | `build: fix webpack config`      |
| `perf:`     | Оптимизация производительности         | `perf: improve loading time`     |

---

## 🌱 Работа с ветками

- **Создать и перейти в ветку**

```bash
git checkout -b name_of_branch
```

- **Переключиться в существующую ветку (например, main)**

```bash
git checkout main
```

---

## 💾 Stash – временное сохранение изменений

- **Спрятать изменения:**

```bash
git stash
```

- **Вернуть изменения обратно:**

```bash
git stash pop
```

---

## 🚀 Как жить в этом мире?

1.  Создай ветку:

```bash
git checkout -b feature_branch
```

2.  Напиши код и зафиксируй изменения:

```bash
git add .
git commit -m 'feat: implement something'
```

3.  Подтяни актуальное состояние основной ветки:

```bash
git pull origin main  # или dev
 ```

4.  Разреши конфликты (если есть)
5.  Запушь ветку:

```bash
git push -u origin feature_branch
```

6.  Создай **Pull Request (PR)** в браузере
7.  Тимлид делает **merge / reject**

---

## 📏 Первое правило гитовского клуба

- Пушить **только в свою ветку** ✅ `feature/abc` → `origin/feature/abc` ❌ `feature/abc` → `origin/dev`
- **Между ветками — только через PR**

---

## 🍒 Cherry-pick — перенос отдельного коммита

```bash
# Перенести один коммит из одной ветки в другую
git cherry-pick <commit_hash>
```

### Если возник конфликт:

1.  Исправь конфликт
2.  Добавь изменения:

```bash
git add .
```

3.  Продолжи:

```bash
git cherry-pick --continue
```

---

## 🧨 Удалить последний коммит

> ⚠️ Будь **очень осторожен**! Особенно при использовании `--force`

### `reset` — полное или мягкое удаление коммита

- **Удалить коммит и все изменения:**

```bash
git reset --hard HEAD~1
```

- **Удалить коммит, но оставить изменения в рабочей директории:**

```bash
git reset --soft HEAD~1
```

- **Принудительно запушить:**

```bash
git push origin main --force
```

### `revert` — отмена коммита с созданием нового

```bash
git revert <commit_hash> --no-edit -n
git commit -m "revert: отмена ненужного коммита"
```

### После git add проверяйте статус, чтобы не закоммитить лишнего

```bash
git status
```

### Что показывает `git status`:

- **Untracked files** — новые файлы, не добавленные в Git
- **Changes not staged for commit** — изменённые файлы, но не добавленные
- **Changes to be committed** — изменения, уже подготовленные (`staged`) для коммита
- Информация о текущей ветке и расхождении с удалённой (если есть)

Пример вывода:

```
On branch feature/login
Your branch is ahead of 'origin/feature/login' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  modified:   src/components/LoginForm.jsx

Untracked files:
  (use "git add <file>..." to include in what will be committed)
  src/utils/validation.js
```
