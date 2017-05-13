# gitrunner

[![Quality Gate](https://sonar.silverbulleters.org/api/badges/gate?key=gitrunner)](https://sonar.silverbulleters.org/component_measures/?id=gitrunner)
[![Quality Gate](https://sonar.silverbulleters.org/api/badges/measure?key=gitrunner&metric=coverage&blinking=true)](https://sonar.silverbulleters.org/component_measures/?id=gitrunner)

## Библиотека для упрощения работы с git из oscript.

Позволяет выполнять рутинные операции с репозиторием в стиле [v8runner](https://github.com/oscript-library/v8runner).

Пример работы:
```bsl
ГитРепозиторий = Новый ГитРепозиторий();
ГитРепозиторий.УстановитьРабочийКаталог(КаталогРепозитория);

ГитРепозиторий.УстановитьНастройку("core.quotePath", "true", РежимУстановкиНастроекGit.Локально);

ГитРепозиторий.ДобавитьВнешнийРепозиторий("origin", ПутьКВнешнемуРепозиторию);

ГитРепозиторий.ПерейтиВВетку("master");
ГитРепозиторий.Получить();

ГитРепозиторий.ОбновитьПодмодули(Истина, Истина);
```

Так же описание функциональности содержится в папке `features`. В прилагающихся `step_definitions` можно подсмотреть больше примеров.

## Публичный интерфейс

### Класс ГитРепозиторий:

> Работа со свойствами объекта ГитРепозиторий

#### УстановитьРабочийКаталог
```bsl
// Установить текущий рабочий каталог.
// Все команды git будут выполняться относительно указанного каталога.
//
// Параметры:
//   ПутьРабочийКаталог - Строка - Путь к рабочему каталогу.
//		Может быть относительным.
//
```

#### ПолучитьРабочийКаталог
```bsl
// Получить текущий рабочий каталог.
//
//  Возвращаемое значение:
//   Строка - Путь к рабочему каталогу
//
```

#### ПолучитьПутьКГит
```bsl
// Получить путь к исполняемому файлу git.
//
//  Возвращаемое значение:
//   Строка - Путь к исполняемому файлу.
//		По умолчанию содержит значение "git".
//
```

#### УстановитьПутьКГит
```bsl
// Установить путь к исполняемому файлу git.
//
// Параметры:
//   Путь - Строка - Путь к исполняемому файлу.
//
```

#### ПолучитьВыводКоманды
```bsl
// Получить вывод последней выполненной команды.
//
//  Возвращаемое значение:
//   Строка - Вывод команды
//
```

> Общие команды git

#### Инициализировать
```bsl
// Выполняет инициализиацию репозитория в рабочем каталоге
// git init
//
```

#### Статус
```bsl
// Получает состояние репозитория
// git status
//
//  Возвращаемое значение:
//   Строка   - Вывод команды
//
```

#### ДобавитьФайлВИндекс
```bsl
// Добавляет файл в индекс git
// git add
//
// Параметры:
//   ПутьКДобавляемомуФайлу - Строка - Путь к файлу на диске
//
```

#### Закоммитить
```bsl
// Зафиксировать проиндексированные изменения в истории git
// git commit
//
// Параметры:
//   ТекстСообщения - Строка - Текст сообщения коммита (-m ТекстСообщения)
//   ПроиндексироватьОтслеживаемыеФайлы - Булево - Автоматически добавить
//     в индекс файлы, уже отслеживаемые git (-a)
//   ПутьКФайлуКоммита - Строка - путь к файлу с текстом комментария (-F ПутьКФайлуСтекстомКоммита)
//   АвторКоммита - Строка - Автор комментария, передается в случае необходимости (--author=АвторКоммита)
//   ДатаАвтораКоммита - Дата - Дата комментария (--date=ДатаАвтораКоммита)
//   Коммитер - Строка - Коммитер комментария, передается в случае, если требуется
//   ДатаКоммита - Дата - Дата произведения коммита
//
```

#### ВывестиИсторию
```bsl
// Вывести историю репозитория
// git log
//
// Параметры:
//   Графически - Булево - Вывести историю в виде графа (--graph)
//
```

#### Получить
```bsl
// Получить изменения из удаленного репозитория
// git pull
//
// Параметры:
//   ИмяРепозитория - Строка - Имя репозитория, из которого необходимо
// 		получить изменения
//   ИмяВетки - Строка - Имя ветки, из которой необходимо получить изменения
//
```

#### Отправить
```bsl
// git push
//
// Параметры:
//   ИмяРепозитория - Строка - Имя репозитория, в который необходимо
// 		отправить изменения
//   ИмяВетки - Строка - Имя ветки, в который необходимо отправить изменения
//   ПерезаписатьИсторию - Булево - Флаг отправки с перезаписью истории (--force)
//
```

#### УстановитьНастройкиРежимаОтправки
```bsl
// Установить настройки отправки изменений.
// Позволяет произвести тонкую настройку необходимых флагов команды отправки изменений
//
// Параметры:
//   НастройкиРежимаОтправки - НастройкиРежимаОтправкиGit - инстанс класса НастройкиРежимаОтправкиGit с необходимыми
//                                                          настройками
//
```

#### КлонироватьРепозиторий
```bsl
// git clone
//
// Параметры:
//   ПутьУдаленномуРепозиторию - Строка - Путь к удаленному репозиторию
//   КаталогКлонирования - Строка - Каталог, в который необходимо выполнить
//		клонирование
//
```

> Работа с ветками

#### ПолучитьТекущуюВетку
```bsl
// Получить имя текущей ветки
//
//  Возвращаемое значение:
//   Строка   - Имя текущей ветки
//
```

#### ПерейтиВВетку
```bsl
// Выполнить переход в ветку
// git checkout
//
// Параметры:
//   ИмяВетки - Строка - Имя ветки, в которую необходимо перейти
//   СоздатьНовую - Булево - Флаг необходимости создания новой ветки (-b)
//
// @unstable
//
```

#### СоздатьВетку
```bsl
// Создать новую ветку без выполнения перехода в нее
// git branch
//
// Параметры:
//   ИмяВетки - Строка - Имя создаваемой ветки
//
```

#### ПолучитьСписокВеток
```bsl
// Получить список веток
//
// Параметры:
//   ВключаяУдаленные - Булево - Включать информацию об удаленных ветках
//
//  Возвращаемое значение:
//   ТаблицаЗначений   - Таблица с информацией о текущих ветках.
//		Содержит колонки:
//			Текущая - Булево - Признак текущей ветки
//			Имя - Строка - Имя ветки
//
```

> Работа с внешними репозиториями

#### ДобавитьВнешнийРепозиторий
```bsl
// Добавить внешний репозиторий
// git remote add 
//
// Параметры:
//   ИмяРепозитория - Строка - Имя внешнего репозитория
//   АдресВнешнегоРепозитория - Строка - Путь к внешнему репозиторию
//
```

#### УдалитьВнешнийРепозиторий
```bsl
// Удалить внешний репозиторий
// git remote remove
//
// Параметры:
//   ИмяРепозитория - Строка - Имя внешнего репозитория
//
```

#### ПолучитьСписокВнешнихРепозиториев
```bsl
// Получить список внешних репозиториев
//
//  Возвращаемое значение:
//   ТаблицаЗначений   - Таблица с информацией о внешних репозиториях.
//		Содержит колонки:
//			Имя - Строка - Имя внешнего репозитория
//			Адрес - Строка - Путь к внешнему репозиторию
//			Режим - Строка - Режим работы с внешним репозиторием (push/fetch)
//
```

> Работа с подмодулями

#### ДобавитьПодмодуль
```bsl
// Добавить новый подмодуль
// git submodule add
//
// Параметры:
//   АдресВнешнегоРепозитория - Строка - Путь к внешнему репозиторию
//   Местоположение - Строка - Каталог, в который необходимо поместить
//		указанный подмодуль
//   Ветка - Строка - Имя ветки внешнего репозитория для получения
//   ИмяПодмодуля - Строка - Имя, под которым подмодуль будет сохранен
//		в настройках
//
```

#### ОбновитьПодмодули
```bsl
// Обновить данные о зарегистрированных подмодулях
// git submodule update
//
// Параметры:
//   Инициализировать - Булево - Выполнять инициализацию подмодуля
//   Рекурсивно - Рекурсивно - Обновлять подмодули подмодулей
//
```

#### ПолучитьСостояниеПодмодулей
```bsl
// Получить состояние подмодулей
//
//  Возвращаемое значение:
//   ТаблицаЗначений - Таблица с информацией о подмодулях.
//		Содержит колонки:
//			ХэшКоммита - Строка - Хэш коммита, на который указывает подмодуль
//			Имя - Строка - Имя подмодуля
//			Указатель - Строка - указатель на внешний репозиторий
//
```

> Работа с настройками

#### ПолучитьНастройку
```bsl
// Получить значение настройки git
//
// Параметры:
//   ИмяНастройки - Строка - Имя настройки
//   РежимУстановкиНастроекGit - РежимУстановкиНастроекGit - Режим установки настройки.
//		Значения параметра содержатся в перечислении РежимУстановкиНастроекGit
//
//  Возвращаемое значение:
//   Строка - Значение настройки
//
```

#### УстановитьНастройку
```bsl
// Установить настройку git
// git config
//
// Параметры:
//   ИмяНастройки - Строка - Имя настройки
//   ЗначениеНастройки - Строка - Устанавливаемое значение
//   РежимУстановкиНастроекGit - РежимУстановкиНастроекGit - Режим установки настройки.
//		Значения параметра содержатся в перечислении РежимУстановкиНастроекGit
//
```

#### УдалитьСекциюНастроек
```bsl
// Удаление секции настроек git
//
// Параметры:
//   ИмяСекции - Строка - Имя секции
//   РежимУстановкиНастроекGit - РежимУстановкиНастроекGit - Режим установки настройки.
//
```

#### ПолучитьСписокНастроек
```bsl
// Получить список настроек git
//
// Параметры:
//   РежимУстановкиНастроекGit - РежимУстановкиНастроекGit - Уровень, на котором
//		необходимо искать значения настроек
//
//  Возвращаемое значение:
//   Соответствие - Список настроек.
//		Ключ соответствия - ключ настройки
//		Значение соответствия - значение настройки
//
```

> Выполнение произвольных команд

#### ВыполнитьКоманду
```bsl
// Выполнение произвольной команды git
//
// Параметры:
//   Параметры - Массив - Массив строковых аргументов, передаваемых в командную
//		строку. Добавляются после исполняемого файла.
//
```

### Класс НастройкаРежимаОтправкиGit:

#### ПолучитьНастройки
```bsl

```

#### УстановитьНастройки
```bsl

```

#### ПолучитьПараметрыКоманды
```bsl

```

#### ДобавитьПроизвольныйЗаголовокОтправки
```bsl

```

#### УстановитьURLРепозиторияОтправки
```bsl

```

#### УстановитьЗаголовкиОтправки
```bsl

```

#### УстановитьПараметрыКомандыОтправки
```bsl

```

#### ДобавитьЗаголовкиОтправки
```bsl

```

#### ОтображатьПрогресс
```bsl

```

#### РежимТишины
```bsl

```

#### РежимЗеркала
```bsl

```

#### РежимУдаления
```bsl

```

#### ПолнаяОтправка
```bsl

```

#### ПерезаписатьИсторию
```bsl

```

#### Отслеживать
```bsl

```

#### РежимПрограммнойОбработкаРезультата
```bsl

```

#### ОтправкаТэгов
```bsl

```

#### УстановитьПроизвольныйРежим
```bsl

```

### Перечисления

#### РежимУстановкиНастроекGit:

Значения:
* Локально
* Глобально
* Системно
