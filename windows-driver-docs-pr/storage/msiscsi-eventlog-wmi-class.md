---
title: MSiSCSI\_EventLog WMI 类
description: MSiSCSI\_EventLog WMI 类
ms.assetid: 8fe6c3fd-bb4f-46ac-a69c-5508467b4c70
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 28885833d414c6ee7b2e128f16f9480ee12fede3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379691"
---
# <a name="msiscsieventlog-wmi-class"></a>MSiSCSI\_EventLog WMI 类


MSiSCSI\_EventLog WMI 类用于任何 iSCSI 事件记录到系统事件日志中。 此类定义，如下所示在*Mgmt.mof。*

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_EventLog** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_msiscsi_eventlog)数据结构。

 

 





