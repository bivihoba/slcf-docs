BEMXML
=========

BEMXML – XML-формат для БЭМ.

## Синтаксис

### Блок

Блок задается тегом в пространстве имен "b:"

Исходный код:

```
<b:logo>Блок логотипа</b:logo>
```

Результат:

```
<div class="b-logo">Блок логотипа</div>
```


### Элемент

Элемент блока задается тегом в пространстве имен "e:"

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

Для элемента, блоком по умолчанию является ближайший узел блока выше по дереву. Можно задать элементу произвольный блок, используя атрибут block.

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

В сложных БЭМ-деревьях какой-нибудь отдельный блок может мешать наследованию "блочности" для элементов другого блока, стоящего выше по дереву. В такой ситуации логично исключить мешающий блок из потока возможных "родителей". Это можно сделать с помощью атрибута noblock.

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

### Модификатор

Модификатор задается пустым тегом в пространстве имен "m:".
Имя модификатора задается тегом, а значение – атрибутом val.

Модификатор всегда применяется к родительскому узлу в БЭМ-дереве. Количество модификаторов не ограничено.

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

### Дополнительная (дополняющая) сущность

Одному узлу дерева может соответствовать несколько БЭМ-сущностей. Сущности, которые добавляются на узел, называются дополнительными. Дополнительной сущностью может быть блок или элемент, которые, в свою очередь, могут иметь свои модификаторы.

Дополнительная сущность задается тегом в пространстве имен "a:".
По умолчанию дополнительная сущность это блок. Примешивая элемент, нужно указать на это, задав для него блок через атрибут block-of.

Дополнительная сущность всегда добавляется к родительскому узлу в БЭМ-дереве. Количество дополнительных сущностей не ограничено.

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

Блок, являющийся дополнительной сущностью, не оказывает влияния на элементы, которые вложены в тот же узел. Элементы будут искать родительский блок выше по дереву. Чтобы стать участником цепочки возможных родителей, дополнительному блоку нужно добавить атрибут block="true". В этом случае он становится родительским блоком для всех элементов вложенных в тот же узел, что и он сам, пока внутри не появится другой блок.

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

Контент должен заключаться в тег cdata и CDATA область. В простых случаях, если в текстовом фрагменте нет спец. символов или разметки, этого можно не делать.

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

### НеБЭМ-классы

Использование CSS-классов вне БЭМ-поля не поощряется, но иногда необходимость в этом все-таки возникает.
Для таких случаем предусмотрена возможность навесить класс как дополнительную сущность, через пространство имен "alxc:".


Исходный код:

```
<b:control>
    <alxc:select-2>
</b:control>
```

Результат:

```
<div class="b-control select-2"></div>
```