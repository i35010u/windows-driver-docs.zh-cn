---
title: ISCSI\_RedirectPortalInfo WMI 类
description: ISCSI\_RedirectPortalInfo WMI 类
ms.assetid: 55730446-7c8b-4c9d-9473-f9bb6edd603e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 989941d75c5afe36e02d88dacd5de81a56bb3cfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542107"
---
# <a name="iscsiredirectportalinfo-wmi-class"></a>ISCSI\_RedirectPortalInfo WMI 类


ISCSI\_RedirectPortalInfo WMI 类包含一系列 iSCSI 门户有关的信息。 此类定义中，如下所示*Mgmt.mof*。

```cpp
class ISCSI_RedirectPortalInfo
{
    [read,
     WmiDataId(1),
     Description("A uniquely generated connection ID. Do not confuse this with CID."): amended,
     WmiVersion(1)
     ] uint64 UniqueConnectionId;

    [read,
     WmiDataId(2),
     Description("Original Target IP Address given in the login"): amended,
     WmiVersion(1)] ISCSI_IP_Address OriginalIPAddr;

    [read,
     WmiDataId(3),
     Description("Original Target portal&#39;s socket number given in the login"): amended,
     WmiVersion(1)] uint32 OriginalPort;

    [read,
     WmiDataId(4),
     Description("Redirected Target IP Address"): amended,
     WmiVersion(1)] ISCSI_IP_Address RedirectedIPAddr;

    [read,
     WmiDataId(5),
     Description("Redirected Target portal&#39;s socket number"): amended,
     WmiVersion(1)] uint32 RedirectedPort;

    [read,
     WmiDataId(6),
     Description("TRUE if login was redirected. RedirectedIPAddr and RedirectedPort are valid then."): amended,
     WmiVersion(1)] uint8 Redirected;

    [read,
     WmiDataId(7),
     Description("TRUE if the redirection is temporary. FALSE otherwise"): amended,
     WmiVersion(1)] uint8 TemporaryRedirect;
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_RedirectPortalInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff561561)数据结构。

 

 





