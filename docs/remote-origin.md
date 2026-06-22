# difference between local and remote repository:
Локальный репозиторий - это репозиторий который находиться на вашем комьютере, он хранит файлы проекта и историю ваших изменений. Вы можете подтягивать файлы из удалённого репозитория и так же отправлять файлы на удалённый репозиторий. Без git push закоммиченные изменения остаются только в локальном репозитории.

Удалённый репозиторий remote (например, origin) - хранит историю коммитов и состояние проекта, нужен для работы в команде, review, CI. Незакомиченные и untracked файлы не попадают в remote, перед публикацией обязательно стоит проверить локальное состояние и URL remote

# origin:
origin является именем удалённого репозитория remote, это не ветка и не команда. Данное имя даётся по умолчанию при клонировании репозитория, его можно поменять.

# git remote -v example:
origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)
origin	git@github.com:hassagenok/ecommerce-platform.git (push)

# scheme:
local repository -> origin -> remote repository

# перед git push:
Перед git push проверяем состояние проекта:
make check
git status --short
git remote -v

# SSH work URL:
git@github.com:hassagenok/ecommerce-platform.git
# HTTPS review URL:
https://github.com/hassagenok/ecommerce-platform.git

# git remote add:
Данная команда добавляет связь между локальным и удалённым репозиторием, она не делает commit, не создаёт новых репозиториев и не отправляет код. Для отправки кода потребуется дополнительная команда: git push.
