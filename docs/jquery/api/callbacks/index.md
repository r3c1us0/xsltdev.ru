# Callbacks

Начиная с версии jQuery 1.7 была представлена функция `$.Callbacks()`, она возвращает многоцелевой объект **Callbacks**, который обеспечивает мощный способ управления списками обратного вызова. Другими словами фабричная функция `$.Callbacks()` создает экземпляр объекта Callbacks.

Объект Callbacks поддерживает добавление, удаление, запуск и отключение обратных вызовов, в настоящее время этот объект используется внутри такой популярной функции как `$.ajax()` и объекта [`Deferred`](../deferred/index.md). Объект Callbacks подходит, например, для того, чтобы определить функциональность для новых компонентов.

После создания объекта Callbacks можно использовать любой из приведенных ниже методов, связывая его непосредственно с объектом, либо сохраняя объект в отдельной переменной и вызывая один или несколько методов для этой переменной.

## Синтаксис

```js
// без параметра
let myCallbacksObject = $.Callbacks()

// с указанием одного, или нескольких строковых значений (флагов)
let myCallbacksObject = $.Callbacks(flag)
let myCallbacksObject = $.Callbacks(flag, flag)
```

flag - String

## Значения

`flags`
: Необязательное строковое значение, или список разделенных пробелами строковых значений (флагов), которые изменяют поведение списка обратного вызова.

Возможные значения флагов:

- `once` - гарантирует, что список обратного вызова может быть запущен только один раз (как и объект `Deferred`).
- `memory` - отслеживает предыдущие значения и вызовет любой обратный вызов, добавленный после того как список обратного вызова был вызван с последними "запомненными" значениями (как и объект `Deferred`).
- `unique` - гарантирует, что конкретный обратный вызов может быть добавлен в список обратных вызовов только один раз (поэтому в списке нет дубликатов).
- `stopOnFalse` - прерывает вызовы, когда один из обратных вызов возвращает значение `false`.

По умолчанию, список обратного вызова будет действовать как список обратного вызова определенного события, и может быть вызван несколько раз.

Более подробную информацию и примеры использования вы можете получить в описании функции `$.Callbacks()`.

## Методы объекта `Callbacks` и функция `$.Callbacks()`

`$.Callbacks()`
: Фабричная функция, которая возвращает многоцелевой объект (Callbacks), который обеспечивает мощный способ управления списками обратного вызова.

`callbacks.add()`
: Добаляет функцию, или массив функций обратного вызова в список обратных вызовов объекта.

`callbacks.disable()`
: Позволяет отключить список обратных вызовов от выполнения чего-либо еще.

`callbacks.disabled()`
: Возвращает логическое значение, которое указывает на то, был ли отключен список обратных вызовов, или нет.

`callbacks.empty()`
: Удаляет все функции обратного вызова из списка обратных вызовов объекта.

`callbacks.fire()`
: Вызывает все ранее добавленные функции обратного вызова с заданными аргументами.

`callbacks.fired()`
: Возвращает логическое значение, которое определяет вызывались ли обратные вызовы объекта по крайней мере один раз.

`callbacks.fireWith()`
: Вызывает все ранее добавленные функции обратного вызова с заданным контекстом и аргументами.

`callbacks.has()`
: Возвращает логическое значение, которое определяет имеются ли в списке подключенные функции обратного вызова, или конкретная функция обратного вызова.

`callbacks.lock()`
: Позволяет заблокировать список обратных вызовов в текущем состоянии.

`callbacks.locked()`
: Возвращает логическое значение, которое указывает на то, заблокирован ли список обратных вызовов, или нет.

`callbacks.remove()`
: Удаляет функцию, или несколько функций обратного вызова из списка обратных вызовов объекта.