# allowed types, explanation, good and bad examples:

Conventional Commits используют фиксированный набор типов, которые помогают разработчикам, ревьюерам, CI и инструментам автоматизации быстро понять назначение коммита. Есть базовые allowed types: feat, fix, docs, refactor, test, chore. Но в некоторых командах добалвяют свои allowed types. В данной заметке для урока мы будем рассматривать имеенно базовые:

1. feat - новая функциональность (feature). Используется, когда вы добавляете новое поведение, которого раньше не было. Examles:
Good: feat: add user registration
Bad: feat: update

2. fix - исправление ошибки. Используется, когда исправляется неисправности в существующих функционалах. Examples:
Good: fix: correct payment rounding error
Bad: fix: payment

3. docs - документация. Используется, когда изменяется документация. Examples:
Good: docs(note): add allowed types explanation with examples
Bad: docs: fix note

4. refactor - изменения в структуре кода, без изменения поведения самого кода. Используется, когда вы улучшили код, но фукнционал остался таким же. Examples:
Good: refactor(cart): extract price calculation service
Bad: refactor: fix payment method

5. test - изменение тестов. Используется, когда добавляются новые тесты или изменяются текущие. Examples:
Good: test: update tests for make check command
Bad: test: tests

6. chore - техническое обслуживание. Используется для изменений, которые не меняют бизнес-логику приложения. Examples:
Good: chore(repo): ignore local coverage output
Bad: chore: important bug

# allowed scopes:

В Conventional Commits scope — это необязательная часть сообщения, которая показывает область кода или функциональность, которую затрагивает коммит.
* catalog - данный scope предназначен для Каталога товаров: товары, категории, поиск, фильтры, цены.
* cart - данный scope предназначен для корзины: добавление товаров, удаление товаров, количество товара, расчёт суммы товара.
* checkout - данный scope предназначен для процесса оформления заказа: адрес, доставка, подтверждения заказа.
* orders - заказы: создание, изменения статуса, история.
* payment - оплата: транзакции, методы, возвраты, интеграции.
* auth - аунтефикация: регистрация, логин, права доступа.
* api - общий api слой: endpoints, документация API
* repo - работа с репозиторием: структура, хуки, шаблоны, настройка.
* release - подготовка релиза: версия, логи изменений, скрипт релиза.

# Breaking changes explanation and examples:

Breaking changes - это ломающие или критические изменения: обновление в коде, добавление или удаление библиотеке, изменение названия файла, которые нарушают обратную совместимость.
Данные изменения мы обозначаем двумя способами:

1. Флаг (!) после type(scope). Example:
feat(api)!: rename user_name field to username

2. BREAKING CHANGE в footer. Example:
BREAKING CHANGE: user_name field was removed and replaced with username

# Breaking change and SemVer, Release note, Review:
Breaking change означает, что старые клиенты могут перестать работать → увеличиваем MAJOR версию.
Breaking changes должны быть явно указаны в описании релиза, чтобы пользователи знали, что нужно изменить.
Reviewer проверяет type, scope, breaking marker.

Review checlist:
1. Правильный ли Type?
2. Соотвествует ли scope изменённой области?
3. Есть ли breaking change? Если есть, добавлен ли ! или BREAKING CHANGE?
4. Понятно ли, что нужно изменить пользователю?

# Local checks:
make check
git status --short

Провёл проверку make check до staging area:
git diff --check показал пустое состояние (значит никаких проблем с файлом не обнаружено)
git status short показал новый файл: ?? docs/types-scopes-breaking.md

Провёл проверку make check после staging area:
git diff --check показал пустое состояние (значит никаких проблем с файлом не обнаружено)
git status short показал подготовленные к коммиту файлы: A  docs/types-scopes-breaking.md

Провёл проверку make check после commit:
git diff --check и git status short пустые, значит нет никаких файлов в work tree.
