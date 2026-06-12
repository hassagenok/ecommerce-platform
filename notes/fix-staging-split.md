# Что делать если в staging area случайно попали две разные задачи:
# В качестве примера возьму ситуацию с заметкой урока и изменением Makefile
Представим ситуацию, что мы сделали заметку урока и изменения в Makefile.
Оба изменения случайно попали в staging area через git add
Проверяем git diff --staged и видим, что staged diff содержит изменения из двух разных причин.
Убираем Makefile из staging area, но не удаляем его через: git restore --staged Makefile
После данной команды файл останеться в working tree, но удалится из staging area
Собираем первый маленький коммит: git commit -m "Lesson notes"
После возвращаемся ко второй задаче отдельно: git add Makefile
Собираем второй маленький коммит: git commit -m "changes in Makefile"

Не нужно удалять файлы только ради исправления staging. Удаление может быть отдельным осознанным действием.
git restore --staged решает другую задачу: меняет будущий commit.

# Перед commit делаем обязательно локальную проверку:
make status
make diff
git diff --staged
make check

# После commit делаем проверку состояния:
git status --short