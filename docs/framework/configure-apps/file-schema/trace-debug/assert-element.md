---
title: Элемент <assert>
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/assert
- http://schemas.microsoft.com/.NetConfiguration/v2.0#assert
helpviewer_keywords:
- <assert> element
- assert element
ms.assetid: ef4c3229-b151-4d85-8091-e6456af9b935
ms.openlocfilehash: eb29701912a45a484b1716195b449e8a97d1d4b5
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91149300"
---
# <a name="assert-element"></a>Элемент \<assert>

Определяет, должно ли выводиться окно сообщения при вызове метода <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=nameWithType>. Кроме того, задает имя файла, в который записываются сообщения.  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.diagnostics>**](system-diagnostics-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<assert>**

## <a name="syntax"></a>Синтаксис  
  
```xml  
<assert assertuienabled="true|false" logfilename="file name"/>  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  

 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|`assertuienabled`|Необязательный атрибут.<br /><br /> Указывает, следует ли отображать окно сообщения, если метод **Debug. Assert** возвращает **значение false**.|  
|`logfilename`|Необязательный атрибут.<br /><br /> Указывает имя файла, в который будет записано сообщение, если **Debug. Assert** имеет значение **false**.|  
  
## <a name="assertuienabled-attribute"></a>Атрибут ассертуиенаблед  
  
|Значение|Описание|  
|-----------|-----------------|  
|`true`|Отображает окно сообщения. Это значение по умолчанию.|  
|`false`|Не отображает окно сообщения.|  
  
### <a name="child-elements"></a>Дочерние элементы  

 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|  
|`system.diagnostics`|Задает прослушиватели трассировки, собирающие, хранящие и маршрутизирующие сообщения, а также уровень, на котором установлен ключ трассировки.|  
  
## <a name="remarks"></a>Remarks  

 Оба атрибута в **\<assert>** элементе являются необязательными. Можно отключить окна сообщений, не указывая файл для записи в него, или указать файл для записи сообщений при включении входящих в него окон сообщений.  
  
## <a name="example"></a>Пример  

 В следующем примере показано, как отключить отображение окон сообщений при вызове **Debug. Assert** и записи сообщений в `c:\log.txt` .  
  
```xml  
<configuration>  
   <system.diagnostics>  
      <assert assertuienabled="false" logfilename="c:\log.txt"/>  
   </system.diagnostics>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.Diagnostics.Debug>
- [Схема параметров трассировки и отладки](index.md)
