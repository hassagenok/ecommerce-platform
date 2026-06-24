# SSH URL для работы:
git@github.com:hassagenok/ecommerce-platform.git

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

# Authentication error
`Permission denied (publickey)` — SSH authentication failed because no valid SSH key was found or configured for the repository access.
# Configuration error
`wrong URL` — repository remote URL is incorrect or points to a non-existent/unauthorized repository.

# Ошибки подключения.
Обе ошибки относятся к уровню подключения, поэтому изменения branch name или force push не применяются, так как Git ещё не выполняет операции с ветками или историей коммитов.

# Local checks:
make check
git status --short
git remote -v

