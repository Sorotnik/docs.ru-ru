---
title: Количество прерванных операций с поддержкой транзакций в секунду
ms.date: 03/30/2017
ms.assetid: 19fc993f-2b3d-4898-852e-3b98ec2153a5
ms.openlocfilehash: bf7d13f04f0bad315c879f1b4299a78e9515cc56
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90550655"
---
# <a name="transacted-operations-aborted-per-second"></a>Количество прерванных операций с поддержкой транзакций в секунду
Имя счетчика: Количество прерванных операций с поддержкой транзакций в секунду.  
  
## <a name="description"></a>Описание  
 Количество транзакционных операций, прерванных в этой службе за секунду.  
  
 Этот счетчик имеет тип счетчика производительности [PERF_COUNTER_COUNTER](/previous-versions/windows/it-pro/windows-server-2003/cc740048(v=ws.10)), значение которого вычисляется с помощью следующей формулы.  
  
 (N 1 - N 0 ) / ( (D 1 -D 0 ) / F)
