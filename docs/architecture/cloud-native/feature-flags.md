---
title: Флаги компонентов
description: Реализация флагов функций в собственных облачных приложениях с использованием конфигурации приложения Azure
author: robvet
ms.date: 05/13/2020
ms.openlocfilehash: ee45c9f187b056887ea6dd3a08da508afca51987
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91158101"
---
# <a name="feature-flags"></a>Флаги компонентов

В главе 1 мы подтверждаем, что облачная машинная поддержка очень важна для ускорения и гибкости. Пользователи предполагают быстрое реагирование, инновационные функции и нулевое время простоя. `Feature flags` — Это современный метод развертывания, который помогает повысить гибкость облачных приложений. Они позволяют развертывать новые функции в рабочей среде, но ограничивать их доступность. С помощью жеста коммутатора можно активировать новую функцию для конкретных пользователей без перезапуска приложения или развертывания нового кода. Они отделяют выпуск новых функций от развертывания кода.

Флаги функций создаются на основе условной логики, которая контролирует видимость функций для пользователей во время выполнения. В современных облачных системах часто развертывать новые функции в рабочей среде, но тестировать их с ограниченной аудиторией. По мере роста уверенности функция может быть постепенно сведена к более широкой аудитории.

Ниже приведены другие варианты использования флагов компонентов.

- Ограничьте функциональные возможности уровня "Премиум" конкретными группами клиентов, которые хотят платить более высокие платежи по подписке.
- Стабилизация системы за счет быстрой деактивации функции, которая позволяет избежать риска отката или немедленного исправления.
- Отключите дополнительную функцию с высоким потреблением ресурсов во время пиковых периодов использования.
- Проведите `experimental feature releases` до небольших сегментов пользователей, чтобы проверить возможность и популярность.

Флаги функций также доразвивают `trunk-based` разработку. Это модель ветвления системы управления версиями, в которой разработчики совместно работают над функциями в одной ветви. Этот подход позволяет снизить риск и сложность объединения большого числа длительно выполняемых ветвей компонентов. Функции недоступны до тех пор, пока не будут активированы.

## <a name="implementing-feature-flags"></a>Реализация флагов функций

По сути, флаг функции является ссылкой на простой `decision object` . Он возвращает логическое состояние `on` или `off` . Флаг обычно заключает в оболочку блок кода, который инкапсулирует возможность функции. Состояние флага определяет, выполняется ли этот блок кода для данного пользователя. На рис. 10-11 показана реализация.

```csharp
if (featureFlag) {
    // Run this code block if the featureFlag value is true
} else {
    // Run this code block if the featureFlag value is false
}
```

**Рис. 10-11** -простая реализация флага функции.

Обратите внимание, что этот подход отделяет логику принятия решений от кода функции.

В главе 1 мы обсуждали `Twelve-Factor App` . Рекомендуется хранить параметры конфигурации, которые являются внешними по отношению к исполняемому коду приложения. При необходимости параметры можно считывать из внешнего источника. Значения конфигурации флагов компонентов также должны быть независимыми от своей базы кода. По конфигурации флага выведения в отдельном репозитории можно изменить состояние флага без изменения и повторного развертывания приложения.

[Конфигурация приложений Azure](/azure/azure-app-configuration/overview) предоставляет централизованный репозиторий для флагов функций. С его помощью вы можете быстро и уверенно определять различные типы флагов функций и манипулировать их состояниями. Добавьте клиентские библиотеки конфигурации приложений в приложение, чтобы включить функцию флагов компонентов. Поддерживаются различные платформы языка программирования.

Флаги компонентов можно легко реализовать в [службе ASP.NET Core](/azure/azure-app-configuration/use-feature-flags-dotnet-core). Установка библиотек управления функциями .NET и поставщика конфигурации приложений позволяет декларативно добавлять в код флаги компонентов. Они включают `FeatureGate` атрибуты, чтобы не нужно было вручную писать операторы if в базе кода.

После настройки в классе Startup можно добавить функциональные возможности флагов компонентов на уровне контроллера, действия или по промежуточного слоя. На рисунке 10-12 представлена реализация контроллера и действия:

```csharp
[FeatureGate(MyFeatureFlags.FeatureA)]
public class ProductController : Controller
{
    ...
}
```

```csharp
[FeatureGate(MyFeatureFlags.FeatureA)]
public IActionResult UpdateProductStatus()
{
    return ObjectResult(ProductDto);
}
```

**Рис. 10-12** . Реализация флага функции в контроллере и действии.

Если флаг функции отключен, пользователь получит код состояния 404 (не найдено) без текста ответа.

Флаги компонентов также можно внедрять непосредственно в классы C#. На рис. 10-13 показано внедрение флагов функций:

```csharp
public class ProductController : Controller
{
    private readonly IFeatureManager _featureManager;

    public ProductController(IFeatureManager featureManager)
    {
        _featureManager = featureManager;
    }
}
```

**Рис. 10-13** . Встраивание флага функции в класс.

Библиотеки управления функциями управляют жизненным циклом флага компонента в фоновом режиме. Например, чтобы максимально ограничить большое число вызовов хранилища конфигурации, в библиотеках флаги кэшируют состояние на указанный период времени. Они могут гарантировать неизменность состояний флага во время вызова запроса. Они также предлагают `Point-in-time snapshot` . Вы можете восстановить историю любого значения ключа и предоставить свое значение в любое время в течение предыдущих семи дней.

>[!div class="step-by-step"]
>[Назад](devops.md)
>[Вперед](infrastructure-as-code.md)
