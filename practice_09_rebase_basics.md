# Практика 9: Основы Rebase

## Цель
Научиться использовать rebase для линейной истории, понять различие между merge и rebase, и научиться интерактивному rebase.

## Уровень сложности
⭐⭐⭐⭐⭐ Экспертный

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "api-service", изучите разницу между merge и rebase, освойте интерактивный rebase.

### Шаги выполнения

#### Шаг 1: Создайте проект
```bash
cd ~/Documents
mkdir api-service
cd api-service
git init
```

#### Шаг 2: Создайте базовую структуру
```bash
echo "# API Service" > README.md
git add README.md
git commit -m "Initial commit"
```

#### Шаг 3: Добавьте функционал в master
```bash
echo "const express = require('express');" > server.js
git add server.js
git commit -m "Add express server"
```

#### Шаг 4: Создайте ветку для новой фичи
```bash
git checkout -b feature-auth
echo "function authenticate() {}" > auth.js
git add auth.js
git commit -m "Add auth function"
```

#### Шаг 5: Добавьте ещё коммит в feature-auth
```bash
echo "function validateToken() {}" >> auth.js
git add auth.js
git commit -m "Add token validation"
```

#### Шаг 6: Вернитесь на master и добавьте коммиты
```bash
git checkout master
echo "const config = {};" > config.js
git add config.js
git commit -m "Add configuration"
```

#### Шаг 7: Ещё один коммит в master
```bash
echo "const db = require('db');" >> server.js
git add server.js
git commit -m "Add database connection"
```

#### Шаг 8: Посмотрите граф
```bash
git log --oneline --graph --all
```

**Вы увидите расхождение:**
```
* e4f5g6h (HEAD -> master) Add database connection
* d5e6f7g Add configuration
| * c4d5e6f (feature-auth) Add token validation
| * b3c4d5e Add auth function
|/
* a2b3c4d Add express server
* a1b2c3d Initial commit
```

#### Шаг 9: Переключитесь на feature-auth
```bash
git checkout feature-auth
```

#### Шаг 10: Сделайте rebase на master
```bash
git rebase master
```

**Git "пересаживает" коммиты feature-auth на вершину master!**

#### Шаг 11: Посмотрите граф снова
```bash
git log --oneline --graph --all
```

**Теперь линейная история:**
```
* f6g7h8i (HEAD -> feature-auth) Add token validation
* e5f6g7h Add auth function
* e4f5g6h (master) Add database connection
* d5e6f7g Add configuration
* a2b3c4d Add express server
* a1b2c3d Initial commit
```

#### Шаг 12: Вернитесь на master и сделайте fast-forward merge
```bash
git checkout master
git merge feature-auth
```

**Fast-forward! Линейная история сохранена.**

#### Шаг 13: Посмотрите финальный граф
```bash
git log --oneline --graph
```

**Красивая прямая линия!**

---

### Интерактивный Rebase

#### Шаг 14: Создайте несколько "грязных" коммитов
```bash
echo "line1" > test.js
git add test.js
git commit -m "Add test file"

echo "line2" >> test.js
git add test.js
git commit -m "Update test"

echo "line3" >> test.js
git add test.js
git commit -m "Fix typo"

echo "line4" >> test.js
git add test.js
git commit -m "More changes"
```

#### Шаг 15: Посмотрите историю
```bash
git log --oneline
```

**Много мелких коммитов!**

#### Шаг 16: Запустите интерактивный rebase (последние 4 коммита)
```bash
git rebase -i HEAD~4
```

**Откроется редактор с коммитами:**
```
pick a1b2c3d Add test file
pick b2c3d4e Update test
pick c3d4e5f Fix typo
pick d4e5f6g More changes
```

#### Шаг 17: Изменим команды (для примера используем команды)
Мы объединим последние 3 коммита с первым. 

**В реальном редакторе измените на:**
```
pick a1b2c3d Add test file
squash b2c3d4e Update test
squash c3d4e5f Fix typo
squash d4e5f6g More changes
```

**Но через командную строку сделаем проще:**
Создадим скрипт для rebase:
```bash
git rebase -i HEAD~4
```

**Если хотите просто потренироваться, можно отменить:**
```bash
git rebase --abort
```

#### Шаг 18: Создадим более практичный пример
Сначала отменим последние коммиты:
```bash
git reset --hard HEAD~4
```

#### Шаг 19: Создадим новые коммиты для редактирования
```bash
echo "function add(a, b) {" > math.js
echo "  return a + b" >> math.js
echo "}" >> math.js
git add math.js
git commit -m "Add function"

echo "function subtract(a, b) {" >> math.js
echo "  return a - b" >> math.js
echo "}" >> math.js
git add math.js
git commit -m "Add subtract"

echo "// TODO: add multiply" >> math.js
git add math.js
git commit -m "Add TODO"
```

