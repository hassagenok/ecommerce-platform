# feature branch как линия задачи:
feature branch - это отдельная ветка разработки новой задачи без изменений в основной ветки проекта.

# Простое правило naming: prefix, lowercase slug, дефисы вместо пробелов:
В naming convention для feature branch мы пользуемся таким правилом:
prefix - указывает на тип изменений, slug - объясняет суть изменений в lowercase style, разделяем слова дефисами, вместо пробелов, иногда используем issueID
формула: prefix/lowercase-slug-issueID(sometimes)
пример: feature/catalog-filter-142

# Примеры хороших и плохим branch names:
Хорошие:
1. feature/catalog-filter - новые изменения касательно catalog + filter
2. docs/change-makefile-rules - изменения в виде документации в правилах Makefile
3. chore/homework-feature-branches-naming - техническая работа с домашним заданием.
4. docs/feature-branches-naming - документация объясняющая нейминг касательно новыъ веток
5. bugfix/login-error-proj1 - изменения в виде исправки бага связанным с ошибкой логани в Проекте 1
Плохие:
1. test - неизвестны изменения
2. feature/fix1 - есть префикс, но slug ничего не объясняет.
3. README-change - нет префикса, uppercase-slug
4. docs/Fix file - есть префикс, нарушен lowercase-slug, разделяет слова через пробел
5. final-test - нет префикса, неизвестны изменения.

# Схема:
feature branch -> review -> protected main

# Важжное уточнение на счёт feature branch:
Мы не делаем push напрямую в main, так как это не отвечает определению feature branch. Сначала мы создаем новую ветку - делаем в ней нужные нам изменения - делаем коммит и пуш ветки - после идёт review - pull request - marge feature branch с основным состоянием.

# Локальные проверки перед commit:
make status
make diff
git diff --staged
make check

# Локальная проверка после commit:
git status --short


