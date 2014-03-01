Обновление рабочих проектов
=========

Ручное обновление c 3.0.* до 3.1.0

1. Склонировать куда-нибудь рядом с проектом [slcf-boilerplate 3.1.0](https://github.com/bivihoba/slcf-boilerplate), чтобы копировать из него нужные файлы.
2. Из проекта удалить папку с node-модулями и закоммитить удаление.
3. Заменить .gitignore (node_modules внесены в игнор)
4. Заменить Gruntfile.js
5. Заменить package.json
6. Переместить всю негенерируемую статику из code/dev/ в бандл bundles/__assets
7. Скопировать в корень проекта папку grunt
8. Обновить сабмодуль slcf-compiler
9. Переключить остальные внешние библиотеки на новую версию, соответствующую обновленной структуре бандлов.
Если такой версии нет, то надо сделать ее самому, взяв за пример бандл main из boilerplate
(операции будут те же, что и для проектных бандлов, о которых далее)
10. Переименовать папку blocks.less в less.blocks и сделать соответстующие исправления в путях к файлам этой папки
11. В основном файле стилей styles.less вместо файла blocks.less подключить blocks.auto.used.less
12. Перенести файл default-semantic.xml в папку html.blocks и поправить путь к нему в settings.xml
13. Исправить пути в подключениях внешних библиотек:
	- "/blocks.less/b-block.less" => "/less.blocks/b-block.less" (пример точечной зависимости)
	- "/blocks.less/blocks.less" => "/less.blocks/blocks.auto.less"
	- "/settings/default-semantic.xml" => "/settings/html.blocks/default-semantic.xml"
14. Все подключения внешних библиотек перенести в файл blocks.deps.less
15. При необходимости внести нужные зависимости в blocks.hard.deps.less (см. [про сборку стилей](css-tech.md))
16. Переименовать в шаблонах файлы стилей. Примеры:
	- "styles_main.css" => "main.styles.css"
	- "ie.css" => "main.styles.ie7.css"
17. Повторить действия 10-16 для всех проектных бандлов.
18. Очистить проект и запустить сборку
> ```
$ grunt cleanProject
$ grunt buildProject
```
19. Протестировать, в т.ч. production-версию.
20. Закоммитить все изменения и слить в мастер.
21. ...
22. PROFIT!!!
