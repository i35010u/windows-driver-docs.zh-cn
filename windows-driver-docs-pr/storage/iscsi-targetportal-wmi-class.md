---
title: ISCSI \_ TARGETPORTAL WMI 类
description: ISCSI \_ TARGETPORTAL WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 419d219219f0b7ce73ead8b05516fa18349d98ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835077"
---
# <a name="iscsi_targetportal-wmi-class"></a>ISCSI \_ TARGETPORTAL WMI 类


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI \_ TargetPortal 类定义目标门户。 此定义包含套接字号和 IP 地址，独立于发起方和目标使用的 IP 协议的版本。

此类在 *Common mof* 中定义为：

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ TargetPortal**](/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportal) 数据结构。

 

