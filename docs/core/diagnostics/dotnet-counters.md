---
title: dotnet-counters (.NET Core)
description: Сведения о том, как установить и использовать программу командной строки dotnet-counter.
ms.date: 02/26/2020
ms.openlocfilehash: 6a4fd92540dbc16173dfa3a10ff9dfaa1f31f7d0
ms.sourcegitcommit: 7476c20d2f911a834a00b8a7f5e8926bae6804d9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/11/2020
ms.locfileid: "88062903"
---
# <a name="dotnet-counters"></a>dotnet-counters

**Эта статья относится к следующему.** ✔️ SDK для .NET Core 3.0 и более поздних версий

## <a name="install-dotnet-counters"></a>Установка dotnet-counters

Чтобы установить последнюю версию [пакета NuGet](https://www.nuget.org/packages/dotnet-counters) `dotnet-counters`, используйте команду [dotnet tool install](../tools/dotnet-tool-install.md).

```dotnetcli
dotnet tool install --global dotnet-counters
```

## <a name="synopsis"></a>Краткий обзор

```console
dotnet-counters [-h|--help] [--version] <command>
```

## <a name="description"></a>Описание

`dotnet-counters` — это средство мониторинга производительности и первого уровня анализа производительности. Оно умеет отслеживать значения счетчиков производительности, опубликованные через API <xref:System.Diagnostics.Tracing.EventCounter>. Например, вы можете быстро отслеживать такие параметры, как загрузка ЦП или частота возникновения исключений в приложении .NET Core, чтобы обнаружить подозрительное поведение перед началом более серьезных расследований с помощью `PerfView` или `dotnet-trace`.

## <a name="options"></a>Параметры

- **`--version`**

  Отображение версии служебной программы dotnet-counters.

- **`-h|--help`**

  Отображение справки в командной строке.

## <a name="commands"></a>Команды

| Команда                                             |
|-----------------------------------------------------|
| [dotnet-counters collect](#dotnet-counters-collect) |
| [dotnet-counters list](#dotnet-counters-list)       |
| [dotnet-counters monitor](#dotnet-counters-monitor) |
| [dotnet-counters ps](#dotnet-counters-ps)           |

## <a name="dotnet-counters-collect"></a>dotnet-counters collect

Периодический сбор выбранных значений счетчиков и их экспорт в указанном формате файла для последующей обработки.

### <a name="synopsis"></a>Краткий обзор

```console
dotnet-counters collect [-h|--help] [-p|--process-id] [--refreshInterval] [counter_list] [--format] [-o|--output]
```

### <a name="options"></a>Параметры

- **`-p|--process-id <PID>`**

  Идентификатор отслеживаемого процесса.

- **`--refresh-interval <SECONDS>`**

  Время (в секундах) между обновлением значений отображаемых счетчиков

- **`counter_list <COUNTERS>`**

  Список счетчиков, разделенный пробелами. Вы можете объявить счетчики как `provider_name[:counter_name]`. Если используется `provider_name` без указания `counter_name`, отображаются все счетчики. Для обнаружения имен поставщиков и счетчиков используйте команду [dotnet-counters list](#dotnet-counters-list).

- **`--format <csv|json>`**

  Экспортируемый формат. В настоящее время доступно: csv, json.

- **`-o|--output <output>`**

  Имя выходного файла.

### <a name="examples"></a>Примеры

- Сбор всех счетчиков с интервалом обновления в 3 секунды и создание CSV-файла в качестве выходных данных:

  ```console
  > dotnet-counters collect --process-id 1902 --refresh-interval 3 --format csv

  counter_list is unspecified. Monitoring all counters by default.
  Starting a counter session. Press Q to quit.
  ```

## <a name="dotnet-counters-list"></a>dotnet-counters list

Отображение списка имен и описаний счетчиков, сгруппированных по поставщикам.

### <a name="synopsis"></a>Краткий обзор

```console
dotnet-counters list [-h|--help]
```

### <a name="example"></a>Пример

```console
> dotnet-counters list
Showing well-known counters only. Specific processes may support additional counters.

System.Runtime
    cpu-usage                                    Amount of time the process has utilized the CPU (ms)
    working-set                                  Amount of working set used by the process (MB)
    gc-heap-size                                 Total heap size reported by the GC (MB)
    gen-0-gc-count                               Number of Gen 0 GCs / min
    gen-1-gc-count                               Number of Gen 1 GCs / min
    gen-2-gc-count                               Number of Gen 2 GCs / min
    time-in-gc                                   % time in GC since the last GC
    gen-0-size                                   Gen 0 Heap Size
    gen-1-size                                   Gen 1 Heap Size
    gen-2-size                                   Gen 2 Heap Size
    loh-size                                     LOH Heap Size
    alloc-rate                                   Allocation Rate
    assembly-count                               Number of Assemblies Loaded
    exception-count                              Number of Exceptions / sec
    threadpool-thread-count                      Number of ThreadPool Threads
    monitor-lock-contention-count                Monitor Lock Contention Count
    threadpool-queue-length                      ThreadPool Work Items Queue Length
    threadpool-completed-items-count             ThreadPool Completed Work Items Count
    active-timer-count                           Active Timers Count

Microsoft.AspNetCore.Hosting
    requests-per-second                  Request rate
    total-requests                       Total number of requests
    current-requests                     Current number of requests
    failed-requests                      Failed number of requests
```

> [!NOTE]
> Счетчики `Microsoft.AspNetCore.Hosting` отображаются при обнаружении процессов, поддерживающих эти счетчики, например при запуске приложения ASP.NET Core на хост-компьютере.

## <a name="dotnet-counters-monitor"></a>dotnet-counters monitor

Отображение периодически обновляемых значений для выбранных счетчиков.

### <a name="synopsis"></a>Краткий обзор

```console
dotnet-counters monitor [-h|--help] [-p|--process-id] [--refreshInterval] [counter_list]
```

### <a name="options"></a>Параметры

- **`-p|--process-id <PID>`**

  Идентификатор отслеживаемого процесса.

- **`--refresh-interval <SECONDS>`**

  Время (в секундах) между обновлением значений отображаемых счетчиков

- **`counter_list <COUNTERS>`**

  Список счетчиков, разделенный пробелами. Вы можете объявить счетчики как `provider_name[:counter_name]`. Если используется `provider_name` без указания `counter_name`, отображаются все счетчики. Для обнаружения имен поставщиков и счетчиков используйте команду [dotnet-counters list](#dotnet-counters-list).

### <a name="examples"></a>Примеры

- Мониторинг всех счетчиков из `System.Runtime` с интервалом обновления 3 секунды:

  ```console
  > dotnet-counters monitor --process-id 1902  --refresh-interval 3 System.Runtime

  Press p to pause, r to resume, q to quit.
    System.Runtime:
      CPU Usage (%)                                 24
      Working Set (MB)                            1982
      GC Heap Size (MB)                            811
      Gen 0 GC / second                             20
      Gen 1 GC / second                              4
      Gen 2 GC / second                              1
      Number of Exceptions / sec                     4
  ```

- Мониторинг только счетчиков использования ЦП и размера кучи GC из `System.Runtime`:

  ```console
  > dotnet-counters monitor --process-id 1902 System.Runtime[cpu-usage,gc-heap-size]

  Press p to pause, r to resume, q to quit.
    System.Runtime:
      CPU Usage (%)                                 24
      GC Heap Size (MB)                            811
  ```

- Мониторинг значений `EventCounter` из определяемых пользователем `EventSource`: Дополнительные сведения см. в статье [Руководство. Измерение производительности с помощью EventCounters в .NET Core](event-counter-perf.md).

  ```console
  > dotnet-counters monitor --process-id 1902 Samples-EventCounterDemos-Minimal

  Press p to pause, r to resume, q to quit.
      request                                      100
  ```
  
## <a name="dotnet-counters-ps"></a>dotnet-counters ps

Отображение списка процессов dotnet, которые можно отслеживать.

### <a name="synopsis"></a>Краткий обзор

```console
dotnet-counters ps [-h|--help]
```

### <a name="example"></a>Пример

```console
> dotnet-counters ps
  
  15683 WebApi     /home/suwhang/repos/WebApi/WebApi
  16324 dotnet     /usr/local/share/dotnet/dotnet
```
