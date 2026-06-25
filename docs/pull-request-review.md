# Pull Request:
Pull Request состоит из таких частей, как: Source Branch, Target Branch, diff, commits, comments, checks, merge decisions. Подробнее опишем их:
1. Source Branch - ветка, в которой находятся изменения. Из неё беруться новые коммиты
2. Target Branch - ветка, в которую предлагается влить изменения (main)
3. Diff - Сравнение изменений между двумя ветками Source Branch and Target Branch.
4. Commits - Набор коммитов, которые есть в Source Branch, но отсутствуют в Target Branch. RP не хранит их, а ссылается через git refs.
5. Comments - обсуждение внутри PR
6. Checks - Автоматические проверки чтобы проверить, что код проходит требования проекта.
7. Merge decisions - Текущее состояние проекта. Показывает можно ли выполнить merge, есть ли конфликты или был ли проект уже смерджен или закрыт.

# PR description:
1. Context: Зачем это изменение существует?
2. Changes: Какие файлы затронуты?
3. Local checks: Как проверить результат?
4. Risks: Какие риски или ограничения есть?

# Review protection:
Review является защитой общей ветки, так как review проверяет, что изменения соотвествуют поставленной задаче, не с одержит несвязанных изменений или конфликтов, проходит необходимые проверки, не вводят рисков для текущих и будущих веток и что изменения понятны для других разработчиков.

Коротко: review защищает основную ветку от некачественных изменений, проверяя корректность, читабельность и риски кода.

# Плохой PR:
1. Отсутствует discription - нет описания, неизвестно зачем были сделаны изменения и какую проблему это решило.
2. Смешанные задачи - в одном PR находятся несколько несвязанных изменений.
3. Отсутствие локальных проверок - нет подтверждения, что автор сделал локальные проверки проекта
4. Непонятный заголовок (title) - заголовок не отображает суть изменений.
5. force push после комментария без объяснения - изменения без контекста усложняют review.

# Что проверить перед отправкой:
make check
git status --short
git branch -vv

# Что показали локальные проверки:
git status --short
A  docs/pull-request-review.md

make check - пустой

git branch -vv указывает на: * homework-v3-04-04-pull-request-review      f426688 Merge pull request #13 from hassagenok/homework-v3-04-03-ssh-remote-https-review

# SSH URL для работы:
Проверяем подключение: ssh -T git@github.com - Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
SSH URL: origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git

Рабочая публикация ветки идет через SSH remote, а в Tyfoon отправляется HTTPS repository URL.
