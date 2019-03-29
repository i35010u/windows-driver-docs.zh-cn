---
title: ISCSI\_路径 WMI 类
description: ISCSI\_路径 WMI 类
ms.assetid: d4067869-2c67-42d3-988e-af825549853d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b9a3c1dad6878eba817bf4ceb7bf23419ab89e8e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566993"
---
# <a name="iscsipath-wmi-class"></a>ISCSI\_路径 WMI 类


ISCSI\_路径 WMI 类包含有关 iSCSI 门户的连接的信息。 此类定义，如下所示在*Mgmt.mof。*

```cpp
class ISCSI_Path
{
    [WmiDataId(1),
     Description("iSCSI Unique connection id") : amended
    ]
    uint64 UniqueConnectionId;

    [WmiDataId(2),
     Description("Estimated speed of the connection in MegaBits Per Second") : amended
    ]
    uint64 EstimatedLinkSpeed;

    [WmiDataId(3),
     Description("Weight assigned to the path") : amended
    ]
    uint32 PathWeight;

    [WmiDataId(4),
     Description("Flag set to 1 if the path is a primary path, 0 otherwise.") : amended
    ]
    uint32 PrimaryPath;

    [WmiDataId(5),
     Description("Status of the path - connected, disconnected, reconnecting") : amended,
     Values{"Connected",
            "Disconnected",
            "Reconnecting"} : amended,
     DefineValues{"CONNECTION_STATE_CONNECTED",
                  "CONNECTION_STATE_DISCONNECTED",
                  "CONNECTION_STATE_RECONNECTING"
                 },
     ValueMap{"1", "2", "3"}
    ]
    uint32 ConnectionStatus;

    [WmiDataId(6),
     Description("Flag set to 1 if TCP offload is supported for this connection, 0 otherwise.") : amended
    ]
    uint32 TCPOffLoadAvailable;
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_路径**](https://msdn.microsoft.com/library/windows/hardware/ff561550)数据结构。

 

 





