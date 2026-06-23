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
origin/<branch> — это локальный remote-tracking reference, который обновляется только через git fetch и хранит последний известный Git снимок состояния удалённой ветки для сравнения с локальной веткой.

# Покажу пример вывода git branch -vv с upstream tracking:
Полный вывод: 
  homework-v3-03-01-branch-task-isolation    8741316 [origin/homework-v3-03-01-branch-task-isolation] docs: add file with git branch explanation
  homework-v3-03-02-feature-branches-naming  a8e8176 [origin/homework-v3-03-02-feature-branches-naming] docs: explain feature branch naming
  homework-v3-03-03-merge-fast-forward       8d81dff [origin/homework-v3-03-03-merge-fast-forward] fix: correct logs in file
  homework-v3-03-04-rebase-personal-branch   8d0db34 [origin/homework-v3-03-04-rebase-personal-branch] fix: correct Makefile
  homework-v3-03-05-worktree-parallel-work   108659f [origin/homework-v3-03-05-worktree-parallel-work] fix: correct worktree note
  homework-v3-04-01-remote-origin            cfdcb73 [origin/homework-v3-04-01-remote-origin] docs: add remote origin explanation
* homework-v3-04-02-fetch-pull-push-tracking 0f6613a [origin/homework-v3-04-02-fetch-pull-push-tracking] docs: add notes about fetch, pull, push and tracking
  main                                       d902d08 [origin/main] Merge pull request #11 from hassagenok/homework-v3-04-01-remote-origin
  practice/ff-source                         1656f61 file: add practice ff source txt
  practice/merge-source                      b1f60b7 file: add practice merge source txt
  practice/rebase-base                       8c734ab feat: add practice/rebase-base.txt
  practice/rebase-topic                      10bc32c feat: add practice/rebase-topic.txt

Разберу одну ветку:
Локальная ветка: homework-v3-03-05-worktree-parallel-work
Upstream: origin/homework-v3-03-05-worktree-parallel-work
HEAD: 108659f
last commit: fix: correct worktree note

ahead - количество коммитов, которые есть в локальной ветке, но отсутствуют в remote-tracking ref.
behind - количество коммитов, которые есть в remote-tracking ref, но отсутствуют в локальной ветке.
ahead/behind считаются как разница между локальной веткой и её upstream после git fetch.

# Non-fast-forward:
Данная ошибка возникает при попытке выполнить git push, когда remote branch уже содержит коммиты, которых нет в локальной ветке.
beginner-readable модель: remote branch содержит commits, которых нет локально, поэтому первым шагом нужен git fetch origin и анализ истории, а не force push.

# Local checks:
make check
git status --short
git remote -v
git branch -vv

Рабочий remote остается SSH URL: git@github.com:hassagenok/ecommerce-platform.git
для Tyfoon мы отправляем HTTPS URL repository: https://github.com/hassagenok/ecommerce-platform.git

