# полный github flow:
* create new feature branch from the current stable “protected main” branch.
* делаем commit изменения в текущей feature.
* проходим local checks перед тем, как сделать push в remote.
* после прохождения всех локальных проверок, делаем push в remote.
* создаём pull request, где описываем суть изменения.
* review + status checks (CI).
* после прохождения всех проверок - делаем merge to protected main.
* deploy or release decision- финальная стадия.
* rollback plan - на случай проблем.

# branch naming rule:
Branch naming rule - это соглашение об именовании веток, которое кодирует смысл изменения прямо в названии, для того, чтобы reviewer и другие члены команды понимали суть изменения из данной ветки.

branch naming rule указывает:
* какой тип изменения (type)
* какой scope (область) затрагивается
* короткое описание

type/scope/short-description - feature/github-flow

# PR checklist:
- Branch is short-lived and based on current main
- PR description clearly states scope of the change
- Tests are added/updated for the change
- make check / local checks pass locally
- CI is green
- Reviewer understands scope and risk
- No direct push to main (branch protection enforced)
- Breaking changes are explicitly called out (if any)
- Rollback or revert path is written
- Release impact is clear

# required checks:
- passes local make check
- git diff --check passes (no whitespace error, no merge conflicts)
- CI is green
- Review approval
- Protected main rule enforced

# Release and rollback:
Команда узнаёт, что сейчас в проде, по release tag + deployed commit SHA (плюс это должно быть где-то видно всем — Slack/дашборд//version endpoint, иначе "знание" есть только у того, кто деплоил).
При плохом деплое команда откатывается по заранее написанному в PR rollback plan: либо revert (новый коммит в main, отменяющий изменение), либо rollback (передеплой предыдущего release tag).

# Not enough when:
GitHub Flow хорошо работает для continuous deployment одного продукта с одной живой версией; там, где нужны несколько версий, строгий release-процесс или долгие фичи — обычно берут Git Flow или его вариации.

# local checks:
make check
git status --short
git diff --check
