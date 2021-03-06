---
title: Использование System.Xml
ms.date: 10/22/2008
ms.assetid: 82302f0d-a621-4c6f-b57d-999bd61f21a6
ms.openlocfilehash: a01799bd130de0222d4d66dee4955375c1a1911f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/18/2020
ms.locfileid: "94828599"
---
# <a name="systemxml-usage"></a>Использование System.Xml
В этом разделе рассказывается об использовании нескольких типов, находящихся в <xref:System.Xml?displayProperty=nameWithType> пространствах имен, которые могут использоваться для представления XML-данных.

 ❌ НЕ используйте <xref:System.Xml.XmlNode> или <xref:System.Xml.XmlDocument> для представления XML-данных. Используйте <xref:System.Xml.XPath.IXPathNavigable> вместо этого экземпляры, <xref:System.Xml.XmlReader> , <xref:System.Xml.XmlWriter> или подтипы <xref:System.Xml.Linq.XNode> . `XmlNode` и `XmlDocument` не предназначены для предоставления открытым API.

 ✔️ использовать `XmlReader` `IXPathNavigable` подтипы, или `XNode` в качестве входных или выходных данных членов, принимающих или возвращающих XML.

 Используйте эти абстракции вместо `XmlDocument` , `XmlNode` или <xref:System.Xml.XPath.XPathDocument> , так как это отделяет методы от конкретных реализаций XML-документа в памяти и позволяет им работать с виртуальными ИСТОЧНИКами данных XML, которые предоставляют `XNode` , `XmlReader` или <xref:System.Xml.XPath.XPathNavigator> .

 ❌ НЕ подклассировать, `XmlDocument` Если необходимо создать тип, представляющий представление XML базовой объектной модели или источника данных.

 *Части © 2005, 2009 Корпорация Майкрософт. Все права защищены.*

 *Перепечатано с разрешения Pearson Education, Inc. из книги [Инфраструктура программных проектов. Соглашения, идиомы и шаблоны для многократно используемых библиотек .NET (2-е издание)](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619), авторы: Кржиштоф Цвалина (Krzysztof Cwalina) и Брэд Абрамс (Brad Abrams). Книга опубликована 22 октября 2008 г. издательством Addison-Wesley Professional в рамках серии, посвященной разработке для Microsoft Windows.*

## <a name="see-also"></a>См. также статью

- [Рекомендации по проектированию платформы](index.md)
- [Рекомендации по использованию](usage-guidelines.md)
