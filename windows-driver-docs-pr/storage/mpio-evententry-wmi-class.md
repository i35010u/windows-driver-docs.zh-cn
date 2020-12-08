---
title: MPIO \_ EVENTENTRY WMI 类
description: MPIO \_ EVENTENTRY WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e403ba34f2da9ab79c8e2b40540ddc944966510f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811561"
---
# <a name="mpio_evententry-wmi-class"></a>MPIO \_ EVENTENTRY WMI 类


MPIO 驱动程序使用 MPIO \_ EVENTENTRY WMI 类来报告与 MPIO 相关的任何事件。 当前未实现此类。

```cpp
class MPIO_EventEntry : WMIEvent
{
        [key, read]
        string InstanceName;

        [read]
        boolean Active;

        //
        // Current system time at time of logging.
        //
        [WmiDataId(1),
         read,
         Description("Time Stamp") : amended,
         WmiTimeStamp
        ] uint64 TimeStamp;

        //
        // Indicates severity of event being logged.
        //
        [WmiDataId(2),
        read,
        Values{"Fatal Error",
               "Error",
               "Warning",
               "Information"} : amended,

        DefineValues{"MPIO_FATAL_ERROR",
                     "MPIO_ERROR",
                     "MPIO_WARNING",
                     "MPIO_INFORMATION"},

        ValueMap{"1", "2", "3", "4"}
        ] uint32 Severity;

        //
        // Multi-path disk's name that this event is being logged for.
        //
        [WmiDataId(3),
        read,
        MaxLen(63),
        Description("Component") : amended
        ] string Component;

        //
        // Description of event.
        //
        [WmiDataId(4),
        read,
        MaxLen(63),
        Description("Event Description") : amended
        ] string EventDescription;
};
```

没有与此 WMI 类相关联的方法。

 

 





