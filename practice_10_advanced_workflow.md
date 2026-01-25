# Практика 10: Продвинутый рабочий процесс

## Цель
Объединить все изученные навыки: ветки, merge, rebase, stash, конфликты, работа с удалённым репозиторием и создать полноценный рабочий процесс.

## Уровень сложности
⭐⭐⭐⭐⭐ Экспертный

---

## Часть 1: Практика с примером (копируйте команды)

### Задание
Создайте проект "e-commerce-platform" с полным циклом разработки: несколько разработчиков, фичи, баг-фиксы, code review симуляция.

### Шаги выполнения

#### Этап 1: Инициализация проекта

```bash
cd ~/Documents
mkdir e-commerce-platform
cd e-commerce-platform
git init
```

```bash
echo "# E-Commerce Platform" > README.md
echo "## Features" >> README.md
echo "- Shopping cart" >> README.md
echo "- Payment processing" >> README.md
git add README.md
git commit -m "docs: initial project documentation"
```

```bash
echo "const app = require('express')();" > app.js
echo "const PORT = 3000;" >> app.js
git add app.js
git commit -m "feat: setup express server"
```

#### Этап 2: Создание удалённого репозитория

```bash
cd ~/Documents
git init --bare ecommerce-remote.git
cd e-commerce-platform
git remote add origin ~/Documents/ecommerce-remote.git
git push -u origin master
```

#### Этап 3: Разработка фичи "Shopping Cart"

```bash
git checkout -b feature/shopping-cart
echo "class ShoppingCart {" > cart.js
echo "  constructor() {" >> cart.js
echo "    this.items = [];" >> cart.js
echo "  }" >> cart.js
echo "}" >> cart.js
git add cart.js
git commit -m "feat: add shopping cart class"
```

```bash
echo "  addItem(item) {" >> cart.js
echo "    this.items.push(item);" >> cart.js
echo "  }" >> cart.js
git add cart.js
git commit -m "feat: add item to cart functionality"
```

```bash
echo "  removeItem(id) {" >> cart.js
echo "    this.items = this.items.filter(item => item.id !== id);" >> cart.js
echo "  }" >> cart.js
git add cart.js
git commit -m "feat: remove item from cart"
```

```bash
git push -u origin feature/shopping-cart
```

#### Этап 4: СРОЧНЫЙ БАГ в production!

```bash
git checkout master
git checkout -b hotfix/critical-crash
echo "// Bugfix: handle null values" >> app.js
git add app.js
git commit -m "fix: prevent null pointer exception"
```

```bash
git checkout master
git merge hotfix/critical-crash
git push
```

```bash
git branch -d hotfix/critical-crash
```

#### Этап 5: Продолжаем работу над Shopping Cart (нужен rebase)

```bash
git checkout feature/shopping-cart
git rebase master
```

```bash
echo "  getTotal() {" >> cart.js
echo "    return this.items.reduce((sum, item) => sum + item.price, 0);" >> cart.js
echo "  }" >> cart.js
git add cart.js
git commit -m "feat: calculate cart total"
```

#### Этап 6: Второй разработчик работает над Payment

```bash
cd ~/Documents
git clone ecommerce-remote.git ecommerce-developer2
cd ecommerce-developer2
```

```bash
git checkout -b feature/payment
echo "class Payment {" > payment.js
echo "  processPayment(amount) {" >> payment.js
echo "    return true;" >> payment.js
echo "  }" >> payment.js
echo "}" >> payment.js
git add payment.js
git commit -m "feat: add payment processing"
```

```bash
git push -u origin feature/payment
```

#### Этап 7: Первый разработчик хочет взять изменения

```bash
cd ~/Documents/e-commerce-platform
git fetch origin
git branch -a
```

#### Этап 8: Начинаем работу над User Auth, но отвлеклись

```bash
git checkout -b feature/auth
echo "function login(username, password) {" > auth.js
echo "  // TODO: implement" >> auth.js
git add auth.js
```

```bash
echo "function register(username, email, password) {" >> auth.js
echo "  // TODO: implement" >> auth.js
```

**Незакоммиченные изменения!**

#### Этап 9: Нужно срочно проверить feature/payment

```bash
git stash push -u -m "WIP: user authentication"
```

