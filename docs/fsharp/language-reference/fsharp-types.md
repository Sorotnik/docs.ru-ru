---
title: Типы
description: 'Сведения о типах, используемых в F #, и о том, как типы F # именуются и описаны.'
ms.date: 08/15/2020
ms.openlocfilehash: a86d8e8f672d8399b02bb193ae04e1f0d46720b6
ms.sourcegitcommit: 9c45035b781caebc63ec8ecf912dc83fb6723b1f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "88812072"
---
# <a name="f-types"></a>Типы языка F#

В этом разделе описываются типы, используемые в F #, а также способы именования и описания типов F #.

## <a name="summary-of-f-types"></a>Общие сведения о типах F #

Некоторые типы считаются *примитивными типами*, такими как логический тип `bool` и целочисленные типы с плавающей запятой различных размеров, в том числе типы для байтов и символов. Эти типы описаны в [типах-примитивах](basic-types.md).

Другие типы, встроенные в язык, включают кортежи, списки, массивы, последовательности, записи и размеченные объединения. Если у вас есть опыт работы с другими языками .NET и вы изучаете F #, ознакомьтесь со статьями по каждому из этих типов. Эти специальные типы F # поддерживают стили программирования, которые являются общими для языков функционального программирования. Многие из этих типов имеют связанные модули в библиотеке F #, которые поддерживают общие операции с этими типами.

Тип функции включает сведения о типах параметров и возвращаемых типах.

.NET Framework является источником типов объектов, типов интерфейсов, типов делегатов и других. Вы можете определить собственные типы объектов так же, как и на любом другом языке .NET.

Кроме того, код F # может определять псевдонимы, представляющие собой именованные *сокращения типов*, которые являются альтернативными именами для типов. Аббревиатуры типов можно использовать, когда тип может измениться в будущем и необходимо избежать изменения кода, который зависит от типа. Также можно использовать аббревиатуру типа в качестве понятного имени для типа, который может облегчить чтение и понимание кода.

F # предоставляет полезные типы коллекций, разработанные с учетом функционального программирования. Использование этих типов коллекций помогает написать код, который более функциональн в стиле. Дополнительные сведения см. в статье [типы коллекций F #](fsharp-collection-types.md).

## <a name="syntax-for-types"></a>Синтаксис типов

В коде F # часто приходится записывать имена типов. Каждый тип имеет синтаксическую форму, и вы используете эти синтаксические формы в аннотациях типов, объявлениях абстрактных методов, объявлениях делегатов, сигнатурах и других конструкциях. При объявлении новой конструкции программы в интерпретаторе интерпретатор выводит имя конструкции и синтаксис для его типа. Этот синтаксис может быть просто идентификатором для определяемого пользователем типа или встроенным идентификатором, например `int` , для или `string` , но для более сложных типов синтаксис более сложен.

В следующей таблице показаны аспекты синтаксиса типов для типов F #.

