---
title: ISCSI \_ REDIRECTPORTALINFO WMI 类
description: ISCSI \_ REDIRECTPORTALINFO WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d5a2d88ce20b1fff52370bab73fb7980b7992114
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811639"
---
# <a name="iscsi_redirectportalinfo-wmi-class"></a>ISCSI \_ REDIRECTPORTALINFO WMI 类


ISCSI \_ REDIRECTPORTALINFO WMI 类包含有关 ISCSI 门户集合的信息。 此类在 *管理 mof* 中定义为：

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
     Description("Original Target portal's socket number given in the login"): amended,
     WmiVersion(1)] uint32 OriginalPort;

    [read,
     WmiDataId(4),
     Description("Redirected Target IP Address"): amended,
     WmiVersion(1)] ISCSI_IP_Address RedirectedIPAddr;

    [read,
     WmiDataId(5),
     Description("Redirected Target portal's socket number"): amended,
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

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ RedirectPortalInfo**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_redirectportalinfo) 数据结构。

 

