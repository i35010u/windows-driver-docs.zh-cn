---
title: ISCSI \_ TARGETPORTAL WMI 类
description: ISCSI \_ TARGETPORTAL WMI 类
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5f2e628616717f1e549a727b2e6a73276414ac91
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187807"
---
# <a name="iscsi_targetportal-wmi-class"></a>ISCSI \_ TARGETPORTAL WMI 类


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI \_ TargetPortal 类定义目标门户。 此定义包含套接字号和 IP 地址，独立于发起方和目标使用的 IP 协议的版本。

此类在 *Common mof*中定义为：

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ TargetPortal**](/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportal) 数据结构。

 

