---
ms.openlocfilehash: 2edb06106283c26573863f230e5e9956728cdfa3
ms.sourcegitcommit: b1442669f1982d3a1cb18ea35b5acfb0fc7d93e4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/30/2020
ms.locfileid: "93135967"
---

### <a name="install-the-sdk"></a>Установка пакета SDK

Пакет SDK для .NET Core позволяет разрабатывать приложения с помощью .NET Core. При установке пакета SDK для .NET Core не нужно устанавливать соответствующую среду выполнения. Чтобы установить пакет SDK для .NET Core, выполните следующие команды:

```bash
sudo dnf install dotnet-sdk-3.1
```

### <a name="install-the-runtime"></a>Установка среды выполнения

Среда выполнения .NET Core позволяет запускать приложения, созданные с помощью версии .NET Core без поддержки среды выполнения. Приведенные ниже команды позволяют установить среду выполнения ASP.NET Core, которая больше всего совместима с .NET Core. В терминале выполните приведенные ниже команды.

```bash
sudo dnf install aspnetcore-runtime-3.1
```

В качестве альтернативы среде выполнения ASP.NET Core вы можете установить среду выполнения .NET Core без поддержки ASP.NET Core. Для этого в приведенной выше команде замените `aspnetcore-runtime-3.1` на `dotnet-runtime-3.1`.

```bash
sudo dnf install dotnet-runtime-3.1
```
