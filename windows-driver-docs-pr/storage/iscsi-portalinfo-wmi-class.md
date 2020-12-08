---
title: ISCSI \_ PORTALINFO WMI 类
description: ISCSI \_ PORTALINFO WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0dc35dc8201132594f3ef7205b8758154a4115f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835107"
---
# <a name="iscsi_portalinfo-wmi-class"></a>ISCSI \_ PORTALINFO WMI 类


## <span id="ddk_iscsi_portalinfo_wmi_class_kr"></span><span id="DDK_ISCSI_PORTALINFO_WMI_CLASS_KR"></span>


ISCSI \_ PORTALINFO WMI 类包含与 ISCSI 门户相关的信息。 此类在 *管理 mof* 中定义为：

```cpp
class ISCSI_PortalInfo
{
    [read,
     WmiDataId(1),
     description("An integer used to uniquely identify a paticular port"),
     WmiVersion(1)] uint32 Index;

    [read,
     WmiDataId(2),
     ISCSI_PORTAL_TYPE_QUALIFIERS,
     description("**typedef** The type of portal (Initiator or Target) \n"),
     WmiVersion(1)] ISCSI_PORTAL_TYPE PortalType;

    [read,
     WmiDataId(3),
     ISCSI_CONNECTION_PROTOCOL_TYPE_QUALIFIERS,
     //Description("The portal's transport protocol"): amended,
     description("The portal's transport protocol"),
     WmiVersion(1)] ISCSI_CONNECTION_PROTOCOL_TYPE Protocol;

    [read,
     WmiDataId(4),
     WmiVersion(1)] uint8 Reserved1;

    [read,
     WmiDataId(5),
     WmiVersion(1)] uint8 Reserved2;
 
    [read,
     WmiDataId(6),
     description("The portal's network address"),
     WmiVersion(1)] ISCSI_IP_Address IPAddr;

    [read,
     WmiDataId(7),
     description("The portal's socket number"),
     WmiVersion(1)] uint32 Port;

    [read,
     WmiDataId(8),
     description("The portal's aggregation tag"),
     WmiVersion(1)] uint16 PortalTag;
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ PortalInfo**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_portalinfo) 数据结构。

 

