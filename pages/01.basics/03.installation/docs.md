---
title: Популярые правки
taxonomy:
    category: docs
---

## Обрезается название айтема в фильтре при поиске


Т.к речь про автодополнение, то дополнительно к правке VARCHAR нужно изменить контроллер.

```media\zoo\applications\jbuniversal\framework\controllers\autocomplete.php```
Константа MAX_LENGTH

## Автоматическая генерация названий

```\media\zoo\applications\jbuniversal\templates\auto\assets\js\widget\namecreator.js```

```
/**
 * JBZoo App is universal Joomla CCK, application for YooTheme Zoo component
 *
 * @package     jbzoo
 * @version     2.x Pro
 * @author      JBZoo App http://jbzoo.com
 * @copyright   Copyright (C) JBZoo.com,  All rights reserved.
 * @license     http://jbzoo.com/license-pro.php JBZoo Licence
 * @coder       Sergey Kalistratov <kalistratov.s.m@jgmail.com>
 */
 
;
(function ($, window, document, undefined) {
 
    /**
     * NameCreator widget
     */
    JBZoo.widget('JBZoo.NameCreator', {
        'elResYear'  : '.jsNameYear',
        'elResColor' : '.jsNameColor',
        'elRestCity' : '.jsNameCity',
        'elRestCat'  : '.jsNameCat',
        'elCity'     : '#elements66f74b23-cd70-4f76-8a7e-a24412fad598option',
        'elYear'     : 'f83cbbe4-bb47-46f0-81cd-b885ae7a388e',
        'elColor'    : 'b8b4f50f-34ab-49f3-a56f-0e684d72a2f2',
        'elCategory' : '#elements_itemcategoryvalue',
        'elName'     : '_itemname'
    }, {
 
        init : function($this){
            $this.setupName($this);
        },
 
        /**
         * Setup name on submit form.
         *
         * @param $this
         */
        setupName : function($this) {
            $this.$('#submit-button').on('click', function (e) {
                $this._processCity($this);
                $this._processYear($this);
                $this._processColor($this);
                $this._processCategories($this);
 
                var itemName, category, color, year, city;
 
                category = $($this.options.elRestCat).text();
                year     = $($this.options.elResYear).text();
                color    = $($this.options.elResColor).text();
                city     = $($this.options.elRestCity).text();
 
                itemName = category + color + year + city;
 
                $('input[name*=' + $this.options.elName + ']').attr('value', itemName);
 
                setTimeout(function () {
                    document.submissionForm.submit();
                }, 200);
 
                e.preventDefault();
            });
        },
 
        /**
         * Find and set city value.
         *
         * @param $this
         * @private
         */
        _processCity : function ($this) {
            var city = $this.$($this.options.elCity + ' option:selected').text();
 
            //  Write city selected value.
            $($this.options.elRestCity).text(city);
        },
 
        /**
         * Find and ser color value.
         *
         * @param $this
         * @private
         */
        _processColor : function ($this) {
            var queryColor = 'input[name*=' + $this.options.elColor + ']';
            var color      = $this.$(queryColor + ':checked').val();
 
            //  Write color selected value.
            if (color) {
                $($this.options.elResColor).text(' (' + color + ')');
            }
        },
 
        /**
         * Find and set year.
         *
         * @param $this
         * @private
         */
        _processYear : function ($this) {
            //  Write year value.
            $($this.options.elResYear).text(' - ' +  $this.$('input[name*=' + $this.options.elYear + ']').val() + ', ');
        },
 
        /**
         * Find and set category values.
         *
         * @param $this
         * @private
         */
        _processCategories : function ($this) {
            var categoryName = '';
 
            $this.$($this.options.elCategory+ ' option:selected').each(function (index, value) {
 
                categoryName = categoryName + $this._clearStr($(this).html());
 
                if (index == 0) {
                    categoryName = categoryName + ' / ';
                }
 
            });
 
            $($this.options.elRestCat).text(categoryName);
        },
 
        /**
         * Clear string.
         *
         * @param str
         * @returns {*}
         * @private
         */
        _clearStr : function (str) {
            return str.replace(/(&nbsp;|\.&nbsp;|-&nbsp;)/g, '');
        }
 
    });
 
})(jQuery, window, document);
 
 ```
 
 ```
 И все-таки у меня не получается задать свои элементы формы, которые бы участвовали в автособирании названия. Если я подставлю ID элемента вместо elYear, то нормально. Но если я создаю свое, то не получамба. 
Новый метод который вы сделали по аналогу  _processYear добавьте в метод setupName, что бы он вызывался. В вашем случае необходимо добавить:


$this._processSn($this);

```

## Создание названии объявлений при подаче
 
``` Например, если взять строку "'elResYear'  : '.jsNameYear'" то elResYear - Это название в котором хранится jQuery объект (html).

Он выбирается с помощью селектора-класса jsNameYear из страницы. ```

 
Далее сборка имени происходит с помощью этого метода.

![image](https://user-images.githubusercontent.com/1074710/36245947-80cbecd2-123e-11e8-9983-ed7c52990cbe.png)

Т.е через функцию $.text() берется значение поле и объединяется через запятую прямо перед отправкой формы по кнопке #submit-button

Посмотрите шаблон сабмишен, там используется стиль позиции jbads, который и расставляет нужные классы у нужных полей.

``` jbuniversal\templates\auto\renderer\element\jbads.php```


## Убрать 0 в сервисе доставки

![image](https://user-images.githubusercontent.com/1074710/36245971-9a1d28d6-123e-11e8-91a2-fc3bfa39f5e0.png)

``` <?php
if ($element->identifier == 'element_id_1' || $element->identifier == 'element_id_2') {
echo 'по тарифам ТК';
} else {
echo $rate->html();
}
?>```

