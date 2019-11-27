---
ms.openlocfilehash: 7d40324e6b0bc4afab9dd39b236f0909f360cc9b
ms.sourcegitcommit: 2e95559d957a1a942e490c5fd916df04b39d73a9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2019
ms.locfileid: "72394270"
---
### <a name="caching-compactonmemorypressure-property-removed"></a><span data-ttu-id="cdb95-101">Кэширование: свойство CompactOnMemoryPressure удалено</span><span class="sxs-lookup"><span data-stu-id="cdb95-101">Caching: CompactOnMemoryPressure property removed</span></span>

<span data-ttu-id="cdb95-102">В выпуске ASP.NET Core 3.0 недоступны [устаревшие API MemoryCacheOptions](https://github.com/aspnet/Extensions/blob/dc5c593da7b72c82e6fe85abb91d03818f9b700c/src/Caching/Memory/src/MemoryCacheOptions.cs#L17-L18).</span><span class="sxs-lookup"><span data-stu-id="cdb95-102">The ASP.NET Core 3.0 release removed the [obsolete MemoryCacheOptions APIs](https://github.com/aspnet/Extensions/blob/dc5c593da7b72c82e6fe85abb91d03818f9b700c/src/Caching/Memory/src/MemoryCacheOptions.cs#L17-L18).</span></span>

#### <a name="change-description"></a><span data-ttu-id="cdb95-103">Описание изменений</span><span class="sxs-lookup"><span data-stu-id="cdb95-103">Change description</span></span>

<span data-ttu-id="cdb95-104">Это изменение реализовано в рамках исправления [aspnet/Caching#221](https://github.com/aspnet/Caching/issues/221).</span><span class="sxs-lookup"><span data-stu-id="cdb95-104">This change is a follow-up to [aspnet/Caching#221](https://github.com/aspnet/Caching/issues/221).</span></span> <span data-ttu-id="cdb95-105">Обсуждение этого вопроса см. на странице [aspnet/Extensions#1062](https://github.com/aspnet/Extensions/issues/1062).</span><span class="sxs-lookup"><span data-stu-id="cdb95-105">For discussion, see [aspnet/Extensions#1062](https://github.com/aspnet/Extensions/issues/1062).</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="cdb95-106">Представленная версия</span><span class="sxs-lookup"><span data-stu-id="cdb95-106">Version introduced</span></span>

<span data-ttu-id="cdb95-107">3.0</span><span class="sxs-lookup"><span data-stu-id="cdb95-107">3.0</span></span>

#### <a name="old-behavior"></a><span data-ttu-id="cdb95-108">Старое поведение</span><span class="sxs-lookup"><span data-stu-id="cdb95-108">Old behavior</span></span>

<span data-ttu-id="cdb95-109">Свойство `MemoryCacheOptions.CompactOnMemoryPressure` было доступно.</span><span class="sxs-lookup"><span data-stu-id="cdb95-109">`MemoryCacheOptions.CompactOnMemoryPressure` property was available.</span></span>

#### <a name="new-behavior"></a><span data-ttu-id="cdb95-110">Новое поведение</span><span class="sxs-lookup"><span data-stu-id="cdb95-110">New behavior</span></span>

<span data-ttu-id="cdb95-111">Свойство `MemoryCacheOptions.CompactOnMemoryPressure` было удалено.</span><span class="sxs-lookup"><span data-stu-id="cdb95-111">The `MemoryCacheOptions.CompactOnMemoryPressure` property has been removed.</span></span>

#### <a name="reason-for-change"></a><span data-ttu-id="cdb95-112">Причина изменения</span><span class="sxs-lookup"><span data-stu-id="cdb95-112">Reason for change</span></span>

<span data-ttu-id="cdb95-113">Автоматическое сжатие кэша приводило к возникновению проблем.</span><span class="sxs-lookup"><span data-stu-id="cdb95-113">Automatically compacting the cache caused problems.</span></span> <span data-ttu-id="cdb95-114">Чтобы не допустить непредвиденное поведение, сжимайте кэш только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="cdb95-114">To avoid unexpected behavior, the cache should only be compacted when needed.</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="cdb95-115">Рекомендуемое действие</span><span class="sxs-lookup"><span data-stu-id="cdb95-115">Recommended action</span></span>

<span data-ttu-id="cdb95-116">Чтобы сжать кэш, выполните приведение с понижением к `MemoryCache` и вызовите `Compact` при необходимости.</span><span class="sxs-lookup"><span data-stu-id="cdb95-116">To compact the cache, downcast to `MemoryCache` and call `Compact` when needed.</span></span>

#### <a name="category"></a><span data-ttu-id="cdb95-117">Категория</span><span class="sxs-lookup"><span data-stu-id="cdb95-117">Category</span></span>

<span data-ttu-id="cdb95-118">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="cdb95-118">ASP.NET Core</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="cdb95-119">Затронутые API</span><span class="sxs-lookup"><span data-stu-id="cdb95-119">Affected APIs</span></span>

<xref:Microsoft.Extensions.Caching.Memory.MemoryCacheOptions.CompactOnMemoryPressure%2A?displayProperty=nameWithType>

<!--

#### Affected APIs

`Overload:Microsoft.Extensions.Caching.Memory.MemoryCacheOptions.CompactOnMemoryPressure`

-->