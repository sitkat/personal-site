---
name: js-jquery
description: JavaScript, jQuery и jQuery UI на страницах учебного сайта (ПР 2) — подключение библиотек с CDN, минимум 5 методов jQuery, минимум 2 компонента jQuery UI (виджет и плагин), обработка формы и меню. Использовать при написании js/script.js, добавлении интерактива, аккордеонов, вкладок, датапикеров, drag-and-drop.
---

# JavaScript, jQuery, jQuery UI

Весь скрипт — в `js/script.js`. Обработчики вешаются из кода, атрибуты
`onclick="..."` в разметке не использовать.

## Подключение (в конце `<body>`, порядок важен)

```html
  <link rel="stylesheet" href="https://code.jquery.com/ui/1.13.2/themes/base/jquery-ui.css">
  ...
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script src="https://code.jquery.com/ui/1.13.2/jquery-ui.min.js"></script>
  <script src="js/script.js"></script>
```

Сначала jQuery, потом jQuery UI, потом свой скрипт. Стили jQuery UI — в `<head>`.

## Обязательный чек-лист ПР 2

- [ ] минимум **5 разных методов jQuery**, каждый помечен комментарием
- [ ] минимум **2 компонента jQuery UI**: один виджет (`accordion`, `tabs`,
      `datepicker`, `dialog`, `slider`, `menu`, `progressbar`, `autocomplete`)
      и один плагин-взаимодействие (`draggable`, `droppable`, `resizable`,
      `selectable`, `sortable`) либо эффект (`.effect()`, `.toggle()` с эффектом)
- [ ] всё работает без ошибок в консоли браузера

Каждый использованный метод помечать комментарием — по ним собирается отчёт:

```js
// Метод 3: .toggleClass() — переключение класса подсветки
$(this).toggleClass('is-active');
```

## Каркас script.js

```js
// Метод 1: .ready() — код выполняется после построения DOM
$(function () {
  'use strict';

  // Метод 2: .addClass() — подсветка текущего пункта меню
  var page = location.pathname.split('/').pop() || 'index.html';
  $('.nav__link[href="' + page + '"]').addClass('nav__link--active');

  // Метод 3: .click() + .toggleClass() — сворачивание левой колонки
  $('#sidebar-toggle').click(function () {
    $('.sidebar--left').toggleClass('sidebar--hidden');
  });

  // Метод 4: .find() + .css() — подкрашиваем чётные строки таблицы
  $('.table').find('tr:even').css('background-color', '#eaf7ea');

  // Метод 5: .filter() + .append() — помечаем внешние ссылки
  $('a').filter('[href^="http"]').append(' ↗');

  // --- jQuery UI ---

  // Виджет: аккордеон в правой колонке
  $('#faq').accordion({ collapsible: true, heightStyle: 'content' });

  // Виджет: датапикер в форме
  $('#date').datepicker({ dateFormat: 'dd.mm.yy' });

  // Плагин-взаимодействие: перетаскиваемая карточка
  $('.card').draggable({ containment: 'parent' });
});
```

## Валидация формы (без отправки на сервер)

```js
$('.form').on('submit', function (event) {
  event.preventDefault();                       // отменяем отправку

  var $name = $('#name');
  if ($.trim($name.val()) === '') {
    $name.addClass('form__input--error').focus();
    $('#form-message').text('Введите имя').show();
    return;
  }

  $name.removeClass('form__input--error');
  $('#form-message').text('Спасибо, сообщение отправлено!').show();
  this.reset();
});
```

## Правила

- Селекторы кэшировать в переменные с `$` в имени: `var $menu = $('#main-menu');`.
- Классы состояния навешивать через jQuery, а описывать в `style.css`
  (`.is-active`, `.sidebar--hidden`) — не задавать оформление через `.css()`
  там, где хватает класса. Исключение — один-два демонстрационных `.css()`
  для отчёта.
- Разметку под jQuery UI делать по документации виджета (для `accordion` —
  чередование `h3` и `div`, для `tabs` — `ul` со ссылками на `#id` секций).
- Проверять консоль браузера: не должно быть ни ошибок, ни предупреждений
  «$ is not defined» (значит, порядок подключения нарушен).
- CDN-ссылки с точной версией, не `latest`.

Документация: https://html5css.ru/jquery/default.php, http://jquery.page2page.ru,
https://api.jqueryui.com/, https://learn.javascript.ru/

После выполнения ПР — написать отчёт по скиллу `pr-report`.
