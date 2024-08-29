![alt text](image.png)

# Дата и время

**Встречайте новый встроенный объект: Date. Он содержит дату и время, а также предоставляет методы управления ими.**

**Например, его можно использовать для хранения времени создания/изменения, для измерения времени или просто для вывода текущей даты.**

### Создание
> Для создания нового объекта Date нужно вызвать конструктор ```new Date()``` с одним из следующих аргументов:

```new Date()```
**Без аргументов – создать объект Date с текущими датой и временем:**
```java
let now = new Date();
alert( now ); // показывает текущие дату и время
new Date(milliseconds)
```
***Создать объект Date с временем, равным количеству миллисекунд (тысячная доля секунды), прошедших с 1 января 1970 года UTC+0.***
```java
// 0 соответствует 01.01.1970 UTC+0
let Jan01_1970 = new Date(0);
alert( Jan01_1970 );

// теперь добавим 24 часа и получим 02.01.1970 UTC+0
let Jan02_1970 = new Date(24 * 3600 * 1000);
alert( Jan02_1970 );
```
**Целое число, представляющее собой количество миллисекунд, прошедших с начала 1970 года, называется таймстамп (англ. timestamp).**

**Это – легковесное численное представление даты. Из таймстампа всегда можно получить дату с помощью ``new Date(timestamp)`` и преобразовать существующий объект Date в таймстамп, используя метод ``date.getTime() (см. ниже).``**

**Датам до 1 января 1970 будут соответствовать отрицательные таймстампы, например:**
```java
// 31 декабря 1969 года
let Dec31_1969 = new Date(-24 * 3600 * 1000);
alert( Dec31_1969 );
new Date(datestring)
```
> Если аргумент всего один, и это строка, то из неё «прочитывается» дата. Алгоритм разбора – такой же, как в Date.parse, который мы рассмотрим позже.
```java
let date = new Date("2017-01-26");
alert(date);
```

>// Время не указано, поэтому оно ставится в полночь по Гринвичу и
// меняется в соответствии с часовым поясом места выполнения кода
// Так что в результате можно получить
// Thu Jan 26 2017 11:00:00 GMT+1100 (восточно-австралийское время)
// или
// Wed Jan 25 2017 16:00:00 GMT-0800 (тихоокеанское время)
new Date(year, month, date, hours, minutes, seconds, ms)
Создать объект Date с заданными компонентами в местном часовом поясе. Обязательны только первые два аргумента.

### Year должен состоять из четырёх цифр. Для совместимости также принимаются 2 цифры и рассматриваются как 19xx, к примеру, 98 здесь это тоже самое, что и 1998, но настоятельно рекомендуется всегда использовать 4 цифры.
**month начинается с 0 (январь) по 11 (декабрь).
Параметр date здесь представляет собой день месяца. Если параметр не задан, то принимается значение 1.
Если параметры hours/minutes/seconds/ms отсутствуют, их значением становится 0.
Например:**
```java
new Date(2011, 0, 1, 0, 0, 0, 0); // // 1 Jan 2011, 00:00:00
new Date(2011, 0, 1); // то же самое, так как часы и проч. равны 0
Максимальная точность – 1 мс (до 1/1000 секунды):

let date = new Date(2011, 0, 1, 2, 3, 4, 567);
alert( date ); // 1.01.2011, 02:03:04.567
```
Получение компонентов даты

**Существуют методы получения года, месяца и т.д. из объекта ``Date``:**

> getFullYear()
Получить год (4 цифры)
getMonth()
Получить месяц, от 0 до 11.
getDate()
Получить день месяца, от 1 до 31, что несколько противоречит названию метода.
getHours(), getMinutes(), getSeconds(), getMilliseconds()
Получить, соответственно, часы, минуты, секунды или миллисекунды.
Никакого getYear(). Только getFullYear()
Многие интерпретаторы JavaScript реализуют нестандартный и устаревший метод getYear(), который порой возвращает год в виде двух цифр. Пожалуйста, обходите его стороной. Если нужно значение года, используйте getFullYear().

