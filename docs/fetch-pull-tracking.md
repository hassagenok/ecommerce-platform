# Разница между git fetch, git pull и git push
git fetch - исследует remote repository и подтягивает objects в local repository.
При fetch двигает remote-tracking refs

git pull - по умолчанию выполняет действия git fetch и интегрирует их в текущую ветку локального репозитория. В зависимости от настроек данная интеграция меняется между merge и rebase. Он может создать новый merge commit, запустить rebase или остановиться на conflict.
При pull Git после fetch пытается совместить remote-tracking ref с текущей веткой

git push - отправляет локальные commits в remote repository и просит сервер обновить remote branch.
При push локальный Git отправляет objects на сервер, а сервер решает, можно ли обновить ref

# Схема:
remote branch -> fetch -> origin/<branch> -> pull -> local branch
local branch -> push -> remote branch

# Объяснение для git push -u origin <branch> и зачем нужен upstream tracking:
Данная команда записывает в конфигурацию репозитория, что данная ветка связана с remote и соотвествует branch ref. В последствии это позволяет выполнять git push и git pull без указания remote и branch. upstream помогает быстро ответить на практические вопросы: опубликованы ли последние commits, отстал ли автор от remote, куда уйдет push, почему PR не обновился после локального commit.

# Покажу пример вывода git branch -vv с upstream tracking:
Локальная ветка: homework-v3-03-05-worktree-parallel-work
Upstream: origin/homework-v3-03-05-worktree-parallel-work
HEAD: 108659f
last commit: fix: correct worktree note

ahead показывает сколько коммитов есть на локальной машине, но нет на remote.
behind показывает сколько коммитов есть на remote, но нет на локальной машине.

# Non-fast-forward:
Данная ошибка возникает при попытке выполнить git push, когда remote branch уже содержит коммиты, которых нет в локальной ветке.
beginner-readable модель: remote branch содержит commits, которых нет локально, поэтому первым шагом нужен git fetch origin и анализ истории, а не force push.

# Local checks:
make check
git status --short
git remote -v
git branch -vv

Рабочий remote остается SSH URL, для Tyfoon мы отправляем HTTPS URL repository.