|Тип|Синтаксис типа|Примеры|
|----|-----------|--------|
|тип-примитив|*имя типа*|`int`<br /><br />`float`<br /><br />`string`|
|агрегатный тип (класс, структура, объединение, запись, перечисление и т. д.)|*имя типа*|`System.DateTime`<br /><br />`Color`|
|Сокращенная форма типа|*Тип-сокращенное имя*|`bigint`|
|полный тип|*пространства имен. Type-Name*<br /><br />или диспетчер конфигурации служб<br /><br />*modules. Type-Name*<br /><br />или диспетчер конфигурации служб<br /><br />*пространства имен. modules. Type-Name*|`System.IO.StreamWriter`|
|массиве|*Type-Name*[] или<br /><br />*тип-имя* массива|`int[]`<br /><br />`array<int>`<br /><br />`int array`|
|двухмерный массив|*Type-Name*[,]|`int[,]`<br /><br />`float[,]`|
|трехмерный массив|*Type-Name*[,,]|`float[,,]`|
|tuple|*Type-name1* &#42; *Type-имя2* ...|Например, `(1,'b',3)` имеет тип `int * char * int`|
|универсальный тип|*тип-параметр* *Generic-Type-Name*<br /><br />или диспетчер конфигурации служб<br /><br />*Generic-Type-Name* &lt; *тип-Parameter-список*&gt;|`'a list`<br /><br />`list<'a>`<br /><br />`Dictionary<'key, 'value>`|
|сконструированный тип (универсальный тип с указанным аргументом типа)|*Argument-аргумент типа* *Generic-Type-Name*<br /><br />или диспетчер конфигурации служб<br /><br />*Generic-Type-Name* &lt; *тип-Argument-список*&gt;|`int option`<br /><br />`string list`<br /><br />`int ref`<br /><br />`option<int>`<br /><br />`list<string>`<br /><br />`ref<int>`<br /><br />`Dictionary<int, string>`|
|тип функции с одним параметром|*параметр-Type1*  - &gt; *тип возвращаемого* значения|Функция, которая принимает `int` и возвращает, `string` имеет тип `int -> string`|
|тип функции с несколькими параметрами|*параметр-Type1*  - &gt; *параметр-тип2*  - &gt; ...- &gt; *тип возвращаемого* значения|Функция, которая принимает, и `int` `float` возвращает, `string` имеет тип `int -> float -> string`|
|функция с более высоким порядком в качестве параметра|(*функция-тип*)|`List.map` имеет тип `('a -> 'b) -> 'a list -> 'b list`|
|delegate|Делегат *функции-типа*|`delegate of unit -> int`|
|гибкий тип|#*имя типа*|`#System.Windows.Forms.Control`<br /><br />`#seq<int>`|

## <a name="related-topics"></a>См. также

|Раздел|Описание|
|-----|-----------|
|[Примитивные типы](basic-types.md)|Описывает встроенные простые типы, такие как целочисленные типы, логический тип и символьные типы.|
|[Тип Unit](unit-type.md)|Описывает `unit` тип, тип которого имеет одно значение и указывает (); эквивалент `void` в в C# и `Nothing` в Visual Basic.|
|[Кортежи](tuples.md)|Описывает тип кортежа — тип, состоящий из связанных значений любого типа, сгруппированных по парам, Triple, четверных и т. д.|
|[Параметры](options.md)|Описывает тип параметра — тип, который может иметь значение или быть пустым.|
|[Списки](lists.md)|Описывает списки, которые являются упорядоченными, неизменяемые последовательности элементов одного типа.|
|[Массивы](arrays.md)|Описывает массивы, которые представляют собой упорядоченные наборы изменяемых элементов того же типа, которые занимают непрерывный блок памяти и имеют фиксированный размер.|
|[Последовательности](sequences.md)|Описывает тип последовательности, представляющий логический ряд значений; отдельные значения вычисляются только по мере необходимости.|
|[Записи](records.md)|Описывает тип записи, небольшое статистическое выражение именованных значений.|
|[Размеченные объединения](discriminated-unions.md)|Описывает тип размеченного объединения — тип, значения которого могут быть любого одного из набора возможных типов.|
|[Функции](./functions/index.md)|Описывает значения функций.|
|[Классы](classes.md)|Описывает тип класса — тип объекта, соответствующий ссылочному типу .NET. Типы классов могут содержать члены, свойства, реализованные интерфейсы и базовый тип.|
|[Структуры](structures.md)|Описывает `struct` тип, тип объекта, соответствующий типу значения .NET. `struct`Тип обычно представляет небольшое статистическое выражение данных.|
|[Интерфейсы](interfaces.md)|Описывает типы интерфейсов, представляющие набор элементов, которые предоставляют определенные функциональные возможности, но не содержат данных. Тип интерфейса должен быть реализован типом объекта, чтобы быть полезным.|
|[Делегаты](delegates.md)|Описывает тип делегата, который представляет функцию в виде объекта.|
|[Перечисления](enumerations.md)|Описывает типы перечислений, значения которых принадлежат набору именованных значений.|
|[Атрибуты](attributes.md)|Описывает атрибуты, которые используются для указания метаданных для другого типа.|
|[Типы исключения](./exception-handling/exception-types.md)|Описывает исключения, которые указывают сведения об ошибке.|