```bash
git checkout feature/payment
git pull origin feature/payment
cat payment.js
```

#### Этап 10: Вернёмся к auth

```bash
git checkout feature/auth
git stash pop
```

```bash
git add auth.js
git commit -m "feat: add auth functions skeleton"
```

#### Этап 11: Мердж Shopping Cart в master

```bash
git checkout feature/shopping-cart
git log --oneline
```

**Хотим объединить последние 3 коммита про cart в один:**
```bash
git rebase -i HEAD~3
```

В редакторе (симулируем):
```bash
git reset --soft HEAD~3
git commit -m "feat: implement shopping cart with add, remove and total"
```

```bash
git checkout master
git merge feature/shopping-cart
git push
```

#### Этап 12: Обновляем feature/payment

```bash
cd ~/Documents/ecommerce-developer2
git checkout feature/payment
git fetch origin
git rebase origin/master
```

#### Этап 13: Добавим тесты для payment

```bash
echo "describe('Payment', () => {" > payment.test.js
echo "  it('should process payment', () => {" >> payment.test.js
echo "    expect(true).toBe(true);" >> payment.test.js
echo "  });" >> payment.test.js
echo "});" >> payment.test.js
git add payment.test.js
git commit -m "test: add payment tests"
```

```bash
git push
```

#### Этап 14: Мердж Payment в master

```bash
git checkout master
git pull
git merge feature/payment -m "feat: merge payment system"
git push
```

#### Этап 15: Первый разработчик обновляется и завершает auth

```bash
cd ~/Documents/e-commerce-platform
git checkout master
git pull
```

```bash
git checkout feature/auth
git rebase master
```

```bash
echo "  return { token: 'abc123' };" >> auth.js
echo "}" >> auth.js
git add auth.js
git commit -m "feat: complete login implementation"
```

```bash
git push -u origin feature/auth
```

#### Этап 16: Создаём конфликт для практики

```bash
git checkout master
echo "const version = '1.0.0';" >> app.js
git add app.js
git commit -m "chore: bump version to 1.0.0"
git push
```

```bash
cd ~/Documents/ecommerce-developer2
git checkout master
git pull
echo "const version = '1.0.1';" >> app.js
git add app.js
git commit -m "chore: bump version to 1.0.1"
```

**Попытка push:**
```bash
git push
```

**Отклонено! Нужен pull:**
```bash
git pull
```

**КОНФЛИКТ!**

```bash
cat app.js
```

**Разрешаем:**
```bash
echo "const app = require('express')();" > app.js
echo "const PORT = 3000;" >> app.js
echo "// Bugfix: handle null values" >> app.js
echo "const version = '1.1.0';" >> app.js
git add app.js
git commit -m "chore: resolve version conflict, set to 1.1.0"
git push
```

#### Этап 17: Финализация

```bash
cd ~/Documents/e-commerce-platform
git checkout master
git pull
```

```bash
git log --oneline --graph --all
```

```bash
git checkout feature/auth
git rebase master
git checkout master
git merge feature/auth
git push
```

```bash
git branch -d feature/auth
git branch -d feature/shopping-cart
git push origin --delete feature/auth
git push origin --delete feature/shopping-cart
```

```bash
cd ~/Documents/ecommerce-developer2
git checkout master
git pull
git branch -d feature/payment
```

#### Этап 18: Просмотр итоговой истории

```bash
cd ~/Documents/e-commerce-platform
git log --oneline --graph --all --decorate
```

---

## Часть 2: Самостоятельная работа

### Задание
Создайте проект "social-network" и пройдите полный цикл разработки с 2 разработчиками.

### Требования

#### Инициализация (Developer 1)
1. Создайте папку `social-network` и инициализируйте Git
2. Создайте файл `network.js` с текстом "const SocialNetwork = {};"
3. Коммит: "Initial social network platform"
4. Создайте bare репозиторий `social-remote.git`
5. Добавьте remote origin и сделайте push

#### Фича: Posts (Developer 1)
6. Создайте ветку `feature/posts`
7. Создайте файл `posts.js` с классом Post
8. Коммит: "Add post class"
9. Добавьте функцию createPost в posts.js
10. Коммит: "Add create post function"
11. Push ветки на remote

