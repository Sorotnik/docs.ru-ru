---
title: Практическое руководство. Как обращаться с запросами о сведениях
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e538d288-2070-40ca-9da6-4fbc68cd6ad0
ms.openlocfilehash: d45fdfa8b8976e3cdc86b905443bf7bcea578714
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91166408"
---
# <a name="how-to-query-for-information"></a>Практическое руководство. Как обращаться с запросами о сведениях

Запросы в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] используют тот же синтаксис, что и запросы в LINQ. Единственное отличие заключается в том, что объекты, на которые имеются ссылки в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] запросах, сопоставляются с элементами в базе данных. Дополнительные сведения см. в разделе [Введение в запросы LINQ (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md).  
  
 Технология [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] преобразует написанные пользователем запросы в эквивалентные запросы SQL и отправляет их на сервер для обработки.  
  
 Некоторые функции запросов LINQ могут потребовать особого внимания в [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] приложениях. Дополнительные сведения см. в разделе [Основные понятия запросов](query-concepts.md).  
  
## <a name="example"></a>Пример  

 Следующий запрос возвращает список клиентов из Лондона. В этом примере используется таблица `Customers` из учебной базы данных "Northwind".  
  
 [!code-csharp[DLinqQuerying#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#1)]
 [!code-vb[DLinqQuerying#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>См. также раздел

- [Создание модели объектов](creating-the-object-model.md)
- [Загрузка примеров баз данных](downloading-sample-databases.md)
- [Запрос к базе данных](querying-the-database.md)
