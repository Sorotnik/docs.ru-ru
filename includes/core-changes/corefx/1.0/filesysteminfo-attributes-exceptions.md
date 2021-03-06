---
ms.openlocfilehash: 2ea9abca7578c2ddf92712a1c597f8f1ff4a5c0c
ms.sourcegitcommit: 348bb052d5cef109a61a3d5253faa5d7167d55ac
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "82021813"
---
### <a name="unauthorizedaccessexception-thrown-by-filesysteminfoattributes"></a>Исключение UnauthorizedAccessException, вызванное FileSystemInfo.Attributes

В .NET Core <xref:System.UnauthorizedAccessException> возникает, когда вызывающий пытается задать значение атрибута файла, но у него нет разрешений на запись.

#### <a name="change-description"></a>Описание изменений

В .NET Framework <xref:System.ArgumentException> возникает, когда вызывающий пытается задать значение атрибута файла в <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType>, но у него нет разрешений на запись. В .NET Core вместо него возникает <xref:System.UnauthorizedAccessException> (в .NET Core <xref:System.ArgumentException> по-прежнему возникает, если вызывающий пытается задать недопустимый атрибут файла).

#### <a name="version-introduced"></a>Представленная версия

1.0

#### <a name="recommended-action"></a>Рекомендованное действие

Изменяйте любые инструкции `catch`, чтобы получить <xref:System.UnauthorizedAccessException> вместо или в дополнение к <xref:System.ArgumentException> по мере необходимости.

#### <a name="category"></a>Категория

Библиотеки Core .NET

#### <a name="affected-apis"></a>Затронутые API

- <xref:System.IO.FileSystemInfo.Attributes?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.IO.FileSystemInfo.Attributes`

-->
