---
title: ISCSI\_TargetPortal WMI 类
description: ISCSI\_TargetPortal WMI 类
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c093c046615a6849309a77a43bdf5f572799cd60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841620"
---
# <a name="iscsi_targetportal-wmi-class"></a>ISCSI\_TargetPortal WMI 类


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI\_TargetPortal 类定义目标门户。 此定义包含套接字号和 IP 地址，独立于发起方和目标使用的 IP 协议的版本。

此类在*Common mof*中定义为：

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

当 WMI 工具套件编译上述类定义时，它将生成[**ISCSI\_TargetPortal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportal)数据结构。

 

 





