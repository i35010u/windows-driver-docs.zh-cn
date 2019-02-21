---
title: ISCSI\_RedirectSessionInfo WMI 类
description: ISCSI\_RedirectSessionInfo WMI 类
ms.assetid: eb1ec866-2dcd-4099-a24f-ae1d0c702b95
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 498f01f3adecde383d40df806b3be6b3db9cb3bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534555"
---
# <a name="iscsiredirectsessioninfo-wmi-class"></a>ISCSI\_RedirectSessionInfo WMI 类


ISCSI\_RedirectSessionInfo WMI 类包含 iSCSI 会话的连接的集合。 此类定义，如下所示在*Mgmt.mof。*

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_RedirectSessionInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff561563)数据结构。

 

 