#### Hotfix (Developer 1)
12. Переключитесь на master
13. Создайте ветку `hotfix/security`
14. Добавьте в network.js комментарий "// Security patch applied"
15. Коммит: "Security vulnerability fixed"
16. Merge hotfix в master
17. Push master
18. Удалите ветку hotfix

#### Фича: Comments (Developer 2)
19. Клонируйте репозиторий в папку `social-network-dev2`
20. Создайте ветку `feature/comments`
21. Создайте файл `comments.js` с функцией addComment
22. Коммит: "Add comments functionality"
23. Push ветки

#### Продолжение Posts + Stash (Developer 1)
24. Переключитесь на feature/posts
25. Rebase на master (чтобы получить hotfix)
26. Начните добавлять функцию deletePost (не коммитьте)
27. Сохраните в stash "WIP: delete post"
28. Переключитесь на master
29. Pull изменения
30. Вернитесь на feature/posts
31. Восстановите stash
32. Завершите deletePost
33. Коммит: "Add delete post function"

#### Merge и конфликты
34. (Dev 1) На master: измените network.js, добавьте "version: 2.0"
35. Коммит: "Update version to 2.0"
36. Push
37. (Dev 2) На master: измените network.js, добавьте "version: 2.1"
38. Коммит: "Update version to 2.1"
39. Попытайтесь push (будет ошибка)
40. Pull (будет конфликт)
41. Разрешите конфликт: выберите версию 2.2
42. Push

#### Финализация
43. (Dev 1) Pull master
44. Merge feature/posts в master
45. Push
46. (Dev 2) Переключитесь на feature/comments
47. Rebase на master
48. Push с флагом --force-with-lease
49. (Dev 1) Pull и merge feature/comments
50. Оба: удалите локальные и удалённые ветки фич

### Проверьте себя
- `git log --oneline` должен показать около 10+ коммитов
- Должны присутствовать файлы: network.js, posts.js, comments.js
- Обе копии репозитория синхронизированы
- Все feature ветки удалены
- `git status` чистый

---

## Подсказки для продвинутого workflow
- **Commit messages:** используйте префиксы (feat:, fix:, docs:, chore:, test:)
- **Ветки:** используйте префиксы (feature/, hotfix/, bugfix/)
- **Pull перед push:** всегда делайте `git pull` перед `git push`
- **Rebase feature веток:** держите ветки актуальными через `git rebase master`
- **Squash коммитов:** объединяйте мелкие коммиты перед merge
- **Stash:** используйте для быстрого переключения контекста
- **--force-with-lease:** безопаснее чем --force при push после rebase
- **git fetch:** проверяйте обновления без автоматического merge

---

## Полезные команды для команд

```bash
# Посмотреть все ветки (локальные и удалённые)
git branch -a

# Удалить удалённую ветку
git push origin --delete название-ветки

# Обновить список удалённых веток
git fetch --prune

# Посмотреть, кто что менял
git blame файл

# Найти коммит, который сломал функционал
git bisect start

# Красивый лог
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Сохранить алиас
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

---

## Что вы изучили

✓ Полный цикл разработки с Git  
✓ Работу нескольких разработчиков  
✓ Управление feature branches  
✓ Hotfix workflow  
✓ Разрешение конфликтов в командной работе  
✓ Комбинирование merge, rebase, stash  
✓ Синхронизацию через remote  
✓ Очистку веток после завершения  
✓ Best practices для commit messages  
✓ Продвинутые стратегии ветвления  

---

## Поздравляем! 🎉

Вы завершили все 10 практических занятий по Git!

Теперь вы умеете:
- Базовые операции (init, add, commit, log)
- Работу с изменениями (diff, restore)
- Ветвление (branch, checkout, merge)
- Разрешение конфликтов
- Удалённые репозитории (remote, push, pull, clone)
- Временное сохранение (stash)
- Rebase и очистку истории
- Командную разработку

**Следующие шаги:**
1. Примените навыки на реальных проектах
2. Изучите GitHub Flow или Git Flow
3. Настройте Git hooks для автоматизации
4. Изучите GitHub Pull Requests
5. Практикуйтесь ежедневно!

---

**Предыдущая практика:** practice_09_rebase_basics.md  
**Вернуться к началу:** practice_01_basic_workflow.md
