# matrix
1. Solo learning project
* Team size: 1
* Release cadence: Anytime
* CI maturity: Basic. Один разработчик, достаточно простых проверок перед запуском.
* Rollback cost: Low. Ошибки легко исправить, нет большого влияния на пользователей.
* Deploy model: Manual
* Regulatory needs: None
* Support model: Self
* Recommended workflow: Feature branches + PR. Помогает изучить Git и review без лишней сложности.
* Required gates: Basic CI
* Why not heavier: Сложный workflow не нужен одному разработчику.
* When to evolve: Когда в проекте появятся другие разработчики.

2. Small SaaS team
* Team size: 3–8
* Release cadence: Daily / Weekly
* CI maturity: Medium. Нужны автоматические тесты и проверки, чтобы команда могла часто выпускать изменения.
* Rollback cost: Medium. Ошибка может повлиять на пользователей, но её можно быстро исправить.
* Deploy model: Continuous deployment
* Regulatory needs: Low
* Support model: Team on-call
* Recommended workflow: Trunk-Based Development. Подходит для частых деплоев и небольшой команды.
* Required gates: PR review, CI, protected main
* Why not heavier: Git Flow добавит лишнюю сложность.
* When to evolve: Когда появятся сложные релизы или несколько версий продукта.

3. Enterprise release train
* Team size: 20+
* Release cadence: Scheduled
* CI maturity: High. Много разработчиков, поэтому нужны автоматизация, тесты и контроль качества.
* Rollback cost: High. Ошибка в релизе может дорого стоить, поэтому нужны проверки перед выпуском.
* Deploy model: Planned releases
* Regulatory needs: Medium
* Support model: Dedicated support
* Recommended workflow: Git Flow. Позволяет работать с параллельными релизами, hotfix и версиями продукта.
* Required gates: PR review, CI, approvals, protected branches
* Why not heavier: Этого достаточно для управления параллельными релизами.
* When to evolve: При изменении процесса релизов или структуры команд.

4. Regulated product
* Team size: 10+
* Release cadence: Planned
* CI maturity: High. Нужны автоматические проверки и доказательства качества для соответствия требованиям.
* Rollback cost: Very high. Ошибка может иметь серьёзные последствия, поэтому изменения проходят строгий контроль.
* Deploy model: Controlled deployment
* Regulatory needs: High
* Support model: Long-term support
* Recommended workflow: Git Flow + release/hotfix branches. Нужен контроль версий, история изменений и управляемые релизы.
* Required gates: CI, code review, approvals, audit trail
* Why not heavier: Более простой workflow не соответствует требованиям аудита и регуляторов.
* When to evolve: При изменении требований регуляторов или процесса поставки продукта.

# matrix for ecommerce-platform:

Для ecommerce-platform достаточно workflow Feature branches + PR, так как проект ведёт один разработчик и он используется для обучения, а не для реальных релизов. Обязательные gates — PR перед merge и базовые CI checks. Workflow стоит пересмотреть, если появятся другие разработчики, production deployment или необходимость более строгого контроля изменений.

# branch names without names:
Предупреждение: Branch names без определённых правил могут быстро стать непоследовательными и запутанными, особенно при росте проекта. Даже в небольшом проекте лучше заранее определить простое правило именования веток.

# local checks:
make check
git status --short
git diff --check
