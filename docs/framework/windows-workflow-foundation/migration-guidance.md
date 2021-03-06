---
title: Руководство по миграции
ms.date: 03/30/2017
ms.assetid: cb65c132-58c9-4028-b3d4-1efc71d5e60e
ms.openlocfilehash: 16f725dcb5d6f6e5d06771b7836fa187be005910
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90559204"
---
# <a name="migration-guidance"></a>Руководство по миграции

В .NET Framework 4 корпорация Майкрософт выпускает вторую основную версию Windows Workflow Foundation (WF). [!INCLUDE[wf1](../../../includes/wf1-md.md)] был выпущен в WinFX (он включал в себя типы в System. Workflow. \* пространства имен, теперь НАЗЫВАЕТСЯ WF3) и улучшен в .NET Framework 3,5. WF3 также является частью .NET Framework 4, но она существует вместе с новой технологией рабочих процессов (типы в System. Activitys. \* пространство_именs; называются WF4). При принятии решения об использовании WF4 важно помнить, что управление временем осуществляет пользователь.  
  
- WF3 является полностью поддерживаемой частью .NET Framework 4.  
  
- Приложения WF3 выполняются на .NET Framework 4 без изменений и продолжают поддерживаться полностью.  
  
- Можно создавать новые приложения WF3, а существующие приложения можно редактировать в Visual Studio 2012 и полностью поддерживаются.  
  
 Таким решением, решение об принятии .NET Framework 4 отделено от вашего решения о переходе на WF4 (System. Activity. \* ) из WF3 (System. Workflow. \* ). В этом разделе приведены ссылки на руководство по миграции в WF, в котором описывается работа с WF3 и WF4.  
  
## <a name="wf-migration-white-papers-and-cookbooks"></a>Технические документы и справочники по переносу WF

 В разделе [Обзор миграции WF](/previous-versions/appfabric/ff383417(v=azure.10)) представлен общий обзор отношений между WF3 и WF4 и стратегиями миграции. В сопутствующих разделах описываются следующие темы.  
  
 [Общие сведения о миграции в WF](/previous-versions/appfabric/ff383417(v=azure.10))  
 Описывает связи между WF3 и WF4, а также новые возможности пользователей технологии рабочих процессов в .NET 4.  
  
 [Миграция в WF: рекомендации для разработки в WF3](/previous-versions/appfabric/ff383417(v=azure.10))  
 Описывается разработка артефактов WF3 с учетом возможностей упрощения миграции на WF4.  
  
 [Руководство по WF: правила](/previous-versions/appfabric/ff383417(v=azure.10))  
 Описывает, как перенести связанные с правилами инвестиции в решения .NET Framework 4.  
  
 [Руководство WF: Конечный автомат](/previous-versions/appfabric/ff383417(v=azure.10))  
 Описывает моделирование потока управления WF4 при отсутствии действия конечного автомата.  
  
 Обратите внимание, что это руководство относится только к проектам рабочих процессов, использующих платформу .NET Framework 4. Рабочие процессы конечного автомата были добавлены в .NET 4.0.1 с выпуском обновления платформы версии 1 и являлись частью платформы .NET Framework 4.5. Дополнительные сведения о рабочих процессах конечного автомата в .NET 4.0.1-4.0.3 и .NET Framework 4,5 см. в разделе [Обновление 4.0.1 для функций Microsoft .NET Framework 4](/previous-versions/dotnet/netframework-4.0/hh290669(v=vs.100)) и [рабочих процессов конечного автомата](state-machine-workflows.md).  
  
 [Рецепты миграции WF: пользовательские действия](/previous-versions/appfabric/ff383417(v=azure.10))  
 Обеспечивает примеры и инструкции по изменению структуры настраиваемых действий WF3 в WF4.  
  
 [Рецепты миграции WF: расширенные пользовательские действия](/previous-versions/appfabric/ff383417(v=azure.10))  
 Предоставляет рекомендации по перепроектированию расширенных пользовательских действий WF3, использующих очереди WF3 и планирование дочерних действий в виде пользовательских действий WF4.  
  
 [Рецепты миграции WF: рабочие процессы](/previous-versions/appfabric/ff383417(v=azure.10))  
 Обеспечивает примеры и инструкции по изменению структуры рабочих процессов WF3 в WF4.  
  
 [Рецепты миграции WF: размещение рабочего процесса](/previous-versions/appfabric/ff383417(v=azure.10))  
 Предоставляет рекомендации по перепроектированию кода размещения WF3 как кода размещения для WF4. Цель - описать ключевые различия процессов размещения рабочего процесса в WF3 и WF4.  
  
 [Рецепты миграции WF: отслеживание рабочего процесса](/previous-versions/appfabric/ff383417(v=azure.10))  
 Предоставляет рекомендации по перепроектированию кода отслеживания и конфигурации WF3 при помощи эквивалентного кода отслеживания и конфигурации для WF4.  
  
 [Рекомендации по WF: службы рабочих процессов](/previous-versions/appfabric/ff383417(v=azure.10))  
 Предоставляет построенные на примерах пошаговые инструкции по перепроектированию часто используемых рабочих процессов, которые реализуют веб-службы Windows Communication Foundation (WCF) (называемые службами рабочих процессов), созданные в WF3, для использования средств WF4.  
  
## <a name="see-also"></a>См. также

- <xref:System.Activities.Statements.Interop>
