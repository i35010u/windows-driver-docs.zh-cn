---
title: ISCSI\_LUNList WMI 类
description: ISCSI\_LUNList WMI 类
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 86e03ce1c8d728c97856355f8fbac608010e2022
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378423"
---
# <a name="iscsilunlist-wmi-class"></a>ISCSI\_LUNList WMI 类


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI\_LUNList WMI 类描述了从操作系统定义本地若要为与目标的逻辑单元属于名称唯一标识逻辑的 64 位号的逻辑单元号 (LUN) 的映射单元和全球网络中的任意位置有效。 此类定义中，如下所示*Common.mof*。

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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_LUNList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_lunlist)数据结构。

 

 





