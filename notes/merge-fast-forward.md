* 2828d7d (HEAD -> homework-v3-03-03-merge-fast-forward, origin/homework-v3-03-03-merge-fast-forward) docs: add logs and explain merge
*   725228a Merge branch 'practice/merge-source' into homework-v3-03-03-merge-fast-forward
|\  
| * b1f60b7 (practice/merge-source) file: add practice merge source txt
* | 8f54577 file: add practice merge target txt
|/  
* 1656f61 (practice/ff-source) file: add practice ff source txt
* a8e8176 (origin/homework-v3-03-02-feature-branches-naming, homework-v3-03-02-feature-branches-naming) docs: explain feature branch naming
*   14175ab (origin/main, origin/HEAD, main) Merge pull request #4 from hassagenok/homework-v3-02-05-history-for-review
|\  
| * 0d119f9 (origin/homework-v3-02-05-history-for-review) docs: add readable history checklish


# Почему первый merge был fast-forward, а второй создал merge comit:
Первый merge был fast-forward так как после отвлетления не было никаких изменений в ветке homework. Поэтому Git попросту сдвинул point ветки вперёд.
Второй merge был merge commit так как истории обеих веток разошлись: в обоих ветках мы сделали по коммиту и Git попросту объеденил их через отдельный коммит.

# Corporate note:
Feature branch в командной работе идет через review и CI, а не напрямую в protected main

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
