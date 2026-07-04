# Перед откатом нужно проверить:
git status --short - показывает, какие файлы изменены и staged ли они.
git diff - показывает unstaged изменения.
git diff --staged - показывает то, что уже готовится к commit.
git log --oneline --decorate 5 - показывает последние commits и положение ветки.

Только после данной проверки стоит выбирать какой откат нужен в данный момент.

# Слои:
working tree - локальная рабочая область, в которой все файлы твои сейчас.
безопасной командой undo является git restore, потому что, мы отбрасываем локальные незакомиченные изменения в файле, не трогая другие слои.

staging area - это область подготовки к будущему commit.
git restore --staged - убирает файл и staging area, но оставляет в working tree.

local commit - это область в который ты сделал commit изменения, но ещё не сделан push в remote.
git reset - перезапишет локальную историю.
1. --soft - откат коммита, но изменения остаются в staging
2. --mixed - откат коммита, но изменения будут в working tree (default)
3. --hard - полностью удаляет изменения.

published history - это коммиты, которые уже отправлены в remote и могут быть базой для чужой работы.
git revert - создаётся новый коммит, который отменяет изменения старого коммита.

# Почему я не использую reset --hard:
reset --hard это полное удаление изменения из working, staging и commit, из-за чего легко потерять работу и сложнее понять Git.

# Makefile:
Добавил Makefile с такими targets: help, status, diff, log, check.
1. make help - показывает справку
2. make status - показывает состояние репозитория (какие файлы изменены, какие добавлены в staging, какие новые)
3. make diff - проверяет лишние проблемы, ошибки форматирования, какие файлы изменены, сколько строк добавлено или удалено.
4. make log - показывает последние 5 коммитов.
5. make check - показывает изменения status, проверяет ошибки форматирования.

# make check:
> $ make check
git status --short
M  Makefile
A  docs/restore-reset-revert.md
git diff --check

Мы видим что после make check - Makefile был редактирован и добавлен в staging и появился новый файл который тоже находиться в staging.
А git diff --check показывает пустой вывод, значит что нет проблем с форматированием и diff не обнаружил нарушений.

# local checks:
Перед коммитом выполняем проверку:
1. make check (проверка на ошибки)
2. git status --short (убедиться, что нет случайного мусора)
3. git diff --staged (после того как прошли проверки и добавили файл в stage)

После коммита выполняем проверку:
1. git status --short (вызываем повторно, чтобы убедиться, что рабочее дерево пустое)
2. make check (проверка после фиксации состояния)

# SSH URL for work:
ssh -T git@github.com
Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
git@github.com:hassagenok/ecommerce-platform.git

# HTTPS URL:
https://github.com/hassagenok/ecommerce-platform.git
