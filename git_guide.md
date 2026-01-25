# Полная инструкция по Git и GitHub для начинающих

## Содержание
1. [Что такое Git и GitHub?](#что-такое-git-и-github)
2. [Установка Git](#установка-git)
3. [Первоначальная настройка Git](#первоначальная-настройка-git)
4. [Регистрация на GitHub](#регистрация-на-github)
5. [Создание репозитория на GitHub](#создание-репозитория-на-github)
6. [Работа с терминалом](#работа-с-терминалом)
7. [Инициализация проекта](#инициализация-проекта)
8. [Настройка аутентификации](#настройка-аутентификации)
9. [Загрузка проекта на GitHub](#загрузка-проекта-на-github)
10. [Работа с изменениями](#работа-с-изменениями)
11. [Полезные команды](#полезные-команды)

---

## 1. Что такое Git и GitHub?

### Git
**Git** — это система контроля версий, которая позволяет:
- Отслеживать все изменения в коде
- Возвращаться к предыдущим версиям
- Работать над проектом параллельно с другими разработчиками
- Сохранять историю всех изменений

**Аналогия:** Представьте, что вы пишете книгу и сохраняете каждую версию с комментарием "что изменилось". Git делает это автоматически для вашего кода.

### GitHub
**GitHub** — это облачная платформа для хранения Git-репозиториев, которая предоставляет:
- Облачное хранение вашего кода
- Инструменты для совместной работы
- Pull requests (запросы на внесение изменений)
- Code review (проверка кода)
- Issue tracking (отслеживание задач и багов)
- Wiki и документацию
- GitHub Actions (автоматизация)

**Статистика:** Более 100+ миллионов разработчиков используют GitHub.

---

## 2. Установка Git

### Для Windows:

#### Шаг 1: Скачивание установщика
1. Перейдите на официальный сайт: [git-scm.com](https://git-scm.com/)
2. Нажмите на кнопку **"Download for Windows"**
3. Скачается файл `Git-2.xx.x-64-bit.exe`

#### Шаг 2: Установка Git
1. Запустите скачанный файл
2. Нажмите **"Next"** на экране приветствия
3. **Выбор компонентов:** оставьте настройки по умолчанию, нажмите **"Next"**
4. **Выбор редактора:** выберите редактор (рекомендуется оставить по умолчанию), нажмите **"Next"**
5. **Название ветки по умолчанию:** выберите "Override the default branch name" и введите `main`, нажмите **"Next"**
6. **PATH environment:** выберите "Git from the command line and also from 3rd-party software", нажмите **"Next"**
7. Для остальных настроек оставляйте значения по умолчанию и нажимайте **"Next"**
8. В конце нажмите **"Install"**
9. После установки нажмите **"Finish"**

#### Шаг 3: Проверка установки
1. Откройте **PowerShell** или **Command Prompt**
   - Нажмите `Win + R`
   - Введите `powershell` или `cmd`
   - Нажмите Enter
2. Введите команду:
```bash
git --version
```
3. Вы должны увидеть что-то вроде:
```
git version 2.43.0.windows.1
```

Если версия отображается — **Git успешно установлен!** ✓

### Для macOS:

#### Способ 1: Через Homebrew (рекомендуется)
1. Установите Homebrew (если еще не установлен):
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
2. Установите Git:
```bash
brew install git
```

#### Способ 2: Через официальный установщик
1. Перейдите на [git-scm.com](https://git-scm.com/)
2. Скачайте установщик для macOS
3. Запустите файл `.dmg` и следуйте инструкциям

#### Проверка установки:
```bash
git --version
```

### Для Linux:

#### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install git
```

#### Fedora:
```bash
sudo dnf install git
```

#### Arch Linux:
```bash
sudo pacman -S git
```

#### Проверка установки:
```bash
git --version
```

---

## 3. Первоначальная настройка Git

После установки Git необходимо настроить ваше имя и email. Эта информация будет добавляться к каждому вашему коммиту.

### Настройка имени и email

Откройте терминал и выполните следующие команды:

```bash
git config --global user.name "Ваше Имя"
```

```bash
git config --global user.email "your.email@example.com"
```

**Важно:** 
- Используйте тот же email, который будете использовать на GitHub
- Замените "Ваше Имя" на ваше реальное имя (можно на русском)
- Замените "your.email@example.com" на ваш реальный email

**Пример:**
```bash
git config --global user.name "Иван Иванов"
git config --global user.email "ivan.ivanov@gmail.com"
```

### Проверка настроек

Чтобы проверить, что настройки применились:

```bash
git config --global --list
```

Вы увидите:
```
user.name=Иван Иванов
user.email=ivan.ivanov@gmail.com
```

### Дополнительные полезные настройки

#### Установка редактора по умолчанию (опционально)

Для Visual Studio Code:
```bash
git config --global core.editor "code --wait"
```

Для Notepad++ (Windows):
```bash
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"
```

#### Цветной вывод в терминале
```bash
git config --global color.ui auto
```

#### Настройка окончаний строк

Для Windows:
```bash
git config --global core.autocrlf true
```

Для macOS/Linux:
```bash
git config --global core.autocrlf input
```

---

## 4. Регистрация на GitHub

Если у вас еще нет аккаунта на GitHub:

### Шаг 1: Создание аккаунта
1. Перейдите на [github.com](https://github.com/)
2. Нажмите **"Sign up"** в правом верхнем углу
3. Введите ваш **email**
4. Придумайте **пароль** (минимум 8 символов)
5. Придумайте **username** (имя пользователя)
   - Может содержать только буквы, цифры и дефисы
   - Должно быть уникальным
   - Пример: `ivan-ivanov`, `john-smith-dev`
6. Решите, хотите ли получать email-уведомления (можно выбрать `n`)
7. Пройдите верификацию (решите головоломку)
8. Нажмите **"Create account"**

### Шаг 2: Подтверждение email
1. Проверьте вашу почту
2. Найдите письмо от GitHub
3. Нажмите на ссылку подтверждения или введите код

### Шаг 3: Настройка профиля (опционально)
1. Войдите в свой аккаунт
2. Нажмите на иконку профиля в правом верхнем углу
3. Выберите **"Settings"**
4. В разделе "Profile" можно добавить:
   - Фото профиля
   - Описание (Bio)
   - Локацию
   - Ссылки на социальные сети

**Поздравляем! Теперь у вас есть аккаунт на GitHub!** ✓

---

## 5. Создание репозитория на GitHub

### Шаг 1: Переход к созданию репозитория
1. Убедитесь, что вы вошли в свой аккаунт на [github.com](https://github.com/)
2. В правом верхнем углу страницы найдите иконку **"+"**
3. Нажмите на нее
4. В выпадающем меню выберите **"New repository"**

### Шаг 2: Заполнение данных репозитория

#### Repository name (Имя репозитория) — обязательно
- Введите название вашего проекта
- Используйте буквы, цифры, дефисы или подчеркивания
- **Примеры:** `my-first-project`, `todo-app`, `portfolio-website`

#### Description (Описание) — опционально
- Краткое описание проекта (1-2 предложения)
- **Примеры:** 
  - "Мой первый проект на GitHub"
  - "Todo-приложение на React"
  - "Портфолио веб-разработчика"

#### Public или Private — выберите видимость

**Public** (Публичный):
- ✓ Код видят все пользователи интернета
- ✓ Подходит для open-source проектов
- ✓ Другие могут клонировать ваш проект
- ✓ Бесплатно

**Private** (Приватный):
- ✓ Код видите только вы и те, кому дадите доступ
- ✓ Подходит для личных или коммерческих проектов
- ✓ Бесплатно на GitHub

**Рекомендация:** Для учебных проектов можно выбрать Public, для личных — Private.

#### Дополнительные опции — НЕ ОТМЕЧАЙТЕ!

**ВАЖНО:** Если вы будете загружать существующий проект с компьютера, НЕ ставьте галочки на:
- ☐ Add a README file
- ☐ Add .gitignore
- ☐ Choose a license

**Почему?** Мы создадим эти файлы локально и загрузим их вместе с проектом.

❗ **Примечание:** Если создаете репозиторий с нуля (без локального проекта), можете отметить "Add a README file". ❗

### Шаг 3: Создание репозитория
1. Проверьте все введенные данные
2. Нажмите зеленую кнопку **"Create repository"**

### Шаг 4: Сохранение URL репозитория

После создания откроется страница с инструкциями. Вы увидите URL вашего репозитория:

```
https://github.com/your-username/your-repository-name.git
```

**ВАЖНО:** Скопируйте этот URL — он понадобится для загрузки проекта!

**Пример:**
```
https://github.com/ivan-ivanov/my-first-project.git
```

---

## 6. Работа с терминалом

### Что такое терминал?

**Терминал** (или консоль, командная строка) — это текстовый интерфейс для управления компьютером. Вместо кликов мышкой вы вводите команды.

### Открытие терминала

#### Windows:
**Способ 1: PowerShell** (рекомендуется)
- Нажмите `Win + R`
- Введите `powershell`
- Нажмите Enter

**Способ 2: Через меню Пуск**
- Откройте меню Пуск
- Введите "PowerShell"
- Нажмите Enter

**Способ 3: Command Prompt**
- Нажмите `Win + R`
- Введите `cmd`
- Нажмите Enter

**Способ 4: Windows Terminal** (если установлен)
- Нажмите `Win + R`
- Введите `wt`
- Нажмите Enter

#### macOS:
- Нажмите `Cmd + Space`
- Введите "Terminal"
- Нажмите Enter

#### Linux:
- Нажмите `Ctrl + Alt + T`

### Основные команды терминала

#### Узнать текущую директорию (где вы находитесь)

**Windows (PowerShell):**
```powershell
pwd
```

**macOS/Linux:**
```bash
pwd
```

**Результат:**
```
C:\Users\YourName\Documents
```

#### Просмотр содержимого папки

**Windows (PowerShell):**
```powershell
ls
```
или **(CMD)**
```powershell
dir
```

**macOS/Linux:**
```bash
ls
```

**Результат:**
```
Desktop
Documents
Downloads
my-project
```

#### Перемещение между папками

**Синтаксис:**
```bash
cd путь/к/папке
```

**Примеры:**

Перейти в папку Documents:
```bash
cd Documents
```

Перейти в папку my-project внутри Documents:
```bash
cd Documents/my-project
```

**Windows** — можно использовать и прямые, и обратные слеши:
```powershell
cd Documents\my-project
```
или
```powershell
cd Documents/my-project
```

Вернуться на уровень выше:
```bash
cd ..
```

Перейти в домашнюю директорию:

**Windows:**
```powershell
cd ~
```

**macOS/Linux:**
```bash
cd ~
```

Перейти к определенному диску (только Windows):
```powershell
cd D:\Projects
```

#### Создание новой папки

```bash
mkdir название-папки
```

**Пример:**
```bash
mkdir my-new-project
```

#### Очистка экрана терминала

**Windows (PowerShell):**
```powershell
clear
```
или
```powershell
cls
```

**macOS/Linux:**
```bash
clear
```

### Полезные советы по работе с терминалом

#### Автодополнение путей
- Начните вводить название папки/файла
- Нажмите `Tab`
- Терминал автоматически дополнит название

#### Работа с пробелами в названиях

Если в пути есть пробелы, заключайте путь в кавычки:

```bash
cd "My Projects/Project Name"
```

или используйте обратный слеш (на macOS/Linux):
```bash
cd My\ Projects/Project\ Name
```

#### История команд
- Нажмите `↑` (стрелка вверх), чтобы увидеть предыдущие команды
- Нажмите `↓` (стрелка вниз), чтобы перемещаться вперед по истории

#### Копирование и вставка в терминал

**Windows (PowerShell):**
- Копировать: выделите текст мышкой, нажмите `Ctrl + C` или правая кнопка мыши
- Вставить: `Ctrl + V` или ❗правая кнопка мыши❗

**macOS:**
- Копировать: `Cmd + C`
- Вставить: `Cmd + V`

**Linux:**
- Копировать: `Ctrl + Shift + C`
- Вставить: `Ctrl + Shift + V`

---

## 7. Инициализация проекта

### Шаг 1: Переход в папку проекта

У вас уже есть папка с проектом на компьютере, или вы хотите создать новую?

#### Если папка уже существует:

1. Откройте терминал
2. Перейдите в папку проекта:

**Пример для Windows:**
```powershell
cd C:\Users\YourName\Documents\my-project
```

**Пример для macOS/Linux:**
```bash
cd ~/Documents/my-project
```

**Универсальная команда:**
```bash
cd ~/Documents/my-project
```

#### Если нужно создать новую папку:

1. Перейдите в место, где хотите создать проект:
```bash
cd ~/Documents
```

2. Создайте папку:
```bash
mkdir my-project
```

3. Перейдите в созданную папку:
```bash
cd my-project
```

### Шаг 2: Проверка содержимого папки

Убедитесь, что вы находитесь в правильной папке:

```bash
ls
```

**Результат покажет файлы проекта:**
```
index.html
style.css
script.js
README.md
```

Если папка пустая — это нормально, можете создать первый файл:

```bash
echo "# My Project" > README.md
```

### Шаг 3: Проверка текущего пути

Убедитесь, что находитесь в нужной директории:

```bash
pwd
```

**Результат (пример для Windows):**
```
C:\Users\YourName\Documents\my-project
```

**Результат (пример для macOS/Linux):**
```
/Users/yourname/Documents/my-project
```

### Шаг 4: Инициализация Git-репозитория

Теперь превратим обычную папку в Git-репозиторий:

```bash
git init
```

**Результат:**
```
Initialized empty Git repository in C:/Users/YourName/Documents/my-project/.git/
```

**Что произошло?**
- Git создал скрытую папку `.git` в вашем проекте
- В этой папке будет храниться вся история изменений
- Теперь Git отслеживает изменения в этой папке

### Шаг 5: Проверка состояния репозитория

Проверьте текущее состояние:

```bash
git status
```

**Результат:**
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        index.html
        style.css
        script.js

nothing added to commit but untracked files present (use "git add" to track)
```

**Объяснение:**
- `On branch main` — вы находитесь на ветке main
- `Untracked files` — файлы, которые Git пока не отслеживает

### Шаг 6: Добавление файлов в staging area

**Staging area** — это промежуточная область, куда мы помещаем файлы перед сохранением (коммитом).

Добавьте все файлы:

```bash
git add .
```

**Что означает точка `.` ?**
- Точка означает "все файлы и папки в текущей директории"
- Git добавит все файлы в staging area

**Альтернативы:**

Добавить конкретный файл:
```bash
git add README.md
```

Добавить несколько файлов:
```bash
git add index.html style.css
```

Добавить все файлы определенного типа:
```bash
git add *.js
```

### Шаг 7: Проверка статуса после добавления

```bash
git status
```

**Результат:**
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   README.md
        new file:   index.html
        new file:   script.js
        new file:   style.css
```

**Отлично!** Файлы готовы к коммиту (зеленым цветом).

### Шаг 8: Создание первого коммита

**Коммит** — это сохраненная версия вашего проекта с описанием изменений.

```bash
git commit -m "Initial commit"
```

**Объяснение команды:**
- `git commit` — создать коммит
- `-m` — флаг для добавления сообщения
- `"Initial commit"` — сообщение коммита

**Результат:**
```
[main (root-commit) a1b2c3d] Initial commit
 4 files changed, 150 insertions(+)
 create mode 100644 README.md
 create mode 100644 index.html
 create mode 100644 script.js
 create mode 100644 style.css
```

**Что такое хорошее сообщение коммита?**

✓ **Хорошие примеры:**
- `"Initial commit"`
- `"Add login form"`
- `"Fix navigation bug"`
- `"Update README with installation instructions"`

✗ **Плохие примеры:**
- `"asdfgh"`
- `"Changes"`
- `"Fix"`
- `"Update"`

### Шаг 9: Установка главной ветки

Убедимся, что основная ветка называется `main`:

```bash
git branch -M main
```

**Объяснение:**
- `git branch` — работа с ветками
- `-M` — переименовать текущую ветку
- `main` — новое название

**Примечание:** Раньше по умолчанию использовалось имя `master`, сейчас стандарт — `main`.

### Шаг 10: Проверка истории коммитов

Посмотрите историю:

```bash
git log
```

**Результат:**
```
commit a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6 (HEAD -> main)
Author: Иван Иванов <ivan.ivanov@gmail.com>
Date:   Sun Jan 26 14:30:00 2026 +0300

    Initial commit
```

Для краткого вывода:
```bash
git log --oneline
```

**Результат:**
```
a1b2c3d (HEAD -> main) Initial commit
```

---

## 8. Настройка аутентификации

Чтобы загружать код на GitHub, нужно настроить авторизацию. GitHub предлагает два основных способа: **Personal Access Token** и **SSH ключ**.

---

### Способ 1: Personal Access Token (PAT) — Рекомендуется для начинающих

Personal Access Token — это специальный пароль для доступа к GitHub через командную строку.

#### Шаг 1: Создание токена

1. Войдите в свой аккаунт на [github.com](https://github.com/)
2. Нажмите на иконку профиля в правом верхнем углу
3. Выберите **"Settings"** (Настройки)
4. Прокрутите вниз в левом меню
5. Нажмите **"Developer settings"** (Настройки разработчика)
6. Нажмите **"Personal access tokens"**
7. Выберите **"Tokens (classic)"**
8. Нажмите **"Generate new token"**
9. Выберите **"Generate new token (classic)"**

#### Шаг 2: Настройка токена

**Note (Название токена):**
- Введите понятное название, например: `"My Laptop"`, `"Git Access Token"`, `"Desktop PC"`
- Это поможет понять, для чего используется токен

**Expiration (Срок действия):**
- Выберите, как долго токен будет действовать
- **Рекомендация:** `90 days` (90 дней) для начала
- Можно выбрать `No expiration` (без срока действия), но это менее безопасно

**Select scopes (Выбор разрешений):**
- ☑ Отметьте галочкой **`repo`** (весь раздел)
  - Это даст полный доступ к вашим репозиториям
  - Включает возможность читать и записывать код

**Дополнительно (опционально):**
- `workflow` — если планируете использовать GitHub Actions
- `delete_repo` — если нужна возможность удалять репозитории

#### Шаг 3: Генерация и сохранение токена

1. Прокрутите вниз
2. Нажмите зеленую кнопку **"Generate token"**
3. **ОЧЕНЬ ВАЖНО:** Токен отобразится только один раз!
4. Скопируйте токен (выглядит примерно так: `ghp_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`)
5. **Сохраните токен в надежном месте:**
   - В текстовом файле на компьютере
   - В менеджере паролей (например, LastPass, 1Password)
   - В заметках (но не в публичных!)

**ВНИМАНИЕ:** Если потеряете токен, придется создавать новый!

#### Шаг 4: Использование токена

Токен будет использован вместо пароля при первой загрузке на GitHub (см. раздел 9).

#### Шаг 5: Сохранение токена в системе (опционально)

Чтобы не вводить токен каждый раз, можно настроить его сохранение.

**Для Windows:**

Используйте Git Credential Manager (устанавливается вместе с Git):
```powershell
git config --global credential.helper manager-core
```

**Для macOS:**

Используйте Keychain:
```bash
git config --global credential.helper osxkeychain
```

**Для Linux:**

Используйте cache (токен сохранится на 15 минут):
```bash
git config --global credential.helper cache
```

Или сохранить навсегда (менее безопасно):
```bash
git config --global credential.helper store
```

---

### Способ 2: SSH ключ — Для продвинутых пользователей

SSH — более безопасный и удобный способ авторизации, но требует больше настроек.

#### Шаг 1: Проверка существующих SSH ключей

```bash
ls -al ~/.ssh
```

Если видите файлы `id_rsa.pub`, `id_ed25519.pub` или подобные — у вас уже есть ключи.

#### Шаг 2: Генерация нового SSH ключа

Если ключей нет, создайте новый:

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

**Замените** `your.email@example.com` на ваш email с GitHub.

**Процесс:**

1. `Enter file in which to save the key:` — нажмите Enter (сохранится в стандартное место)
2. `Enter passphrase:` — придумайте пароль для дополнительной защиты (можно оставить пустым, просто нажав Enter)
3. `Enter same passphrase again:` — повторите пароль

**Результат:**
```
Your identification has been saved in /Users/yourname/.ssh/id_ed25519
Your public key has been saved in /Users/yourname/.ssh/id_ed25519.pub
```

#### Шаг 3: Запуск SSH-агента

**macOS/Linux:**
```bash
eval "$(ssh-agent -s)"
```

**Windows (PowerShell):**
```powershell
Start-Service ssh-agent
```

#### Шаг 4: Добавление ключа в SSH-агент

**macOS:**
```bash
ssh-add ~/.ssh/id_ed25519
```

**Linux/Windows:**
```bash
ssh-add ~/.ssh/id_ed25519
```

#### Шаг 5: Копирование публичного ключа

**macOS:**
```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

**Linux:**
```bash
cat ~/.ssh/id_ed25519.pub
```
Затем выделите и скопируйте вывод.

**Windows (PowerShell):**
```powershell
Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
```

Или:
```powershell
cat ~/.ssh/id_ed25519.pub
```
Затем скопируйте вывод.

#### Шаг 6: Добавление SSH ключа на GitHub

1. Войдите на [github.com](https://github.com/)
2. Нажмите на иконку профиля → **"Settings"**
3. В левом меню выберите **"SSH and GPG keys"**
4. Нажмите **"New SSH key"** или **"Add SSH key"**
5. **Title:** введите название (например, "My Laptop", "Work PC")
6. **Key type:** выберите "Authentication Key"
7. **Key:** вставьте скопированный публичный ключ
8. Нажмите **"Add SSH key"**
9. Подтвердите действие паролем GitHub (если требуется)

#### Шаг 7: Проверка подключения

```bash
ssh -T git@github.com
```

**При первом подключении:**
```
The authenticity of host 'github.com' can't be established.
...
Are you sure you want to continue connecting (yes/no)?
```

Введите `yes` и нажмите Enter.

**Успешный результат:**
```
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

**Отлично! SSH настроен!** ✓

---

## 9. Загрузка проекта на GitHub

### Шаг 1: Подключение локального репозитория к GitHub

Нужно "связать" ваш локальный проект с репозиторием на GitHub.

**Команда:**
```bash
git remote add origin https://github.com/your-username/your-repository-name.git
```

**Объяснение:**
- `git remote add` — добавить удаленный репозиторий
- `origin` — стандартное имя для главного удаленного репозитория
- URL — адрес вашего репозитория на GitHub

**ВАЖНО:** Замените URL на ваш собственный!

**Пример:**
```bash
git remote add origin https://github.com/ivan-ivanov/my-first-project.git
```

**Где взять URL?**
1. Откройте ваш репозиторий на GitHub
2. Нажмите зеленую кнопку **"Code"**
3. Во вкладке **"HTTPS"** скопируйте URL

**Если используете SSH:**
```bash
git remote add origin git@github.com:your-username/your-repository-name.git
```

### Шаг 2: Проверка удаленного репозитория

Убедитесь, что remote добавлен:

```bash
git remote -v
```

**Результат:**
```
origin  https://github.com/your-username/your-repository-name.git (fetch)
origin  https://github.com/your-username/your-repository-name.git (push)
```

**Если допустили ошибку в URL:**

Удалите remote:
```bash
git remote remove origin
```

Добавьте заново с правильным URL:
```bash
git remote add origin https://github.com/your-username/correct-repository-name.git
```

### Шаг 3: Первая загрузка (Push) на GitHub

Теперь загрузим код на GitHub:

```bash
git push -u origin main
```

**Объяснение команды:**
- `git push` — отправить коммиты на удаленный репозиторий
- `-u` — установить связь между локальной и удаленной веткой (используется только в первый раз)
- `origin` — имя удаленного репозитория
- `main` — название ветки

### Шаг 4: Авторизация при первом push

#### Если используете Personal Access Token (PAT):

При первом push GitHub запросит авторизацию.

**Windows (Git Credential Manager):**

Откроется окно авторизации:
1. Выберите **"Token"** или **"Personal Access Token"**
2. Вставьте ваш токен (тот, что скопировали ранее)
3. Нажмите **"Sign in"** или **"OK"**

**Или через командную строку:**

```
Username for 'https://github.com': your-username
Password for 'https://your-username@github.com': 
```

- **Username:** введите ваш логин на GitHub
- **Password:** вставьте ваш Personal Access Token (НЕ обычный пароль!)

**macOS:**

Появится окно Keychain для сохранения пароля:
1. Введите username
2. В поле password вставьте токен
3. Нажмите "Always Allow" для сохранения

**Linux:**

В терминале:
1. Введите username
2. Вставьте токен вместо пароля

**ВАЖНО:** 
- Используйте токен, а не обычный пароль!
- Токен начинается с `ghp_`
- При вставке токена курсор может не двигаться — это нормально, просто вставьте и нажмите Enter

#### Если используете SSH:

Авторизация произойдет автоматически через SSH ключ.

Если установили passphrase для ключа, введите его.

### Шаг 5: Ожидание загрузки

Вы увидите процесс загрузки:

```
Enumerating objects: 8, done.
Counting objects: 100% (8/8), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (8/8), 2.43 KiB | 2.43 MiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/your-username/your-repository-name.git
 * [new branch]      main -> main
Branch 'main' set up to track remote branch 'main' from 'origin'.
```

**Поздравляем! Код загружен на GitHub!** ✓

### Шаг 6: Проверка на GitHub

1. Обновите страницу репозитория на GitHub
2. Вы должны увидеть все ваши файлы
3. Коммиты отобразятся в истории

---

## 10. Работа с изменениями

### Ежедневный рабочий процесс

После первоначальной загрузки вы будете регулярно вносить изменения и загружать их на GitHub.

### Шаг 1: Внесение изменений

Редактируйте файлы в вашем проекте как обычно в любом редакторе.

### Шаг 2: Проверка изменений

Посмотрите, какие файлы изменились:

```bash
git status
```

**Результат:**
```
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html
        modified:   style.css

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        about.html
```

**Объяснение:**
- `modified:` — файлы были изменены
- `Untracked files:` — новые файлы, которые Git еще не отслеживает

### Шаг 3: Просмотр конкретных изменений

Посмотрите, что именно изменилось:

```bash
git diff
```

**Результат покажет:**
- Красным (с `-`) — удаленные строки
- Зеленым (с `+`) — добавленные строки

Для просмотра изменений в конкретном файле:
```bash
git diff index.html
```

### Шаг 4: Добавление изменений

Добавьте все изменения:
```bash
git add .
```

Или добавьте конкретные файлы:
```bash
git add index.html style.css
```

### Шаг 5: Создание коммита

```bash
git commit -m "Add about page and update styles"
```

**Примеры хороших сообщений:**
- `"Add contact form"`
- `"Fix header alignment"`
- `"Update README with new features"`
- `"Refactor authentication logic"`

### Шаг 6: Загрузка на GitHub

```bash
git push
```

**Примечание:** Флаг `-u` больше не нужен — связь уже установлена при первом push.

**Результат:**
```
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.21 KiB | 1.21 MiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To https://github.com/your-username/your-repository-name.git
   a1b2c3d..e4f5g6h  main -> main
```

### Типичный рабочий процесс

```bash
# 1. Проверьте текущее состояние
git status

# 2. Добавьте изменения
git add .

# 3. Создайте коммит
git commit -m "Описание изменений"

# 4. Загрузите на GitHub
git push
```

**Повторяйте эти 4 шага каждый раз, когда хотите сохранить изменения!**

### Получение изменений с GitHub

Если вы работаете с нескольких компьютеров или с командой:

```bash
git pull
```

Эта команда загружает изменения с GitHub и объединяет их с вашим локальным кодом.

### Отмена изменений

#### Отменить изменения в файле (до git add):
```bash
git restore index.html
```

#### Убрать файл из staging (после git add, но до commit):
```bash
git restore --staged index.html
```

#### Изменить последний коммит:
```bash
git commit --amend -m "Новое сообщение"
```

**ВНИМАНИЕ:** Не используйте `--amend` для коммитов, которые уже загружены на GitHub!

---

## 11. Полезные команды

### Основные команды Git

#### Инициализация и настройка

```bash
# Создать новый репозиторий
git init

# Клонировать существующий репозиторий
git clone https://github.com/username/repository.git

# Настроить имя пользователя
git config --global user.name "Ваше Имя"

# Настроить email
git config --global user.email "your.email@example.com"

# Посмотреть все настройки
git config --list
```

#### Базовые операции

```bash
# Проверить статус
git status

# Добавить файлы
git add filename.txt        # один файл
git add file1.txt file2.txt # несколько файлов
git add *.js                # все файлы с расширением .js
git add .                   # все файлы

# Создать коммит
git commit -m "Сообщение"

# Добавить и закоммитить одновременно (только для измененных файлов)
git commit -am "Сообщение"

# Загрузить изменения на GitHub
git push

# Получить изменения с GitHub
git pull
```

#### Просмотр истории

```bash
# Полная история коммитов
git log

# Краткая история
git log --oneline

# История с графиком веток
git log --graph --oneline --all

# История конкретного файла
git log filename.txt

# Показать изменения в коммите
git show commit-hash

# Показать последний коммит
git show HEAD
```

#### Просмотр изменений

```bash
# Показать изменения (до git add)
git diff

# Показать изменения в конкретном файле
git diff filename.txt

# Показать изменения в staging area (после git add)
git diff --staged

# Сравнить с конкретным коммитом
git diff commit-hash
```

#### Работа с ветками

```bash
# Показать все ветки
git branch

# Создать новую ветку
git branch feature-name

# Переключиться на другую ветку
git checkout feature-name

# Создать и переключиться на новую ветку
git checkout -b feature-name

# Переименовать ветку
git branch -m old-name new-name

# Удалить ветку
git branch -d feature-name

# Слить ветку в текущую
git merge feature-name
```

#### Работа с удаленными репозиториями

```bash
# Показать удаленные репозитории
git remote -v

# Добавить удаленный репозиторий
git remote add origin https://github.com/username/repo.git

# Изменить URL удаленного репозитория
git remote set-url origin new-url

# Удалить удаленный репозиторий
git remote remove origin

# Показать информацию об удаленном репозитории
git remote show origin
```

#### Отмена изменений

```bash
# Отменить изменения в файле (до git add)
git restore filename.txt

# Отменить все изменения
git restore .

# Убрать файл из staging (после git add)
git restore --staged filename.txt

# Изменить последний коммит
git commit --amend -m "Новое сообщение"

# Отменить последний коммит (оставить изменения)
git reset --soft HEAD~1

# Отменить последний коммит (удалить изменения)
git reset --hard HEAD~1
```

**ОСТОРОЖНО:** Команды `reset --hard` и `clean -f` безвозвратно удаляют данные!

#### Прочее

```bash
# Показать, кто изменял каждую строку файла
git blame filename.txt

# Поиск в истории
git log --all --grep="search term"

# Показать изменения между ветками
git diff branch1..branch2

# Создать тег (версию)
git tag v1.0.0

# Загрузить теги на GitHub
git push --tags
```

### Полезные алиасы (сокращения)

Добавьте эти алиасы для ускорения работы:

```bash
# Короткий статус
git config --global alias.st status

# Короткий лог
git config --global alias.lg "log --oneline --graph --all"

# Короткий коммит
git config --global alias.cm "commit -m"

# Последний коммит
git config --global alias.last "log -1 HEAD"
```

Теперь можно использовать:
```bash
git st          # вместо git status
git lg          # вместо git log --oneline --graph --all
git cm "message" # вместо git commit -m "message"
git last        # показать последний коммит
```

### Файл .gitignore

`.gitignore` — файл, в котором указываются файлы и папки, которые Git должен игнорировать.

#### Создание .gitignore

В корне проекта создайте файл `.gitignore`:

**Windows (PowerShell):**
```powershell
New-Item .gitignore
```

**macOS/Linux:**
```bash
touch .gitignore
```

#### Примеры содержимого .gitignore

```gitignore
# Зависимости
node_modules/
vendor/

# Файлы окружения
.env
.env.local

# Логи
*.log
logs/

# Кэш
.cache/
*.tmp

# Системные файлы
.DS_Store
Thumbs.db
desktop.ini

# IDE
.vscode/
.idea/
*.swp

# Скомпилированные файлы
*.class
*.pyc
__pycache__/
dist/
build/

# Конфиденциальные данные
config/secrets.yml
credentials.json
```

#### Шаблоны .gitignore

GitHub предоставляет готовые шаблоны: [github.com/github/gitignore](https://github.com/github/gitignore)

Найдите шаблон для вашего языка/фреймворка и скопируйте его.

### Работа с GitHub через веб-интерфейс

#### Редактирование файлов онлайн

1. Откройте файл на GitHub
2. Нажмите иконку карандаша (Edit)
3. Внесите изменения
4. Внизу страницы напишите сообщение коммита
5. Нажмите "Commit changes"

**Важно:** После этого не забудьте выполнить `git pull` локально!

#### Загрузка файлов через интерфейс

1. Откройте репозиторий на GitHub
2. Нажмите "Add file" → "Upload files"
3. Перетащите файлы или выберите их
4. Напишите сообщение коммита
5. Нажмите "Commit changes"

#### Создание Issues (задач)

1. Перейдите на вкладку "Issues"
2. Нажмите "New issue"
3. Введите название и описание
4. Можете добавить метки (labels)
5. Нажмите "Submit new issue"

---

## Решение типичных проблем

### Ошибка: "fatal: not a git repository"

**Причина:** Вы не находитесь в Git-репозитории.

**Решение:**
1. Перейдите в папку проекта: `cd path/to/project`
2. Инициализируйте Git: `git init`

### Ошибка: "remote origin already exists"

**Причина:** Remote с именем "origin" уже добавлен.

**Решение:**
```bash
# Удалите существующий remote
git remote remove origin

# Добавьте правильный
git remote add origin your-correct-url
```

### Ошибка: "failed to push some refs"

**Причина:** На GitHub есть изменения, которых нет у вас локально.

**Решение:**
```bash
# Получите изменения с GitHub
git pull origin main

# Затем загрузите ваши изменения
git push
```

### Ошибка: "Permission denied (publickey)"

**Причина:** SSH ключ не настроен или не добавлен на GitHub.

**Решение:**
1. Проверьте SSH подключение: `ssh -T git@github.com`
2. Если ошибка — перечитайте раздел про настройку SSH
3. Или используйте HTTPS вместо SSH

### Ошибка: "Authentication failed"

**Причина:** Неправильный логин, пароль или токен.

**Решение:**
1. Убедитесь, что используете токен, а не обычный пароль
2. Проверьте, что токен активен (не истек срок)
3. Создайте новый токен при необходимости

### Забыли добавить файл в последний коммит

```bash
# Добавьте забытый файл
git add forgotten-file.txt

# Измените последний коммит
git commit --amend --no-edit
```

### Случайно закоммитили секретные данные

**ВНИМАНИЕ:** Если вы уже сделали `git push`, данные попали на GitHub!

**Для уже загруженных данных:**
1. Немедленно смените пароли/токены/ключи
2. Используйте BFG Repo-Cleaner или `git filter-branch` для очистки истории
3. Обратитесь к документации GitHub: [github.com/removing-sensitive-data](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository)

**Для еще не загруженных:**
```bash
# Отмените последний коммит
git reset --soft HEAD~1

# Удалите секретные данные из файлов

# Создайте коммит заново
git commit -m "Your message"
```

### Конфликты при слиянии

**Что это:** Git не может автоматически объединить изменения.

**Решение:**
1. Git отметит конфликтные файлы
2. Откройте их в редакторе
3. Найдите блоки с `<<<<<<<`, `=======`, `>>>>>>>`
4. Выберите нужную версию или объедините вручную
5. Удалите маркеры конфликта
6. Сохраните файл
7. Выполните:
```bash
git add conflicted-file.txt
git commit -m "Resolve merge conflict"
```

---

## Дополнительные ресурсы

### Официальная документация
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Docs](https://docs.github.com/)
- [Git Book (на русском)](https://git-scm.com/book/ru/v2)

### Интерактивное обучение
- [Learn Git Branching](https://learngitbranching.js.org/?locale=ru_RU) — интерактивная игра
- [GitHub Skills](https://skills.github.com/) — курсы от GitHub
- [Git-it](https://github.com/jlord/git-it-electron) — настольное приложение для обучения

### Шпаргалки
- [GitHub Git Cheat Sheet (PDF)](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Cheat Sheet](https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet)

### Визуализация Git
- [Visualizing Git](http://git-school.github.io/visualizing-git/)
- [Git Graph extension для VS Code](https://marketplace.visualstudio.com/items?itemName=mhutchie.git-graph)

### YouTube каналы (на русском)
- [Git и GitHub Курс Для Новичков](https://www.youtube.com/watch?v=zZBiln_2FhM)
- [Основы Git](https://www.youtube.com/watch?v=O00FTZDxD0o)

---

## Заключение

Поздравляем! Теперь вы знаете:

✓ Что такое Git и GitHub  
✓ Как установить и настроить Git  
✓ Как создать репозиторий на GitHub  
✓ Как инициализировать проект  
✓ Как настроить авторизацию (Token и SSH)  
✓ Как загрузить проект на GitHub  
✓ Как работать с изменениями  
✓ Основные команды Git  

### Следующие шаги

1. **Практикуйтесь:** Создайте тестовый проект и загрузите его на GitHub
2. **Изучите ветки:** Научитесь работать с `git branch` и `git merge`
3. **Поработайте с командой:** Попробуйте Pull Requests и Code Review
4. **Изучите GitHub Actions:** Автоматизируйте развертывание и тестирование
5. **Ведите красивый README:** Используйте Markdown для документации

### Помните

- **Коммитьте часто:** Делайте небольшие логические коммиты
- **Пишите понятные сообщения:** Будущий вы скажет спасибо
- **Используйте .gitignore:** Не загружайте ненужные файлы
- **Делайте резервные копии:** GitHub — это тоже бэкап вашего кода
- **Не бойтесь экспериментировать:** С Git всегда можно откатиться назад

---

**Версия документа:** 1.0  
**Дата обновления:** 26 января 2026  
**Автор:** Git Manual Guide

**Лицензия:** Этот документ распространяется свободно. Вы можете копировать, изменять и распространять его.

---

## Обратная связь

Нашли ошибку или хотите дополнить инструкцию?  
Создайте Issue в репозитории или отправьте Pull Request!

**Удачи в изучении Git!** 🚀