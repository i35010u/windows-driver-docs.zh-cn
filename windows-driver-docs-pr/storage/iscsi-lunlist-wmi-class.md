---
title: ISCSI \_ LUNLIST WMI 类
description: ISCSI \_ LUNLIST WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 958ced83eff2a6f1d58dea53be615da58c4cae73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835111"
---
# <a name="iscsi_lunlist-wmi-class"></a>ISCSI \_ LUNLIST WMI 类


## <span id="ddk_iscsi_lunlist_wmi_class_kr"></span><span id="DDK_ISCSI_LUNLIST_WMI_CLASS_KR"></span>


ISCSI \_ LUNLIST WMI 类描述了一个从逻辑单元号到 (LUN) 的映射，操作系统将本地定义为64位数字，该数字与逻辑单元所属的目标的名称一起唯一标识，并且在网络中的任何位置都是全局有效的。 此类在 *Common mof* 中定义为：

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

 

