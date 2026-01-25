# Практика 3: Отмена изменений

## Цель
Научиться отменять изменения в файлах, убирать файлы из staging area и исправлять коммиты.

## Уровень сложности
⭐⭐ Базовый

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "notes-app" и потренируйтесь отменять различные типы изменений.

### Шаги выполнения

#### Шаг 1: Создайте проект
```bash
cd ~/Documents
mkdir notes-app
cd notes-app
git init
```

#### Шаг 2: Создайте файл с заметками
```bash
echo "# My Notes" > notes.txt
echo "" >> notes.txt
echo "Note 1: Git is awesome" >> notes.txt
git add notes.txt
git commit -m "Add first note"
```

#### Шаг 3: Добавьте ошибочное изменение
```bash
echo "Note 2: This is a mistake" >> notes.txt
```

#### Шаг 4: Проверьте изменения
```bash
git status
git diff
```

#### Шаг 5: Отмените изменения в файле (до git add)
```bash
git restore notes.txt
```

#### Шаг 6: Проверьте, что изменения отменены
```bash
git status
cat notes.txt
```

**Файл вернулся к состоянию последнего коммита!**

#### Шаг 7: Добавьте правильное изменение
```bash
echo "Note 2: Git helps track changes" >> notes.txt
git add notes.txt
```

#### Шаг 8: Создайте коммит
```bash
git commit -m "Add second note"
```

#### Шаг 9: Добавьте новый файл и измените существующий
```bash
echo "# Ideas" > ideas.txt
echo "Idea 1: Learn Git branches" >> ideas.txt
echo "Note 3: Practice makes perfect" >> notes.txt
```

#### Шаг 10: Добавьте изменения в staging
```bash
git add ideas.txt notes.txt
```

#### Шаг 11: Проверьте статус
```bash
git status
```

**Оба файла в staging area (зелёным цветом)**

#### Шаг 12: Уберите ideas.txt из staging (но сохраните изменения)
```bash
git restore --staged ideas.txt
```

#### Шаг 13: Проверьте статус снова
```bash
git status
```

**Теперь:**
- notes.txt — в staging (зелёный)
- ideas.txt — не в staging (красный)

#### Шаг 14: Создайте коммит только для notes.txt
```bash
git commit -m "Add third note"
```

#### Шаг 15: Добавьте ideas.txt в следующий коммит
```bash
git add ideas.txt
git commit -m "Add ideas file"
```

#### Шаг 16: Исправьте сообщение последнего коммита
```bash
git commit --amend -m "Add ideas file for future projects"
```

#### Шаг 17: Просмотрите историю
```bash
git log --oneline
```

#### Шаг 18: Создайте файл с опечаткой в имени
```bash
echo "TODO: Fix bugs" > todoo.txt
git add todoo.txt
git commit -m "Add TODO file"
```

#### Шаг 19: Поймите, что имя файла неправильное, отмените коммит
```bash
git reset --soft HEAD~1
```

#### Шаг 20: Проверьте статус
```bash
git status
```

**Файл todoo.txt всё ещё в staging, но коммит отменён!**

#### Шаг 21: Уберите файл из staging и удалите его
```bash
git restore --staged todoo.txt
rm todoo.txt
```

#### Шаг 22: Создайте файл с правильным именем
```bash
echo "TODO: Fix bugs" > todo.txt
git add todo.txt
git commit -m "Add TODO file"
```

#### Шаг 23: Просмотрите финальную историю
```bash
git log --oneline
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "recipe-book" и потренируйтесь отменять различные операции.

### Требования
1. Создайте папку `recipe-book` и инициализируйте Git
2. Создайте файл `recipes.txt` с текстом "# My Recipes"
3. Создайте коммит "Initial recipe book"
4. Добавьте строку "Recipe 1: Wrong recipe" в файл
5. Посмотрите изменения командой `git diff`
6. Отмените изменения командой `git restore recipes.txt`
7. Проверьте, что файл вернулся к исходному состоянию
8. Добавьте строку "Recipe 1: Pasta Carbonara" в файл
9. Добавьте файл в staging и создайте коммит "Add first recipe"
10. Создайте файл `ingredients.txt` с текстом "Eggs, Bacon, Pasta"
11. Создайте файл `notes.txt` с текстом "Personal notes"
12. Добавьте оба файла в staging командой `git add .`
13. Уберите notes.txt из staging командой `git restore --staged notes.txt`
14. Создайте коммит только для ingredients.txt с сообщением "Add ingredient list"
15. Исправьте сообщение последнего коммита на "Add ingredients for pasta" используя `git commit --amend`

### Проверьте себя
- `git log --oneline` должен показать 3 коммита
- `git status` должен показать, что notes.txt не отслеживается (Untracked)
- Последний коммит должен иметь сообщение "Add ingredients for pasta"

---

## Подсказки
- `git restore файл` — отменить изменения в файле (до git add)
- `git restore --staged файл` — убрать из staging (после git add)
- `git commit --amend` — исправить последний коммит
- `git reset --soft HEAD~1` — отменить последний коммит, но сохранить изменения
- `rm файл` — удалить файл из файловой системы

---

## Что вы изучили
✓ Отмена изменений в рабочей директории (`git restore`)  
✓ Удаление файлов из staging area (`git restore --staged`)  
✓ Исправление последнего коммита (`git commit --amend`)  
✓ Отмена последнего коммита (`git reset --soft HEAD~1`)  
✓ Разница между рабочей директорией и staging area  

---

**Предыдущая практика:** practice_02_editing_files.md  
**Следующая практика:** practice_04_branching_basics.md
