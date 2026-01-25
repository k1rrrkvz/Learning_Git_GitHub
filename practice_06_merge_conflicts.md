# Практика 6: Разрешение конфликтов слияния

## Цель
Научиться распознавать и разрешать конфликты, возникающие при слиянии веток.

## Уровень сложности
⭐⭐⭐⭐ Продвинутый

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "team-project", намеренно создайте конфликт и научитесь его решать.

### Шаги выполнения

#### Шаг 1: Создайте проект
```bash
cd ~/Documents
mkdir team-project
cd team-project
git init
```

#### Шаг 2: Создайте файл конфигурации
```bash
echo "# Project Configuration" > config.txt
echo "version: 1.0" >> config.txt
echo "author: Team" >> config.txt
git add config.txt
git commit -m "Add initial config"
```

#### Шаг 3: Создайте ветку для изменений от разработчика A
```bash
git checkout -b developer-a
```

#### Шаг 4: Разработчик A меняет версию и автора
```bash
echo "# Project Configuration" > config.txt
echo "version: 2.0" >> config.txt
echo "author: Developer A" >> config.txt
git add config.txt
git commit -m "Update version to 2.0 and author"
```

#### Шаг 5: Вернитесь на master
```bash
git checkout master
```

#### Шаг 6: Создайте ветку для разработчика B
```bash
git checkout -b developer-b
```

#### Шаг 7: Разработчик B тоже меняет версию и автора
```bash
echo "# Project Configuration" > config.txt
echo "version: 1.5" >> config.txt
echo "author: Developer B" >> config.txt
git add config.txt
git commit -m "Update version to 1.5 and change author"
```

#### Шаг 8: Вернитесь на master
```bash
git checkout master
```

#### Шаг 9: Попробуйте объединить ветку developer-a (успешно)
```bash
git merge developer-a
```

**Успех! Fast-forward merge.**

#### Шаг 10: Попробуйте объединить developer-b
```bash
git merge developer-b
```

**КОНФЛИКТ!**
```
Auto-merging config.txt
CONFLICT (content): Merge conflict in config.txt
Automatic merge failed; fix conflicts and then commit the result.
```

#### Шаг 11: Проверьте статус
```bash
git status
```

**Вы увидите:**
```
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   config.txt
```

#### Шаг 12: Посмотрите содержимое конфликтного файла
```bash
cat config.txt
```

**Вы увидите:**
```
# Project Configuration
<<<<<<< HEAD
version: 2.0
author: Developer A
=======
version: 1.5
author: Developer B
>>>>>>> developer-b
```

**Разбор маркеров:**
- `<<<<<<< HEAD` — начало вашей версии (текущая ветка)
- `=======` — разделитель
- `>>>>>>> developer-b` — версия из вливаемой ветки

#### Шаг 13: Откройте файл в текстовом редакторе (или через echo)
Решим конфликт: возьмём версию 2.0 и автора "Team"
```bash
echo "# Project Configuration" > config.txt
echo "version: 2.0" >> config.txt
echo "author: Team" >> config.txt
```

#### Шаг 14: Проверьте, что конфликт разрешён
```bash
cat config.txt
```

**Не должно быть маркеров конфликта!**

#### Шаг 15: Отметьте конфликт как разрешённый
```bash
git add config.txt
```

#### Шаг 16: Проверьте статус
```bash
git status
```

**Вы увидите:**
```
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)
```

#### Шаг 17: Завершите слияние
```bash
git commit -m "Resolve conflict: keep version 2.0 and set author to Team"
```

#### Шаг 18: Посмотрите историю
```bash
git log --oneline --graph --all
```

#### Шаг 19: Создайте ещё один конфликт с несколькими файлами
```bash
git checkout -b feature-x
echo "Feature X content" > feature.txt
echo "# Project Configuration" > config.txt
echo "version: 3.0" >> config.txt
echo "author: Feature X Developer" >> config.txt
git add .
git commit -m "Add feature X and update config"
```

#### Шаг 20: Вернитесь на master и сделайте другие изменения
```bash
git checkout master
echo "Documentation update" > docs.txt
echo "# Project Configuration" > config.txt
echo "version: 2.5" >> config.txt
echo "author: Team Lead" >> config.txt
git add .
git commit -m "Add docs and update config"
```

#### Шаг 21: Попробуйте слить feature-x
```bash
git merge feature-x
```

**Конфликт только в config.txt!**

#### Шаг 22: Проверьте статус
```bash
git status
```

#### Шаг 23: Разрешите конфликт
```bash
echo "# Project Configuration" > config.txt
echo "version: 3.0" >> config.txt
echo "author: Team Lead" >> config.txt
git add config.txt
git commit -m "Merge feature-x: use version 3.0"
```

#### Шаг 24: Проверьте финальное состояние
```bash
ls
git log --oneline --graph
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "website-redesign" и разрешите конфликты при слиянии.

### Требования
1. Создайте папку `website-redesign` и инициализируйте Git
2. Создайте файл `style.txt` с содержимым:
   ```
   color: blue
   font: Arial
   ```
3. Создайте коммит "Initial styles"
4. Создайте ветку `designer-1` и переключитесь на неё
5. Измените style.txt на:
   ```
   color: red
   font: Helvetica
   ```
6. Создайте коммит "Designer 1: update colors and font"
7. Вернитесь на master
8. Создайте ветку `designer-2` и переключитесь на неё
9. Измените style.txt на:
   ```
   color: green
   font: Times
   ```
10. Создайте коммит "Designer 2: new color scheme"
11. Вернитесь на master
12. Объедините ветку `designer-1` (должно быть успешно)
13. Попробуйте объединить ветку `designer-2` (будет конфликт!)
14. Посмотрите статус и содержимое файла с конфликтом
15. Разрешите конфликт, выбрав: `color: red` и `font: Times`
16. Добавьте файл и завершите слияние с сообщением "Merge designer-2: combine best choices"
17. Посмотрите граф истории
18. Удалите обе ветки: `designer-1` и `designer-2`

### Проверьте себя
- Файл style.txt должен содержать: `color: red` и `font: Times`
- `git status` должен показать "working tree clean"
- `git log --oneline` должен показать merge commit
- `git branch` должен показать только master

---

## Подсказки
- Конфликт возникает, когда одна строка изменена в обеих ветках
- `<<<<<<< HEAD` — ваша текущая версия
- `=======` — разделитель
- `>>>>>>> ветка` — версия из вливаемой ветки
- Удалите маркеры конфликта вручную
- После разрешения: `git add` → `git commit`
- Можно выбрать одну версию, обе или написать новую

---

## Что вы изучили
✓ Понимание причин конфликтов слияния  
✓ Распознавание маркеров конфликта (`<<<<<<<`, `=======`, `>>>>>>>`)  
✓ Ручное разрешение конфликтов  
✓ Завершение слияния после разрешения конфликтов  
✓ Работа с конфликтами в нескольких файлах  

---

**Предыдущая практика:** practice_05_merging_branches.md  
**Следующая практика:** practice_07_remote_basics.md
