# Практика 4: Основы работы с ветками

## Цель
Научиться создавать ветки, переключаться между ними и понимать их назначение.

## Уровень сложности
⭐⭐⭐ Средний

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "website" и поработайте с ветками для разных фич.

### Шаги выполнения

#### Шаг 1: Создайте проект
```bash
cd ~/Documents
mkdir website
cd website
git init
```

#### Шаг 2: Создайте основной файл
```bash
echo "# My Website" > index.html
echo "<h1>Welcome</h1>" >> index.html
git add index.html
git commit -m "Add home page"
```

#### Шаг 3: Посмотрите текущую ветку
```bash
git branch
```

**Вы увидите:**
```
* master
```

Звёздочка (*) показывает активную ветку.

#### Шаг 4: Создайте новую ветку для добавления меню
```bash
git branch add-navigation
```

#### Шаг 5: Посмотрите список веток
```bash
git branch
```

**Вы увидите:**
```
  add-navigation
* master
```

#### Шаг 6: Переключитесь на новую ветку
```bash
git checkout add-navigation
```

#### Шаг 7: Проверьте активную ветку
```bash
git branch
```

**Теперь:**
```
* add-navigation
  master
```

#### Шаг 8: Добавьте навигацию
```bash
echo "<nav>Home | About | Contact</nav>" >> index.html
```

#### Шаг 9: Посмотрите изменения
```bash
git diff
```

#### Шаг 10: Создайте коммит в ветке add-navigation
```bash
git add index.html
git commit -m "Add navigation menu"
```

#### Шаг 11: Переключитесь обратно на master
```bash
git checkout master
```

#### Шаг 12: Посмотрите содержимое файла
```bash
cat index.html
```

**Навигации нет! Мы на ветке master.**

#### Шаг 13: Посмотрите историю обеих веток
```bash
git log --oneline --all --graph
```

**Вы увидите:**
```
* b2c3d4e (add-navigation) Add navigation menu
* a1b2c3d (HEAD -> master) Add home page
```

#### Шаг 14: Создайте ещё одну ветку от master
```bash
git branch add-footer
git checkout add-footer
```

**Или одной командой:**
```bash
git checkout -b add-footer
```

Но мы уже создали ветку, так что просто переключитесь:
```bash
git checkout add-footer
```

#### Шаг 15: Добавьте футер
```bash
echo "<footer>© 2026 My Website</footer>" >> index.html
git add index.html
git commit -m "Add footer"
```

#### Шаг 16: Посмотрите граф всех веток
```bash
git log --oneline --all --graph
```

**Структура:**
```
* c4d5e6f (HEAD -> add-footer) Add footer
| * b2c3d4e (add-navigation) Add navigation menu
|/
* a1b2c3d (master) Add home page
```

#### Шаг 17: Вернитесь на master
```bash
git checkout master
```

#### Шаг 18: Проверьте содержимое
```bash
cat index.html
```

**Только базовое содержимое!**

#### Шаг 19: Создайте ещё один файл на master
```bash
echo "# About Us" > about.html
git add about.html
git commit -m "Add about page"
```

#### Шаг 20: Посмотрите финальный граф
```bash
git log --oneline --all --graph
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "online-store" и поработайте с тремя разными ветками.

### Требования
1. Создайте папку `online-store` и инициализируйте Git
2. Создайте файл `products.txt` с текстом "# Products"
3. Создайте коммит "Initial product list"
4. Проверьте текущую ветку командой `git branch`
5. Создайте ветку `add-electronics` (не переключайтесь на неё)
6. Создайте ветку `add-clothing` (не переключайтесь на неё)
7. Проверьте список всех веток
8. Переключитесь на ветку `add-electronics`
9. Добавьте в файл products.txt строку "- Laptop"
10. Создайте коммит "Add laptop to electronics"
11. Переключитесь на ветку `add-clothing`
12. Добавьте в файл products.txt строку "- T-Shirt"
13. Создайте коммит "Add t-shirt to clothing"
14. Переключитесь обратно на master
15. Посмотрите содержимое products.txt (должен быть только заголовок)
16. Создайте новый файл `categories.txt` с текстом "Electronics, Clothing"
17. Создайте коммит "Add categories file"
18. Посмотрите граф всех веток командой `git log --oneline --all --graph`

### Проверьте себя
- `git branch` должен показать 3 ветки: master, add-electronics, add-clothing
- На ветке master файл products.txt содержит только "# Products"
- График должен показывать разветвление от master на две ветки

---

## Подсказки
- `git branch название` — создать новую ветку
- `git checkout название` — переключиться на ветку
- `git checkout -b название` — создать и переключиться (2 в 1)
- `git branch` — посмотреть список веток
- `git log --oneline --all --graph` — визуализировать историю
- Каждая ветка имеет независимую историю коммитов

---

## Что вы изучили
✓ Создание веток (`git branch название`)  
✓ Переключение между ветками (`git checkout название`)  
✓ Создание и переключение одновременно (`git checkout -b название`)  
✓ Просмотр списка веток (`git branch`)  
✓ Визуализация истории веток (`git log --graph`)  
✓ Понимание независимости веток  

---

**Предыдущая практика:** practice_03_undoing_changes.md  
**Следующая практика:** practice_05_merging_branches.md
