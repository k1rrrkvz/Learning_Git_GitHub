# Практика 7: Работа с удалёнными репозиториями

## Цель
Научиться подключать удалённые репозитории, настраивать remote и понимать разницу между локальными и удалёнными ветками.

## Уровень сложности
⭐⭐⭐ Средний

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте локальный проект, настройте связь с удалённым репозиторием (симуляция) и изучите команды работы с remote.

### Шаги выполнения

#### Шаг 1: Создайте основной проект
```bash
cd ~/Documents
mkdir my-app
cd my-app
git init
```

#### Шаг 2: Создайте файлы проекта
```bash
echo "# My Application" > README.md
echo "print('Hello World')" > app.py
git add .
git commit -m "Initial commit"
```

#### Шаг 3: Создайте "удалённый" репозиторий (симуляция GitHub)
```bash
cd ~/Documents
git init --bare remote-repo.git
```

**`--bare` создаёт репозиторий без рабочей директории (как на GitHub)**

#### Шаг 4: Вернитесь в проект
```bash
cd my-app
```

#### Шаг 5: Проверьте список удалённых репозиториев
```bash
git remote -v
```

**Пусто! Удалённых репозиториев нет.**

#### Шаг 6: Добавьте удалённый репозиторий
```bash
git remote add origin ~/Documents/remote-repo.git
```

**`origin` — стандартное имя для главного удалённого репозитория**

#### Шаг 7: Проверьте снова
```bash
git remote -v
```

**Вы увидите:**
```
origin  /Users/yourname/Documents/remote-repo.git (fetch)
origin  /Users/yourname/Documents/remote-repo.git (push)
```

#### Шаг 8: Посмотрите детальную информацию о remote
```bash
git remote show origin
```

#### Шаг 9: Отправьте код на удалённый репозиторий
```bash
git push -u origin master
```

**`-u` устанавливает связь между локальной и удалённой веткой**

#### Шаг 10: Создайте новый коммит
```bash
echo "def greet():" >> app.py
echo "    return 'Hello!'" >> app.py
git add app.py
git commit -m "Add greet function"
```

#### Шаг 11: Отправьте изменения (теперь проще)
```bash
git push
```

**Флаг -u больше не нужен!**

#### Шаг 12: Посмотрите информацию о ветках
```bash
git branch -a
```

**Вы увидите:**
```
* master
  remotes/origin/master
```

**`remotes/origin/master` — удалённая ветка**

#### Шаг 13: Создайте новую локальную ветку
```bash
git checkout -b feature-login
echo "# Login System" > login.py
git add login.py
git commit -m "Add login system"
```

#### Шаг 14: Отправьте новую ветку на remote
```bash
git push -u origin feature-login
```

#### Шаг 15: Посмотрите все ветки снова
```bash
git branch -a
```

**Теперь:**
```
* feature-login
  master
  remotes/origin/feature-login
  remotes/origin/master
```

#### Шаг 16: Создайте второй "клон" репозитория (симуляция работы с другого компьютера)
```bash
cd ~/Documents
git clone remote-repo.git my-app-clone
```

#### Шаг 17: Перейдите в клон
```bash
cd my-app-clone
```

#### Шаг 18: Посмотрите список файлов
```bash
ls
git log --oneline
```

**Всё на месте!**

#### Шаг 19: Посмотрите ветки в клоне
```bash
git branch -a
```

**Вы увидите:**
```
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-login
  remotes/origin/master
```

#### Шаг 20: Создайте изменение в клоне
```bash
echo "# Documentation" > DOCS.md
git add DOCS.md
git commit -m "Add documentation"
git push
```

#### Шаг 21: Вернитесь в оригинальный репозиторий
```bash
cd ~/Documents/my-app
```

#### Шаг 22: Получите изменения
```bash
git checkout master
git pull
```

**Файл DOCS.md появился!**

#### Шаг 23: Посмотрите историю
```bash
git log --oneline
```

#### Шаг 24: Переименуйте remote (опционально)
```bash
git remote rename origin upstream
git remote -v
```

