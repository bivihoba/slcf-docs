SLCF Docs
=========

SLCF — каркас для верстки по БЭМ-методологии.

Ориентирован на статичную верстку страниц в HTML и CSS.

Основные возможности:

- разметка в БЭМ-терминах,
- простая система шаблонов,
- сборка CSS, раскиданного по файлам блоков,
- настроенные инструменты оптимизации.

Используемые технологии: 

- [Grunt](https://github.com/gruntjs/grunt) для сборки проекта.
- [SLCF Compiler](https://github.com/bivihoba/slcf-compiler) для БЭМ-разметки.
- [LESS](https://github.com/less/less.js/)/[Stylus](https://github.com/learnboost/stylus) в качестве препроцессора CSS.
- [Autoprefixer](https://github.com/postcss/autoprefixer) для расстановки вендорных префиксов
- [CSSO](https://github.com/css/csso/) для оптимизации CSS.


Документация:

1. [БЭМ в рамках SLCF-проекта](theory.md)
2. [Файловая структура SLCF-проекта](file-system.md)
3. [Использование Grunt](grunt.md)
4. [Сборка стилей](css.md)
5. [Как развернуть SLCF-проект?](installation.md)
6. [Обновление существующего проекта](update.md)
7. [BEMXML](bemxml.md)
	- [Атрибуты](bemxml-attributes.md)
8. [HTML в BEMXML](html.md)
9. [Структура BEMXML-страницы](bemxml-page.md)
10. [Шаблоны BEMXML](bemxml-templates.md)
