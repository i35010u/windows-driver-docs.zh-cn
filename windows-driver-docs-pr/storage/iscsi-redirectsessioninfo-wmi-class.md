---
title: ISCSI \_ REDIRECTSESSIONINFO WMI 类
description: ISCSI \_ REDIRECTSESSIONINFO WMI 类
ms.assetid: eb1ec866-2dcd-4099-a24f-ae1d0c702b95
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c447af8ed94ca355de963a7c90adf29382883960
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188519"
---
# <a name="iscsi_redirectsessioninfo-wmi-class"></a>ISCSI \_ REDIRECTSESSIONINFO WMI 类


ISCSI \_ REDIRECTSESSIONINFO WMI 类包含 iscsi 会话的连接集合。 此类在*管理 mof*中定义为：

```cpp
class ISCSI_RedirectSessionInfo
{
    [read,
     WmiDataId(1),
     Description("A uniquely generated session ID, it is the same id returned by the LoginToTarget method.  Do not confuse this with ISID or SSID."): amended,
     WmiVersion(1)] uint64 UniqueSessionId;

    [read,
     WmiDataId(2),
     Description("Target portal group tag for this Session "): amended,
     WmiVersion(1)] uint32 TargetPortalGroupTag;

    [read,
     WmiDataId(3),
     DisplayName("Number of elements in RedirectPortalList array") : amended,
     cpp_quote("\n    // Number of elements in RedirectPortalList array\n"),
     Description("Number of elements in RedirectPortalList array") : amended,
     WmiVersion(1)
    ] uint32 ConnectionCount;

    [read,
     WmiDataId(4),
     DisplayName("Redirect Portal info for each connection") : amended,
     Description("Redirect portal info - one element for each connection in the session") : amended,
     WmiSizeIs("ConnectionCount"),
     WmiVersion(1)
    ] ISCSI_RedirectPortalInfo RedirectPortalList[];
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ RedirectSessionInfo**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_redirectsessioninfo) 数据结构。

 

