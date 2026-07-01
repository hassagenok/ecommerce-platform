# Branch vs Environment:
Git branch - это ref на коммит, в котором хранится определённая версия кода. После того как правки доходят до готовности, после проверок изменения могут быть merged
Environment - это среда, в которой код запускается и работает (dev, staging, production)

# scheme:
develop
-> staging candidate
-> staging environment
-> release/1.8.0
-> main
-> tag v1.8.0
-> production artifact

# staging checks:
staging checks contains:
1. smoke checks - данная проверка отвечает на вопрос "жив ли проект вообще?"
2. QA scenarios - это тесты, которые проверяют самые важные пути пользователя в приложении.
3. acceptance notes - описание того, что было проверено и как система должна работать.
4. фиксация commit или version - фиксация версии означает создание tag на конкретно коммите, который считается стабильным релизом.

# что разрешено в release/1.8.0:
1. release-blocking fixes - исправление багов, которые мешают релизу.
2. version bump - обновление версии приложения, чтобы зафиксировать новый релиз.
3. release notes - описание изменения в версии.
4. небольшие decomentation updates - мелкие правки в документации, чтобы она соотвестовала новой версии.

Важно, новые features не добавляют в release.

# tag при наличии main и release:
tag нужен чтобы навсегда зафиксировать конкретную версию продукта, вне зависимости от того, как дальше будут двигаться main и release.

# ошибки процесса:
1. тестировали одну сборку, выпустили другую - данная ошибка возникает, когда не зафиксировали конкретный коммит или билд и нет связи между тестами и тем, что ушло в product.
2. не знают, какой commit задеплоен в staging - из-за того, что отсутсвуют теги или же стабильная сборка невозможно точно понять, что в данный момент тестируется.
3. Забыли вернуть release fix обратно в integration line (develop) - исправили все баги в release, но не сделали merge в develop и проблема возникает снова в следующем релизе.
4. Production описывают как “примерно latest main” - production постоянно меняется, поэтому данная формулировка даёт непредсказуемый результат, нет точной фиксации версии.

# local checks:
make check
git status --short

# SSH URL for work:
ssh -T git@github.com
Hi hassagenok! You've successfully authenticated, but GitHub does not provide shell access.
git@github.com:hassagenok/ecommerce-platform.git

# HTTPS URL:
https://github.com/hassagenok/ecommerce-platform.git
