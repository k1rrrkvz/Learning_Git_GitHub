# Практика 1: Базовый рабочий процесс Git

## Цель
Научиться создавать репозиторий, делать коммиты и просматривать историю.

## Уровень сложности
⭐ Начальный

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "my-blog" с тремя HTML файлами и отследите изменения в Git.

### Шаги выполнения

#### Шаг 1: Создайте папку проекта и перейдите в неё
```bash
cd ~/Documents
mkdir my-blog
cd my-blog
```

#### Шаг 2: Инициализируйте Git репозиторий
```bash
git init
```

**Ожидаемый результат:**
```
Initialized empty Git repository in /Users/yourname/Documents/my-blog/.git/
```

#### Шаг 3: Создайте первый файл
```bash
echo "<!DOCTYPE html><html><head><title>My Blog</title></head><body><h1>Welcome to My Blog</h1></body></html>" > index.html
```

#### Шаг 4: Проверьте статус
```bash
git status
```

**Вы увидите:**
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html
```

#### Шаг 5: Добавьте файл в staging area
```bash
git add index.html
```

#### Шаг 6: Создайте первый коммит
```bash
git commit -m "Add index page"
```

#### Шаг 7: Создайте второй файл
```bash
echo "<!DOCTYPE html><html><head><title>About</title></head><body><h1>About Me</h1></body></html>" > about.html
```

#### Шаг 8: Создайте третий файл
```bash
echo "<!DOCTYPE html><html><head><title>Contact</title></head><body><h1>Contact Me</h1></body></html>" > contact.html
```

#### Шаг 9: Добавьте оба файла одновременно
```bash
git add about.html contact.html
```

#### Шаг 10: Создайте второй коммит
```bash
git commit -m "Add about and contact pages"
```

#### Шаг 11: Просмотрите историю
```bash
git log --oneline
```

**Вы увидите:**
```
b2c3d4e (HEAD -> master) Add about and contact pages
a1b2c3d Add index page
```

#### Шаг 12: Просмотрите подробную историю
```bash
git log
```

#### Шаг 13: Проверьте текущий статус
```bash
git status
```

**Вы увидите:**
```
On branch master
nothing to commit, working tree clean
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте новый проект "my-portfolio" с файлами для портфолио и отследите изменения.

### Требования
1. Создайте папку `my-portfolio` в директории Documents
2. Инициализируйте Git репозиторий
3. Создайте файл `home.html` с любым содержимым
4. Добавьте файл в staging area и создайте коммит с сообщением "Create home page"
5. Создайте два новых файла: `projects.html` и `skills.html`
6. Добавьте оба файла и создайте коммит с сообщением "Add projects and skills pages"
7. Просмотрите историю в кратком формате

### Проверьте себя
Выполните команду `git log --oneline`. Вы должны увидеть 2 коммита:
- Первый: "Create home page"
- Второй: "Add projects and skills pages"

---

## Подсказки
- Используйте `cd ~/Documents` для перехода в папку Documents
- Используйте `mkdir название` для создания папки
- Используйте `git init` для инициализации репозитория
- Используйте `echo "текст" > файл.html` для создания файла
- Используйте `git add .` чтобы добавить все файлы сразу
- Используйте `git status` для проверки состояния

---

## Что вы изучили
✓ Инициализация Git репозитория (`git init`)  
✓ Проверка статуса (`git status`)  
✓ Добавление файлов в staging area (`git add`)  
✓ Создание коммитов (`git commit -m`)  
✓ Просмотр истории (`git log`, `git log --oneline`)  

---

**Следующая практика:** practice_02_editing_files.md
