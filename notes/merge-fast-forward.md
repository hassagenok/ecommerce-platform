* b016d7d (HEAD -> main, origin/main, origin/HEAD) refactor: remove subprocess in favor of dbus and wire up to javascript (#606)
* 44dfa51 refactor: load scene-script builtins from a generated header (#608)
* ce06c02 refactor: read puppet mesh data via BinaryReader/MemoryStream (#604)
* ab76bc0 fix: mute video wallpapers when --silent is used (#605)
* 100b664 chore: cleanup and optimization of scripting engine + anonymous namespace methods (#599)
* f38303d refactor: make CImage::resolveTransform iterative and reuse computed transform (#602)
* 8a00ff7 Improve text rendering compatibility (5/5) (#571)
* a1efb83 Add media thumbnail texture fallback (#570)

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
