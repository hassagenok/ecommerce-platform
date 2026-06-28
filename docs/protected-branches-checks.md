# Protected branch enforceable rule:
Protected branch это не просто устное соглашение внутри команды, а набор технических правил внутри репозитория (enforceable rules), данные правила настраиваются на уровне репозитория и не позволяют нарушить процесс разработки даже случайно.

К примеру, для ветки main обычный набор правил выглядит так:
1. No direct push — запрещены прямые push в main.
2. No force push — запрещён force push, который может переписать историю коммитов.
3. PR/MR required — перед тем, как изменение попадёт в main, оно должно обязательно пройти PR/MR.
4. At least one review — перед слиянием требуется минимум одно одобрение от другого разработчика.
5. Required checks green — все обязательные проверки должны успешно завершиться перед merge.

Схема для понимания работы правил:
feature branch -> PR/MR -> review -> required checks -> protected main

# SSH доступ к repository не означает право direct push в protected branch:
SSH подтверждает личность пользователя и его доступ к репозиторию, но не даёт автоматически вносить правки в любую ветку. Protected branch проверяется на уровне сервера репозитория отдельно для каждой ветки (каждую ветку можно настроить по разному), поэтому даже если у пользователя есть права на просмотр репозитория, у него могут не быть права на direct push / force push в main.

# local make check vs required remote checks:
Локальная проверка (make check) важна, но она не заменяет required remote checks.
Required checks выступают в роли автоматического gate перед merge: пока все обязательные проверки не завершатся успешно, PR/MR невозможно объединить с защищённой веткой (protected branch).

Проверки могут быть такими:
tests, linters, build, static analysis, security scanning, make check.

Локальный запуск этих проверок помогает разработчику обнаружить ошибки раньше, чем произойдёт push, но только удалённые проверки (remote checks) будут гарантировать, что код, попадающий в main, был проверен верно.

# beginner-readable объяснение красного check:
Если пользователель получить красный check, то он должен:
1. открыть log
2. найти failing command
3. воспроизвести локально (если возможно)
4. исправить
5. снова запустить make check
6. push новый commit

# Связь с Module 05:
protected branch и checks готовят corporate flow с integration line, staging и release path.
Эти правила — основа corporate workflow из Module 05, где изменения проходят через PR, проверки и review перед попаданием в integration line, staging и release.

# SSH URL для работы:
Проверяем подключение: ssh -T git@github.com - Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
SSH URL: origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git

# Local checks:
make check
git status --short
git branch -vv
