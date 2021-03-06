---
title: <endpoint> - элемент
ms.date: 03/30/2017
ms.assetid: 2fc8fedc-78d0-4e87-8142-fbfd26c15a4e
ms.openlocfilehash: befebc090900576b1e0f7ca679e1f5f5cd15af9a
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/24/2020
ms.locfileid: "91183810"
---
# <a name="endpoint-element"></a>Элемент \<endpoint>

Задает свойства привязки, контракта и адреса для конечной точки службы, которая используется для предоставления доступа к службам.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<services>**](services.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<service>**](service.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<endpoint>**  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<endpoint address="String"
          behaviorConfiguration="String"
          binding="String"
          bindingConfiguration="String"
          bindingName="String"
          bindingNamespace="String"
          contract="String"
          endpointConfiguration="String"
          isSystemEndpoint="Boolean"
          kind="String"
          listenUriMode="Explicit/Unique"
          listenUri="Uri">
</endpoint>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  

 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|address|Строка, содержащая адрес конечной точки. Адрес может быть указан как абсолютный или относительный адрес. Если указан относительный адрес, от соответствующего узла ожидается предоставление базового адреса, подходящего для схемы транспорта, используемой в привязке. Если адрес не настроен, в качестве базового адреса используется адрес соответствующей конечной точки.<br /><br /> Значением по умолчанию является пустая строка.|  
|behaviorConfiguration|Строка, содержащая имя поведения для использования в конечной точке.|  
|binding|Требуемый строковый атрибут, указывающий тип используемой привязки. Чтобы на тип можно было ссылаться, он должен иметь зарегистрированный раздел конфигурации. Тип регистрируется по имени раздела, а не по имени типа привязки.|  
|bindingConfiguration|Строка, указывающая имя привязки для использования при создании экземпляра конечной точки. Имя привязки должно входить в область в точке определения конечной точки. Значение по умолчанию - пустая строка.<br /><br /> Этот атрибут используется вместе с атрибутом `binding` для ссылки на конкретную конфигурацию привязки в файле конфигурации. Задайте этот атрибут, если выполняется попытка использовать пользовательскую привязку. В противном случае может быть создано исключение.|  
|bindingName|Строка, указывающая уникальное полное имя привязки для экспорта определения посредством WSDL. Значением по умолчанию является пустая строка.|  
|bindingNamespace|Строка, указывающая уникальное полное имя пространства имен привязки для экспорта определения посредством WSDL. Значением по умолчанию является пустая строка.|  
|contract|Строка, указывающая, к какому контракту предоставляется доступ этой конечной точкой. В сборке должен быть реализован данный тип контракта. Если реализация службы реализует один тип контракта, это свойство может быть опущено. Значением по умолчанию является пустая строка.|  
|endpointConfiguration|Строка, указывающая имя стандартной конечной точки, задаваемой атрибутом `kind`, который ссылается на дополнительные сведения конфигурации этой конечной точки. Такое же имя должно быть задано в разделе `<standardEndpoints>`.|  
|isSystemEndpoint|Логическое значение, указывающее, является ли конечная точка конечной точкой инфраструктуры.|  
|kind|Строка, указывающая тип применяемой стандартной конечной точки. Тип должен быть зарегистрирован в разделе `<extensions>` или файле machine.config. Если ничего не указано, создается общая конечная точка службы.|  
|listenUriMode|Указывает способ обработки транспортом значения `ListenUri`, предоставленного для ожидания передачи данных службой. Допустимы следующие значения:<br /><br /> -Explicit<br />— Уникальный<br /><br /> Значение по умолчанию - Explicit.|  
|listenUri|Строка, указывающая URI, по которому конечная точка службы ожидает передачи данных. Значением по умолчанию является пустая строка.|  
|name|Необязательный атрибут. Строка, указывающая имя конечной точки службы. По умолчанию используется объединение имени привязки и имя описания контракта. Службы могут иметь несколько конечных точек, поэтому атрибут конечной точки `name` отличается от имени службы.|  
  
### <a name="child-elements"></a>Дочерние элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<headers>](headers.md)|Коллекция заголовков адреса.|  
|[\<identity>](identity.md)|Удостоверение, обеспечивающее проверку подлинности конечной точки другими конечными точками, которые обмениваются с ней сообщениями.|  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<service>](service.md)|Раздел конфигурации, определяющий список конечных точек, к которым может подключаться клиент.|  
  
## <a name="example"></a>Пример  

 Ниже приведен пример конфигурации конечной точки службы.  
  
```xml  
<endpoint address="/HelloWorld/"
          bindingConfiguration="usingDefaults"
          bindingName="MyBinding"
          binding="customBinding"
          contract="HelloWorld">
  <headers>
    <region xmlns="http://tempuri.org/">EastCoast</region>
    <member xmlns="http://tempuri.org/">Gold</member>
  </headers>
</endpoint>
```  
  
## <a name="see-also"></a>См. также раздел

- <xref:System.ServiceModel.Configuration.ServiceEndpointElement>
- <xref:System.ServiceModel.EndpointAddress>
- <xref:System.ServiceModel.Description.ServiceEndpoint>
- [Конечные точки: адреса, привязки и контракты](../../../wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)
- [Практическое руководство. Создание конечной точки службы в конфигурации](../../../wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)
