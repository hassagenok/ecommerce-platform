# Почему reviewer читает историю, а не только финальные файлы:
Reviewer читает историю для того, чтобы понять: ход мыслей автора коммита, проверить качество коммитов, найти в истории ошибки и решения этих ошибок, увидеть масштаб изменений.

# Что проверяют make status, make diff, make history, make check:
make status - проверяет состояние рабочего каталога на данный момент
make diff - выясняет какие изменения были внесены между: working tree, staging area, HEAD
make history - показывает историю последних 5 коммитов (git log --oneline --decorate -5)
make check - запускает минимальные проверки проекта.

# Что нужно увидеть в последнем commit через git show HEAD:
После команды git show HEAD нам нужно увидеть: Автора коммита, дату, сообщение которое было заложено в commit.

# Почему messages вроде fix и misc мешают review:
Сообщения по типу: "fix", "misc", "docs", попросту не дают никакой информации, неизвестно что именно было исправлено, почему это изменения понадобилось, к какой части проекта это относится.

# Как readable history помогает review, future self и release process:
Readable history помогает быстро найти конкретные изменения, помогает в откате, снижает шум в истории.

# Перед commit делаем базовую проверку:
make status
make diff
git diff --staged
make history
make check

# После commit сделаем завершающую проверку:
make history
git show HEAD
git status --short
