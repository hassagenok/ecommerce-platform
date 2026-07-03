# decision matrix:
Solo - один разработчик работает над проектом самостоятельно.
1. Recommended flow - короткоживущие feature-branch
2. Required gates - локальные тесты и резервные копии.
3. Release cadence - по мере готовности.
4. Rollback cost - низкий.
5. Why this is enough - один разработчик не тратит время на координацию, так как он один разработчик.
6. What would be too much - PR/MR, иногда develop, release
7. Residual risk - можно пропустить ошибку из-за того, что отсутствуют вторые взгляды и какие-то доп проверки.

Small Team - небольшая команда, где люди общаются между собой и быстро синхранизируются между собой.
1. Recommend flow - feature branch, PR/MR, review, merge, deploy
2. Required gates - review, CI, green checks
3. Release cadence - ежедневные релизы
4. Rollback cost - средняя
5. Why this is enough - команда маленькая, но уже нуждается в защите от случайных ошибок
6. What would be too much - длительные release
7. Residual risk - зависимость от ключевых разработчиков.

SaaS -это модель предоставления ПО, при которой приложение размещается в облаке
1. Recommended flow - Feature branch → PR → Review → CI → Staging → Production deployment
2. Required gates - review, CI, tests, release monitoring.
3. Release cadence - ежедневно
4. Rollback cost - средний
5. Why this is enough - нужно быстро выпускать новые функции.
6. What would be too much - долгие согласования каждого изменения.
7. Residual risk - некоторые ошибки появляются только у настоящих пользователей.

Enterprise - крупный бизнес
1. Recommended flow - Feature branch → PR → Multiple reviews → CI/CD → Staging → Approval → Production
2. Required gates - несколько review, approval, CI, tests
3. Release cadence - раз в несколько недель или месяцев
4. Rollback cost - высокий
5. Why this is enough - Большое количество команд требует отвественности и координации
6. What would be too much - ручная проверка каждой мелочи
7. Residual risk - Возможны проблемы из-за сложности системы

Regulated - Проекты в регулируемых сферах, где существуют внешние требования к аудиту и соответствию стандартам
1. Recommended flow - Всё делается по строгим правилам и документируется. Feature branch → PR → Multiple reviews → CI/CD → Staging → Approval → Production
2. Required gates - review, CI, audit, traceability, documentation approved.
3. Release cadence - по графику
4. Rollback cost - очень высокая
5. Why this is enough - Ошибки могут привести к серьёзным последствиям, поэтому используется максимальное количество проверок и аудитов.
6. What would be too much - дополнительная бюрократия без реальной пользы, скорее путает, чем помогает.
7. Residual risk - нельзя исключить ошибки полностью

# two flow example:
short feature branch -> PR -> protected main -> deploy/tag
feature/* -> review -> develop -> staging -> release/* -> main -> tag -> production

# decision note:
Максимально простой флоу, по типу feature-branch, PR in main, self-review, tests перед merge.
CI мы ещё не делали, но если будем, то скорее всего делать его минимальным (линтер, базовые тесты).
Релизы по мере готовности, без какого либо фиксированного графика.
Rollback на данной стадии дешёвый, я могу быстро откатывать коммит или исправлять баг напрямую.
Такого процесса на моё мнение достаточно, так как это учебный репозиторий.
Более сложные процессы, такие как - staging, approval gates, сложный CI, review от вторых лиц сейчас будут скорее мешать скорости обучения.
Однако я придерживаюсь базовым вещам, что говорилось в данном курсе, чтобы вырабатывалась привычка.
Если проект будет усложняться в разных аспектах, тогда нужно усиливать процесс. Добавить обязатльный CI, более тчательные тесты, возможно staging и review от другого человека.
Чем сложнее становится flow, тем выше стоимость каждого изменения (больше review, CI, staging, approvals), но при этом ниже риск ошибок в продукции.
В учебном проекте стоимость ошибок низкая, поэтому оптимизация идёт в сторону скорости, а не тчательного контроля.

# Проверка решения:
Перед выбором flow нужно задать такие вопросы:
1. team size?
2. release cadence?
3. CI maturity?
4. QA or external acceptance?
5. rollback cost?
6. support old versions?
7. regulatory or audit needs?
8. deployment environments?
9. ownership for broken lines?

# local checks:
Перед коммитом выполняем проверку:
1. make check (проверка на ошибки)
2. git status --short (убедиться, что нет случайного мусора)
3. git diff --staged (после того как прошли проверки и добавили файл в stage)

После коммита выполняем проверку:
1. git status --short (вызываем повторно, чтобы убедиться, что рабочее дерево пустое)
2. make check (проверка после фиксации состояния)

# SSH URL for work:
ssh -T git@github.com
Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
git@github.com:hassagenok/ecommerce-platform.git

# HTTPS URL:
https://github.com/hassagenok/ecommerce-platform.git