#### Шаг 20: Посмотрите историю
```bash
git log --oneline -5
```

#### Шаг 21: Используем rebase для изменения сообщений
Отредактируем последнее сообщение:
```bash
git rebase -i HEAD~1
```

В открывшемся редакторе (или если не откроется):
```bash
git commit --amend -m "Add TODO for multiply function"
git rebase --continue
```

#### Шаг 22: Создайте ветку для демонстрации конфликта при rebase
```bash
git checkout -b feature-multiply
echo "function multiply(a, b) {" >> math.js
echo "  return a * b" >> math.js
echo "}" >> math.js
git add math.js
git commit -m "Implement multiply"
```

#### Шаг 23: Вернитесь на master и измените тот же файл
```bash
git checkout master
echo "function divide(a, b) {" >> math.js
echo "  return a / b" >> math.js
echo "}" >> math.js
git add math.js
git commit -m "Add divide function"
```

#### Шаг 24: Попробуйте rebase feature-multiply на master
```bash
git checkout feature-multiply
git rebase master
```

**КОНФЛИКТ!**

#### Шаг 25: Посмотрите статус
```bash
git status
```

#### Шаг 26: Разрешите конфликт
```bash
cat math.js
```

Исправьте файл (объедините обе функции):
```bash
echo "function add(a, b) {" > math.js
echo "  return a + b" >> math.js
echo "}" >> math.js
echo "function subtract(a, b) {" >> math.js
echo "  return a - b" >> math.js
echo "}" >> math.js
echo "// TODO: add multiply" >> math.js
echo "function divide(a, b) {" >> math.js
echo "  return a / b" >> math.js
echo "}" >> math.js
echo "function multiply(a, b) {" >> math.js
echo "  return a * b" >> math.js
echo "}" >> math.js
```

#### Шаг 27: Продолжите rebase
```bash
git add math.js
git rebase --continue
```

#### Шаг 28: Посмотрите результат
```bash
git log --oneline --graph --all
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "game-engine" и попрактикуйтесь в rebase.

### Требования
1. Создайте папку `game-engine` и инициализируйте Git
2. Создайте файл `engine.js` с текстом "const Engine = {};"
3. Создайте коммит "Initial engine"
4. Создайте ветку `graphics-system` и переключитесь на неё
5. Создайте файл `graphics.js` с текстом "function render() {}"
6. Создайте коммит "Add render function"
7. Добавьте в graphics.js строку "function draw() {}"
8. Создайте коммит "Add draw function"
9. Переключитесь на master
10. Создайте файл `physics.js` с текстом "function calculate() {}"
11. Создайте коммит "Add physics"
12. Создайте файл `sound.js` с текстом "function playSound() {}"
13. Создайте коммит "Add sound system"
14. Посмотрите граф истории (должно быть расхождение)
15. Переключитесь на ветку `graphics-system`
16. Сделайте rebase на master: `git rebase master`
17. Посмотрите граф (должна быть линейная история)
18. Переключитесь на master
19. Сделайте fast-forward merge: `git merge graphics-system`
20. Создайте 3 мелких коммита:
    - Добавьте "// v1" в engine.js → коммит "v1"
    - Добавьте "// v2" в engine.js → коммит "v2"
    - Добавьте "// v3" в engine.js → коммит "v3"
21. Посмотрите последние 5 коммитов
22. Измените сообщение последнего коммита на "Version 3" используя `git commit --amend`

### Проверьте себя
- `git log --oneline --graph` должен показать линейную историю без развилок
- Должно быть 6 коммитов (начальный + physics + sound + 2 graphics + version 3)
- `ls` должен показать 4 файла: engine.js, graphics.js, physics.js, sound.js
- Последний коммит должен иметь сообщение "Version 3"

---

## Подсказки
- `git rebase ветка` — перенести текущую ветку на вершину указанной
- `git rebase -i HEAD~n` — интерактивный rebase последних n коммитов
- `pick` — оставить коммит как есть
- `squash` — объединить с предыдущим коммитом
- `reword` — изменить сообщение коммита
- `edit` — остановиться на коммите для редактирования
- `git rebase --abort` — отменить rebase
- `git rebase --continue` — продолжить после разрешения конфликта
- Rebase изменяет историю (создаёт новые коммиты)
- НЕ делайте rebase для коммитов, которые уже отправлены на сервер!

---

## Что вы изучили
✓ Основы rebase (`git rebase`)  
✓ Разницу между merge и rebase  
✓ Создание линейной истории  
✓ Fast-forward merge после rebase  
✓ Интерактивный rebase (`git rebase -i`)  
✓ Изменение сообщений коммитов (`git commit --amend`)  
✓ Разрешение конфликтов при rebase  
✓ Команды pick, squash для объединения коммитов  

---

**Предыдущая практика:** practice_08_stashing.md  
**Следующая практика:** practice_10_advanced_workflow.md
