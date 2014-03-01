Синтаксис BEMXML
=========

BEMXML - XML-формат БЭМ-разметки.


### Блок

Пространство имен "b:"

Исходный код:

```
<b:logo>Блок логотипа</b:logo>
```

Результат:

```
<div class="b-logo">Блок логотипа</div>
```

### Элемент блока

Пространство имен "e:"

Исходный код:

```
<b:news>
    <e:item>Элемент новостей</e:item>
</b:news>
```

Результат:

```
<div class="b-news">
    <div class="b-news__item">Элемент новостей</div>
</div>
```

Элемент, по умолчанию, принадлежит ближайшему блоку (вверх по дереву). Можно задать для элемента конкретный блок, через атрибут "block".

Исходный код:

```
<b:sidebar>
    <b:news>
        <e:item>Элемент новостей</e:item>
        <e:item block="sidebar">Элемент новостей</e:item>
    </b:news>
</b:sidebar>
```

Результат:

```
<div class="b-sidebar">
    <div class="b-news">
        <div class="b-news__item">Элемент новостей</div>
        <div class="b-sidebar__item">Элемент чего-то другого</div>
    </div>
</div>
```

Иногда какой-нибудь блок может мешать наследованию "блочности" от блока, стоящего выше по дереву, при этом у такого блока нет элементов. В такой ситуации логично исключить его из потока возможных "родителей". Это можно сделать с помощью атрибута "noblock".

Исходный код:

```
<b:news>
    <e:item><b:link><e:item-text>Элемент новостей</e:item-text></b:link></e:item>
    <e:item><b:link noblock="true"><e:item-text>Элемент новостей</e:item-text></b:link></e:item>
</b:news>
```

Результат:

```
<div class="b-news">
    <div class="b-news__item"><a href="#" title="" class="b-link"><span class="b-link__item-text">Элемент новостей</span></a></div>
    <div class="b-news__item"><a href="#" title="" class="b-link"><span class="b-news__item-text">Элемент новостей</span></a></div>
</div>
```

### Модификации

Пространство имен "m:"

Исходный код:

```
<b:logo>
    <m:size val="small" />
    <m:content val="softline" />
        Блок логотипа
</b:logo>
```

Результат:

```
<div class="b-logo b-logo_size_small b-logo_content_softline">Блок логотипа</div>
```

### Дополнительная сущность

Пространство имен "a:"

На один DOM-узел можно навесить несколько БЭМ-сущностей (микс). Сущности, которые добавляются к основной, называются дополнительными.
Дополнительной сущностью может быть и блок и элемент, которые в свою очередь могут иметь свои модификации.
Если дополнительной сущностью является элемент, то нужно указать на это, задав для него блок через атрибут block-of.
Кол-во дополнительных сущностей не ограничено.

Исходный код:

```
<b:news>
	<e:item>
		<m:state val="selected"/>
		<a:link>
			<m:type val="pseudo"/>
		</a:link>
		<a:text block-of="some-block"/>
        Элемент новостей
    </e:item>
</b:news>
```

Результат:

```
<div class="b-news">
    <a class="b-news__item b-news__item_state_selected b-link b-link_type_pseudo b-some-block__text">Элемент новостей</div>
</div>
```

Дополнительный блок может перехватить право быть блоком для вложенных элементов. Это можно сделать при помощи атрибута block="true".

Исходный код:

```
<b:time-period>
	<e:begin>
		<a:time block="true"/>
		<e:hour>08</e:hour><e:delimeter>:</e:delimeter><e:minutes>20</e:minutes>
	</e:begin>
	<e:delimeter><cdata><![CDATA[&#151;]]></cdata></e:delimeter>
	<e:end>
		<a:time block="true"/>
		<e:hour>09</e:hour><e:delimeter>:</e:delimeter><e:minutes>00</e:minutes>
	</e:end>
</b:time-period>
```

Результат:

```
<div class="b-time-period">
	<div class="b-time-period__begin b-time">
		<div class="b-time__hour">08</div><div class="b-time__delimeter">:</div><div class="b-time__minutes">20</div>
	</div>
	<div class="b-time-period__delimeter">&#151;</div>
	<div class="b-time-period__end b-time">
		<div class="b-time__hour">09</div><div class="b-time__delimeter">:</div><div class="b-time__minutes">00</div>
	</div>
</div>
```

### Контент

Всё, что является контентом заключается в CDATA области. В простейших случаях этого можно не делать – если в текстовом фрагменте нет спец. символов или контентной разметки.

Исходный код:

```
<b:product>
    <cdata>
        <![CDATA[
            Описание <strong>нового</strong> супер-продукта
        ]]>
    </cdata>
</b:product>
```

Результат:

```
<div class="b-product">
    Описание <strong>нового</strong> супер-продукта
</div>
```
