---
title: Метод ICorProfilerCallback3::ProfilerDetachSucceeded
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3.ProfilerDetachSucceeded Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3::ProfilerDetachSucceeded
helpviewer_keywords:
- ProfilerDetachSucceeded method [.NET Framework profiling]
- ICorProfilerCallback3::ProfilerDetachSucceeded method [.NET Framework profiling]
ms.assetid: 05164966-16ce-4cc9-a530-43a640c00711
topic_type:
- apiref
ms.openlocfilehash: 93406dddf7babd8cf61032666737b993c2f721f4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499601"
---
# <a name="icorprofilercallback3profilerdetachsucceeded-method"></a>Метод ICorProfilerCallback3::ProfilerDetachSucceeded
Уведомляет профилировщик о том, что среда CLR намерена выгрузить библиотеку DLL профилировщика.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT ProfilerDetachSucceeded();  
```  
  
## <a name="return-value"></a>Возвращаемое значение  
 Возвращаемое значение этого обратного вызова игнорируется.  
  
## <a name="remarks"></a>Примечания  
 Обратный вызов `ProfilerDetachSucceeded` производится после того, как все потоки вышли из кода профилировщика. Когда вызывается этот метод, профилировщик должен выполнить все завершающие задачи, которые не может выполнить его деструктор, такие как уведомление интерфейса пользователя или компонента ведения журнала. Однако профилировщик не должен вызывать функции для интерфейсов, предоставляемых средой CLR во время этого обратного вызова (например, в [ICorProfilerInfo](icorprofilerinfo-interface.md) или `IMetaData*` интерфейсах).  
  
 Среда CLR создает запись в журнале событий приложений Windows о том, что операция отключения выполнена успешно.  
  
 После возврата профилировщика из этого обратного вызова среда CLR освобождает объект профилировщика и выгружает библиотеку DLL профилировщика. Поэтому после возврата из обратного вызова профилировщик не должен выполнять никаких действий, которые вызовут выполнение кода в библиотеке DLL профилировщика. Например, он не должен создавать потоки или регистрировать обратные вызовы таймера.  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** CorProf.idl, CorProf.h  
  
 **Библиотека:** CorGuids.lib  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Интерфейсы метаданных](../metadata/metadata-interfaces.md)
- [Интерфейс ICorProfilerInfo3](icorprofilerinfo3-interface.md)
- [Профилирующие интерфейсы](profiling-interfaces.md)
- [Профилирование](index.md)
