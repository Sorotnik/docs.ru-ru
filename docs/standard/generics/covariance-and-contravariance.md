---
title: Ковариантность и контрвариантность в универсальных шаблонах
description: Сведения о ковариантности, которая позволяет использовать тип с большей степенью наследования, и контрвариантности, которая позволяет использовать тип с меньшей степенью наследования в универсальных шаблонах .NET.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- generics, covariance and contravariance
- generics, variance
- covariance and contravariance in generics
- generic type parameters
ms.assetid: 2678dc63-c7f9-4590-9ddc-0a4df684d42e
ms.openlocfilehash: 1606238b22bd355b997b54cf94e0c28d16ec5cac
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93063180"
---
# <a name="covariance-and-contravariance-in-generics"></a>Ковариантность и контрвариантность в универсальных шаблонах

Термины *ковариантность* и *контрвариантность* относятся к возможности использовать более производный (более конкретный) или менее производный (менее конкретный) тип, чем задано изначально. Параметры универсальных типов поддерживают ковариантность и контрвариантность и обеспечивают большую гибкость в назначении и использовании универсальных типов.

Ниже приведены определения терминов "ковариантность", "контрвариантность" и "инвариантность" в контексте системы типов. В этих примерах предполагается наличие базового класса с именем `Base` и производного класса с именем `Derived`.  
  
- `Covariance`  
  
     Позволяет использовать тип с большей глубиной наследования, чем задано изначально.  
  
     Экземпляр `IEnumerable<Derived>` можно присвоить переменной типа `IEnumerable<Base>`.  
  
- `Contravariance`  
  
     Позволяет использовать более универсальный тип (с меньшей глубиной наследования), чем заданный изначально.  
  
     Экземпляр `Action<Base>` можно присвоить переменной типа `Action<Derived>`.  
  
