---
title: Строки подключения
ms.date: 12/13/2019
description: Поддерживаемые ключевые слова и значения строк подключения.
ms.openlocfilehash: bb54d152bac62a86c2a49192cf678a745159164e
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450276"
---
# <a name="connection-strings"></a>Строки подключения

Строка подключения используется для указания способа подключения к базе данных. Строки подключения в Microsoft. Data. SQLite следуют стандартному [синтаксису ADO.NET](../../../framework/data/adonet/connection-strings.md) в виде разделенного точкой с запятой списка ключевых слов и значений.

## <a name="keywords"></a>Ключевые слова

С Microsoft. Data. SQLite можно использовать следующие ключевые слова строки подключения:

### <a name="data-source"></a>Источник данных

Путь к файлу базы данных. *Источник данных* (без пробела) и *имя файла* являются псевдонимами этого ключевого слова.

SQLite обрабатывает пути относительно текущего рабочего каталога. Можно также указать абсолютные пути.

Если этот параметр **пуст**, SQLite создает временную базу данных на диске, которая удаляется при закрытии соединения.

Если `:memory:`, используется база данных в памяти. Дополнительные сведения см. [в разделе базы данных в памяти](in-memory-databases.md).

Пути, начинающиеся со строки подстановки `|DataDirectory|`, обрабатываются так же, как и относительные пути. Если задано, пути выполняются относительно значения свойства домена приложения DataDirectory.

Это ключевое слово также поддерживает [имена файлов URI](https://www.sqlite.org/uri.html).

### <a name="mode"></a>Режим

Режим подключения.

| {2&gt;Value&lt;2}           | Описание                                                                                        |
| --------------- | -------------------------------------------------------------------------------------------------- |
| реадвритекреате | Открывает базу данных для чтения и записи и создает ее, если она не существует. Это значение по умолчанию. |
| ReadWrite       | Открывает базу данных для чтения и записи.                                                        |
| ReadOnly        | Открывает базу данных в режиме только для чтения.                                                              |
| Память          | Открывает базу данных в памяти.                                                                       |

### <a name="cache"></a>Кэш

Режим кэширования, используемый соединением.

| {2&gt;Value&lt;2}   | Описание                                                                                    |
| ------- | ---------------------------------------------------------------------------------------------- |
| Default | Использует режим по умолчанию базовой библиотеки SQLite. Это значение по умолчанию.                   |
| Private | Для каждого соединения используется частный кэш.                                                          |
| Общий  | Подключения совместно используют кэш. Этот режим может изменить поведение блокировки транзакций и таблиц. |

### <a name="password"></a>Password

Ключ шифрования. Если этот параметр указан, `PRAGMA key` отправляется сразу после открытия соединения.

> [!WARNING]
> Пароль не действует, если шифрование не поддерживается собственной библиотекой SQLite.

### <a name="foreign-keys"></a>Внешние ключи

Значение, указывающее, следует ли включить ограничения внешнего ключа.

| {2&gt;Value&lt;2}   | Описание
| ------- | --- |
| Да    | Отправляет `PRAGMA foreign_keys = 1` сразу после открытия соединения.
| Ложь   | Отправляет `PRAGMA foreign_keys = 0` сразу после открытия соединения.
| (пусто) | Не отправляет `PRAGMA foreign_keys`. Это значение по умолчанию. |

Нет необходимости включать внешние ключи, если, как в e_sqlite3, SQLITE_DEFAULT_FOREIGN_KEYS использовалась для компиляции собственной библиотеки SQLite.

### <a name="recursive-triggers"></a>Рекурсивные триггеры

Значение, указывающее, следует ли включить рекурсивные триггеры.

| {2&gt;Value&lt;2} | Описание                                                                 |
| ----- | --------------------------------------------------------------------------- |
| Да  | Отправляет `PRAGMA recursive_triggers` сразу после открытия соединения. |
| Ложь | Не отправляет `PRAGMA recursive_triggers`. Это значение по умолчанию.              |

## <a name="connection-string-builder"></a>Построитель строк подключения

<xref:Microsoft.Data.Sqlite.SqliteConnectionStringBuilder> можно использовать как строго типизированный способ создания строк подключения. Его также можно использовать для предотвращения атак путем внедрения строки подключения.

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/EncryptionSample/Program.cs?name=snippet_ConnectionStringBuilder)]

## <a name="examples"></a>Примеры

### <a name="basic"></a>Basic

Базовая строка подключения с общим кэшем для повышения параллелизма.

```ConnectionString
Data Source=Application.db;Cache=Shared
```

### <a name="encrypted"></a>Зашифровано

Зашифрованная база данных.

```ConnectionString
Data Source=Encrypted.db;Password=MyEncryptionKey
```

### <a name="read-only"></a>Только чтение

База данных только для чтения, которая не может быть изменена приложением.

```ConnectionString
Data Source=Reference.db;Mode=ReadOnly
```

### <a name="in-memory"></a>In-memory

Закрытая, в памяти база данных.

```ConnectionString
Data Source=:memory:
```

### <a name="sharable-in-memory"></a>Совместное в памяти

Совместно используемая база данных в памяти, определяемая именем, которая является *совместно*используемой.

```ConnectionString
Data Source=Sharable;Mode=Memory;Cache=Shared
```

## <a name="see-also"></a>См. также:

* [Строки подключения в ADO.NET](../../../framework/data/adonet/connection-strings.md)
* [Базы данных в памяти](in-memory-databases.md)
* [Tранзакции](transactions.md)