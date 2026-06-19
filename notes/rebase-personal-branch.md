# rebase and fast-forward:
14b8546 commit: feat: add practice/rebase-topic.txt
210e302 (practice/rebase-base) rebase (start)
c93e987 rebase (pick): feat: add practice/rebase-topic.txt
c93e987 rebase (finish)
c93e987 merge practice/rebase-topic: Fast-forward

Мы видим что 14b8546 commit был переписан и теперь новый хэг выглядит так: c93e987
Стадии rebase: start, pick, finish
Git зафиксировал fast-forward

# logs:
* 14b8546 (HEAD -> practice/rebase-topic) feat: add practice/rebase-topic.txt
| * 210e302 (practice/rebase-base) feat: add practice/rebase-base.txt
|/  
*   851a027 (origin/main, origin/HEAD, main) Merge pull request #7 from hassagenok/homework-v3-03-03-merge-fast-forward
|\  
| * 8d81dff (origin/homework-v3-03-03-merge-fast-forward, homework-v3-03-03-merge-fast-forward) fix: correct logs in file
| * 2828d7d docs: add logs and explain merge
| *   725228a Merge branch 'practice/merge-source' into homework-v3-03-03-merge-fast-forward
| |\  
| | * b1f60b7 (practice/merge-source) file: add practice merge source txt
| * | 8f54577 file: add practice merge target txt
| |/  
| * 1656f61 (practice/ff-source) file: add practice ff source txt
* | 4cd355e Merge pull request #6 from hassagenok/homework-v3-03-02-feature-branches-naming
|\| 

# SHA topic commit:
14b8546

# new graph:
* c93e987 (HEAD -> practice/rebase-topic) feat: add practice/rebase-topic.txt
* 210e302 (practice/rebase-base) feat: add practice/rebase-base.txt
*   851a027 (origin/main, origin/HEAD, main) Merge pull request #7 from hassagenok/homework-v3-03-03-merge-fast-forward
|\  
| * 8d81dff (origin/homework-v3-03-03-merge-fast-forward, homework-v3-03-03-merge-fast-forward) fix: correct logs in file
| * 2828d7d docs: add logs and explain merge
| *   725228a Merge branch 'practice/merge-source' into homework-v3-03-03-merge-fast-forward
| |\  
| | * b1f60b7 (practice/merge-source) file: add practice merge source txt
| * | 8f54577 file: add practice merge target txt
| |/  
| * 1656f61 (practice/ff-source) file: add practice ff source txt
* | 4cd355e Merge pull request #6 from hassagenok/homework-v3-03-02-feature-branches-naming
|\| 

# new SHA topic commit:
c93e987

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
