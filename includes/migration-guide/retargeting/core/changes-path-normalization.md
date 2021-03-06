---
ms.openlocfilehash: 7c4b9faf25853c1c7a546f06c329f6f153eef904
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606652"
---
### <a name="changes-in-path-normalization"></a>Изменения нормализации путей

#### <a name="details"></a>Подробнее

Начиная с приложений, предназначенных для .NET Framework 4.6.2, был изменен способ нормализации путей в среде выполнения. Нормализация пути включает в себя изменение строки, обозначающей путь или файл, чтобы эта строка соответствовала допустимому пути в целевой операционной системе. Нормализация обычно включает в себя:

- канонизацию разделителей компонентов и каталогов;
- применение текущего каталога к относительному пути;
- оценку относительного каталога (.) или родительского каталога (..) в пути;
- обрезку указанных символов.
Начиная с приложений, предназначенных для .NET Framework 4.6.2, следующие изменения в нормализации пути включены по умолчанию:
  - Среда выполнения перекладывает нормализацию путей на функцию [GetFullPathName](/windows/desktop/api/fileapi/nf-fileapi-getfullpathnamew) операционной системы.
- Нормализация больше не предусматривает обрезки окончания сегментов каталогов (например, пробела в конце имени каталога).
- Поддержка синтаксиса пути устройства в режиме полного доверия, включая `\\.\` и (для API-интерфейсов файлового ввода-вывода в mscorlib.dll) `\\?\`.
- Среда выполнения не проверяет пути с синтаксисом устройства.
- Поддерживается использование синтаксиса устройства для доступа к альтернативным потокам данных.
Эти изменения улучшают производительность, позволяя методам получать доступ к ранее недоступным путям. Это изменение не влияет на приложения, предназначенные для .NET Framework 4.6.1 и более ранних версий, но работающие на платформе .NET Framework 4.6.2 или более новой версии.

#### <a name="suggestion"></a>Предложение

В приложениях, предназначенных для .NET Framework 4.6.2 или более поздней версии, данное изменение можно отключить и использовать устаревшую нормализацию, добавив следующее в раздел `<runtime>` файла конфигурации приложения:

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=true" />
</runtime>
```

В приложениях, предназначенных для .NET Framework 4.6.1 или более ранней версии, но работающих на платформе .NET Framework 4.6.2 или более поздней версии, можно включить изменения в нормализацию пути, добавив следующее в раздел `<runtime>` файла конфигурации приложения:

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.IO.UseLegacyPathHandling=false" />
</runtime>
```

| name    | Значение       |
|:--------|:------------|
| Область   | Дополнительный номер       |
| Version | 4.6.2       |
| Type    | Изменение целевой платформы |
