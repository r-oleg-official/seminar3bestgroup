## Instruction of Git for Linux.

Установка `git` на Linux Mint 20.

    $ sudo apt install git

### Глобальная настройка `git`
Перед началом работы с `git`, необходимо представиться:

    $ git config --global user.name 'User name'
    $ git config --global user.email "example@mail.com"

Создать каталог проекта и перейти в него:

    $ mkdir -p /home/user/my_project && cd /home/user/my_project

### Добавление лицензии к проекту. [Подробности.](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-license-to-a-repository)

    $ git add LICENSE
В сети есть шпаргалка по работе с [Git](https://training.github.com/downloads/ru/github-git-cheat-sheet/).

Дальнейшие команды выполняются как в отдельном терминале, так и в терминале `VS Code` (далее `VS`). Терминал `VS` поддерживает такие же возможности `BASH`, что и терминал Linux. В окне терминала `VS`, в правом углу  есть кнопка ![](submit_bash.png), которая указывает какой используется интерпретатор.

Инициализация(создание репозитория), нужно добавить каталог для отлеживания `git`'ом:

    $ git init

После внесения изменения в проект нужно сохранить файл, **`Ctrl+S`**. 
После сохранения файла используют след. команды: **`git add`**, **`git commit`**, синтаксис ниже.

### Работа с файлами проекта

    $ git add [file] - индексация "file" для последующего комментирования. 
    $ git commit -m "Comment." - фиксация проиндексированного изменения файла проекта и сохранение его в историю версий.
    $ git rm [file] - удаляет файл из директории с индексацией.
    $ git rm --cached [file] - удаляет файл из контроля версий, без физ. удаления из директории
    $ git mv [orig_file] [new_file] - переименование файла из "orig_file" в "new_file" c индексацией для последующего комментирования.

> ## Цитата из [git-scm](https://git-scm.com/ "Всё рядом")
> **_`Git` --everything-is-local_**

![](to-bee-continued_250px.jpg)

## ДЗ.
Дооформить инструкцию по работе с Git, используя возможности Markdown (цитаты, картинки, ссылки и др.). Приложить свой проект в заархивированном виде (всю папку целиком, 3 комита).
