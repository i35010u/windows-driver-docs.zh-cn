---
title: ISCSI\_TargetPortal WMI 类
description: ISCSI\_TargetPortal WMI 类
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b02bf8a7cc56a90f63d477db31cef6eea05c4e98
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366112"
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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_TargetPortal** ](https://msdn.microsoft.com/library/windows/hardware/ff561574)数据结构。

 

 





