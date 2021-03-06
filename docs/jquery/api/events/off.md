# .off()

Метод **`.off()`** позволяет удалить обработчик, или обработчики событий, присоединенные методом [`.on()`](on.md).

## Синтаксис

Синтаксис 1.7:

```js
$(selector).off() // метод используется без параметров
$(selector).off(event)
```

- `event` - `jQuery.Event Object`

```js
$(selector).off(events, selector)
```

- `events` - `PlainObject`
- `selector` - `String` // необязательный параметр

```js
$( selector ).off( events, selector, handler( Event eventObject ) )
```

- `events` - `String`
- `selector` - `String` // необязательный параметр
- `handler` - `Function( Event eventObject )` // необязательный параметр

Метод `.off()`, вызванный без параметров удаляет все обработчики, присоединенные к элементу или элементам. Определенные обработчики событий могут быть удалены для элементов путем предоставления комбинаций имен событий, пространств имен, селекторов или имен функций обработчика. Если задано несколько аргументов фильтрации, все предоставленные аргументы должны совпадать для удаления обработчика событий.

Если указано простое имя события, например "`click`", то все события этого типа (как прямые, так и делегированные) удаляются из элементов набора совпавших элементов jQuery. Более подробную информацию об этих событиях вы можете прочитать в описании метода `.on()`.

При написании кода, который будет использоваться в качестве плагина, или просто при работе с большим объемом кода, рекомендуется присоединять и удалять события с помощью пространств имен, чтобы избежать ситуации, когда код случайно удаляет обработчики событий, присоединенные другим кодом. Все события всех типов в определенном пространстве имен можно удалить из элемента, предоставив только пространство имен, например "`.myNamespace`". В обязательном порядке должно быть хотя бы указано пространство имен или имя события.

Чтобы удалить определенные обработчики делегированных событий, укажите строковый параметр `selector`, при этом он должен точно соответствовать значению переданному методу `.on()`, когда был присоединен обработчик событий. Чтобы удалить все делегированные события у элемента без удаления прямых событий, используйте специальное значение "`**`".

Обработчик событий также могут быть удалены с использованием функции, переданной в качестве параметра метода `.off()`. Когда jQuery присоединяет обработчик событий, он присваивает уникальный идентификатор функции обработчика. Обработчики на которых был вызван метод [`$.proxy()`](jquery.proxy.md), или подобные механизмы будут иметь одинаковый уникальный идентификатор, поэтому передавать такие обработчики методу `.off()` не имеет смысла, так как это может привести к ошибкам в ходе которых могут быть удалены те обработчики, удаление которых не предполагалось. В таких ситуациях лучше присоединять и удалять обработчики событий с помощью пространств имен.

Добавлен в версии jQuery 1.7

## Параметры

`event`
: Объект события `jQuery.Event`. jQuery скрывает различия реализации между браузерами, определяя свой собственный объект события. Большинство свойств исходного события копируются и нормализуются в новый объект события.

`events`
: В качестве значения параметра используется либо строковое значение, либо объект.

: Когда значение передается в виде строки, то необходимо указывать один или несколько типов событий, разделенных пробелами, дополнительно допускается указать пространство имен для события или просто пространство имен (например, "`click`", "`click dblclick`", "`click.myNamespace`" или "`.myNamespace`".

: Когда значение передается в виде объекта, то его строковые ключи должны соответствовать одному или нескольким разделенных пробелами типов событий (при необходимости пространств имен), а значения представляют функции обработчика, ранее присоединенные для этих событий (например, `{"click": myFunction, "dblclick.myNamespace": myFunction2}`).

`selector`
: Строка селектор, которая должна соответствовать той, которая первоначально передана методу `.on()` для присоединения обработчика, или обработчиков событий. Используется для удаления определенных обработчиков делегированных событий. Специальное значение "`**`" позволяет удалить все делегированные события у элемента, при этом прямые события не удаляются. Необязательный параметр.

`handler`
: Функция обработчика, которая ранее была присоединена к событию (событиям), или специальное значение `false`. Необязательный параметр.

## Пример

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Использование jQuery метода .off()</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
    <script>
      $(document).ready(function () {
        $('.addEvent').click(function () {
          // задаем функцию при нажатиии на элемент с классом addEvent
          $('.increaseWidth').on('click dblclick', function () {
            // присоединяем элементу обработчик события "click" и "dblclick"
            $('p').width(function (index, currentValue) {
              // увеличиваем значение ширины элемента на 50 пикселей
              return currentValue + 50
            })
          })
        })
        $('.removeEvent').click(function () {
          // задаем функцию при нажатиии на элемент с классом removeEvent
          // удаляем обработчик события "click", присоединенный методом .on()
          $('.increaseWidth').off('click')
        })
      })
    </script>
  </head>
  <body>
    <button class="increaseWidth">Увеличить ширину</button>
    <button class="addEvent">on</button>
    <button class="removeEvent">off</button>
    <div style="width:50px; height:50px; background: blue"></div>
  </body>
</html>
```

В этом примере с использованием метода `.click()` мы задаем функции при нажатии на элемент с классом `addEvent` и `removeEvent`.

При нажатии на элемент с классом `addEvent` мы с помощью метода `.on()` приcоединяем для элемента с классом `increaseWidth` функцию обработчика событий "`click`" и "`dblclick`", которая с помощью метода `.width()` и функции, переданной в качестве параметра этого метода увеличивает ширину элемента `<div>` прибавляя к текущему значению ширины элемента 50 пикселей.

При нажатии на элемент с классом `removeEvent` мы с помощью метода `.off()` удаляем обработчик события "`click`" у элемента с классом `increaseWidth`, присоединенный методом `.on()`. Обратите внимание, что обработчик события "`dblclick`" мы при этом не удаляем. Для удаления всех обработчиков событий достаточно было вызвать метод `.off()` без параметров.

Результат:

![Пример использования метода .off()](729.png)

Пример использования метода `.off()`
