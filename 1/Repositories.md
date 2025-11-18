# 1. Создание удалённого репозитория 

### Через веб-интерфейс

1. Зайдите на [https://github.com](https://github.com) и войдите в аккаунт.
2. Нажмите ➕ (правый верхний угол) → **New repository**.
3. Заполните:

   * **Repository name** — имя репозитория (например `my-repo`).
   * Описание — опционально.
   * Public / Private — публичный или приватный.
   * Можно поставить галочку **Initialize this repository with a README** (если хотите сразу увидеть файл).
4. Нажмите **Create repository**.

### Через GitHub CLI (`gh`)

(если установлен `gh`)

```bash
gh auth login            # один раз — для авторизации
gh repo create my-repo --public --confirm
```

`gh` может автоматически создать удалённый репозиторий и сразу привязать локальную папку.

# 2. Способы загрузки файлов в удалённый репозиторий

### A) Через веб-интерфейс (для отдельных файлов)

* Откройте репозиторий → **Add file** → **Upload files** → перетащите файлы → Commit.

### B) Через Git (рекомендуется для разработки)

* Для **нового локального проекта**, привязать к удалённому:

```bash
cd /путь/к/проекту
git init
git add .
git commit -m "Initial commit"
git branch -M main           # приведёт ветку к main (если нужно)
git remote add origin git@github.com:USERNAME/REPO.git   # SSH
# или через HTTPS:
# git remote add origin https://github.com/USERNAME/REPO.git
git push -u origin main
```

* Для **клонирования существующего** удалённого репозитория:

```bash
git clone git@github.com:USERNAME/REPO.git   # SSH
# или
git clone https://github.com/USERNAME/REPO.git  # HTTPS
```

### C) Через GitHub Desktop (GUI)

1. Установите GitHub Desktop.
2. File → Clone repository → или Create new repository → Publish repository.
3. Интерфейс проводит за вас коммиты и push.

### D) Через VS Code (GUI/команды)

(подробно в секции VS Code ниже)

# 3. Аутентификация: [SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh) (рекомендую — удобнее и безопаснее)

1. Сгенерировать ключ (ed25519 — современный):

```bash
ssh-keygen -t ed25519 -C "you@example.com"
# по умолчанию ключи будут в ~/.ssh/id_ed25519 и id_ed25519.pub
```

2. Запустить ssh-agent и добавить ключ:

```bash
# macOS / Linux
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Windows (Git Bash)
eval $(ssh-agent -s)
ssh-add /c/Users/You/.ssh/id_ed25519
```

3. Скопировать публичный ключ:

```bash
cat ~/.ssh/id_ed25519.pub
# или откройте файл и скопируйте содержимое
```

4. На GitHub: Settings → SSH and GPG keys → New SSH key → вставьте ключ и сохраните.
5. Проверка:

```bash
ssh -T git@github.com
# ожидается приветствие GitHub (без пароля)
```

6. Используйте URL вида `git@github.com:USERNAME/REPO.git`.


# 4. Интеграция и рабочий процесс с VS Code

### Подготовка

1. Установите VS Code.
2. Убедитесь, что Git установлен и доступен в PATH.
3. (Опционально) Установите расширения:

   * **GitHub Pull Requests and Issues**
   * **GitLens — Git supercharged** (по желанию)

### a) Открытие локальной папки и инициализация

1. Откройте папку проекта: `File → Open Folder`.
2. В боковой панели нажмите значок **Source Control** (или Ctrl+Shift+G).
3. Если репозиторий не инициализирован — появится кнопка **Initialize Repository** → нажмите.
4. Дождитесь появления списка изменений — сделайте Staging (плюс рядом с файлом) и Commit.

### b) Publish (опубликовать в GitHub) — быстрый путь

* Если репозиторий локальный и вы не добавляли remote, внизу VS Code часто появляется кнопка **Publish to GitHub**. Нажмите — придется авторизоваться в GitHub и затем VS Code создаст удалённый репозиторий и запушит.
* Альтернативно через Command Palette (Ctrl+Shift+P): `Git: Publish Branch`.

### c) Клонирование репозитория через VS Code

* Command Palette → `Git: Clone` → вставьте SSH/HTTPS URL → выберите папку → откройте склонированный репозиторий.

### d) Работа: изменения → commit → push / pull

* В Source Control: введите сообщение Commit и нажмите ✓ (Commit).
* Для Push/Pull используйте кнопки в статус-баре или `...` меню → Push / Pull.
* Можно также открыть встроенный терминал (`Ctrl+``) и выполнять обычные `git` команды.

### e) Авторизация в VS Code (если нужно)

* Нажмите на иконку аккаунта (левый нижний угол) → Sign in to GitHub. Это позволит использовать GitHub features (PR, issues).

# 5. Основные команды

```bash
# связать локальную папку с новым удалённым (если репозиторий уже создан на GitHub)
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin git@github.com:USERNAME/REPO.git
git push -u origin main

# клонировать
git clone git@github.com:USERNAME/REPO.git

# синхронизация
git pull      # подтянуть изменения
git push      # отправить ваши коммиты

# создать ветку и перейти
git checkout -b feature-x
git push -u origin feature-x
```

# 6. Частые ошибки и как их решать

* `Permission denied (publickey)` — SSH ключ не добавлен на GitHub или ssh-agent не запущен. Проверьте `ssh -T git@github.com`.
* `error: failed to push some refs` (non-fast-forward) — сначала сделайте `git pull --rebase` или `git pull` чтобы слить удалённые изменения, затем `git push`.
* `remote origin already exists` — удалённый уже добавлен; посмотреть `git remote -v`. Удалить: `git remote remove origin` и добавить снова.
