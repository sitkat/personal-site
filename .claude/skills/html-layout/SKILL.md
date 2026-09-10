---
name: html-layout
description: Вёрстка HTML-страниц учебного персонального сайта (ПР 1.1) — базовая структура документа, блочный макет «шапка / меню / две колонки / подвал», обязательные элементы страницы (заголовок, текст, изображение, ссылка, список, таблица, форма). Использовать при создании новых страниц, правке разметки, добавлении форм и таблиц.
---

# Вёрстка HTML

## Обязательный чек-лист страницы (требование ПР 1.1)

На **каждой** странице сайта должны быть:

- [ ] `<title>` — свой, осмысленный, вида «Раздел — Фамилия И. О.»
- [ ] заголовок (`<h1>`, ниже по иерархии `<h2>`/`<h3>`)
- [ ] текст (`<p>`)
- [ ] изображение (`<img>` с `alt`)
- [ ] ссылка на другую страницу этого же сайта
- [ ] список (`<ul>`/`<ol>`)
- [ ] таблица (`<table>`)
- [ ] форма (`<form>`)

Меню сайта — это список `<ul>` внутри `<nav>`; оно же и есть «список», который
на этапах CSS и JS превращается в меню. Но на странице должен быть ещё
содержательный список в контенте, а не только навигация.

## Скелет страницы

```html
<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Главная — Иванов И. И.</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <header class="header">
    <h1>Иванов Иван Иванович</h1>
    <p class="header__subtitle">Студент, веб-разработчик</p>
  </header>

  <nav class="nav">
    <ul class="nav__list">
      <li class="nav__item"><a class="nav__link" href="index.html">Главная</a></li>
      <li class="nav__item"><a class="nav__link" href="sitemap.html">Карта сайта</a></li>
      <li class="nav__item"><a class="nav__link" href="about.html">О себе</a></li>
      <li class="nav__item"><a class="nav__link" href="services.html">Услуги</a></li>
      <li class="nav__item"><a class="nav__link" href="contacts.html">Контакты</a></li>
    </ul>
  </nav>

  <div class="layout">
    <aside class="sidebar sidebar--left">
      <h3>Левая колонка</h3>
    </aside>

    <main class="content">
      <h2>Заголовок раздела</h2>
      <p>Текст страницы.</p>
    </main>

    <aside class="sidebar sidebar--right">
      <h3>Правая колонка</h3>
    </aside>
  </div>

  <footer class="footer">
    <p>&copy; 2026 Иванов И. И.</p>
  </footer>

  <script src="js/script.js"></script>
</body>
</html>
```

Порядок блоков в `body` фиксирован: `header` → `nav` → `.layout` (левая колонка,
контент, правая колонка) → `footer`. Он одинаков на всех страницах — меняется
только содержимое `main` и активный пункт меню (`class="nav__link nav__link--active"`).

## Правила

- Семантические теги: `header`, `nav`, `main`, `aside`, `footer`, `section`,
  `figure`/`figcaption`. Не заменять их на `div` где подходит семантика.
- Классы — латиницей, в стиле БЭМ (`block__element--modifier`), как в примере выше.
- `id` — только там, где элемент действительно один и к нему обращаются из JS или
  по якорю.
- Изображения — в `img/`, обязательно `alt`, ширину/высоту задавать в CSS.
- Ссылки между страницами — относительные (`about.html`), без `../` и абсолютных путей.
- Кодировка UTF-8, отступ 2 пробела, атрибуты в двойных кавычках.
- Никаких `style="..."` и `onclick="..."` в разметке.

## Таблица

```html
<table class="table">
  <caption>Расписание консультаций</caption>
  <thead>
    <tr><th>День</th><th>Время</th><th>Аудитория</th></tr>
  </thead>
  <tbody>
    <tr><td>Понедельник</td><td>10:00–12:00</td><td>301</td></tr>
    <tr><td>Четверг</td><td>14:00–16:00</td><td>412</td></tr>
  </tbody>
</table>
```

Обязательно `caption`, `thead`/`tbody`, заголовки через `th`.

## Форма

```html
<form class="form" action="#" method="post">
  <fieldset>
    <legend>Обратная связь</legend>

    <p class="form__row">
      <label class="form__label" for="name">Имя</label>
      <input class="form__input" type="text" id="name" name="name" required
             placeholder="Как вас зовут">
    </p>

    <p class="form__row">
      <label class="form__label" for="email">E-mail</label>
      <input class="form__input" type="email" id="email" name="email" required>
    </p>

    <p class="form__row">
      <label class="form__label" for="topic">Тема</label>
      <select class="form__input" id="topic" name="topic">
        <option value="order">Заказ</option>
        <option value="question">Вопрос</option>
      </select>
    </p>

    <p class="form__row">
      <label class="form__label" for="message">Сообщение</label>
      <textarea class="form__input" id="message" name="message" rows="5"></textarea>
    </p>

    <p class="form__row">
      <label><input type="checkbox" name="agree" checked> Согласен на обработку данных</label>
    </p>

    <p class="form__row">
      <button class="button" type="submit">Отправить</button>
      <button class="button button--ghost" type="reset">Очистить</button>
    </p>
  </fieldset>
</form>
```

Каждому полю — свой `label` с `for`, привязанным к `id` поля. Использовать типы
HTML5 (`email`, `tel`, `date`, `number`) и атрибуты `required`, `placeholder`.

## Проверка перед сдачей

1. Пройтись по чек-листу выше на каждой странице.
2. Открыть страницы в браузере, проверить, что все ссылки меню работают.
3. Проверить, что нет битых картинок и незакрытых тегов
   (`grep -c '<div' file.html` против `grep -c '</div>' file.html`).
4. Валидация: https://validator.w3.org/

После выполнения ПР — написать отчёт по скиллу `pr-report`.
