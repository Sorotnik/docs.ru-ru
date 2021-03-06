---
title: Список атрибутов
ms.date: 07/20/2015
helpviewer_keywords:
- attribute list
- attributes [Visual Basic], applying
ms.assetid: 5880073a-68a4-4b6b-8a07-ace32959a4e2
ms.openlocfilehash: e566239c56efa8ca8e83bff92486fec4c434e92b
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "90874737"
---
# <a name="attribute-list-visual-basic"></a>Список атрибутов (Visual Basic)

Задает атрибуты, применяемые к объявленному программному элементу. Несколько атрибутов разделяются запятыми. Ниже приведен синтаксис для одного атрибута.  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
[ attributemodifier ] attributename [ ( attributearguments | attributeinitializer ) ]  
```  
  
## <a name="parts"></a>Компоненты  

|||
|---|---|
|`attributemodifier`|Требуется для атрибутов, применяемых в начале исходного файла. Может быть [сборкой](../modifiers/assembly.md) или [модулем](../modifiers/module-keyword.md).|
|`attributename`| Обязательный элемент. Имя атрибута.|
|`attributearguments`|Необязательный элемент. Список позиций аргументов для этого атрибута. Несколько аргументов разделяются запятыми.|
|`attributeinitializer`|Необязательный элемент. Список инициализаторов переменных или свойств для этого атрибута. Несколько инициализаторов разделяются запятыми.|
  
## <a name="remarks"></a>Remarks  

 Можно применить один или несколько атрибутов практически к любому элементу программирования (типам, процедурам, свойствам и т. д.). Атрибуты отображаются в метаданных сборки, и они могут помочь добавить заметки в код или указать способ использования определенного программного элемента. Можно применять атрибуты, определенные Visual Basic и .NET Framework, а также определять собственные атрибуты.  

 Дополнительные сведения об использовании атрибутов см. в разделе [Общие сведения об атрибутах](../../programming-guide/concepts/attributes/index.md). Дополнительные сведения об именах атрибутов см. в разделе [Имена объявленных элементов](../../programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## <a name="rules"></a>Правила  
  
- **Размещаем.** К большинству объявленных программных элементов можно применять атрибуты. Чтобы применить один или несколько атрибутов, поместите *блок атрибутов* в начало объявления элемента. Каждая запись в списке атрибутов указывает атрибут, который вы хотите применить, и модификатор и аргументы, используемые для этого вызова атрибута.  
  
- **Угловые скобки.** При указании списка атрибутов необходимо заключить его в угловые скобки (" `<` " и " `>` ").  
  
- **Часть объявления.** Атрибут должен быть частью объявления элемента, а не отдельной инструкции. `_`Для расширения оператора объявления на несколько строк исходного кода можно использовать последовательность продолжения строки ("").  
  
- **Модификаторы.** Модификатор атрибута ( `Assembly` или `Module` ) необходим для каждого атрибута, применяемого к программному элементу в начале исходного файла. Использование модификаторов атрибутов не допускается для атрибутов, применяемых к элементам, которые не находятся в начале исходного файла.  
  
- **Даваемых.** Все позиционированные аргументы для атрибута должны предшествовать любым инициализаторам переменных или свойств.  
  
## <a name="example"></a>Пример  

 В следующем примере атрибут применяется <xref:System.Runtime.InteropServices.DllImportAttribute> к скелетному определению `Function` процедуры.  
  
 [!code-vb[VbVbalrStatements#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#1)]  
  
 <xref:System.Runtime.InteropServices.DllImportAttribute> Указывает, что процедура с атрибутом представляет точку входа в неуправляемой библиотеке динамической компоновки (DLL). Атрибут предоставляет имя библиотеки DLL в качестве аргумента, а другие сведения — как Инициализаторы переменных.  
  
## <a name="see-also"></a>См. также

- [Сборка](../modifiers/assembly.md)
- [Модуль \<keyword>](../modifiers/module-keyword.md)
- [Обзор атрибутов](../../programming-guide/concepts/attributes/index.md)
- [Практическое руководство. Разбиение и объединение инструкций в коде](../../programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)
