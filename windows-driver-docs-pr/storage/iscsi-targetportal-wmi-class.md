---
title: ISCSI\_TargetPortal WMI 类
description: ISCSI\_TargetPortal WMI 类
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f081ade43895a41dc5e8e5703f556e70dd762a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385390"
---
# <a name="iscsitargetportal-wmi-class"></a>ISCSI\_TargetPortal WMI 类


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI\_TargetPortal 类定义了目标门户。 此定义包括套接字数量和独立于在发起方和目标使用的 IP 协议版本的 IP 地址。

此类定义中，如下所示*Common.mof*。

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_TargetPortal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_targetportal)数据结构。

 

 





