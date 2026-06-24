# SSH URL для работы:
git@github.com:hassagenok/ecommerce-platform.git
# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git

# Один репозиторий, но разный формат URL:
Для работы мы используем SSH URL, так как он удобен для authenticated Git operations (fetch, pull, push) и используется для работы с репозиторием и внесением изменений. Главное, что он безопасный, ведь при подключении по SSH Git сервер проверяет, что пользователь владеет private key, не передавая сам ключ по сети.

Для проверки мы отправляем HTTPS URL, в контексте Tyfoon — он используется как read-only reference. HTTPS удобен для Tyfoon и браузера и для просмотра и ревью кода без необходимости предоставлять доступ на запись.

# private SSH key:
Важно, не вставлять в документы, чаты, issue, PR, review, Tyfoon свой приватный SSH key, потому что любой, у кого есть этот ключ, сможет выдавать себя за владельца ключа и получать доступ к ресурсам, где этот ключ используется для аутентификации.

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

# короткий error report Permission denied (publickey):
`Permission denied (publickey)` — SSH authentication failed because no valid SSH key was found or configured for the repository access.

# wrong URL, permission denied:
При wrong URL или Permission denied (publickey) сначала нужно проверить remote URL и SSH-доступ. Так как это ошибки с подключением, нет смысла менять branch name или делать force push. Git даже не дошёл до операций с ветками или коммитами — проблема на уровне подключения

# Local checks:
make check
git status --short
git remote -v

