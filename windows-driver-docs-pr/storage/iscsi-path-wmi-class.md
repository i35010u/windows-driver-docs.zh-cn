---
title: ISCSI\_路径 WMI 类
description: ISCSI\_路径 WMI 类
ms.assetid: d4067869-2c67-42d3-988e-af825549853d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3acf193ce8e941cc108bfc0ab288d9ed8dac9b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842265"
---
# <a name="iscsi_path-wmi-class"></a>ISCSI\_路径 WMI 类


ISCSI\_路径 WMI 类包含有关 iSCSI 门户连接的信息。 此类在*管理 mof*中定义为：

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

当 WMI 工具套件编译上述类定义时，它将生成[**ISCSI\_路径**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_path)数据结构。

 

 





