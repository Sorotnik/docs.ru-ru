---
description: '!  — оператор (допускающий значение NULL) — справочник по C#'
title: '!  — оператор (допускающий значение NULL) — справочник по C#'
ms.date: 10/11/2019
f1_keywords:
- nullForgiving_CSharpKeyword
helpviewer_keywords:
- null-forgiving operator [C#]
- '! operator [C#]'
ms.openlocfilehash: 5418f96a3b4515224c49a1c1aa38784c348a86db
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516155"
---
# <a name="-null-forgiving-operator-c-reference"></a>!  — оператор (допускающий значение NULL) (справочник по C#)

Унарный постфиксный оператор `!`, доступный в C# 8.0 и более поздних версиях, допускает значение NULL. При включенном [контексте аннотаций с поддержкой значения NULL](../../nullable-references.md#nullable-annotation-context) можно использовать оператор, допускающий значение NULL, чтобы объявить, что выражение `x` для ссылочного типа, допускающего значение NULL, не равно `null`: `x!`. Унарный префиксный оператор `!` является [оператором логического отрицания](boolean-logical-operators.md#logical-negation-operator-).

Оператор, допускающий NULL, ни на что не влияет во время выполнения. Он влияет только на статический анализ потока компилятора путем изменения состояния NULL выражения. Во время выполнения выражение `x!` сравнивается с результатом базового выражения `x`.

> [!NOTE]
> В C# 8 оператор, допускающий значение NULL, завершает список предыдущих [условных операций со значением NULL](member-access-operators.md#null-conditional-operators--and-). Например, выражение `x?.y!.z` анализируется как `(x?.y)!.z`. Из-за этой интерпретации `z` вычисляется, даже если `x` — `null`, что может привести к <xref:System.NullReferenceException>.

Дополнительные сведения о ссылочных типах, допускающих значения NULL, см. в разделе [Ссылочные типы, допускающие значение NULL](../builtin-types/nullable-reference-types.md).

## <a name="examples"></a>Примеры

Один из вариантов использования оператора, допускающего значение NULL, — тестирование логики проверки аргументов. Например, рассмотрим следующий класс.

[!code-csharp[Person class](snippets/shared/NullForgivingOperator.cs#PersonClass)]

С помощью [платформы тестирования MSTest](../../../core/testing/unit-testing-with-mstest.md) можно создать следующий тест для логики проверки в конструкторе:

[!code-csharp[Person test](snippets/shared/NullForgivingOperator.cs#TestPerson)]

Без оператора, допускающего значение NULL, компилятор создает следующее предупреждение для предыдущего кода: `Warning CS8625: Cannot convert null literal to non-nullable reference type`. Используя оператор, допускающий значение NULL, вы сообщаете компилятору, что передача `null` ожидается и что о ней не нужно предупреждать.

Можно также использовать оператор, допускающий значение NULL, если вы точно знаете, что выражение не может быть `null`, но компилятор не распознает это. В следующем примере, если метод `IsValid` возвращает `true`, его аргумент не является `null`, и вы можете безопасно отменить его ссылку:

[!code-csharp[Use null-forgiving operator](snippets/shared/NullForgivingOperator.cs#UseNullForgiving)]

Без оператора, допускающего значение NULL, компилятор создает следующее предупреждение для кода `p.Name`: `Warning CS8602: Dereference of a possibly null reference`.

Если вы можете изменить метод `IsValid`, можно использовать атрибут [NotNullWhen](xref:System.Diagnostics.CodeAnalysis.NotNullWhenAttribute), чтобы сообщить компилятору, что аргумент метода `IsValid` не может быть `null`, когда метод возвращает `true`:

[!code-csharp[Use an attribute](snippets/shared/NullForgivingOperator.cs#UseAttribute)]

В предыдущем примере не нужно использовать оператор, допускающий значение NULL, поскольку компилятор содержит достаточно информации, чтобы определить, что `p` не может быть `null` внутри `if`. См. сведения об атрибутах, позволяющих указать дополнительную информацию о состоянии NULL для переменной, в руководстве по [включению в API атрибутов для определения ожидаемых значений NULL](../attributes/nullable-analysis.md).

## <a name="c-language-specification"></a>Спецификация языка C#

См. сведения об [операторе, допускающем значение NULL](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator), в [черновике спецификации по ссылочным типам допускающим значение NULL](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md).

## <a name="see-also"></a>См. также

- [справочник по C#](../index.md)
- [Операторы и выражения C#](index.md)
- [Учебник. Разработка с использованием ссылочных типов, допускающих значение NULL](../../tutorials/nullable-reference-types.md)
