---
description: О выборе версии PHP и тонкостях неявного преобразования типов.
---

# Какую версию PHP использовать?

Функциональный стиль можно использовать с версии _5.3_, когда появился класс `Closure`. Но лучше использовать _PHP7_, он быстрее, современнее и позволяет _типизировать_ данные.

_PHP_, являясь динамическим языком, всегда пытается конвертировать значения неверного типа данных к ожидаемому скалярному типу.

```php
<?php
function increment($i) {
  return ++$i;
}
echo increment('a'); //выведет b
```

Подобного неявного приведения аргументов можно избежать включив режим строгого типирования, указав вверху файла:

```php
<?php
declare(strict_types = 1);
```
