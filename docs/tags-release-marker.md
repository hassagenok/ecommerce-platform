# difference between "branch" and "tags":
* Branch — это подвижный указатель на последний коммит. При новых коммитах и merge ветка автоматически перемещается вперёд и отражает текущее состояние разработки.
* Tag — это неподвижная метка на конкретном коммите. После создания тег не перемещается и используется для обозначения важных точек в истории, например релизов.

# task 5, 6, 7, 8, 9:
1. Создал локальный annotated tag для текущего коммит: git tag -a v1.5.0 -m "Release v1.5.0"

2. Не пушил tag, так как в домашней работе он нужен как локальная тренировка.

3. Пока тег существует, делаю проверку тега и вставляю вывод:

* git show --no-patch v1.5.0 показал:
tag v1.5.0
Tagger: hassagenok <daniil.kononenko@proton.me>
Date:   Fri Jul 17 13:43:46 2026 +0200

Release v1.5.0

commit 4426bc46e08652d48bedc99014decccf60cae240 (HEAD -> homework-v3-07-04-tags-release-marker, tag: v1.5.0, origin/main, origin/HEAD, main)
Merge: b46e6f8 2dc30b6
Author: Daniil Kononenko <116737236+hassagenok@users.noreply.github.com>
Date:   Thu Jul 16 14:31:31 2026 +0200

Merge pull request #29 from hassagenok/homework-v3-07-03-semver-release-impact
    
docs(notes): semver explanation with examples
    
* git tag --list показал:
v1.5.0

4. Запишем команды просмотра:
* git tag --list - показывает список всех локальных тегов.
* git show v1.5.0 - показывает информацию о теге v1.5.0 (если это аннотированный тег: имя тега, автора, дату, сообщение) и коммите, на который он указывает.
* git log v1.4.0...v1.5.0 --oneline - покажет список изменений, которые были добавлены между двумя релизами.

5. Правило: Tag — это публичная отметка версии. Пушить его стоит только после release decision, чтобы не создать ошибочный релиз. git push --tags отправляет все локальные теги и может случайно опубликовать лишние.

# Связь tag c changelog, release notes, rollback, incident investigation:
Tag связывает конкретную версию кода с процессами релиза:
* Changelog / Release notes — tag фиксирует версию, для которой создаётся список изменений и описание релиза.
* Rollback — tag позволяет быстро вернуться к последней стабильной версии, так как он указывает на конкретный коммит.
* Incident investigation — tag помогает определить, какой код был в продакшене во время инцидента, и сравнить изменения между версиями.

# tag delete:
Удалил локальный тренировочный tag командой git tag -d v1.5.0, чтобы случайно не отправить его позже.
После проверил список тегов с помощью: git tag --list, вывод оказался пустым, это означает, что удаление прошло успешно.

# local checks:
make check
git status --short
git tag --list
