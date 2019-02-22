---
title: ISCSI\_LUNList WMI 类
description: ISCSI\_LUNList WMI 类
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 56318f4eea7591a5ae01d56369c470470dac6349
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544803"
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

当 WMI 工具套件编译前面的类定义时，它会生成[ **ISCSI\_LUNList** ](https://msdn.microsoft.com/library/windows/hardware/ff561544)数据结构。

 

 





