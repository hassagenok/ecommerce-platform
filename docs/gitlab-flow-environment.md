# Terms:

- Branch - это git ref на определённый коммит в истории. Ветка (branch) показывает отдельную линию разработки и перемещается вперёд при добавлении новых commit.
- Pipeline - это автоматический процесс, который запускается для конкретного commit и выполняет такие действия с кодом: build, tests, проверки качества, create artifact.
- Artifact - это результат работы pipeline, готовый объект, который можно сохранить и развернуть в environment.
- Environment - это место, где запущен конкретный artifact или commit.

# flow-scheme:
**feature/* -> MR -> pipeline/review app -> main -> staging -> approval -> production**

# Environment table:

1. Review/dev:
* Environment: review/dev
* Source: Artifact created from feature branch pipeline
* Owner: release owner
* Checks: CI, smoke check, acceptance notes
* Approval: Developer decides if changes are ready for merge
* Rollback note: Redeploy previous working artifact or remove broken review deployment

2. Staging:
* Environment: staging
* Source: artifact from main pipeline
* Owner: release owner
* Checks: CI, smoke check, acceptance notes
* Approval: Manual approval before production deployment
* Rollback note: Redeploy previous stable artifact from staging/production

3. Production:
* Environment: Production
* Source: artifact that passed staging verification
* Owner: release owner
* Checks: deploy checks, monitoring.
* Approval: Manual approval before release
* Rollback note: Roll back to previous production artifact

# Deployment gate:
Deployment gate - это набор проверок, которые должны быть выполнены перед тем, как версия приложения попадёт в следующее окружение.
Не каждый commit автоматически должен попадать дальше. Перед продвижением версии нужно убедиться, что она стабильна.

# Environment branch variant:
Environment branch variant - предполагает использование staging и production branches. Иногда отдельные ветки по типу этих нужны, например:
* если нужно долго поддерживать разные версии приложения.
* если production нуждается в отдельном контроле изменений и качества.
* если релизы выходят редко.

- drift rist данных веток:
После добавления environment branch могут возникнуть вопросы:
* Какая ветка содержит актуальные изменения?
* Почему staging отличается от production
* Какие тесты были запущены для конкретного коммит и были ли они запущены вовсе?
* Не попала ли в production старая версия изменения?

- Исходя из данных рисков, environment branch требует дополнительного контроля:
* постоянная синхронизация веток
* фиксация deployed commit SHA
* понятного процесса merge между environments.

Ветки окружения могут быть полезны, но они увеличивают сложность и риски, если ввести их без дополнительного контроля.

# Troubleshooting:

1. Окружение (environment) запущено не из того artifact.
* Pipeline создал новый artifact, но окружение использует старое.
- Команда может думать, что тестирует новую версию, но на самом деле проверяет старую.
- Решение: связывать deployment с конкретным artifact and commit SHA.

2. Branch показывает одно, а Environment содержит другое
* Ветка говорит одно, а реально запущено другое.
- Нельзя точно определить, какая версия работает у пользователей.
- Решение: Хранить информацию о деплой коммитах или артифактах для каждого окружения.

3. Изменения попали в production без нужных проверок
- Нет гарантий, что версия была протестирована.
- Решение: Исользовать deployment gates: main - staging checks - approval - production

# local checks:
make check
git status --short
git diff --check

