# Практика 8: Временное сохранение изменений (Stash)

## Цель
Научиться временно сохранять незакоммиченные изменения, переключаться между задачами и возвращать сохранённые изменения.

## Уровень сложности
⭐⭐⭐⭐ Продвинутый

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "web-app", начните работу над фичей, временно отложите её для исправления бага и верните изменения обратно.

### Шаги выполнения

#### Шаг 1: Создайте проект
```bash
cd ~/Documents
mkdir web-app
cd web-app
git init
```

#### Шаг 2: Создайте начальные файлы
```bash
echo "# Web Application" > README.md
echo "const app = 'main';" > app.js
git add .
git commit -m "Initial commit"
```

#### Шаг 3: Начните работу над новой фичей
```bash
echo "const feature = 'new feature';" >> app.js
echo "// TODO: implement feature" >> app.js
```

#### Шаг 4: Создайте новый файл для фичи
```bash
echo "function newFeature() {" > feature.js
echo "  // in progress" >> feature.js
echo "}" >> feature.js
```

#### Шаг 5: Проверьте статус
```bash
git status
```

**Вы увидите:**
```
Changes not staged for commit:
        modified:   app.js

Untracked files:
        feature.js
```

#### Шаг 6: СРОЧНО! Нужно исправить баг в master
Но у нас незакоммиченные изменения. Сохраним их временно!

```bash
git stash push -m "Work in progress: new feature"
```

**Если нужно включить untracked файлы:**
```bash
git stash push -u -m "WIP: new feature with new files"
```

Используем вторую команду:
```bash
git stash push -u -m "WIP: new feature with new files"
```

#### Шаг 7: Проверьте статус
```bash
git status
```

**Чисто!**
```
On branch master
nothing to commit, working tree clean
```

#### Шаг 8: Проверьте файлы
```bash
cat app.js
ls
```

**Изменения исчезли! feature.js тоже пропал!**

#### Шаг 9: Посмотрите список сохранённых stash
```bash
git stash list
```

**Вы увидите:**
```
stash@{0}: On master: WIP: new feature with new files
```

#### Шаг 10: Исправьте "баг"
```bash
echo "const bugFix = 'fixed';" >> app.js
git add app.js
git commit -m "Fix critical bug"
```

#### Шаг 11: Теперь верните сохранённые изменения
```bash
git stash pop
```

**`pop` применяет последний stash и удаляет его из списка**

#### Шаг 12: Проверьте файлы
```bash
cat app.js
ls
```

**Всё вернулось! И bugFix, и изменения фичи!**

#### Шаг 13: Завершите работу над фичей
```bash
echo "  return 'feature complete';" >> feature.js
git add .
git commit -m "Complete new feature"
```

#### Шаг 14: Создайте несколько stash для практики
```bash
echo "test1" > test1.txt
git stash push -u -m "Test stash 1"

echo "test2" > test2.txt
git stash push -u -m "Test stash 2"

echo "test3" > test3.txt
git stash push -u -m "Test stash 3"
```

#### Шаг 15: Посмотрите список
```bash
git stash list
```

**Вы увидите:**
```
stash@{0}: On master: Test stash 3
stash@{1}: On master: Test stash 2
stash@{2}: On master: Test stash 1
```

**Номера начинаются с 0, новые в начале!**

#### Шаг 16: Посмотрите содержимое конкретного stash
```bash
git stash show stash@{1}
```

#### Шаг 17: Посмотрите детальное содержимое
```bash
git stash show -p stash@{1}
```

**`-p` показывает patch (изменения построчно)**

#### Шаг 18: Примените stash БЕЗ удаления из списка
```bash
git stash apply stash@{2}
```

**Теперь test1.txt появился!**

#### Шаг 19: Проверьте список
```bash
git stash list
```

**Все 3 stash всё ещё на месте!**

#### Шаг 20: Удалите конкретный stash
```bash
git stash drop stash@{2}
```

#### Шаг 21: Очистите все stash
```bash
git stash clear
```

#### Шаг 22: Проверьте
```bash
git stash list
```

**Пусто!**

#### Шаг 23: Создайте stash с частью изменений
```bash
echo "change1" >> app.js
echo "change2" >> feature.js
```

#### Шаг 24: Добавьте только app.js в stash
```bash
git stash push -m "Only app.js changes" app.js
```

#### Шаг 25: Проверьте статус
```bash
git status
```

**feature.js всё ещё изменён, но app.js — нет!**

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "mobile-app" и потренируйтесь работать со stash в реальных сценариях.

### Требования
1. Создайте папку `mobile-app` и инициализируйте Git
2. Создайте файл `main.dart` с текстом "void main() {}"
3. Создайте коммит "Initial mobile app"
4. Начните работу: добавьте в main.dart строку "print('Loading...');"
5. Создайте новый файл `screens.dart` с текстом "class HomeScreen {}"
6. Проверьте статус (должно быть: 1 изменённый, 1 новый)
7. Сохраните изменения в stash с сообщением "WIP: home screen" и флагом `-u`
8. Проверьте, что рабочая директория чистая
9. Создайте файл `config.dart` с текстом "const API_URL = 'https://api.example.com';"
10. Создайте коммит "Add API configuration"
11. Посмотрите список stash
12. Верните сохранённые изменения командой `git stash pop`
13. Проверьте, что оба файла появились (main.dart изменён, screens.dart создан)
14. Создайте ещё изменения: добавьте в config.dart строку "const TIMEOUT = 30;"
15. Создайте второе изменение: добавьте файл `utils.dart` с текстом "helper functions"
16. Сохраните только config.dart в stash с сообщением "Config timeout update"
17. Проверьте статус (должен остаться только utils.dart)
18. Посмотрите детали stash командой `git stash show -p stash@{0}`
19. Очистите все stash командой `git stash clear`
20. Добавьте все оставшиеся файлы и создайте коммит "Complete initial development"

### Проверьте себя
- `git stash list` должен быть пуст
- `git log --oneline` должен показать 3 коммита
- `ls` должен показать 4 файла: main.dart, screens.dart, config.dart, utils.dart
- `git status` должен показать "working tree clean"

---

## Подсказки
- `git stash` или `git stash push` — сохранить изменения
- `git stash push -u` — включить untracked файлы
- `git stash push -m "описание"` — добавить сообщение
- `git stash list` — список всех stash
- `git stash pop` — применить и удалить последний stash
- `git stash apply` — применить БЕЗ удаления
- `git stash drop stash@{n}` — удалить конкретный stash
- `git stash clear` — удалить все stash
- `git stash show -p stash@{n}` — посмотреть детали
- Stash работает как стек: последний добавленный — первый применяется

---

## Что вы изучили
✓ Временное сохранение изменений (`git stash`)  
✓ Включение untracked файлов (`-u`)  
✓ Просмотр списка stash (`git stash list`)  
✓ Применение stash с удалением (`git stash pop`)  
✓ Применение stash без удаления (`git stash apply`)  
✓ Работа с конкретными stash (`stash@{n}`)  
✓ Удаление stash (`git stash drop`, `git stash clear`)  
✓ Выборочное сохранение файлов  

---

**Предыдущая практика:** practice_07_remote_basics.md  
**Следующая практика:** practice_09_rebase_basics.md
