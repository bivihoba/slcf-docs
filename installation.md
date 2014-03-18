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

**Важно!** Вне зависимости от разрядности Windows следует устанавливать именно 32-битную версию xsltproc.
Опытным путем было установлено, что 64-битная на 64-битной винде не работает.

К сожалению, это не все проблемы с Windows.
В npm-зависимости SLCF входит [libxml](https://github.com/polotek/libxmljs).
Под Windows его установка требует дополнительных библиотек.
Нужно глобально установить [node-gyp](https://github.com/TooTallNate/node-gyp),
а также необходимые для него Python и Express (в зависимости от версии Windows, подробнее см. на странице node-gyp).

### Разворачивание нового SLCF-проекта из [шаблона](https://github.com/bivihoba/slcf-boilerplate)

> Считается, что в системе уже стоят:
node > 0.10,
grunt-cli (установлен глобально),
xsltproc,
и в случае Windows, все, о чем написано в предыдущем разделе.

Склонировать slcf-boilerplate:

```
$ git clone https://github.com/bivihoba/slcf-boilerplate projectName
```

Перейти в папку проекта.

В package.json изменить url проекта на реальный:

```
"repository": {
	"type": "git",
	"url": "https://github.com/bivihoba/slcf-boilerplate.git"
},
```

Установить npm-зависимости:

```
$ npm install
```

Очистить шаблонные файлы:

```
$ grunt cleanBoilerplate

```

Инициализировать проект:

```
$ grunt initProject
```

После этих действий в папке проекта должен быть создан гит-репозиторий с ремоутом на указанный ранее адрес,
подключены стандартные библиотеки и сделан первый коммит.
Можно переходить к работе над проектом. [Использование Grunt](grunt.md).

### [Об обновлении существующего проекта](update.md)