- `Invariance`  
  
     Это означает, что можно использовать только изначально указанный тип. Таким образом, параметр инвариантного универсального типа не является ни ковариантным, ни контрвариантным.  
  
     Экземпляр `List<Base>` нельзя присвоить переменной типа `List<Derived>` (и наоборот).  
  
 Параметры ковариантного типа позволяют создавать назначения, которые выглядят очень похоже на обычный [полиморфизм](../../csharp/programming-guide/classes-and-structs/polymorphism.md), как показывает следующий код.  
  
 [!code-csharp[CoContraSimpleIEnum#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleienum/cs/example.cs#1)]
 [!code-vb[CoContraSimpleIEnum#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleienum/vb/example.vb#1)]  
  
 Класс <xref:System.Collections.Generic.List%601> реализует интерфейс <xref:System.Collections.Generic.IEnumerable%601> , поэтому `List<Derived>` (`List(Of Derived)` в Visual Basic) реализует `IEnumerable<Derived>`. Параметр ковариантного типа делает все остальное.  
  
 Контрвариантность, с другой стороны, выглядит нелогичной. Следующий пример создает делегат типа `Action<Base>` (`Action(Of Base)` в Visual Basic), а затем назначает этот делегат переменной типа `Action<Derived>`.  
  
 [!code-csharp[CoContraSimpleAction#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontrasimpleaction/cs/example.cs#1)]
 [!code-vb[CoContraSimpleAction#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontrasimpleaction/vb/example.vb#1)]  
  
 Это может показаться шагом назад, но это типобезопасный код, который компилируется и выполняется. Лямбда-выражение соответствует делегату, которому присвоено, и определяет метод, который принимает один параметр типа `Base` и не имеет возвращаемого значения. Результирующий делегат может быть присвоен переменной типа `Action<Derived>` , так как параметр типа `T` делегата <xref:System.Action%601> является контравариантным. Код является типобезопасным, потому что `T` задает тип параметра. Когда делегат типа `Action<Base>` вызван так, как если бы он был делегатом типа `Action<Derived>`, его аргумент должен быть аргументом типа `Derived`. Этот аргумент всегда может быть безопасно передан базовому методу, потому что параметр метода является параметром типа `Base`.  
  
 В общем случае, параметр ковариантного типа может быть использован в качестве возвращаемого типа делегата, и параметры контравариантного типа могут быть использованы в качестве типов параметра. Для интерфейса параметры ковариантного типа могут быть использованы в качестве возвращаемых типов методов интерфейса, и параметры контравариантного типа могут быть использованы как типы параметра методов интерфейса.  
  
 Вместе ковариантность и контравариантность называются *вариацией*. Параметр универсального типа, который не отмечен как ковариантный или контравариантный, называется *инвариантным*. Краткие сведения о вариативности в общеязыковой среде выполнения:  
  
- Параметры вариантного типа ограничены типами универсального интерфейса и универсального метода-делегата.  
  
- Тип универсального интерфейса или универсального метода-делегата может иметь как ковариантные, так и контравариантные параметры типа.  
  
- Вариативность применяется только к ссылочным типам; если указать тип значения для параметра вариантного типа, этот параметр типа является инвариантным для типа, созданного в результате.  
  
- Вариативность не применима к объединению делегатов. Поэтому для заданных двух делегатов типов `Action<Derived>` и `Action<Base>` (`Action(Of Derived)` и `Action(Of Base)` в Visual Basic) нельзя объединять первый делегат со вторым, несмотря на то что результат будет безопасным типом. Вариативность позволяет присвоить второй делегат переменной типа `Action<Derived>`, но делегаты можно объединять, только если их типы точно совпадают.

- Начиная с C# 9, поддерживаются ковариантные типы возвращаемого значения. В переопределяющем методе может объявляться более производный тип возвращаемого значения, чем в переопределяемом, и для переопределяющего доступного только для чтения свойства может объявляться более производный тип.

<a name="InterfaceCovariantTypeParameters"></a>
## <a name="generic-interfaces-with-covariant-type-parameters"></a>Универсальные интерфейсы с ковариантными параметрами типа

Несколько универсальных интерфейсов имеют ковариантные параметры типа, например <xref:System.Collections.Generic.IEnumerable%601>, <xref:System.Collections.Generic.IEnumerator%601>, <xref:System.Linq.IQueryable%601> и <xref:System.Linq.IGrouping%602>. Эти интерфейсы имеют только параметры ковариантного типа. Таким образом, параметры типа используются только для возвращаемых типов в членах.  
  
 В следующем примере демонстрируются ковариантные параметры типа. В примере определяются два типа: `Base` имеет статический метод с именем `PrintBases` , принимающий `IEnumerable<Base>` (`IEnumerable(Of Base)` в Visual Basic) и выводящий эти элементы. Тип `Derived` наследуется от типа `Base`. В примере создается пустой список `List<Derived>` (`List(Of Derived)` в Visual Basic) и показывается, что этот тип может быть передан методу `PrintBases` и назначен переменной типа `IEnumerable<Base>` без приведения. Класс<xref:System.Collections.Generic.List%601> реализует интерфейс <xref:System.Collections.Generic.IEnumerable%601>, который имеет единственный параметр ковариантного типа. Параметр ковариантного типа — это причина, по которой экземпляр `IEnumerable<Derived>` может быть использован вместо `IEnumerable<Base>`.  
  
 [!code-csharp[CoContravarianceInClrGenericI#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici/vb/example.vb#1)]  
  
## <a name="generic-interfaces-with-contravariant-type-parameters"></a>Универсальные интерфейсы с контрвариантными параметрами типа

Несколько универсальных интерфейсов имеют контрвариантные параметры типа, например <xref:System.Collections.Generic.IComparer%601>, <xref:System.IComparable%601> и <xref:System.Collections.Generic.IEqualityComparer%601>. Эти интерфейсы имеют только параметры контравариантного типа, таким образом, параметры типа используются только как типы параметра в членах интерфейсов.  
  
 В следующем примере демонстрируются контравариантные параметры типа. В примере определяется абстрактный (`MustInherit` в Visual Basic) класс `Shape` со свойством `Area` . В примере также определяется класс `ShapeAreaComparer` , реализующий `IComparer<Shape>` (`IComparer(Of Shape)` в Visual Basic). Реализация метода <xref:System.Collections.Generic.IComparer%601.Compare%2A?displayProperty=nameWithType> основывается на значении свойства `Area` , поэтому с помощью `ShapeAreaComparer` можно сортировать объекты `Shape` по областям.  
  
 Класс `Circle` наследует `Shape` и переопределяет `Area`. В примере создается набор <xref:System.Collections.Generic.SortedSet%601> объектов `Circle` с помощью конструктора, принимающего `IComparer<Circle>` (`IComparer(Of Circle)` в Visual Basic). Однако вместо передачи `IComparer<Circle>`, в примере передается объект `ShapeAreaComparer` , реализующий `IComparer<Shape>`. В примере может передаваться компаратор типа меньшей глубины наследования (`Shape`), когда код вызывает компаратор типа большей глубины наследования (`Circle`), поскольку параметр типа универсального интерфейса <xref:System.Collections.Generic.IComparer%601> контрвариантен.  
  
 При добавлении нового объекта `Circle` в `SortedSet<Circle>` метод `IComparer<Shape>.Compare` (метод`IComparer(Of Shape).Compare` в Visual Basic) объекта `ShapeAreaComparer` вызывается всякий раз, когда новый элемент сравнивается с существующим элементом. Тип параметра метода (`Shape`) является менее производным, чем передаваемый тип (`Circle`), поэтому этот вызов является типобезопасным. Контрвариантность позволяет объекту `ShapeAreaComparer` сортировать коллекцию какого-либо одного типа, а также смешанную коллекцию типов, унаследованных от `Shape`.  
  
 [!code-csharp[CoContravarianceInClrGenericI2#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravarianceinclrgenerici2/cs/example.cs#1)]
 [!code-vb[CoContravarianceInClrGenericI2#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravarianceinclrgenerici2/vb/example.vb#1)]  

## <a name="generic-delegates-with-variant-type-parameters"></a>Универсальные делегаты с параметрами вариантного типа

Универсальные методы-делегаты `Func`, такие как <xref:System.Func%602>, имеют ковариантные типы возвращаемого значения и контрвариантные типы параметров. Универсальные методы-делегаты `Action` , такие как <xref:System.Action%602>, имеют контравариантные типы параметров. Это означает, что делегаты можно присваивать переменным, имеющим более производные типы параметров и (в случае универсальных методов-делегатов `Func` ) менее производные возвращаемые типы.  
  
> [!NOTE]
> Последний параметр универсального типа универсальных методов-делегатов `Func` указывает тип возвращаемого значения в сигнатуре делегата. Он является ковариантным (ключевое слово`out` ), в то время как остальные параметры универсального типа являются контравариантными (ключевое слово`in` ).  
  
 Это проиллюстрировано в следующем коде. Первая часть кода определяет класс с именем `Base`, класс с именем `Derived` , наследующий от класса `Base`, и еще один класс с методом типа `static` (`Shared` в Visual Basic) и именем `MyMethod`. Этот метод принимает экземпляр класса `Base` и возвращает экземпляр класса `Derived`. (Если аргумент является экземпляром класса `Derived`, метод `MyMethod` возвращает его; если аргумент является экземпляром класса `Base`, метод `MyMethod` возвращает новый экземпляр класса `Derived`.) В функции `Main()` примера создается экземпляр `Func<Base, Derived>` (`Func(Of Base, Derived)` в Visual Basic), представляющий метод `MyMethod`, и он сохраняется в переменной `f1`.  
  
 [!code-csharp[CoContravarianceDelegates#2](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#2)]
 [!code-vb[CoContravarianceDelegates#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#2)]  
  
 Вторая часть кода показывает, что делегат может быть присвоен переменной типа `Func<Base, Base>` (`Func(Of Base, Base)` в Visual Basic), так как возвращаемый тип является ковариантным.  
  
 [!code-csharp[CoContravarianceDelegates#3](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#3)]
 [!code-vb[CoContravarianceDelegates#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#3)]  
  
 Третья часть кода показывает, что делегат может быть присвоен переменной типа `Func<Derived, Derived>` (`Func(Of Derived, Derived)` в Visual Basic), так как тип параметра является контравариантным.  
  
 [!code-csharp[CoContravarianceDelegates#4](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#4)]
 [!code-vb[CoContravarianceDelegates#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#4)]  
  
 Заключительная часть кода показывает, что делегат может быть присвоен переменной типа `Func<Derived, Base>` (`Func(Of Derived, Base)` в Visual Basic), объединяя эффекты контравариантного параметра типа и ковариантного возвращаемого типа.  
  
 [!code-csharp[CoContravarianceDelegates#5](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegates/cs/example.cs#5)]
 [!code-vb[CoContravarianceDelegates#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegates/vb/example.vb#5)]  
  
### <a name="variance-in-non-generic-delegates"></a>Вариативность в неуниверсальных делегатах

 В предыдущем коде сигнатура метода `MyMethod` точно соответствует сигнатуре сконструированного универсального делегата: `Func<Base, Derived>` (`Func(Of Base, Derived)` в Visual Basic). Пример показывает, что этот универсальный делегат может храниться в параметрах переменных или метода, имеющих более производные типы параметров и менее производные возвращаемые типы, при условии, что все типы делегата сконструированы из универсального типа делегата <xref:System.Func%602>.  
  
 Это важное правило. Влияние ковариантности и контрвариантности в параметрах типа универсального делегата аналогично влиянию ковариантности и контрвариантности в обыкновенной привязке делегата (см. статьи [Вариативность в делегатах (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md) и [Вариативность в делегатах (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)). Однако вариативность в привязке делегата работает для всех типов делегата, а не только с типами универсального метода-делегата, имеющего вариантные параметры типа. Более того, вариативность в привязке делегата допускает привязку метода к любому делегату, имеющему более строгие типы параметров и менее строгий возвращаемый тип, в то время как назначение универсальных делегатов работает только в том случае, если оба типа делегата сконструированы из одного определения универсального типа.  
  
 В следующем примере показан суммарный эффект вариантности в привязке делегата и в параметрах универсального типа. В примере определяется иерархия типов, содержащая три типа, от наименее производного (`Type1`) до наиболее производного (`Type3`). Вариантность в обычной привязке делегата используется для привязки метода с типом параметра `Type1` и возвращаемым типом `Type3` к универсальному делегату с типом параметра `Type2` и возвращаемым типом `Type2`. Получившийся универсальный метод-делегат затем присваивается другой переменной, тип универсального метода-делегата которой имеет тип параметра `Type3` и тип возвращаемого значения `Type1`, с использованием ковариантности и контрвариантности параметров универсального типа. Для второго присваивания требуется, чтобы тип переменной и тип делегата были сконструированы из одного определения универсального типа, в данном случае — <xref:System.Func%602>.  
  
 [!code-csharp[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/csharp/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/cs/example.cs#1)]
 [!code-vb[CoContravarianceDelegatesGenRelaxed#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/cocontravariancedelegatesgenrelaxed/vb/example.vb#1)]  

## <a name="define-variant-generic-interfaces-and-delegates"></a>Определение вариантных универсальных интерфейсов и делегатов

Языки Visual Basic и C# содержат ключевые слова, позволяющие помечать параметры универсального типа для интерфейсов и делегатов как ковариантные или контрвариантные.
  
 Параметр ковариантного типа помечается ключевым словом `out` (ключевым словом `Out` в Visual Basic). Параметр ковариантного типа можно использовать как возвращаемое значение метода, принадлежащего интерфейсу, или как возвращаемый тип делегата. Параметр ковариантного типа нельзя использовать как ограничение универсального типа для методов интерфейса.  
  
> [!NOTE]
> Если метод интерфейса имеет параметр с типом универсального метода-делегата, параметр ковариантного типа этого типа интерфейса может использоваться для указания параметра контравариантного типа этого типа делегата.  
  
 Параметр контрвариантного типа помечается ключевым словом `in` (ключевым словом `In` в Visual Basic). Параметр контравариантного типа можно использовать как тип параметра метода, принадлежащего интерфейсу, или как тип параметра делегата. Параметр контравариантного типа можно использовать как ограничение универсального типа для метода интерфейса.  
  
 Параметры вариантного типа могут иметь только типы интерфейса и типы делегата. Тип интерфейса или тип делегата может иметь как ковариантные, так и контравариантные параметры типа.  
  
 Языки Visual Basic и C# не позволяют нарушать правила использования параметров ковариантного и контравариантного типов или добавлять заметки ковариантности или контрвариантности в параметры типа, имеющие тип, отличный от интерфейсов и делегатов.
  
 Дополнительные сведения и пример кода см. в разделах [Вариативность в универсальных интерфейсах (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md) и [Вариативность в универсальных интерфейсах (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-generic-interfaces.md).  

## <a name="list-of-types"></a>Список типов

Перечисленные ниже типы интерфейсов и делегатов имеют параметры ковариантного и/или контрвариантного типа.  
  
|Type|Параметры ковариантного типа|Параметры контравариантного типа|  
|----------|-------------------------------|-----------------------------------|  
|<xref:System.Action%601> — <xref:System.Action%6016>||Да|  
|<xref:System.Comparison%601>||Да|  
|<xref:System.Converter%602>|Да|Да|  
|<xref:System.Func%601>|Да||  
|<xref:System.Func%602> — <xref:System.Func%6017>|Да|Да|  
|<xref:System.IComparable%601>||Да|  
|<xref:System.Predicate%601>||Да|  
|<xref:System.Collections.Generic.IComparer%601>||Да|  
|<xref:System.Collections.Generic.IEnumerable%601>|Да||  
|<xref:System.Collections.Generic.IEnumerator%601>|Да||  
|<xref:System.Collections.Generic.IEqualityComparer%601>||Да|  
|<xref:System.Linq.IGrouping%602>|Да||  
|<xref:System.Linq.IOrderedEnumerable%601>|Да||  
|<xref:System.Linq.IOrderedQueryable%601>|Да||  
|<xref:System.Linq.IQueryable%601>|Да||  
  
## <a name="see-also"></a>См. также

- [Ковариация и контрвариантность (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/index.md)
- [Ковариация и контрвариантность (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/index.md)
- [Вариативность в делегатах (C#)](../../csharp/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [Вариативность в делегатах (Visual Basic)](../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
