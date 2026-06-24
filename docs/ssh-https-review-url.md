# SSH URL для работы:
Проверяем подключение: ssh -T git@github.com - Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
SSH URL: origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

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

repository not found чаще говорит про wrong URL или права на конкретный repository.
Проводим диагностику:
1. Проверяем URL репозитория: git remote -v
2. Проверяем, существует ли репозиторий: https://github.com/<user>/<repo> (Если выдаёт ошибку - репозиторий не существует, либо нет доступа)
3. Проверяем доступ SSH: ssh -T git@github.com (Если все хорошо, будет вывод: Hi username! You've successfully authenticated). Если нет, то ключ не добавлен или не тот аккаунт. Тут же можно и узнать под каким аккаунтом вы работаете на данный момент.

remote: Permission to owner/repo denied означает, что GitHub узнал account, но не разрешил запись в этот repository.
Проводим диагностику: 
1. Проверяем аккаунт: ssh -T git@github.com (Hi, username!)
2. Проверяем доступ к репозиторию на странице репозитория: https://github.com/owner/repo (смотрим список collaborators, есть ли права на редактирование)

protected branch hook declined или похожий текст означает, что SSH доступ есть, но branch policy запрещает прямое обновление ref.
Проводим диагностику:
1. Проверяем в какую ветку мы пушим (git branch, git status, git push origin main)
2. Проверяем branch protection rules: GitHub → repo → Settings → Branches (Тут смотрим protected branches)

Эти ошибки не связаны с ветками или историей коммитов, поэтому branch rename и force push не применяются. Неправильная реакция на SSH ошибку: менять branch name, делать force push, удалять origin, вставлять private key в комментарий или переходить на случайный HTTPS URL без понимания token/auth. Правильная реакция: проверить git remote -v, проверить ssh -T git@github.com, убедиться, что public key добавлен в правильный account, и отделить проблему аутентификации от проблемы permissions и protected branch.

# Local checks:
make check
git status --short
git remote -v

