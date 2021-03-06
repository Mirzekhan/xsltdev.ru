# Подключение файлов в PHP

В PHP есть поддержка вызова одного сценария из другого. С помощью специальной конструкции языка можно вызвать сценарий из отдельного файла по его имени, также как по имени вызываются функции. Такая способность называется подключением файлов. Причём таковым файлом может являться как php-сценарий, так и любой другой текстовый файл. Например, HTML-страница.

## Зачем разделять и подключать php-сценарии

PHP-разработчики дробят весь исходный код проекта на отдельные сценарии, чтобы с ними проще было работать. Если бы пришлось писать весь код в одном файле, то такой сценарий стал бы просто необъятным и ориентироваться там стало решительно невозможно. Поэтому разделение кода на разные сценарии — это естественный способ бороться со сложностью.

Есть и ещё один положительный эффект от подобного деления. Если вынести повторяющиеся блоки кода в отдельные сценарии, то появится возможность повторно использовать один код в разных файлах и подключать его только по требованию. Хороший пример — это пользовательские функции. Очень удобно объявлять их в отдельном сценарии, а затем подключать там, где эти функции понадобятся.

## Способы подключения файлов

Для подключения файлов в PHP есть две языковых конструкции: `require` и `require_once`. Чем же они отличаются? На самом деле, отличия между ними минимальны. Оба этих ключевых слова подключают файл с указанным именем и вызывают ошибку, если данный файл не существует.

Однако особенность работы `require_once` состоит в том, что файл будет подключен только один раз, даже если вызвать эту инструкцию несколько раз с одним именем файла.

### Примеры подключения файлов

Для начала посмотрим, как просто подключить один сценарий внутри другого. Для этого воспользуемся инструкцией `require`. Предположим, у нас есть два сценария: `index.php` и `sub.php`.

Содержимое файла `sub.php`:

```php
<?php
print("Привет, я содержимое из sub.php!" . PHP_EOL);
```

В файле `index.php` находится код, который подключит сценарий `sub.php`:

```php
<?php
require 'sub.php';
print("А я - index.php!" . PHP_EOL);
```

Интересный факт: `require` можно использовать как ключевое слово, либо как функцию.

Результат будет одним и тем же:

```php
<?php
require('sub.php'); // использование как функции
print("А я - index.php!" . PHP_EOL);
```

Результат работы:

```
Привет, я содержимое из sub.php!
А я - index.php!
```

Что произошло? Два сценария как бы склеились в один: выполнилось все содержимое `sub.php` и добавилось в начало сценария `index.php`.

## Абсолютные и относительные пути

При подключении файла в качестве его адреса можно указывать абсолютный или относительный путь.

Абсолютный путь включает в себя полный адрес файла от корня диска.

Пример: `/var/www/web/site/inc/sub.php`

Относительный путь содержит адрес только относительно текущей рабочей директории. Так если сценарий лежит в папке `/var/www/web/site`, то для подключения файла можно использовать такой путь: `inc/sub.php`

Всегда предпочитай указывать относительные пути, чтобы сайт продолжал работать, если его переместят в другую папку.

### Полезные константы

В PHP есть полезные встроенные константы, которые пригодятся для использования в пути к подключаемым файла.

- `__DIR__` — Полный путь к директории, в которой находится текущий сценарий
- `__FILE__` — Полный путь к текущему сценарию

## Видимость переменных в подключаемых сценариях

Следует помнить, что так как подключение файлов — это просто их склеивание в один, то и все переменные в разных сценариях тоже получают общую область видимости.

В PHP нет системы модулей, которая существует в других языках программирования (Python, Java, ECMAScript 6). Невозможно «импортировать» только отдельные переменные или функции из подключаемого сценария.

Из этого также следует, что если подключить один сценарий дважды, то переменные и функции из него тоже обьявятся повторно, а это может вызывать ошибку. Поэтому используйте `require_once`, чтобы такого не произошло.
