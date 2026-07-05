# Когда commit считается опубликованным:
Коммит считается опубликованным, когда он был отправлен (git push) в удалённый репозиторий (remote) и стал доступен другим разработчикам. После этого коммит может проходить: PR/MR, code review, CI и тесты.

# почему protected branch нельзя исправлять force push:
Force push заставляет remote ссылку перепрыгнуть на другую историю, перезаписывает историю коммитов и можем случайно удалить чужой коммит, что нарушает работу других пользователей, которые опираются на старую историю. По этой причине нельзя исправлять protected branch через force push.

# безопасный flow для revert:
1. Делаем feature branch от основной ветки - git switch main, git pull, git switch -c (branch-name)
2. После того, как мы создали ветку от основной, мы должны сделать revert commit - git revert (message)
3. Make check - проверяем результаты локально
4. Пуш feature branch в удалённый репозиторий - git push -u origin (branch-name)
5. Открываем PR/MR
6. Ожидаем прохождение проверок (CI, тесты, линтеры)
7. Code review
8. После одобрения выполняем merge в основную ветку.

# Когда переписывание истории допустимо только по командному договору:
Мы можем перезаписать историю только при командном договоре, если в договоре указано, что force push одобрен, мы можем делать force push.

# Makefile:
В проекте уже добавлен Makefile, поэтому дополнительное создание не требуется. Проверку изменений выполнил через make check.

Выполнил make check перед добавлением файла в staging: ?? docs/published-history-safe-undo.md, а тесты показали пустое окно (значит ошибок не обнаружено)
Выполнил make check после добавления файла в staging: A  docs/published-history-safe-undo.md, а тесты показали пустое окно (значит ошибок не обнаружено)

После commit сделал финальный make check:
1. git status --short не показывает изменённых или незакоммиченных файлов
2. git diff --check не выводит ошибок форматирования

# local checks:
make check
git status --short

# SSH URL для работы:
Проверяем подключение: ssh -T git@github.com - Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
SSH URL: origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git
