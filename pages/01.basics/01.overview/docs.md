---
title: Что где лежит или файловая система
taxonomy:
    category: docs
---
Вместо предисловия.
Это моя попытка несколько структурировать почерпнутые из форумных бдений пути к файлам. Данный пост будет редактироваться, дополняться и стремиться стать расширением официальной документации :) Прошу тапками не кидать.
 
В теме приветствуются КОНСТРУКТИВНЫЕ посты. Тут бесполезно спрашивать "где лежит". Создайте отдельную тему, вам ответят. И вот ответ, можно и нужно написать сюда с кратким описанием. Как вариант кинуть мне в личку.
 
На всякий случай, если кто не знает:
 
```administrator/components/com_akeeba/backup```
  - тут лежат ваши бэкапы, при наличии приложения Akeeba ([https://www.akeebabackup.com/](https://www.akeebabackup.com/))
```/templates/template_name```
 - тут лежит ваш шаблон
[hr]
 
Везде далее * - это /media/zoo/applications/jbuniversal
 
**Шаблоны**
```*/templates/catalog/renderer/item```
 - тут создаются новые шаблоны (или редактируются уже существующие) для типов материала [sub](Product, blog, news etc.)[/sub], такие как **favorite, teaser, full и т.п.**
[Пошаговый урок](http://forum.jbzoo.com/topic/2591-kak-dobavit-novyj-shablon-k-tipu-materiala/)
[Ссылка на доку ](http://jbzoo.ru/docs/item-templates)
 

```/modules/mod_jbzoo_search/renderer/item/```
 - тут создаются новые шаблоны фильтров (или редактируются уже существующие), такие как **Inline, Table, 2columns etc.**
 
**Полезная статья про:**
[Настройка фильтров для существующего каталога JBZoo](http://forum.jbzoo.com/topic/2417-nastrojka-filtrov-dlya-suschestvuyuschego-kataloga/?hl=шаблоны+фильтров)
**Доки:**
[Описание JBZoo Search](http://joomla-book.ru/zoo-joomla-advanced-search)
[Основные параметры элементов фильтра](http://joomla-book.ru/jbzoo/jbzoo-filter)
[Документация по настройке полей и элементов от ZOO](http://www.yootheme.com/zoo/documentation?view=docs)
[Переиндексация базы данных](http://forum.jbzoo.com/topic/1976-)

```*\templates\catalog\renderer\category\```
- шаблон вывода категорий
```*/templates/catalog/renderer/comment/```
 - шаблоны комментариев
```*/templates/catalog/renderer/basket/_default.php```
 - шаблон вывода таблицы с товарами в корзине
```*/templates/catalog/renderer/item_columns/_default.php```
 - формирование колонок товаров 
```*\templates\*_TEMPLATE_*\renderer\basket-success\index.php```
- шаблон страницы создания заказа. "Ваш заказ успешно создан" - это оттуда. **ver 2.2**
```*/templates/*_TEMPLATE_*/renderer/payment_success/_default.php ```
- шаблон успешной оплаты **ver 2.2**
```*/templates/*_TEMPLATE_*/renderer/payment_fail/_default.php ```
- шаблон ошибки при оплате **ver 2.2**
  
**Письма**
```*/templates/catalog/renderer/item/order/```
 - шаблон письма заказа
```*/templates/catalog/mail.comment.admin.php```
- письмо админу о добавлении нового / редактировании существующего комментария
```*/templates/catalog/mail.comment.reply.php```
- письмо подписавшемуся на свой комментарий
```*/templates/catalog/mail.submission.new.php```
- письмо о добавлении нового материала
```/administrator/components/com_zoo/helpers/submission.php```
- тема письма о новом материале "New submission notification"
```/administrator/components/com_zoo/helpers/comment.php```
- тема письма о добавлении комментария"Topic reply notification"
 
**Письма для 2.2**
 
```media\zoo\applications\jbuniversal\templates-system\renderer\email\*Ваш шаблон*```
- шаблон письма, если не переопределено.
```media\zoo\applications\jbuniversal\framework\render```
В шаблоне почты $this ссылается на объект класса EmailRenderer. Рендереры JBZoo лежат в этой папке.

Цепочка такова - элемент sendemail нотификации(notificiation) создает renderer.
Renderer парсит шаблон(Позиции), обращаясь к нашим элементам - 
```media\zoo\applications\jbuniversal\cart-elements\email```
В свою очередь, от полученных данных они отображают или не отображают контент.

**Все остальное :)**
```*/jbuniversal/language/ru-RU```
 - языковые константы (т.е. Цена (за 1шт.) меняется тут)
```/language/ru-RU/ru-RU.com_zoo.ini ```
- языковые константы Zoo (если вы что-то не смогли найти в JBZoo, посмотрите тут)
```/components/com_zoo/renderer/element```
 - шаблоны стилей позиций:
block.php — элементы внутри блока div, блоку можно указать class.
comma.php — внутри тега span, так же можно указать класс.
default.php — без форматирования — в строку.
hyphen.php — строку, разделяя дефисом «-».
inline.php — строку, разделяя запятой «,».
list.php — списком — li.
paragraph.php — элементы абзацами.
pipe.php — строку, разделяя «|».
[Ссылка на доку](http://jbzoo.ru/docs/position-styles)
 
**Файлы из 2.2**
 
 

	1. **Блок "таблица с товарами"**
	```*/templates/catalog/renderer/basket/_form.php```
	*Стили:*
	```media/zoo/applications/jbuniversal/templates/uikit/assets/less ```
	[/*]
	1. ***Блок "поля заказа"***
	```*/templates/catalog/renderer/basket/_shipping.php```
	[/*]
	1. ***Блок "сервис доставки"***
	```*/templates/catalog/renderer/basket/_shipping.php```
	[/*]

***Блок "кнопки"***
```*/templates/catalog/renderer/basket/_buttons.php```
**Ошибка при создании заказа**
```*/templates/*_TEMPLATE_*/renderer/payment_fail/_default.php```
**Стили**
```*/assets/css/jbzoo.css```
 - основные стили каталога **ver. 2.1.5**
```*/assets/less```
 - стили каталога для **ver.** **2.2**
 
```/modules/mod_jbzoo_category/assets/styles.less```
 - стили категорий **ver.** **2.2**
 
```*/framework/helpers/jbmoney.php```
 - валюты **ver. 2.2**
```\media\zoo\applications\jbuniversal\templates\catalog\renderer\basket\_buttons.php```
- тут важна единственная строка: 
```<input type="submit" name="create" value="<?php echo JText::_('JBZOO_CART_SUBMIT'); ?>"class="jbbutton green big" />```
Переопределяем класс стилей кнопки намертво. **ver. 2.2**
 
**Изменение tab`ов в v.220-1**
```media/zoo/applications/jbuniversal/templates/uikit/renderer/item/full.php```
Менять в двух местах в файле!!! :) До кучи, если вставляем новый таб, не забудьте прописать его тут:  
```media/zoo/applications/jbuniversal/templates/uikit/renderer/item/positions.xml```
Стили по аналогии с существующими.
 
[hr]
 
**Полезно**
 
[ОЧЕНЬ очень полезный урок по настройке, верстке, uikit ](http://jbzooshop.ru/blog-o-jbzoo/30-kak-verstat-jbzoo)и вообще полезно для общего развития. Еще на эту же тему можно почитать [тут](http://forum.jbzoo.com/topic/8312-shablon-uikit-dlya-jbzoo-jbmarketplace/)
 
Чтобы у вас заработал фильтр по категориям (запомни, блин Женя!!) нужно вставить в шаблон фильтра поле Item Category (Текущая категория (скрытое поле), Простой) и включить в модуле "Зависимость от категории"
 
Импорт на сайт проходит ТОЛЬКО в кодировке utf-8 без BOM. Такое умеет [Open Office](https://www.openoffice.org/ru/)
[Дока по Импорту](http://jbzoo.ru/docs/import-csv-zoo) (очень хорошая дока, между прочим)
 
Очень-очень полезная тема про:
[CSS-фреймворки, гриды, скрипты, утилиты](http://forum.jbzoo.com/topic/9078-css-frejmvorki-gridy-skripty-utility-i-raznye-shtu/page-2#entry50718)... и за Pure Дмитрию огроменное спасибо, да :) Мои пять копеек [http://css-tricks.com/snippets/](http://css-tricks.com/snippets/)- всяко\разно фишки для html,javascript, css отобранные с демками. Прелесть в общем.
 
[Сервера, apache, php5](http://forum.jbzoo.com/topic/9957-nginx-php5-fpm/?p=56058) - полезно читать тем, у кого планируются большие нагрузки, большие выгрузки и т.п.
 
[Изменение стандартного профиля Joomla-пользователя](http://forum.jbzoo.com/topic/9804-izmenenie-standartnogo-profilya-polzovatelya-joomla/?hl=ru-ru) - инструкция по добавлению к профилю своих полей, которые будут работать с 
[JBZoo Userfields](http://forum.jbzoo.com/topic/9781-jbzoo-userfields-jbmarketplace/)
 
[Увеличение количества дополнительных параметров в Jbpriceadvance для версии 2.1.5](http://forum.jbzoo.com/topic/9361-uvelichenie-kolichestva-dop-parametrov-v-jbpriceadvance/?p=51981)
 
 
[УСПЕШНАЯ ОПЛАТА И СОЗДАНИЕ заказа ver. 2.2](http://forum.jbzoo.com/topic/10189-chto-gde-lezhit-ili-fajlovaya-sistema/?p=78024)
 
[hr]
[sub]На правах рекламы:[/sub]
[sub]В русском языке слова аккордЕон и инжЕнер пишутся с буквой Е.[/sub]
 
Тут будут находиться разнообразные полезные темы, по настройке, шаблонизации и т.п. (Постараюсь выкладывать сразу с кодом)
 
В версии 2.1.5 есть такая штука, что номера заказов идут не по порядку. То есть он может в общем списке выкинуть штук 20-30. Это нормально. :) "Четкая нумерация появилась в версии 2.2.0+" (с) SmetDenis
