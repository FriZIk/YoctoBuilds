# YoctoBuild
Пошаговое руководство по сборке специализированного дистрибутива Linux, основанного на Yocto Project, а так же запуску образа, созданного на виртуальной машине Qemu под x86 архитектурой. 
### Шаг первый. Установка необходимых зависимостей для сборки Yocto
Для сборки дистрибутива требуется большое количество зависимостей. Существует два подхода к созданию необходимой программной инфраструктуры.
1. В лоб. Заключается в установке всех необходимых утилит непосредственно в свою Linux систему. Список программ (для Debian):```
          sudo apt-get install sed wget subversion git-core coreutils 
          unzip texi2html texinfo libsdl1.2-dev docbook-utils fop gawk 
          python-pysqlite2 diffstat make gcc build-essential xsltproc 
          g++ desktop-file-utils chrpath libgl1-mesa-dev libglu1-mesa-dev
          autoconf automake groff libtool xterm libxml-parser-perl1
          ```
<<<<<<< HEAD:MinimalBuild/README.md
2. Используя Docker и контейнеризацию. Такой подход является более цивилизованным и предпочтительным. Чтобы установить рабочее окружение необходимо выполнить команду: ```docker run --rm -it -v путь к папке:/workdir crops/poky --workdir=/workdir```
=======
2. Используя Docker и контейнеризацию. Такой подход является более цивилизованным и предпочтительным. Чтобы установить рабочее окружение, необходимо выполнить команду: ```docker run --rm -it -v /home/имя пользователя/название папки:/workdir crops/poky --workdir=/workdir```
>>>>>>> 2e6ce1e8f334d17fbb6af11353835cdd71a3cede:README.md
После ввода этой команды будет запущена среда с уже установленными зависимостями для сборки yocto.
### Шаг второй. Загрузка инструментов YoctoProject
Клонируем репозиторий Yocto Project командой: ```git clone git://git.yoctoproject.org/poky.git```. Далее переходим в папку poky ```cd poky```. Теперь нужно запустить специальный сценарий, который запустит окружение сборки и перенесёт нас в папку build. Для этого используется команда ```source oe-init-build-env```.
### Шаг третий. Редактирование главного конфигурационного файла сборки
В папке **build/conf** хранится главный конфигурационный файл сборки **local.conf**, редактируя его, можно выбрать, под какую платформу собрать проект (мы будем собирать под **qemux86-64**, он выбран по умолчанию). Осталось попросить систему сборки bitbake собрать наш образ. 
### Шаг четвёртый. Сборка образа с помощью Bitbake
Bitbake скачивает необходимые программы и утилиты, собирает их и добавляет в билд системы. Чтобы запустить его для сборки минимального образа, необходимо выполнить команду: ```bitbake core-image-minimal```
После окончания сборки в каталоге **build/tmp/deploy/images** будет находиться готовый образ.
### Шаг пятый. Запуск созданного образа в эмуляторе Qemu
Для его запуска нужно в директории **build** запустить команду ```qemurun qemux86-64```. Откроется новое окно с эмулятором Qemu, запускающим ОС. Имя пользователя **root**, пароль пустой.
###
