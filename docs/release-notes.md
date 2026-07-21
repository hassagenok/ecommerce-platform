# v1.5.0

## Tag:
- v1.5.0

## Summary:
- Release 1.5.0 includes documentation updates

## Included Changes:
- Added CHANGELOG.md with version history.
- Added release notes documentation.

## Checks:
- make check
- git status --short
- git diff --staged

## Risks:
- No major risks identified.

## Rollback:
- Revert to the previous version.

## SemVer v1.5.0:
- Patch - это маленькое изменение, фикс, которые исправляют проблему, но не добавляют новые возможности и ничего не ломают.
- Minor - добавление новых возможностей, но код продолжает работать как прежде.
- Major - самое крупное изменение. Оно означает, что добавилось или изменилось что-то настолько сильно, что старые пользователели могут перестать работать без изменений в коде.

Данный релиз относится к категории patch release.

В SemVer версия PATCH используется для небольших изменений, исправлений и обновлений, которые не добавляют новую функциональность, не изменяют существующее поведение и не нарушают обратную совместимость.

# release notes before production decision:
- Release notes должны быть подготовлены до принятия решения о выпуске в production. Они помогают команде оценить изменения, понять возможные риски и принять обоснованное решение о релизе.

- Release notes не должны создаваться после инцидента. Их цель — заранее предоставить необходимую информацию о релизе, а не описывать проблемы, которые уже произошли.

# local checks:
- make check
- git status --short