## Кроме того, можно получить определённый день недели:

>**getDay()**
>
>Вернуть день недели от 0 (воскресенье) до 6 (суббота). Несмотря на то, что в ряде стран за первый день недели принят понедельник, в JavaScript начало недели приходится на воскресенье.
Все вышеперечисленные методы возвращают значения в соответствии с местным часовым поясом.

Однако существуют и их UTC-варианты, возвращающие день, месяц, год для временной зоны UTC+0: getUTCFullYear(), getUTCMonth(), getUTCDay(). Для их использования требуется после "get" подставить "UTC".

Если ваш местный часовой пояс смещён относительно UTC, то следующий код покажет разные часы:

// текущая дата
let date = new Date();

// час в вашем текущем часовом поясе
alert( date.getHours() );

// час в часовом поясе UTC+0 (лондонское время без перехода на летнее время)
alert( date.getUTCHours() );
Помимо вышеприведённых методов, существуют два особых метода без UTC-варианта:

getTime()
Для заданной даты возвращает таймстамп – количество миллисекунд, прошедших с 1 января 1970 года UTC+0.

getTimezoneOffset()
Возвращает разницу в минутах между UTC и местным часовым поясом:

// если вы в часовом поясе UTC-1, то выводится 60
// если вы в часовом поясе UTC+3, выводится -180
alert( new Date().getTimezoneOffset() );
Установка компонентов даты
Следующие методы позволяют установить компоненты даты и времени:
```java
setFullYear(year, [month], [date])
setMonth(month, [date])
setDate(date)
setHours(hour, [min], [sec], [ms])
setMinutes(min, [sec], [ms])
setSeconds(sec, [ms])
setMilliseconds(ms)
setTime(milliseconds) (устанавливает дату в виде целого количества миллисекунд, прошедших с 01.01.1970 UTC)
У всех этих методов, кроме setTime(), есть UTC-вариант, например: setUTCHours().
```
> Как мы видим, некоторые методы могут устанавливать сразу несколько компонентов даты, например: setHours. Если какая-то компонента не указана, она не меняется.

**Пример:**

```let today = new Date();```
```java
today.setHours(0);
alert(today); // выводится сегодняшняя дата, но значение часа будет 0

today.setHours(0, 0, 0, 0);
alert(today); // всё ещё выводится сегодняшняя дата, но время будет ровно 00:00:00.
```
# Автоисправление даты

**Автоисправление – это очень полезная особенность объектов Date. Можно устанавливать компоненты даты вне обычного диапазона значений, а объект сам себя исправит.**

## Пример:
```java
let date = new Date(2013, 0, 32); // 32 Jan 2013 ?!?
alert(date); // ...1st Feb 2013!
Неправильные компоненты даты автоматически распределяются по остальным.

Предположим, нам требуется увеличить дату «28 февраля 2016» на два дня. В зависимости от того, високосный это год или нет, результатом будет «2 марта» или «1 марта». Нам об этом думать не нужно. Просто прибавляем два дня. Объект Date позаботится об остальном:

let date = new Date(2016, 1, 28);
date.setDate(date.getDate() + 2);

alert( date ); // 1 Mar 2016
Эту возможность часто используют, чтобы получить дату по прошествии заданного отрезка времени. Например, получим дату «спустя 70 секунд с текущего момента»:

let date = new Date();
date.setSeconds(date.getSeconds() + 70);

alert( date ); // выводит правильную дату
Также можно установить нулевые или даже отрицательные значения. Например:

let date = new Date(2016, 0, 2); // 2 Jan 2016

date.setDate(1); // задать первое число месяца
alert( date );

date.setDate(0); // первый день месяца -- это 1, так что выводится последнее число предыдущего месяца
alert( date ); // 31 Dec 2015
```
