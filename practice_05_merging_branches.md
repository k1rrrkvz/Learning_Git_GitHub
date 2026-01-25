# Практика 5: Слияние веток

## Цель
Научиться объединять ветки с помощью merge и понимать fast-forward слияние.

## Уровень сложности
⭐⭐⭐ Средний

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "blog-platform", разработайте фичи в отдельных ветках и объедините их.

### Шаги выполнения

#### Шаг 1: Создайте базовый проект
```bash
cd ~/Documents
mkdir blog-platform
cd blog-platform
git init
echo "# Blog Platform" > README.md
git add README.md
git commit -m "Initial commit"
```

#### Шаг 2: Создайте ветку для аутентификации
```bash
git checkout -b feature-auth
```

#### Шаг 3: Добавьте файл аутентификации
```bash
echo "# Authentication System" > auth.txt
echo "- Login functionality" >> auth.txt
echo "- Registration" >> auth.txt
git add auth.txt
git commit -m "Add authentication system"
```

#### Шаг 4: Добавьте ещё один коммит
```bash
echo "- Password reset" >> auth.txt
git add auth.txt
git commit -m "Add password reset feature"
```

#### Шаг 5: Посмотрите историю
```bash
git log --oneline --graph
```

#### Шаг 6: Вернитесь на главную ветку
```bash
git checkout master
```

#### Шаг 7: Проверьте, что auth.txt не существует
```bash
ls
```

**Вы увидите только README.md**

#### Шаг 8: Объедините ветку feature-auth с master
```bash
git merge feature-auth
```

**Вы увидите:**
```
Updating a1b2c3d..e4f5g6h
Fast-forward
 auth.txt | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 auth.txt
```

**Fast-forward** означает, что master просто переместился вперёд.

#### Шаг 9: Проверьте, что файл появился
```bash
ls
cat auth.txt
```

#### Шаг 10: Посмотрите историю
```bash
git log --oneline --graph
```

**Теперь master содержит все коммиты из feature-auth!**

#### Шаг 11: Создайте новую ветку для комментариев
```bash
git checkout -b feature-comments
echo "# Comments System" > comments.txt
echo "- Add comment" >> comments.txt
git add comments.txt
git commit -m "Add comments functionality"
```

#### Шаг 12: Вернитесь на master и добавьте файл
```bash
git checkout master
echo "# License" > LICENSE
echo "MIT License" >> LICENSE
git add LICENSE
git commit -m "Add license file"
```

#### Шаг 13: Посмотрите граф
```bash
git log --oneline --all --graph
```

**Теперь есть расхождение:**
```
* d5e6f7g (HEAD -> master) Add license file
| * c4d5e6f (feature-comments) Add comments functionality
|/
* b2c3d4e Add password reset feature
* a1b2c3d Add authentication system
* 9z8y7x6 Initial commit
```

#### Шаг 14: Объедините ветку feature-comments
```bash
git merge feature-comments
```

**Откроется редактор для сообщения merge commit. Сохраните и закройте.**

**Или используйте:**
```bash
git merge feature-comments -m "Merge feature-comments into master"
```

#### Шаг 15: Посмотрите результат
```bash
git log --oneline --graph --all
```

**Вы увидите merge commit:**
```
*   e6f7g8h (HEAD -> master) Merge feature-comments into master
|\
| * c4d5e6f (feature-comments) Add comments functionality
* | d5e6f7g Add license file
|/
* b2c3d4e Add password reset feature
```

#### Шаг 16: Проверьте, что все файлы на месте
```bash
ls
```

**Вы увидите:**
```
README.md
auth.txt
comments.txt
LICENSE
```

#### Шаг 17: Удалите ненужные ветки
```bash
git branch -d feature-auth
git branch -d feature-comments
```

#### Шаг 18: Проверьте оставшиеся ветки
```bash
git branch
```

**Должен остаться только master.**

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "task-manager" и попрактикуйтесь в слиянии веток.

### Требования
1. Создайте папку `task-manager` и инициализируйте Git
2. Создайте файл `app.txt` с текстом "# Task Manager App"
3. Создайте коммит "Initial app structure"
4. Создайте и переключитесь на ветку `add-tasks-feature`
5. Создайте файл `tasks.txt` с текстом "Create, Edit, Delete tasks"
6. Создайте коммит "Add tasks management"
7. Добавьте в tasks.txt строку "Mark as completed"
8. Создайте коммит "Add task completion"
9. Вернитесь на master
10. Объедините ветку `add-tasks-feature` в master (это будет fast-forward)
11. Проверьте, что файл tasks.txt появился в master
12. Создайте ветку `add-ui` и переключитесь на неё
13. Создайте файл `interface.txt` с текстом "Beautiful UI"
14. Создайте коммит "Add user interface"
15. Переключитесь на master
16. Создайте файл `config.txt` с текстом "App Configuration"
17. Создайте коммит "Add configuration file"
18. Объедините ветку `add-ui` в master (это будет merge commit)
19. Посмотрите граф истории
20. Удалите обе ветки: `add-tasks-feature` и `add-ui`

### Проверьте себя
- `ls` должен показать 4 файла: app.txt, tasks.txt, interface.txt, config.txt
- `git log --oneline --graph` должен показать merge commit
- `git branch` должен показать только master
- Всего должно быть 6 коммитов (включая merge commit)

---

## Подсказки
- `git merge ветка` — объединить ветку с текущей
- Fast-forward происходит, когда ветки не расходились
- Merge commit создаётся, когда ветки расходились
- `git branch -d ветка` — удалить ветку после слияния
- `-m "сообщение"` в git merge позволяет задать сообщение без редактора
- Merge всегда происходит В текущую ветку ИЗ указанной

---

## Что вы изучили
✓ Fast-forward слияние (когда ветки не расходились)  
✓ Merge commit (когда ветки расходились)  
✓ Команда `git merge`  
✓ Удаление веток после слияния (`git branch -d`)  
✓ Понимание графа истории с merge commits  

---

**Предыдущая практика:** practice_04_branching_basics.md  
**Следующая практика:** practice_06_merge_conflicts.md
