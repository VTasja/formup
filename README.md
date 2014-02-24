
# FormUP 0.1

## О библиотеке

С помощью FormUP вы сможете создать форму которая будет иметь двунаправленную связь с моделью.
Форма создается на основании схемы. Любые изменения в полях формы приведут к изменению данных в моделе и наоборот.

## Сборка

Библиотека создавалась как пакет для NodeJS и для сборки требует чтобы вы сначала установили все необходимые пакеты.

```
# npm install
# node build.js
```

После данных команд вы получите файл lib/formup.min.js, который вы можете использовать на странице.

## Зависимости

Данная библиотека не требует указания каких либо явных зависимостей. Все что ей необходимо находится в библиотеке.
Формы собираются в формате Bootstrap 3 так что при его использовании вы сможете получать красивые формы.

## Использование

После подключения библиотеки на странице создается объект window.FormUP.
У данного объекта есть единственный метод create. Первый аргументом передается объект модели. Модель одноуровневая 
и не может содержать вложенных моделей.

```javascript
var model = {
    field1: 1234.55,
    field2: 'this is a text',
}
```

Поля создаются на основании схемы. Которая указывается вторым аргументом. На данный момент поддерживаются
только теги типа text. Схема задается объектом. Ключами объекта являются названия полей аналогичные 
названиям в модели. Значениями объекта являются объекты содержание параметры отображения данного поля.
Пока поддерживаются параметры label и order. В параметре label указывается текст тега label. В поле order
указывается число определяющее порядок следования полей в форме. Поля с меньшим значением order идут первыми.

```javascript
var schema = {
    field1: { order: 1, label: 'LABEL' },
    field2: { order: 3 }
}
```

Третьим аргументом указывается объект с дополнительными параметрами. Пока есть параметры: label, field и readonly.
Параметры label и field числовые. В них указывается размер полей label и поле ввода, соответственно. Номер в полях аралогичные размерам в Bootstrap.
Т.е. "label: 2" аналогично col-sm-2. Параметр readonly логический и если он равен true, то вместо полей ввода создаются
текстовые поля для просмотра содержимого модели.

Из метода create возвращается DOM элемент тега FORM, который вы можете поместить в любое место страницы.

## Пример

```javascript
var model = {
    field1: 111,
    field2: 'This is a test'
};

var schema = {
    field1: { order: 1, label: 'Age' },
    field2: { order: 2, label: 'Text' }
}

var el = FormUP.create(model,schema,{ label: 2, field: 10 });
```
