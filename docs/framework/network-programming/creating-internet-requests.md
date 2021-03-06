---
title: Создание интернет-запросов
description: Сведения о том, как приложения создают экземпляры WebRequest с помощью метода WebRequest.Create, который создает производный класс на основе передаваемой ему схемы URI.
ms.date: 03/30/2017
helpviewer_keywords:
- WebRequest class, sending and receiving data
- Networking
- HttpWebResponse class, sending and receiving data
- requesting data from Internet, creating requests
- Network Resources
- Internet, requesting data
- data requests, creating requests
ms.assetid: faab683e-3f1e-4eee-b5e9-59f7245033d5
ms.openlocfilehash: 389c7bf5969eca4322aa680a6f28dec0b899709a
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325632"
---
# <a name="create-internet-requests"></a>Создание интернет-запросов

Приложения создают экземпляры <xref:System.Net.WebRequest> с помощью метода <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType>. Статический метод <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> создает класс, производный от <xref:System.Net.WebRequest>, на основе переданной ему схемы URI.  
  
## <a name="web-file-and-ftp-requests"></a>Запросы Web, File и FTP

На платформе .NET Framework представлен класс <xref:System.Net.HttpWebRequest>, который является производным от `WebRequest` и обеспечивает обработку запросов HTTP и HTTPS. В большинстве случаев класс `WebRequest` предоставляет все свойства, необходимые для выполнения запроса. Тем не менее при необходимости вы можете приводить объекты `WebRequest`, созданные методом `WebRequest.Create`, к типу `HttpWebRequest` для доступа к свойствам запроса, относящимся к протоколу HTTP. Аналогичным образом объект `HttpWebResponse` обрабатывает ответы на запросы HTTP и HTTPS. Чтобы получить доступ к свойствам `HttpWebResponse`, относящимся к протоколу HTTP, необходимо привести объекты `WebResponse` к типу `HttpWebResponse`.  
  
Платформа .NET Framework также предоставляет классы <xref:System.Net.FileWebRequest> и <xref:System.Net.FileWebResponse> для обработки запросов ресурсов, использующих схему URI "file:". Аналогичным образом, классы <xref:System.Net.FtpWebRequest> и <xref:System.Net.FtpWebResponse> используются для обработки запросов ресурсов, использующих схему "ftp:". Если вы выполняете запросы к ресурсу, использующему любую из этих схем, то можете получить объект, с помощью которого будет выполняться запрос, используя метод `WebRequest.Create`.  
  
Для обработки запросов, использующих другие протоколы уровня приложений, необходимо реализовать классы для определенного протокола, производные от `WebRequest` и `WebResponse`. Дополнительные сведения см. в разделе [Программирование подключаемых протоколов](programming-pluggable-protocols.md).  
  
## <a name="see-also"></a>См. также

- [Практическое руководство. Запрос данных с помощью класса WebRequest](how-to-request-data-using-the-webrequest-class.md)
- [Запрос данных](requesting-data.md)
