# develop in big team:
Команда может работать одновременно над параллельными задачами, параллельная разработка приводит к частым конфликтам при интеграции, для этого и нужна integration line (develop). В данную ветку попадают изменения из feature branches которые прошли review, checks, но все ещё не готовы к production. Это мост между будущими ветками и main.

# scheme:
feature/catalog-filter
> pull request
> review
> CI
> develop
> integration checks

# merge in develop is not production readiness:
merge в develop означает что изменения прошли нужные проверки, изменения интегрированы с другими изменениями в общей ветке develop, но это ещё не готовый релиз, а промежуточный этап, на котором можно заметить недочёты. Перед тем как изменения становятся production ready проходятся более широкие проверки: QA, integration, staging, bugfix после интеграции с будущими изменениями, только после этого производится merge в main.

# develop rules:
1. Owners - за ветку develop отвечают назначанные владельцы, только они принимают критические изменения и релизы в ветку.
2. Required checks - все изменения проходят ряд проверок (CI, review)
3. Запрет direct push - запрещает делать push прямо в develop.
4. Запрет незавершённой работы - в develop не попадают незавершенные изменения, временные фиксы и так далее. Только готовые изменения.
5. Короткоживущие feature branches - данные ветки не должны долго жить после слияния в develop, так как это наводит шум в историю.

# Цена develop:
Чтобы данная ветка не стала свалкой и выполняла свой функционал, для начала нужно отделить её от обычных feature branch не просто названием, а протоколом правил (owners, checks, запрет на direct push, запрет на незавершённые изменения, короткоживущие feature branches). develop это контролируемая интеграционная среда, которая должна оставаться стабильной.

# Когда develop может быть лишним:
В маленькой команде быстрый review, разработчики могут выпускать по одному небольшому проекту в неделю, поэтому смысла в данной линии отсутсвует. Отличия с main:
1. main является единственной защищённой веткой.
2. все изменения попадают через PR/MR напрямую в main.
3. каждая задача — маленькая и быстро проходит review
4. частые и стабильные изменения

# Local checks:
make check
git status --short

# SSH URL for work:
ssh -T git@github.com
Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
git@github.com:hassagenok/ecommerce-platform.git

# HTTPS URL:
https://github.com/hassagenok/ecommerce-platform.git
