---
title: ISCSI \_ TARGETPORTALGROUP WMI 类
description: ISCSI \_ TARGETPORTALGROUP WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ed325382bc35ec18bac097b7f3c69ac00b0ed4d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811619"
---
# <a name="iscsi_targetportalgroup-wmi-class"></a>ISCSI \_ TARGETPORTALGROUP WMI 类


## <span id="ddk_iscsi_targetportalgroup_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTALGROUP_WMI_CLASS_KR"></span>


ISCSI \_ TargetPortalGroup 类定义目标门户组。

此类在 *Common mof* 中定义为：

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

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ TargetPortalGroup**](/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportalgroup) 数据结构。

 

