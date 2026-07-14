# commit message является контрактом между:
commit message - это контракт между участниками процесса разработки:
1. Автор - исользует commit message, чтобы объяснить, какое изменение было сделано и почему.
2. Reviewer - использует commit message, чтобы быстро понять смысл изменения перед проверкой кода.
3. Release manager - использует commit message, чтобы подготовить релиз, оценки риска, заметки релиза.
4. Future maintainer - использует commit message, чтобы понять причины изменений при исправлении багов и развитии проекта.

# based format commit message:
based format: type(scope): description
* type - категория изменения.
* scope - область проекта, который изменён.
* description - короткое описание изменения.

# good and bad examples:
Good:
1. feat(checkout): add delivery slot selection
2. feat(cart): add coupon validation
3. docs(note): explain commit message format
4. fix(auth): keep session after password change
5. docs(note): describe commit message convention

Bad:
1. fix
2. update
3. temporary changes
4. fix bug
5. test

# Связь с Модулем 05:
Формат commit message помогает на всех этапах release flow.

* Review — reviewer быстрее понимает изменение. Во время code review reviewer смотрит не только код, но и смысл изменения.
* CI — легче сопоставить проверки с коммитом. CI проверяет код автоматически, но commit message помогает людям понимать результаты проверок.
* Release notes — feat и fix удобно использовать при составлении списка изменений. Release notes часто строятся на основе истории коммитов.
* Tag — история релиза становится понятной. Перед созданием release tag важно понимать состав изменений.
* Production — проще найти источник проблемы. После выхода в production команда должна быстро понимать, что попало в релиз.

# Связь с модулем 06:

* Hotfix — легче найти нужное исправление. При срочном исправлении в production важно быстро найти нужный commit.
* Safe undo — проще отменить конкретный коммит. Если нужно отменить изменение, хороший commit message помогает понять последствия.
* Backport — удобно переносить нужные исправления в другую ветку. При переносе исправления в другую ветку нужно найти конкретный commit.
* Поиск в истории — понятные сообщения быстрее находятся через git log. Хорошие сообщения делают историю Git полезной.

# Local checks:
make check - запускает базовые проверки проекта
git status --short - показывает краткое состояние рабочей директории.

Перед отправкой коммита в remote, нам нужно убедиться:
1. нет случайных незакомиченных файлов
2. не добавлены временные файлы
3. все нужные изменения находятся в commit.
