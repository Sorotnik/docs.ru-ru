---
title: Элемент <shadowCopyVerifyByTimestamp>
ms.date: 03/30/2017
helpviewer_keywords:
- <shadowCopyTimeStampVerification> element
- shadowCopyTimeStampVerification element
ms.assetid: 2f1648e5-997b-435e-a4f9-d236c574c66c
ms.openlocfilehash: c0dc190e69ca9650d518ee297b12f79f8c47d58b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183979"
---
# <a name="shadowcopyverifybytimestamp-element"></a>Элемент \<shadowCopyVerifyByTimestamp>

Указывает, использует ли теневое копирование поведение при запуске по умолчанию, представленное в .NET Framework 4, или возвращается к поведению при запуске более ранних версий .NET Framework.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<runtime>**](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp;**\<shadowCopyVerifyByTimestamp>**  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<shadowCopyVerifyByTimestamp enabled="true|false" />  
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  

 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|Включено|Обязательный атрибут.<br /><br /> Указывает, были ли домены приложений, использующие теневое копирование, сравниваются метки времени сборки при запуске, чтобы определить, обновлена ли сборка перед теневым копированием сборки.|  
  
## <a name="enabled-attribute"></a>Атрибут enabled  
  
|Значение|Описание|  
|-----------|-----------------|  
|Да|При запуске копирует только сборки, которые были обновлены с момента последнего копирования в каталог теневых копий. Это значение по умолчанию для .NET Framework 4.|  
|false|Восстанавливает поведение при запуске предыдущих версий .NET Framework, при запуске которого были скопированы все файлы.|  
  
### <a name="child-elements"></a>Дочерние элементы  

 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|`configuration`|Корневой элемент в любом файле конфигурации, используемом средой CLR и приложениями .NET Framework.|  
|`runtime`|Содержит сведения о привязке сборок и сборке мусора.|  
  
## <a name="remarks"></a>Remarks  

 Начиная с .NET Framework 4 сборки копируются только в том случае, если их метки времени указывают, что они изменились с момента последнего копирования в каталог теневых копий. Это улучшает время запуска для многих приложений, использующих теневое копирование, как описано в разделе [теневое копирование сборок](../../../app-domains/shadow-copy-assemblies.md). Для приложений с большим процентом и высокой частотой обновления сборок это изменение в поведении может не быть выгодно. В этом случае можно использовать этот элемент для восстановления поведения предыдущих версий платформы .NET Framework.  
  
## <a name="example"></a>Пример  

 В следующем примере показано, как отключить поведение при запуске теневого копирования по умолчанию в .NET Framework 4 и вернуться к режиму запуска предыдущих версий .NET Framework.  
  
```xml  
<configuration>  
   <runtime>  
      <shadowCopyVerifyByTimestamp enabled="false" />  
   </runtime>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также раздел

- [Схема параметров среды выполнения](index.md)
- [Схема файла конфигурации](../index.md)
- [Теневое копирование сборок](../../../app-domains/shadow-copy-assemblies.md)
