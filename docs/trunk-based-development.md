# integration trunk:
Trunk является основной линией интеграции, в которую разработчики вливают частые маленькие изменения, каждое из которых проходит PR, review, CI, checks. В конечном итоге trunk вливается в main.

Правила trunk:
* Одна основная линия интеграции
* Маленькие изменения (small batches)
* Частая интеграция
* Trunk всегда должен быть рабочим
* CI обязателен
* Короткоживущие ветки
* feature flags
* review перед интеграцией

- Прямой push в main не является зрелым trunk based workflow - потому что он убирает важные механизмы контроля качества перед попаданием изменений в trunk.
Проблемы прямого push:
* Нет обязательного review
* Нет точки проверки перед интеграцией
* Сложнее контролировать качество
* Увеличивается риск

# flow scheme:
short branch -> PR/MR -> checks/review -> trunk -> deploy or release

# readiness checklist:
* branch lifetime - Ветки живут коротко
* PR size - Pull Request маленькие и легко проверяемые
* CI speed - CI достаточно быстрый
* flaky tests ownership - Есть владелец нестабильных тестов
* review latency - Code review происходит быстро
* feature flags - Незавершённые изменения можно безопасно интегрировать
* monitoring - После изменений есть наблюдаемость
* rollback - Есть быстрый способ отката

# Required gates:
* local make check - перед отправкой, разработчик должен локально проверить check, чтобы не отправлять очевидно сломанный код в CI.
* CI - PR не попадает в main, пока CI не будет зелённым.
* review approval - перед merge требуется approval
* protected main - main должен быть защищен строгими правилами: запрещается прямой пуш, merge без CI, merge без approval.
* rollback note - Для рискованных изменений должна быть понятна стратегия отката

# When not to use Trunk-Based Development yet:

1. Feature branches живут неделями. Пример:
* изменения долго не попадают в trunk
* увеличивается размер будущего merge
* растёт количество конфликтов

2. CI не является обязательным gate. Пример:
* trunk может быть сломан
* следующие изменения блокируются
* команда теряет доверие

3. Изменения объединяются только перед релизом. Пример:
* проблема обнаруживается слишком поздно
* сложно понять, какое изменение сломало систему.
* rollback сложнее

4. Нет раннего обнаружения production risk. Пример:
* Чем позже найден баг, тем дороже его исправить.
* Большой радиус ошибки
* Потеря доверия к релизам

# пример slicing большой feature на маленькие mergeable steps:
Например, вместо branch feature/new-checkout на три недели команда может разбить работу:
1. Add checkout service skeleton behind disabled flag
2. Add validation for shipping address
3. Add payment timeout handling
4. Enable new checkout for internal users
5. Expand flag to 10 percent

# local checks:
make check
git status --short
git diff --check



