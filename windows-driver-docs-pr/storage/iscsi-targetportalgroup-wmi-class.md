---
title: ISCSI\_TargetPortalGroup WMI 类
description: ISCSI\_TargetPortalGroup WMI 类
ms.assetid: dff17d52-b308-49cc-97ec-d54eddb4e747
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e59fe196fb8c606300b9f0e23aeae96d1a3d03b7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358457"
---
# <a name="iscsitargetportalgroup-wmi-class"></a>ISCSI\_TargetPortalGroup WMI 类


## <span id="ddk_iscsi_targetportalgroup_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTALGROUP_WMI_CLASS_KR"></span>


ISCSI\_TargetPortalGroup 类定义了目标门户组。

此类定义中，如下所示*Common.mof*。

```cpp
class ISCSI_TargetPortalGroup {
  [WmiDataId(1), description("Number of portals in group") :
    amended]
    uint32  PortalCount;
  [WmiDataId(2), WmiSizeIs("PortalCount"),
    description("Target portals in group") : amended]
    ISCSI_TargetPortal  Portals[];
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_TargetPortalGroup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_targetportalgroup)数据结构。

 

 





