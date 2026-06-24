# SSH URL для работы:
origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git

# Один репозиторий, но разный формат URL:
SSH используется как способ аутентификации и безопасного выполнения Git-операций (fetch, pull, push).
HTTPS используется для доступа к репозиторию в режиме просмотра и ревью (Tyfoon/browser). Также может использоваться Git-клиентом, но чаще применяется без SSH-ключей, через токены или публичный доступ.

# private SSH key:
Важно: приватный SSH key нельзя передавать в документы, чаты, issue, PR или review, так как он даёт полный доступ к аккаунту и всем связанным репозиториям.

# check example:
git remote -v
ssh -T git@github.com

# Вывод проверки:
[18:25:26]
> $ git remote -v                                                                                                                              [±homework-v3-04-03-ssh-remote-https-review ●]
origin  git@github.com:hassagenok/ecommerce-platform.git (fetch)
origin  git@github.com:hassagenok/ecommerce-platform.git (push)

[18:25:33]
> $ ssh -T git@github.com                                                                                                                      [±homework-v3-04-03-ssh-remote-https-review ●]
Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.

# Пример ошибки Permission denied (publickey):
`Permission denied (publickey)` — SSH authentication failed because no valid SSH key was found or configured for the repository access.

# Диагностика ошибок:
Если ошибка `Permission denied (publickey)`:
1. Проверяем SSH ключ
2. Есть ли ключ локально (ls -al ~/.ssh)
3. Добавлен ли ключ к GitHub
4. Загружен ли ключ в ssh-agent (ssh-add -l)

Если remote неправильный:
1. Проверяем git remote -v
2. SSH/HTTPS формат
3. Существует ли репозиторий

Если URL верный, но доступа нет:
1. Проверяем доступ
2. Проверяем права

Эти ошибки не связаны с ветками или историей коммитов, поэтому branch rename и force push не применяются.

# Local checks:
make check
git status --short
git remote -v

