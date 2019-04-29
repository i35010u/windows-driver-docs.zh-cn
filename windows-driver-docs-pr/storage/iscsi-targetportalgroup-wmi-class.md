---
title: ISCSI\_TargetPortalGroup WMI 类
description: ISCSI\_TargetPortalGroup WMI 类
ms.assetid: dff17d52-b308-49cc-97ec-d54eddb4e747
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a45569f06103c00a554358a4b331b45d50c22026
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360898"
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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_TargetPortalGroup** ](https://msdn.microsoft.com/library/windows/hardware/ff561575)数据结构。

 

 





