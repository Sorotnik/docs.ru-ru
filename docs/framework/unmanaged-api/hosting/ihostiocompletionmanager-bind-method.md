---
title: Метод IHostIoCompletionManager::Bind
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.Bind
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::Bind
helpviewer_keywords:
- IHostIoCompletionManager::Bind method [.NET Framework hosting]
- Bind method [.NET Framework hosting]
ms.assetid: acd74cb5-7e22-4a07-83c3-82288e1abd9f
topic_type:
- apiref
ms.openlocfilehash: 8d18e6c1dca7f52b17c19f4638410a08866905f7
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804801"
---
# <a name="ihostiocompletionmanagerbind-method"></a>Метод IHostIoCompletionManager::Bind
Привязывает указанный маркер к порту завершения ввода-вывода, созданному предыдущим вызовом метода [CreateIoCompletionPort](ihostiocompletionmanager-createiocompletionport-method.md).  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
HRESULT Bind (  
    [in] HANDLE hPort,  
    [in] HANDLE hHandle  
);  
```  
  
## <a name="parameters"></a>Параметры  
 `hPort`  
 окне Порт завершения ввода-вывода, к которому выполняется привязка `hHandle` . Если значение `hPort` равно null, `hHandle` привязывается к порту завершения ввода-вывода по умолчанию.  
  
 `hHandle`  
 окне Обработчик операционной системы для привязки `hPort` .  
  
## <a name="return-value"></a>Возвращаемое значение  
  
|HRESULT|Описание|  
|-------------|-----------------|  
|S_OK|`Bind`успешно возвращено.|  
|HOST_E_CLRNOTAVAILABLE|Среда CLR не была загружена в процесс, или среда CLR находится в состоянии, в котором она не может выполнить управляемый код или успешно обработать вызов.|  
|HOST_E_TIMEOUT|Время ожидания вызова истекло.|  
|HOST_E_NOT_OWNER|Вызывающий объект не владеет блокировкой.|  
|HOST_E_ABANDONED|Событие было отменено, пока заблокированный поток или волокно ожидают его.|  
|E_FAIL|Произошла неизвестная фатальная ошибка. Когда метод возвращает E_FAIL, среда CLR больше не может использоваться в процессе. Последующие вызовы методов размещения возвращают HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Замечания  
 Порт завершения ввода-вывода создается с помощью вызова `CreateIoCompletionPort` . Среда CLR вызывает `Bind` для привязки маркера к этому порту.  
  
> [!NOTE]
> По завершении запроса ввода-вывода узел должен вызвать метод [ICLRIoCompletionManager:: OnComplete](iclriocompletionmanager-oncomplete-method.md) .  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../get-started/system-requirements.md).  
  
 **Заголовок:** MSCorEE. h  
  
 **Библиотека:** Включается в качестве ресурса в библиотеку MSCorEE. dll  
  
 **.NET Framework версии:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>См. также статью

- [Интерфейс ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
