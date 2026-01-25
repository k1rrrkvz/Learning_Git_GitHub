# Практика 2: Работа с изменениями в файлах

## Цель
Научиться отслеживать изменения, просматривать различия и создавать коммиты для изменённых файлов.

## Уровень сложности
⭐⭐ Базовый

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "todo-app", добавьте задачи и научитесь отслеживать изменения.

### Шаги выполнения

#### Шаг 1: Создайте проект и инициализируйте Git
```bash
cd ~/Documents
mkdir todo-app
cd todo-app
git init
```

#### Шаг 2: Создайте файл с задачами
```bash
echo "# My TODO List" > tasks.txt
echo "" >> tasks.txt
echo "## Today" >> tasks.txt
echo "- Learn Git basics" >> tasks.txt
```

#### Шаг 3: Создайте первый коммит
```bash
git add tasks.txt
git commit -m "Initial task list"
```

#### Шаг 4: Добавьте новые задачи в файл
```bash
echo "- Practice Git commands" >> tasks.txt
echo "- Read Git documentation" >> tasks.txt
```

#### Шаг 5: Проверьте статус
```bash
git status
```

**Вы увидите:**
```
On branch master
Changes not staged for commit:
        modified:   tasks.txt
```

#### Шаг 6: Посмотрите, что именно изменилось
```bash
git diff
```

**Вы увидите:**
```diff
diff --git a/tasks.txt b/tasks.txt
--- a/tasks.txt
+++ b/tasks.txt
@@ -2,0 +3,2 @@
+- Practice Git commands
+- Read Git documentation
```

#### Шаг 7: Добавьте изменения и создайте коммит
```bash
git add tasks.txt
git commit -m "Add two more tasks"
```

#### Шаг 8: Создайте файл с завершёнными задачами
```bash
echo "# Completed Tasks" > completed.txt
echo "" >> completed.txt
echo "- Learn Git basics" >> completed.txt
```

#### Шаг 9: Измените основной файл задач
```bash
echo "" >> tasks.txt
echo "## Tomorrow" >> tasks.txt
echo "- Create a GitHub account" >> tasks.txt
```

#### Шаг 10: Проверьте статус (2 файла изменены)
```bash
git status
```

#### Шаг 11: Посмотрите различия для конкретного файла
```bash
git diff tasks.txt
```

#### Шаг 12: Добавьте все изменения
```bash
git add .
```

#### Шаг 13: Проверьте статус после добавления
```bash
git status
```

**Вы увидите:**
```
Changes to be committed:
        new file:   completed.txt
        modified:   tasks.txt
```

#### Шаг 14: Создайте коммит
```bash
git commit -m "Add completed tasks file and tomorrow's tasks"
```

#### Шаг 15: Просмотрите историю с деталями
```bash
git log --oneline --all
```

#### Шаг 16: Посмотрите детали последнего коммита
```bash
git show HEAD
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "shopping-list" и поработайте с изменениями в файлах.

### Требования
1. Создайте папку `shopping-list` и инициализируйте Git
2. Создайте файл `groceries.txt` с 3 продуктами (например: milk, bread, eggs)
3. Создайте коммит с сообщением "Add initial grocery list"
4. Добавьте в файл ещё 2 продукта
5. Используйте `git diff` чтобы посмотреть изменения
6. Создайте коммит с сообщением "Add more groceries"
7. Создайте новый файл `bought.txt` с одним купленным продуктом
8. Добавьте в `groceries.txt` ещё один продукт
9. Проверьте статус (должно быть 1 новый файл и 1 изменённый)
10. Добавьте все изменения и создайте коммит "Track bought items and add more groceries"
11. Просмотрите последний коммит командой `git show HEAD`

### Проверьте себя
- Команда `git log --oneline` должна показать 3 коммита
- Команда `ls` должна показать 2 файла: groceries.txt и bought.txt
- Команда `git status` должна показать "working tree clean"

---

## Подсказки
- `git diff` показывает изменения в файлах до `git add`
- `git diff --staged` показывает изменения после `git add`
- `echo "текст" >> файл` добавляет строку в конец файла
- `git show HEAD` показывает детали последнего коммита
- Зелёные строки (+) — добавленные, красные (-) — удалённые

---

## Что вы изучили
✓ Просмотр изменений (`git diff`)  
✓ Работа с изменёнными файлами  
✓ Добавление нескольких файлов одновременно (`git add .`)  
✓ Просмотр деталей коммита (`git show`)  
✓ Различие между новыми и изменёнными файлами  

---

**Предыдущая практика:** practice_01_basic_workflow.md  
**Следующая практика:** practice_03_undoing_changes.md
