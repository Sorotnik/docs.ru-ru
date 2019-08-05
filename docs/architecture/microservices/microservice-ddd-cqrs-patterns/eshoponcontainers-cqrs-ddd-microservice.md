---
title: Применение подходов CQRS и CQS в микрослужбе DDD в eShopOnContainers
description: Архитектура микрослужб .NET для контейнерных приложений .NET | Реализация CQRS в микрослужбе заказов в eShopOnContainers.
ms.date: 10/08/2018
ms.openlocfilehash: 0380e759595e8a159e89f858a5ced4dacfa4e9b4
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674131"
---
# <a name="apply-cqrs-and-cqs-approaches-in-a-ddd-microservice-in-eshoponcontainers"></a>Применение подходов CQRS и CQS в микрослужбе DDD в eShopOnContainers

Проект микрослужбы заказов эталонного приложения eShopOnContainers построен на принципах CQRS. Однако в нем применяется простейший подход, который просто разделяет запросы и команды и использует одну и ту же базу данных для обоих действий.

Важная отличительная особенность этих шаблонов — идемпотентность запросов. Это означает, что состояние системы не изменяется, независимо от количества запросов к ней. Другими словами, выполнение запросов не влечет за собой возможные проблемы.

Следовательно, вы можете использовать для чтения другую модель данных, отличающуюся от модели предметной области записи транзакционной логики, хотя микрослужбы размещения заказов используют ту же базу данных. Следовательно, такой подход CQRS является упрощенным.

С другой стороны, команды, которые инициируют транзакции и обновления данных, изменяют состояние в системе. При использовании команд необходимо соблюдать осторожность, имея дело со сложными и постоянно меняющимися бизнес-правилами. Здесь стоит применять методику DDD, чтобы наилучшим образом смоделировать систему.

Шаблоны DDD, представленные в настоящем руководстве, не должны применяться универсально. Они вводят в ваш проект ограничения. Эти ограничения обеспечивают такие преимущества, как повышение качества с течением времени, особенно в командах и другом коде, который изменяет состояние системы. Однако эти ограничения увеличивают сложность с минимумом преимуществ для чтения и запросов данных.

Одним из таких шаблонов является шаблон агрегата, который мы подробно рассмотрим в последующих разделах. Вкратце, в шаблоне агрегата (Aggregate) многие объекты предметной области обрабатываются как единое целое в результате их связей в предметной области. В запросах не всегда удается извлечь преимущества из этого шаблона; он может увеличить сложность логики запроса. В запросах только на чтение вы не получите никаких преимуществ от обработки нескольких объектов как единого агрегата. Вы получите только сложность.

Как показано на рис. 7-2, в данном руководстве предлагается использовать шаблоны DDD только в области транзакций или обновлений вашей микрослужбы (то есть в том, что инициируется командами). Для запросов можно использовать более простой подход, и согласно концепции CQRS их следует отделить от команд.

Для реализации "стороны запросов" вы можете выбирать между подходами, включая полнофункциональные ORM, например EF Core, проекции AutoMapper, хранимые процедуры, представления, материализованные представления и micro ORM.

В данном руководстве и в приложении eShopOnContainers (в частности, в микрослужбе заказов) мы решили реализовать прямые запросы с помощью micro ORM, например [Dapper](https://github.com/StackExchange/dapper-dot-net). Это позволяет реализовать любой запрос на основе инструкций SQL для получения наилучшей производительности благодаря облегченной инфраструктуре с минимальными накладными расходами.

Обратите внимание, что при использовании этого подхода для любых обновлений модели, влияющих на то, как сущности сохраняются в базе данных SQL, также требуются отдельные обновления запросов SQL, используемых Dapper или любым другим отдельным (не EF) подходом к запросам.

## <a name="cqrs-and-ddd-patterns-are-not-top-level-architectures"></a>Шаблоны DDD и CQRS не относятся к архитектурам верхнего уровня

Важно понимать, что CQRS и большинство шаблонов DDD (например, слои DDD или модель предметной области с агрегатами) являются не архитектурными стилями, а лишь архитектурными шаблонами. Примерами архитектурных стилей являются микрослужбы, SOA и событийно-управляемая архитектура (EDA). Они описывают систему, состоящую из множества компонентов, например из множества микрослужб. Шаблоны DDD и CQRS описывают нечто внутри одной системы или компонента; в данном случае — нечто внутри микрослужбы.

Разные ограниченные контексты (BC) будут использовать разные шаблоны. Они имеют разные сферы ответственности, что ведет к разным решениям. Стоит подчеркнуть, что повсеместное применение одного и того же шаблона приводит к неудаче. Не используйте шаблоны DDD и CQRS повсюду. Многие подсистемы, ограниченные контексты или микрослужбы довольно простые, и их можно реализовать более просто с помощью служб CRUD или другого метода.

Имеется только одна архитектура приложения: архитектура разрабатываемой системы или комплексного приложения (например, архитектура микрослужб). Однако структура каждого ограниченного контекста или микрослужбы в этом приложении отражает их собственные компромиссы и внутренние проектные решения на уровне архитектурных шаблонов. Не пытайтесь везде применять одни и те же архитектурные шаблоны, такие как CQRS или DDD.

### <a name="additional-resources"></a>Дополнительные ресурсы

- **Мартин Фоулер (Martin Fowler). CQRS** \
  <https://martinfowler.com/bliki/CQRS.html>

- **Грег Янг (Greg Young). Документы по CQRS**  \
  <https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf>

- **Уди Дахан (Udi Dahan). Пояснения к CQRS** \
  <http://udidahan.com/2009/12/09/clarified-cqrs/>

>[!div class="step-by-step"]
>[Назад](apply-simplified-microservice-cqrs-ddd-patterns.md)
>[Вперед](cqrs-microservice-reads.md)