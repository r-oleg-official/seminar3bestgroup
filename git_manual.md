### Продолжение инструкции `Git`.

Список веток на экран:

    $ git branch

Создание новой ветки:

    git branch [branch_name]

Создание новой ветки и сразу переход в неё:

    $ git checkout -b [branch_name]

Переход между ветками:

    $ git checkout [branch_name]

Состояние файлов проекта, **`M`**, которые не проиндексированные `git`:

    $ git checkout

Проверка статуса контроля версий проекта:

    $ git status 

Сброс состояния файла до предыдущего commit, с удалением индекса и содержимого, где `sha-1` - хэш commit (достаточно первых уник-х символов хэша), [см](https://ru.stackoverflow.com/questions/431520/%D0%9A%D0%B0%D0%BA-%D0%B2%D0%B5%D1%80%D0%BD%D1%83%D1%82%D1%8C%D1%81%D1%8F-%D0%BE%D1%82%D0%BA%D0%B0%D1%82%D0%B8%D1%82%D1%8C%D1%81%D1%8F-%D0%BA-%D0%B1%D0%BE%D0%BB%D0%B5%D0%B5-%D1%80%D0%B0%D0%BD%D0%BD%D0%B5%D0%BC%D1%83-%D0%BA%D0%BE%D0%BC%D0%BC%D0%B8%D1%82%D1%83):

    $ git reset --hard [sha-1]

Слияние ветки **`branch _name`** с текущей, в которой находишься:

    $ git merge [branch_name]

Удаление ненужной ветки после слияния:

    $ git branch -d [branch_name]

Просмотр лога коммитов с визуализацией:

    $ git log --graph

Просмотр лога коммитов в одну стоку:

    $ git log --graph --oneline

Изменить редактор `git`:

    $ git config --global core.editor your-favorite-text-editor

### Перезапись истории.
>**!Warning.** Если коммит уже отправлен в общий репозиторий, то лучше этого не делать.

Когда используешь этот приём надо понимать, что при этом изменяется хэш коммита (SHA-1).
[Подробности](https://git-scm.com/book/ru/v2/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-Git-%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D0%B8%D1%81%D1%8C-%D0%B8%D1%81%D1%82%D0%BE%D1%80%D0%B8%D0%B8).

Изменить только сообщение последнего commit:

    $ git commit --amend

>При изменении коммита существует возможность изменить как его содержимое, так и сообщение коммита. Если в коммит внесены существенные изменения, то почти наверняка следует обновить и его сообщение, чтобы оно более точно отражало содержимое коммита.

>С другой стороны, если изменения незначительны (исправление опечаток, добавление в коммит забытого файла), то текущее сообщение вполне можно оставить; чтобы лишний раз не вызывать редактор, просто добавьте измененные файлы в индекс и выполните команду:

    $ git commit --amend --no-edit

#### Изменение сообщений нескольких commits.
Например, если вы хотите изменить сообщения последних трёх коммитов, или сообщение какого-то одного коммита этой группы, то передайте как аргумент команде `git rebase -i` родителя последнего коммита, который вы хотите изменить — `HEAD~2^` или `HEAD~3`.
Последние 3-и commits:

    $ git rebase -i HEAD~3

В редакторе будет подсказка как работать с commits. В строке, напротив нужного commit, поменять команду `pick` на нужную. Например, `reword` изменяет сообщение, но не содержимое commit.<br>
После сохранить, выйти из редактора. Если вдруг, передумал изменять, или что-то пошло не так - можно исп. команду, она также может быть в подсказке:

    $ rm -fr ".git/rebase-merge"

Спрятать изменения от `git`'a, [см](https://pingvinus.ru/git/1718):

    $ git stash save "any message"

Материал по `git stash` [atlassian.com](https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash).

# Remote repository.

## 1. Github. Quick setup.

…or create a new repository on the command line - случай, когда еще не создан локальный репозиторий, создается в терминале.

    echo "# test" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git branch -M main
    git remote add origin <url_repo>
    git push -u origin main

…or push an existing repository from the command line - случай, когда имеется репозиторий Github, данные локального загружаются на удаленный.

    git remote add origin <url_repo>
    git branch -M main
    git push -u origin main

Команда `git branch -M main` - переименовывает основную ветку на `main`.<br>
Команда `git remote add origin <url_repo>` - создает связку удаленного репо по адресу `<url_repo>` с локальным через имя-ссылку `origin`.<br>
Команда `git push -u origin main` - загружает данные ветки `main` локального репозитория через имя-ссылку в конфиге на удаленный репозиторий. `Git` должен знать адрес репо-я и быть авторизован в удал-м репо-и.

## 2. Synchronization with a remote repository. 
Материалы:
* [Синхронизация в Git](https://www.atlassian.com/ru/git/tutorials/syncing).
* [Git изнутри - Спецификации ссылок](https://git-scm.com/book/ru/v2/Git-%D0%B8%D0%B7%D0%BD%D1%83%D1%82%D1%80%D0%B8-%D0%A1%D0%BF%D0%B5%D1%86%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D0%B8-%D1%81%D1%81%D1%8B%D0%BB%D0%BE%D0%BA)
* [Что такое git remote add... "и" git push origin master "?](https://ask-dev.ru/info/27355/what-is-git-remote-add-and-git-push-origin-master)
* [Шпаргалка по git-командам](https://highload.today/git-push-git-pull-git-fetch/)

### 2.1. Command `git clone`.

        $ git clone <url_repo> <local_directory> - создать копию удалён-го репо-я в локальном каталоге.
        
 Если `<local_directory>` не задать, то локальный репо-й создаётся с именем удалённого.

    $ git fork - копия чужого репозитория.
    $ git pull - скачать изменения удал-го и слияние с лок-м реп-ми

### 2.3. Command `git remote`.

    $ git remote -v - просмотр ссылок на связь локального репо-я с удаленными репо-ми

## 3. Объединение двух репозиториев.

1. [как объединить два репозитория Git?](https://overcoder.net/q/13252/%D0%BA%D0%B0%D0%BA-%D0%BE%D0%B1%D1%8A%D0%B5%D0%B4%D0%B8%D0%BD%D0%B8%D1%82%D1%8C-%D0%B4%D0%B2%D0%B0-%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F-git);
2. [git, объединить разные репозитории?](https://stackoverflow.com/questions/2949738/git-merge-different-repositories).
3. [Объедините два репозитория Git и сохраните историю](https://ask-dev.ru/info/10867/merge-two-git-repos-and-keep-the-history).

Если нужно объединить project-a с project-b:

    cd path/to/project-b
    git remote add project-a path/to/project-a
    git fetch project-a --tags
    git merge --allow-unrelated-histories project-a/master # or whichever branch you want to merge
    git remote remove project-a # удаляет запись из .git/config о project-a

Этот метод работал очень хорошо для меня, он короче и, на мой взгляд, намного чище.

> Примечание. Параметр --allow-unrelated-histories существует только после того, как git> = 2.9. См. Git - Документация по git merge / --allow-unrelated-history (https://git-scm.com/docs/git-merge#git-merge---allow-unrelated-histories%23git-merge---allow-unrelated-histories)
