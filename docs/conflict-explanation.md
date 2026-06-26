# Пример вывода конфликта:
marker:<<<<<<< HEAD - показывает начало изменений из текущей ветки из которой был вызван git merge.
i am listening piano music
marker:======= - маркер разделяет изменения текущей и изменения входящей ветки.
i am tired of myself
marker:>>>>>>> practice/conflict-incoming - показывает конец изменения и имя ветки которую Git пытается влить.

# show --summary:
commit 02bb1cdf3b7b991434755a770e5fd783d22c59af (HEAD -> homework-03-04-05-conflicts-explanation)
Merge: 7e713fc 7d90b2c
Author: hassagenok <daniil.kononenko@proton.me>
Date:   Fri Jun 26 17:13:41 2026 +0200

    docs: resolve conflicting changes in conflict file

# Почему возник конфликт:
Конфликт возник из-за изменений из двух разных веток в одном файле в одной строке (изменения пересекнулись), в последствии merge возник conflict.
В итоговом смысле я совместил изменения из текущей и входящей ветки в одну строку и получил: i am listening piano music and i am tired of myself.
После чего запустил такие проверки: make check, git status --short, git diff --check, git log --oneline --decorate --graph 8.

# review comment:
Я решил merge conflict вручную путём соеденения изменений обоих сторон в одну строку:
из HEAD (homework-v3-04-05-conflicts-explanation) я взял оригинальный контекст: i am listening piano music
из incoming ветки (practice/conflict-incoming) я взял оригинальный контекст: i am tired of myself
Объединил оба изменения, чтобы сохранить смысл обеих сторон.

# Проверки после решения:
make check
git status --short
git diff --check

# SSH URL для работы:
Проверяем подключение: ssh -T git@github.com - Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
SSH URL: origin	git@github.com:hassagenok/ecommerce-platform.git (fetch)

# HTTPS URL для Tyfoon review:
https://github.com/hassagenok/ecommerce-platform.git


