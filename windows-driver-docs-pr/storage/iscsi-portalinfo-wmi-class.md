---
title: ISCSI\_PortalInfo WMI 类
description: ISCSI\_PortalInfo WMI 类
ms.assetid: b38aa87c-00a5-483e-aa44-23f359783829
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cf4867aa5c2e878b01a8cfdd8b61e22b65cc5276
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378424"
---
# <a name="iscsiportalinfo-wmi-class"></a>ISCSI\_PortalInfo WMI 类


## <span id="ddk_iscsi_portalinfo_wmi_class_kr"></span><span id="DDK_ISCSI_PORTALINFO_WMI_CLASS_KR"></span>


ISCSI\_PortalInfo WMI 类包含与 iSCSI 门户相关的信息。 此类定义中，如下所示*Mgmt.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_PortalInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsimgt/ns-iscsimgt-_iscsi_portalinfo)数据结构。

 

 





