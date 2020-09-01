---
title: MSiSCSI \_ EVENTLOG WMI 类
description: MSiSCSI \_ EVENTLOG WMI 类
ms.assetid: 8fe6c3fd-bb4f-46ac-a69c-5508467b4c70
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7f8f7f5e3fe8b5429883c0c0ebf621fe269ad69b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193189"
---
# <a name="msiscsi_eventlog-wmi-class"></a>MSiSCSI \_ EVENTLOG WMI 类


MSiSCSI \_ EVENTLOG WMI 类用于将任何 iSCSI 事件记录到系统事件日志中。 此类在*管理 mof*中定义为：

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

 

