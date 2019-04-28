---
title: MSiSCSI\_RedirectPortalInfoClass WMI 类
description: MSiSCSI\_RedirectPortalInfoClass WMI 类
ms.assetid: 38f510ed-1f31-4b3c-84c6-515f5d42a1f8
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5283d4a3d717f36082a76a696aa5abd50c2a7e12
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325740"
---
# <a name="msiscsiredirectportalinfoclass-wmi-class"></a>MSiSCSI\_RedirectPortalInfoClass WMI 类


MSiSCSI\_RedirectPortalInfoClass WMI 类的会话集合包含一个适配器 id。 此外，它包含每个会话的门户重定向信息。 此类定义，如下所示在*Mgmt.mof。*

```cpp
class MSiSCSI_RedirectPortalInfoClass
{
    [read,key] String InstanceName;

    [read] boolean Active;

    [read,
     WmiDataId(1),
     DisplayName("Adapter Id") : amended,
     DisplayInHex,
     description("Id that is globally unique for all instances of iSCSI initiators.") : amended,
     WmiVersion(1)
    ]
    uint64 UniqueAdapterId;

    [read,
     WmiDataId(2),
     DisplayName("Number of session on the adapter : Number of elements in RedirectSessionInfo array") : amended,
     Description("Number of elements in RedirectSessionInfo array") : amended,
     WmiVersion(1)
    ] uint32 SessionCount;

    [read,
     WmiDataId(3),
     DisplayName("List Of ISCSI_RedirectSessionInfo ") : amended,
     Description("Variable length array of ISCSI_RedirectSessionInfo. SessionCount specifies the number of elements in the array. NOTE: this is a variable length array.") : amended,
     WmiSizeIs("SessionCount"),
     WmiVersion(1)
    ] ISCSI_RedirectSessionInfo RedirectSessionList[];
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **MSiSCSI\_RedirectPortalInfoClass** ](https://msdn.microsoft.com/library/windows/hardware/ff563117)数据结构。

 

 





