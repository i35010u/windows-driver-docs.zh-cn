---
title: MSiSCSI \_ EVENTLOG WMI 类
description: MSiSCSI \_ EVENTLOG WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ed1af86cd16f9b5a04ee7695f9e39e372b22dcbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785513"
---
# <a name="msiscsi_eventlog-wmi-class"></a>MSiSCSI \_ EVENTLOG WMI 类


MSiSCSI \_ EVENTLOG WMI 类用于将任何 iSCSI 事件记录到系统事件日志中。 此类在 *管理 mof* 中定义为：

```cpp
class MSiSCSI_Eventlog : __ExtrinsicEvent
{
    [key] 
    string InstanceName;
 
    boolean Active;
 
    [WmiDataId(1),
     EVENTLOG_MESSAGE_QUALIFIERS
    ]
    uint32 Type;

    [WmiDataId(2),
     Description("If zero, then this event is not logged to system eventlog") : amended
    ]
    uint32 LogToEventlog;

    [WmiDataId(3),
     Description("Size of Additional Data") : amended
    ]
    uint32 Size;

    [WmiDataId(4),
     WmiSizeIs("Size"),
     Description("Additional data to include in eventlog message, typically iSCSI Header") : amended
    ]
    uint8 AdditionalData[];    
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ EventLog**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_eventlog) 数据结构。

 

