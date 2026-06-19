# logs:
* 125c6fa (HEAD -> practice/rebase-topic) feat: add practice/rebase-topic.txt
| * 8c734ab (practice/rebase-base) feat: add practice/rebase-base.txt
|/  

# SHA:
rebase-topic: 125c6fa
rebase-base: 8c734ab

# new graph:
* 10bc32c (HEAD -> practice/rebase-topic) feat: add practice/rebase-topic.txt
* 8c734ab (practice/rebase-base) feat: add practice/rebase-base.txt

# new SHA :
rebase-topic: 10bc32c
rebase-base: 8c734ab

# logs after fast-forward commit:
* 10bc32c (HEAD -> homework-v3-03-04-rebase-personal-branch, practice/rebase-topic) feat: add practice/rebase-topic.txt
* 8c734ab (practice/rebase-base) feat: add practice/rebase-base.txt
* 813be5e (origin/main, origin/HEAD, main) docs: add proof rebase and fast-forward notes

# Почему topic commit после rebase новый hash:
rebase создало новый коммит поверх нового родителя. Так как родитель входит в метаданные commit, после смены родителя commit получил новый hash.

# Safe zone и Danger zone:
Safe zone - это личная ветка, в которой работает только один человек. В ней можно делать какие либо правки, так как никто от неё не зависит.
Danger zone - это общая ветка, которой пользуются другие люди. Если переписать историю данной ветки через rebase и сделать force push, то на сервере и у коллег будут разные версии одной и той же ветки. Из-за этого могут появится конфликты и история проекта будет запутана. В такую зону входят: published history, protected main, develop, release/*, shared branch и веток с открытым review.

# Почему после rebase нужно запускать make check:
После rebase нужно проверить graph и сделать локальную проверку make check, чтобы убедиться в том что после изменения истории код остаётся корректным и все проверки проходят успешно.

Важно, в рамках этой homework мы не делаем force push. 

# Локальные проверки перед commit:
make status
git diff
git diff --staged
make history
git status --short
git log --oneline --decorate --graph -8
make check

# Локальные проверки после commit:
make check
git status --short
git log --oneline --decorate --graph -8
