---
title: ISCSI\_LUNList WMI 类
description: ISCSI\_LUNList WMI 类
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c7ffa1008fd58567021d28d48c28023456b3a5e5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842267"
---
# <a name="iscsi_lunlist-wmi-class"></a>ISCSI\_LUNList WMI 类


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI\_LUNList WMI 类描述从操作系统定义的逻辑单元号（LUN）到本地定义为64位数字的映射，该数字与逻辑单元所属的目标的名称一起唯一标识逻辑单元和在网络中的任何位置都是全局有效的。 此类在*Common mof*中定义为：

```cpp
class ISCSI_LUNList {
  [WmiDataId(1), description("Target LUN") : amended]
    uint64  TargetLUN;
  [WmiDataId(2), description("OS Scsi bus number target
  is mapped to") : amended]
    uint32  OSLUN;
  [WmiDataId(3), description("Reserved") : amended]
    uint32  Reserved;
};
```

当 WMI 工具套件编译上述类定义时，它将生成[**ISCSI\_LUNList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_lunlist)数据结构。

 

 





