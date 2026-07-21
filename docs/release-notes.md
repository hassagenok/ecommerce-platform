# v1.5.0

## Tag:
- v1.5.0

## Summary:
- Release 1.5.0 includes documentation updates

## Included Changes:
- Improved release tracking and version visibility.
- Added documentation required for maintaining project release history.
- Standardized release information format.

## Checks:
- make check
- git status --short
- git diff --staged

## Risks:
- No major risks identified.

## Rollback:
- Revert deployment to tag v1.4.0 if issues are discovered.

## Owner:
- Daniil Kononenko

## SemVer v1.5.0:
- Patch - это маленькое изменение, фикс, которые исправляют проблему, но не добавляют новые возможности и ничего не ломают.
- Minor - добавление новых возможностей, но код продолжает работать как прежде.
- Major - самое крупное изменение. Оно означает, что добавилось или изменилось что-то настолько сильно, что старые пользователели могут перестать работать без изменений в коде.

Этот релиз относится к категории minor release, потому что он добавляет новые возможности, не нарушая существующее поведение системы.

В данном релизе добавлена структурированная документация для changelog и release notes, что улучшает управление релизами и делает изменения проекта более прозрачными.

# release notes before production decision:
- Release notes должны быть подготовлены до принятия решения о выпуске в production. Они помогают команде оценить изменения, понять возможные риски и принять обоснованное решение о релизе.

- Release notes не должны создаваться после инцидента. Их цель — заранее предоставить необходимую информацию о релизе, а не описывать проблемы, которые уже произошли.

# local checks:
- make check
- git status --short