#### Шаг 25: Верните имя обратно
```bash
git remote rename upstream origin
```

#### Шаг 26: Удалите remote (для теста)
```bash
git remote remove origin
git remote -v
```

**Пусто!**

#### Шаг 27: Добавьте снова
```bash
git remote add origin ~/Documents/remote-repo.git
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "data-analysis", настройте удалённый репозиторий и попрактикуйтесь в синхронизации.

### Требования
1. Создайте папку `data-analysis` и инициализируйте Git
2. Создайте файл `analysis.py` с текстом "import pandas as pd"
3. Создайте коммит "Initial data analysis script"
4. Создайте bare репозиторий `data-remote.git` в ~/Documents
5. Добавьте remote с именем `origin` указывающий на `data-remote.git`
6. Проверьте список удалённых репозиториев командой `git remote -v`
7. Отправьте код командой `git push -u origin master`
8. Создайте новый файл `visualize.py` с текстом "import matplotlib"
9. Создайте коммит "Add visualization module"
10. Отправьте изменения командой `git push`
11. Создайте и переключитесь на ветку `add-tests`
12. Создайте файл `test.py` с текстом "import unittest"
13. Создайте коммит "Add test framework"
14. Отправьте ветку на remote: `git push -u origin add-tests`
15. Посмотрите все ветки (локальные и удалённые) командой `git branch -a`
16. Клонируйте репозиторий в папку `data-analysis-clone`
17. Перейдите в клонированный репозиторий
18. Создайте файл `config.ini` с текстом "[settings]"
19. Создайте коммит "Add configuration file"
20. Отправьте изменения
21. Вернитесь в оригинальный репозиторий
22. Получите изменения командой `git pull`

### Проверьте себя
- В оригинальном репозитории `git remote -v` должен показать origin
- `git branch -a` должен показать 2 локальные и 2 удалённые ветки
- После `git pull` файл config.ini должен появиться
- В клоне `git log --oneline` должен показать 3 коммита на master

---

## Подсказки
- `git remote add имя url` — добавить удалённый репозиторий
- `git remote -v` — список удалённых репозиториев
- `git push -u origin ветка` — отправить ветку первый раз
- `git push` — отправить после установки связи
- `git pull` — получить изменения
- `git clone url` — клонировать репозиторий
- `git branch -a` — все ветки (локальные и удалённые)
- `--bare` создаёт репозиторий без рабочей директории

---

## Бонус: Работа с реальным GitHub

### Подготовка
Если у вас есть аккаунт GitHub и настроен токен/SSH, можете попробовать работу с реальным удалённым репозиторием.

### Шаги для GitHub

1. **Создайте репозиторий на GitHub:**
   - Войдите на github.com
   - Нажмите "+" → "New repository"
   - Назовите: `git-practice-remote`
   - НЕ добавляйте README, .gitignore, license
   - Нажмите "Create repository"

2. **Подключите локальный репозиторий:**
```bash
cd ~/Documents/my-app
git remote remove origin  # удалите локальный remote если есть
git remote add origin https://github.com/ваш-username/git-practice-remote.git
```

3. **Отправьте код:**
```bash
git push -u origin master
```

4. **Обновите страницу GitHub — ваш код там!**

5. **Внесите изменения на GitHub:**
   - Откройте README.md на GitHub
   - Нажмите кнопку редактирования (карандаш)
   - Добавьте строку "Edited on GitHub"
   - Commit changes

6. **Получите изменения локально:**
```bash
git pull
cat README.md  # увидите изменения с GitHub
```

---

## Что вы изучили
✓ Создание bare репозитория (`git init --bare`)  
✓ Добавление удалённого репозитория (`git remote add`)  
✓ Отправка изменений (`git push`)  
✓ Получение изменений (`git pull`)  
✓ Клонирование репозитория (`git clone`)  
✓ Просмотр удалённых веток (`git branch -a`)  
✓ Связывание локальных и удалённых веток (`-u`)  
✓ (Бонус) Работа с реальным GitHub  

---

**Предыдущая практика:** practice_06_merge_conflicts.md  
**Следующая практика:** practice_08_stashing.md
