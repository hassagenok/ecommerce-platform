# assumptions:
- **team size**: один человек (учебный проект)
- **Checks maturity**: main protected, изменения попадают через PR с обязательными проверками CI и code review.
- **Release frequency**: релизы создаются по мере завершения задач и помечаются именованными тегами.
- **Rollback**: rollback низкостоимостный — при необходимости используется откат к предыдущему релизному тегу.
- **Support model**: поддерживается только актуальная версия продукта.

# Branch roles:

## main:
**Role** - main stable project branch.
**Owner** - project developer
**Allowed source** - feature/, release/, hotfix/, develop/
**Required checks** - make check, CI, review approval
**Merge rules** - изменения попадают в ветку через merge, после того, как изменения пройдут соотвествующие проверки. Прямой пуш в main - запрещён.
**Release meaning** - состояние main соотвествует последней стабильной версии и изменения помечаются тегами.

## feature/:
**Role** - ветка для разработчиков для нового функционала или новых изменений.
**Owner** - разработчик, который выполняет задачу.
**Allowed source** - создаётся от актуального состояния main.
**Required checks** - make check, CI, review approval
**Merge rules** - после того, как задача выполнена и прошла все соотвествующие проверки, совершается merge в main.
**Release meaning** - ветка не является релизной и не используется для релиза.

## release/:
**Role** - подготовка конкретного релиза.
**Owner** - project developer.
**Allowed source** - создаётся от main после завершения набора изменений для релиза.
**Required checks** - make check, CI, review approval, проверка готовности к релизу.
**Merge rules** - после завершения релиза изменения возвращаются в main.
**Release meaning** - ветка представляет подготовку определённой версии, которая после завершения получает release tag.

## hotfix/:
**Role** - срочное исправление критической ошибки.
**Owner** - project developer.
**Allowed source** - создаётся от последнего стабильного состояния main.
**Required checks** - make check, CI, review approval
**Merge rules** - после исправления критической ошибки, ветка возвращается в main.
**Release meaning** - hotfix создаёт новую исправленную версию, которая получает новый release tag.

# scheme:
- feature/ - PR + required checks - protected main - release decision - release/ - release tag - deploy

# hotfix rule:
hotfix/*: создаётся от последнего стабильного состояния, принимается владельцем проекта после прохождения required checks, после patch обязательно возвращается в protected main и получает новый release tag при необходимости.

# Rollback assumptions:
Rollback assumptions: released commit определяется по release tag, привязанному к конкретному commit в репозитории. При неудачном deploy команда откатывается на последний стабильный release tag и после исправления создаёт новый hotfix/release tag

# Local checks before review:
- make check — запуск локальных проверок проекта.
- git status --short — проверка изменённых и неотслеживаемых файлов перед commit.
- git diff --check — проверка пробелов и потенциальных ошибок форматирования в diff.

# Forbidden scenarios:
- Direct push to main без review, checks, PR.
Останавливается правилами: protected main, merge rules и required checks.

- hotfix от feature branch и отсутствие возврата в main.
Останавливается правилами: hotfix allowed source, merge hotfix to main.

