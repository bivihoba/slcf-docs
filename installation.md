Как развернуть SLCF-проект?
=========


### Подготовка окружения

Для [SLCF-compiler](https://github.com/bivihoba/slcf-compiler) требуется процессор XSLT-преобразований - [xsltproc](http://xmlsoft.org/XSLT/xsltproc2.html).
Под Unix-системами его установки тривиальна, для Windows это сделать немного сложнее. Нужно:

1. Скачать с ftp://ftp.zlatkovic.com/pub/libxml/ архивы (все последней версии):
	- iconv-версия.win32.zip
	- libxml2-версия.win32.zip
	- libxslt-версия.win32.zip
	- zlib-версия.zip
2. Распаковать и скопировать содержимое из папок /bin в папку C:\WINDOWS\

**Важно!** Вне зависимости от ОС следует устанавливать именно 32-битную версию xsltproc.
Опытным путем было установлено, что 64-битная на 64-битной винде не работает.

К сожалению, это не все проблемы с Windows.
В npm-зависимости SLCF входит [libxml](https://github.com/polotek/libxmljs).
Под Windows его установка требует дополнительных библиотек.
Нужно глобально установить [node-gyp](https://github.com/TooTallNate/node-gyp),
а также необходимые для него Python и Express (в зависимости от версии Windows, подробнее см. на странице node-gyp).

Полноценная работа с SLCF подразумевает использование [Git](http://git-scm.com/). Установка Git для Windows:
 
1. Cкачать Git c http://code.google.com/p/msysgit/downloads/list?q=full+installer+official+git 
2. Установить Git с дефолтными параметрами

Сборка проекта осуществляется с помощью [Grunt](http://gruntjs.com/), который в свою очередь работает на [Nodejs](http://nodejs.org/) и устанавливается через npm (пакетный менеджер node.js). Для установки Grunt нужно:

1. Скачать и установить Nodejs с дефолтными параметрами http://nodejs.org/
2. Запустить GitBash и проверить работу npm, выполнив команду 
	npm --version
3. Установить grunt-cli глобально:
	npm install -g grunt-cli
4. Проверить работу grunt:
	grunt --version

**Важно!** Если команды npm не выполняются в GitBash, то можно попробовать переустановить GitBash после установки NodeJS.   


### Разворачивание SLCF-проекта из [шаблона](https://github.com/bivihoba/slcf-boilerplate)

TODO Написать про cleanBoilerplate, initProject, сабмодули