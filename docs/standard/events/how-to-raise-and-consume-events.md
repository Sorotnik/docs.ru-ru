---
title: Практическое руководство. Вызов и обработка событий
description: Вызывайте и обрабатывайте события в .NET. Ознакомьтесь с примерами, в которых используются делегат EventHandler, делегат EventHandler<TEventArgs> и пользовательский делегат.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- events [.NET], raising
- raising events
- events [.NET], samples
ms.assetid: 42afade7-3a02-4f2e-868b-95845f302f8f
ms.openlocfilehash: c9121c6b2635788ad8ad7abc6d2b5a58448049a6
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93064201"
---
# <a name="how-to-raise-and-consume-events"></a>Практическое руководство. Вызов и обработка событий
В примерах в этом разделе показано, как работать с событиями. Даны примеры делегата <xref:System.EventHandler>, делегата <xref:System.EventHandler%601> и пользовательского делегата, иллюстрирующие события как с данными, так и без.  
  
 В примерах используются понятия, описанные в руководстве по [событиям](index.md).  
  
## <a name="example"></a>Пример  
 В первом примере показано, как вызывать и использовать событие, не содержащее данные. Он содержит класс `Counter` с событием `ThresholdReached`. Это событие возникает, когда значение счетчика больше порогового значения или равно ему. Делегат <xref:System.EventHandler> связан с событием, потому что данные события не предоставляются.  
  
 [!code-csharp[EventsOverview#5](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programnodata.cs#5)]
 [!code-vb[EventsOverview#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1nodata.vb#5)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как вызывать и использовать событие, предоставляющее данные. Делегат <xref:System.EventHandler%601> связан с событием; предоставляется экземпляр объекта данных пользовательского события.  
  
 [!code-cpp[EventsOverview#6](../../../samples/snippets/cpp/VS_Snippets_CLR/eventsoverview/cpp/programwithdata.cpp#6)]
 [!code-csharp[EventsOverview#6](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdata.cs#6)]
 [!code-vb[EventsOverview#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdata.vb#6)]  
  
## <a name="example"></a>Пример  
 В следующем примере показано объявление делегата для события. Имя делегата — `ThresholdReachedEventHandler`. Это всего лишь пример. Как правило, не требуется объявлять делегат для события, поскольку можно использовать делегат <xref:System.EventHandler> или <xref:System.EventHandler%601>. Объявлять делегат необходимо только в редких случаях, например чтобы сделать класс доступным для устаревшего кода, который не может использовать универсальные классы.  
  
 [!code-csharp[EventsOverview#7](../../../samples/snippets/csharp/VS_Snippets_CLR/eventsoverview/cs/programwithdelegate.cs#7)]
 [!code-vb[EventsOverview#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/eventsoverview/vb/module1withdelegate.vb#7)]  
  
## <a name="see-also"></a>См. также

- [События](index.md)
