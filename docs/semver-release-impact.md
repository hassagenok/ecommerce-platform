# patch, minor, major explanation:
На bumb version влияет рад изменений и все они влияют по разному. У нас есть 3 главных изменения версии: patch, minor, major, подробнее распишем их:

Patch - это маленькое изменение, фикс, которые исправляют проблему, но не добавляют новые возможности и ничего не ломают.
Example: fix(payment): round order total before capture
version: 1.4.2 - 1.4.3

Minor - добавление новых возможностей, но код продолжает работать как прежде.
Example: feat(catalog): add filtering by brand
version: 1.4.2 - 1.5.0

Major - самое крупное изменение. Оно означает, что добавилось или изменилось что-то настолько сильно, что старые пользователели могут перестать работать без изменений в коде.
Example: feat(api)!: replace checkout response items field
version: 1.4.2 - 2.0.0

# таблица с примерами:

Commit message: fix(payment): fix rounding bug. Type/scope: fix/payment. User impact: исправлена ошибка. Version impact: patch.
Commit message: feat(catalog): add brand filter. Type/scope: feat/catalog. User impact: Новая возможность без поломки. Version Impact: Minor.
Commit message: feat(api)!: rename items field. Type/scope: feat/api + breaking changes. User impact: Ломает старое поведение API. Version impact: Major.
Commit message: docs(api): update API docs. Type/scope: docs/api. User impact: изменение в документации. Version impact: без изменений.
Commit message: chore(repository): add PR template. Type/scope: chore/repo. User impact: Улучшение процесса работы команды. Version impact: без изменений.

# Самый сильный signal wins:

Представим картину, в новом релизе есть серия коммитов разных типов (fix, chore, feat, breaking changes), опираясь на эти типы, мы выбираем как правильно сделать version impact (version bumb), определяем мы благодаря самому сильному сигналу, а не по количеству коммитов или по последнему коммиту.

Пример: мы подготавливаем релиз, у нас есть задача определить какой version bumb предстоит сделать, для этого:
1. смотрим логи: git log --oneline v1.4.0..HEAD
2. Видим возможный результат:
a31c9d2 feat(catalog): add brand filters
b18a7e1 fix(cart): keep quantity after refresh
8f04ac0 docs(release): add rollback checklist
3. В текущем примере, самый сильный сигнал будет - feat, так как добавился новый функционал, это изменение уровня minor. Version bumb: 1.4.2 - 1.5.0
4. Если бы среди commits был feat(api)!: replace checkout response, то следующим релиз должен был бы быть v2.0.0, так как изменение уровня major и ломает работу старых клиентов API.

fix - patch - (1.4.2 - 1.4.3)
feat - minor - (1.4.2 - 1.5.0)
feat(api)! - (1.4.2 - 2.0.0)
chore/docs/test/refactor - (no version bumb)

# connection to Module 05:
После определения version impact команда принимает решение, какую версию выпускать, процесс обычно выглядит так:
* Собираем коммиты, которые вошли в релиз
* Определяем самый сильный сигнал
* Создаём новую версию
* Создаём гит тег, чтобы отметить конкретное состояние кода.

* Пример: текущая версия 1.4.2
* В релиз вошли: feat(catalog): add brand filters и feat(api)!: replace checkout response
* Самый сильный сигнал: feat(api)!: replace checkout response
* Новая версия: v2.0.0
* Создаём тег: git tag 2.0.0, git push origin v2.0.0

# connection to Module 06:
Иногда после релиза находят критическую ошибку. Тогда не ждут следующего большого релиза, а делают hotfix.

* Пример: текущая версия 1.4.2
* Нашли ошибку: fix(cart): keep quantity after refresh
* Новая версия: 1.4.3, так как, это исправление не добавляет новую функцию и не ломает API.
* patch note: git tag v1.4.3, git push origin v.1.4.3

Если же ошибка была исправлена в новой ветке разработки:
* Пример: от main у нас есть новый релиз v2.0.0, а production все ещё на версии 1.5.0
* Исправление переносим обратно в старую стабильную ветку (backport)
* Видим, то что в main есть нужное нам исправление: fix(cart): keep quantity after refresh
* Берём этот коммит: git cherry-pick (commit-hash)
* Переносим в ветку и меняем версию: 1.5.0 - 1.5.1

# local checks:
make check
git status --short


