---
title: ISCSI \_ LUNLIST WMI 类
description: ISCSI \_ LUNLIST WMI 类
ms.assetid: 2ad0dabe-54b3-4075-966b-491e078f2c8b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 13b8145b2f364a0489d0569fbac112c3a828aaac
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188521"
---
# <a name="iscsi_lunlist-wmi-class"></a>ISCSI \_ LUNLIST WMI 类


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI \_ LUNLIST WMI 类描述了一个从逻辑单元号到 (LUN) 的映射，操作系统将本地定义为64位数字，该数字与逻辑单元所属的目标的名称一起唯一标识，并且在网络中的任何位置都是全局有效的。 此类在 *Common mof*中定义为：

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

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ LUNList**](/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_lunlist) 数据结构。

 

