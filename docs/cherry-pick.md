# branches and SHA:
source branch - practice/cherry-source
target branch - homework-v3-06-04-cherry-pick

Source commit:
SHA: 538da08
Commit message: docs: add small fix in txt file

New commit after cherry-pick:
SHA: 46e2aff
Commit message: docs: add small fix in txt file
The commit was created using: git cherry-pick -x practice/cherry-source
Новый коммит содержит сообщение благодаря флагу -x: (cherry picked from commit 538da081ecd1d8a104d65cd1d032282571bdaff7)

# when cherry-picking is appropriate:
Мы применяем cherry-pick в случае, когда нам нужно перенести один или несколько коммитов из одной ветки в другую.
Пример:
1. перенос небольшого исправления из одной ветки в другую.
2. перенос bug fix в release branch.

Merge же нужен в том случае, когда нам нужно объеденить всю историю изменений из одной ветки в другую.

new fix - в случае если изменения слишком зависят от других коммитов или же проще и безопаснее сделать новый фикс , чем переносить.

# safety way to use cherry pick:
1. Проверяем текущую ветку: git branch
2. Проверяем состояние рабочей директории: git status --short (Рабочая область должна быть чистой перед cherry-pick, иначе могут возникнуть конфликты)
3. git cherry-pick -x (commit) - переносим один коммит из другой ветки в текущую ветку и добавляем информацию об исходном коммите (-x дополнительный флаг, который ужас откуда был взят коммит)
4. Запускаем проверки: make check
5. Проверяем результат: git log --oneline --decorate -3.
6. Перед отправкой изменений выполняем review.

# why cherry-pick commit have new SHA:
Каждый коммит содержит:
1. своего родителя (ссылку на родительский commit)
2. метаданные
3. автора и дату
4. сообщение
5. содержимое изменений

При выполнении cherry-pick, git не копирует оригинальный commit целиком, он применяет только изменения (diff) и создаёт новый commit.

# cherry-pick conflicts:
В случае, когда при cherry-pick возник коммит, нам нужно:
1. git status - проверить состояние, какие файлы есть в рабочей среде.
2. Исправить файлы
3. git add (file) - добавить файл в stage
4. git cherry-pick --continue - продолжить перенос изменений из исходного коммита в новый коммит.

Если переносим не тот commit или же не на ту ветку, то выполняем:
1. git cherry-pick --abort - отменяет операцию.

# Makefile and checks:
Проект уже содержит Makefile из прошлых уроков.
make check есть в Makefile.

Провёл проверку make check до staging area:
git diff --check показал пустое состояние (значит никаких проблем с файлом не обнаружено)
git status short показал новый файл: ?? docs/cherry-pick.md

Провёл проверку make check после staging area:
git diff --check показал пустое состояние (значит никаких проблем с файлом не обнаружено)
git status short показал подготовленные к коммиту файлы: A  docs/cherry-pick.md

Провёл проверку make check после commit:
git diff --check и git status short пустые, значит нет никаких файлов в work tree.

# local checks:
make check
git status --short
git log --oneline --decorate -5
