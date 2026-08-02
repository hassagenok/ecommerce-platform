# anti-patterns:

1. Anti-pattern: direct commits to protected line
* Symptom: прямой пуш в main или release.
* Broken contract: protected lines должны изменяться только через процесс проверки (local checks, PR/MR, review, CI)
* Risk: баги попадают в важные линии разработки без проверки состояния. Есть шанс возникновение поломки или конфликтов.
* Root cause: В проекте нет правил защиты веток или команда их обходит.
* Corrective action: Включить и соблюдать branch protection (PR, review, CI)
* Owner: Repository owner
* Verification signals: Нет прямых пушей в защищенные ветки и изменения перед влитием проходят обязательные проверки.

2. Anti-pattern: long-lived feature branches
* Symptom: feature branches живут неделями или больше недели.
* Broken contract: Изменения должны интегрироваться часто, для уменьшение конфликтов. (Маленькое изменение проверяется быстрее через review, быстрее проходит тесты и быстрее может быть интегрировано в production)
* Risk: Большие конфликты при merge, сложный и долгий review, долгое прохождение тестов. (Неудачных merge)
* Root cause: Большие задачи, медленный review.
* Corrective action: Разбить работу на маленькие PR, использовать features flags, чаще синхронизировать изменения с main.
* Owner: Developer / Team.
* Verification signals: новые ветки живут меньше недели, все изменения проходят PR и тесты быстрые.

3. Anti-pattern: Broken CI ignored.
* Symptom: CI падает, но команда делает merge или bypass.
* Broken contract: CI должен быть надёжным сигналом качества.
* Risk: Команда перестаёт доверять CI, ошибки теряются среди ложный ошибок.
* Root cause: нет отвественного человека за CI, flaky tests не исправляются.
* Corrective action: назначит отвественного человека за CI, исправление нестабильных тестов и трекать причины падения.
* Owner: CI owner / Platform team
* Verification signals: команда доверяет CI, снижается количество flaky failures.

4. Anti-pattern: Release branch is second develop
* Symptom: Ветка release используется как второй develop (продолжают вливать изменения в ветку release)
* Broken contract: нет стабилизации изменений перед релизом (проверить и подготовить изменения)
* Risk: Релизы становятся нестабильными, невозможно определить состояние версии.
* Root cause: нет владельца релиза, команда не понимает назначение release branch.
* Corrective action: Определить правила и отвественного человека за release branch.
* Owner: release owner
* Verification signals: В release branch попадают только одобренные изменения.

5. Anti-pattern: Hotfix not backported.
* Symptom: Изменение было сделано для production, но при этом отсутствует в других поддерживаемых ветках.
* Broken contract: исправление должны вливаться во все поддерживаемые ветки, где проблема может появиться снова.
* Risk: Ошибка возвращается в следующем релизе.
* Root cause: Нет checklist для hotfix и нет процесса backport.
* Corrective action: Добавить hotfix workflow и проверять, попали ли изменения во все нужные ветки, где нужен данный фикс.
* Owner: Release owner
* Verification signals: Каждый hotfix имеет связанный backport или документированное исключение.

6. Anti-pattern: Environment branch confusion
* Symptom: Команда не понимает, какая ветка соответствует staging, production или другим окружениям.
* Broken contract: Каждое окружение должно иметь понятный источник изменений.
* Risk: сложно определеить текущую версию приложения.
* Root cause: нет документации, которая помогает при deploy (deployment flow) и как работать с environment branches.
* Corrective action: ввести документацию между ветками окружения, сохранять SHA каждого deployment.
* Owner: DevOps / Platform owner
* Verification signals: Можно определить, какой commit работает в каждом окружении.

7. Anti-pattern: No rollback plan
* Symptom: Команда не знает как быстро вернуть предыдущую стабильную версию.
* Broken contract: Каждое изменения в production должно иметь безопасный способ восстановления.
* Risk: исправления происходят вручную в аварийной ситуации.
* Root cause: Команда думает исключительно об идеально deployment игнорируя rollback plan.
* Corrective action: Создать rollback plan и регулярно проверять его.
* Owner: Release owner
* Verification signals: Rollback быстрый и безопасный и по происходит по понятной инструкции.

8. Anti-pattern: Branch naming without rules
* Symptom: ветки создаются с непонятными названиями, которые понятны разработчику и недолгое время.
* Broken contract: Название ветки должно помогать понимать её назначение и поддерживать порядок в репозитории.
* Risk: Сложнее искать изменения, автоматизировать процессы и поддерживать workflow.
* Root cause: Нет соглашения о naming convention.
* Corrective action: Ввести правила именования
* Owner: team lead
* Verification signals: Новые ветки соответствуют установленным правилам.

# phased remediation plan:
Days 1-7:
- document current flow
- list protected lines and real bypasses
- add make check to PR checklist
- require CI on main if checks are stable enough

Days 8-20:
- protect release/*
- define release owner and allowed changes
- add hotfix backport checklist
- record deployed SHA for staging and production

Days 21-30:
- measure branch lifetime
- split the largest active PRs
- remove unused branch prefixes
- update onboarding docs and repository settings

# What not to do:
* Не стоит резко вводить новые ограничения без готовности команды и инструментов. Например, нельзя запрещать long-lived branches без feature flags и стабильного CI, делать обязательные approvals без reviewers или включать required CI checks с нестабильными тестами. Сначала нужно подготовить процесс, затем добавлять правила.

# How to verify improvement:
* Улучшение видно по следующим signals: уменьшается время жизни веток, PR становятся меньше, снижается количество конфликтов и обходов процесса, CI становится стабильнее, а deployments и hotfixes становятся более контролируемыми. Главный показатель — workflow снижает риски и помогает команде работать эффективнее.

# local checks:
make check
git status --short
git diff --check
